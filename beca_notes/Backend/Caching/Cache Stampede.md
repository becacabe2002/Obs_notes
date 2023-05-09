
```start-multi-column
ID: ID_ewb0
Number of Columns: 2
Largest Column: right
Border: off
```


* *Nếu cache miss thì sẽ trực tiếp gọi vào DB để lấy dữ liệu.* 
* *Tuy nhiên, khi mới khởi chạy hoặc khi dữ liệu bị hết hạn, cache thường sẽ rỗng nên liên tục  xảy ra cache miss.*
	* *Vào giờ cao điểm, có hàng trăm nghìn request từ backend tới cache, cache miss xảy ra dẫn tới backend tạo ra hàng tăm nghìn query vào DB để lấy dữ liệu.*

--- column-end ---

![[Pasted image 20230417205636.png]]

=== end-multi-column

> [!info] Cache Stampede (thundering herds)
> Vấn đề khi một vài/nhiều threads truy cập vào cache song song cùng lúc nhưng xảy ra cache miss. Khi đó threads sẽ lấy dữ liệu từ source chính như như third-party, database ... làm ảnh hưởng nghiêm trọng tới source chính.

* Cache stampede thường xảy ra khi:
	* Mới khởi tạo hoặc restart cache
	* Truy cập loại dữ liệu mới.

> [!warning] Một số trường hợp xấu khi xảy ra Cache Stampede
> * Hàng trăm nghìn câu query tới DB -> Chết DB hoặc time out queries.
> * Retry khi nhận được thông báo timeout -> database càng căng thẳng.
> * Database căng thẳng -> Xử lý chậm, dẫn tới timeout
> 
> **=> Một vòng tuần hoàn**

## Các cách giải quyết

> [!hint] Cội nguồn nguyên nhân là cache miss quá nhiều.
> Để giải quyết cache miss, có hai hướng:
> * **Giảm thiểu trường hợp cache miss ít nhất có thể**: đảm bảo dữ liệu trong cache luôn tồn tại, tránh cache rỗng.
> 	* External Computation
> 	* Probalilistic Early Expiration
> * **Handle cache miss tốt hơn**: (better choice)
> 	* Lock
> 	* Promise

### External Computation
* Khởi tạo giá trị ban đầu trong cache khi mới start cache.
* Tạo worker để kiểm tra dữ liệu, xem dữ liệu nào sắp hết hạn
	* Nếu sắp hết hạn, worker vào db lấy dữ liệu và lưu vào cache.
	* Sau đó, extend time-to-live cho dữ liệu trong cache.
* Worker có thể được cho **chạy định kì** (schedule, cron job ...) hoặc **trigger theo event expired** từ cache.

> [!failure] Bất lợi
> Trong cache sẽ chứa nhiều dữ liệu dư thừa -> tốn resource.

### Probabilistic Early Expiration

```js
currentTime - ( timeToCompute * beta * log(rand()) ) > expiry
```
* `currentTime`
* `timeToCompute` - thời gian để tính toán lại dữ liệu
* `beta` - giá trị cấu hình luôn >= 0 (default = 1)
* `rand()` 
* `expiry` - thời gian expired tương lai

> [!abstract] Nguyên lý
> Ngoài việc đọc dữ liệu trong cache trả về backend, công thức trên sẽ được chạy để tính toán kết quả.
> * **True** -> lấy dữ liệu mới update vào cache + extends thời gian hết hạn
> * **False** -> không cần update dữ liệu

> [!check] Ưu điểm
> Dựa theo xác suất để biết dữ liệu nên hay không nên được update.
> -> Tránh tình trạng dư thừa mà vẫn đảm bảo hạn chế cache miss.

### Lock 
* Khi một request tới backend, sẽ vào cache để lấy dữ liệu dựa vào key.
* Khi có nhiều request cùng đọc vào một key **đồng thời** và đều gặp cache miss.
-> Các request sẽ vào DB để query cùng 1 câu -> Xảy ra cache stampede.

> [!abstract] Nguyên lí dùng lock
> * Dùng lock để khóa lại key mà các request cần trong cache.
> * Nếu gặp cache mis thì vào db để update cache. 
> * Sau khi update xong, release lock.
> * Các request tiếp theo mới được xử lí nếu cùng key lock.

* Các request ban đầu lũ lượt tràn vào DB từ giờ sẽ qua cổng redlock.
	* Redlock bắt mọi request phải xếp hàng chờ tới lượt.

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.data.redis.core.script.DefaultRedisScript;
import org.springframework.data.redis.core.script.RedisScript;
import org.springframework.stereotype.Service;

import java.util.Collections;
import java.util.concurrent.TimeUnit;

@Service
public class CacheService {

    private final RedisTemplate<String, String> redisTemplate;

    @Autowired
    public CacheService(RedisTemplate<String, String> redisTemplate) {
        this.redisTemplate = redisTemplate;
    }

    public String getDataWithCache(String key) {
        String data = redisTemplate.opsForValue().get(key);
        if (data == null) {
            // Key chưa được cache, thực hiện load data từ backend và lưu vào cache
            data = loadDataFromBackend(key);
            String script = "if redis.call('get', KEYS[1]) == ARGV[1] then return redis.call('del', KEYS[1]) else return 0 end";
            RedisScript<Long> redisScript = new DefaultRedisScript<>(script, Long.class);
            while (true) {
                Boolean lock = redisTemplate.opsForValue().setIfAbsent(key + "_lock", "locked", 10, TimeUnit.SECONDS);
                if (lock != null && lock) {
                // Lưu data vào cache với expire time là 1 giờ
                    redisTemplate.opsForValue().set(key, data, 1, TimeUnit.HOURS); 
                    redisTemplate.delete(key + "_lock");
                    break;
                } else {
                    try {
                        Thread.sleep(100);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    String lockValue = redisTemplate.opsForValue().get(key + "_lock");
                    if (lockValue == null) {
                        continue;
                    }
                    redisTemplate.execute(redisScript, Collections.singletonList(key + "_lock"), lockValue);
                }
            }
        }
        return data;
    }

    private String loadDataFromBackend(String key) {
        // Thực hiện quá trình load dữ liệu từ backend
        return "Data for key " + key;
    }
}

```

### Promise (chỉ dùng trong JS)

![[Pasted image 20230417225540.png]]
* Trong khi lock bắt các request phải xếp hàng chờ đợi, promise gắn các request vào callback của promise.
* Khi một promise được chạy xong, tất cả các request đều có kết quả (ko cần đợi vào cache kiểm tra)

#### Future Object in Java Spring Boot

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.stereotype.Service;

import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.TimeUnit;

@Service
public class CacheService {

    private final RedisTemplate<String, String> redisTemplate;

    @Autowired
    public CacheService(RedisTemplate<String, String> redisTemplate) {
        this.redisTemplate = redisTemplate;
    }

    public String getDataWithCache(String key) {
        String data = redisTemplate.opsForValue().get(key);
        if (data == null) {
            CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> loadDataFromBackend(key));
            try {
                data = future.get();
                redisTemplate.opsForValue().set(key, data, 1, TimeUnit.HOURS);
            } catch (InterruptedException | ExecutionException e) {
                e.printStackTrace();
            }
        }
        return data;
    }

    private String loadDataFromBackend(String key) {
        // Thực hiện quá trình load dữ liệu từ backend
        return "Data for key " + key;
    }
}

```