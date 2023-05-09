> [!note] Nhắc lại về Cache
> * Cache là kỹ thuật dùng để lưu trữ dữ liệu thường xuyên được truy xuất vào bộ nhớ cache, giúp tăng tốc độ truy xuất dữ liệu và giảm tải cho hệ thống.
> * **Bộ nhớ cache** có thể là memory của server hoặc redis.
> 	* Độ phức tạp: O(1)
> 	* Dữ liệu tổ chức theo dạng **key-value**
> 
> * **Cache miss** - truy vấn và không tim thấy dữ liệu nằm trong cache
> * **Cache hit** - truy vấn và tìm thấy dữ liệu trong cache

* Việc lựa chọn chiến lược Caching phụ thuộc vào mô hình sử dụng (write-heavy workloads, read-heavy workloads ...)

## Cache Aside
> [!abstract] Nguyên tắc
> Vùng nhớ cache được đặt 1 bên, application sẽ giao tiếp trực tiếp với cache và database.

![[Pasted image 20230417110656.png]]
> [!note] Cách hoạt động
> 1. Application kiểm tra dữ liệu trong cache
> 	* Nếu trong cache có dữ liệu cần tìm -> kết thúc
> 	* Nếu không, chuyển sang bước 2
> 2. Application chuyển sang database để lấy dữ liệu.
> 3. Application lưu dữ liệu lấy được từ db vào cache.

> [!check] Lợi ích
>* Khi cache server bị chết, lỗi connection, hoặc cache miss, application vẫn có thể lấy dữ liệu từ DB về để sử dụng.
>* Dữ liệu lưu trong cache là dữ liệu thực sự cần dùng -> tiết kiệm chi phí, tài nguyên của cache server
>* Có thể kết hợp nhiều loại dữ liệu từ nguồn vào trong cache. (tính toán một lần duy nhất ở db, sau đó chỉ tốn chi phí truy vấn cache.)

> [!fail] Bất lợi
>  * Hay xảy ra trường hợp cache miss khi truy vấn dữ liệu lần đầu tiên hoặc khi dữ liệu trong cache bị hết hạn.
> 	 * Giải quyết vấn đề này bằng cách load dữ liệu thủ công vào cache.
> * Thời gian xử lý cache miss lâu, ảnh hưởng tới trải nghiệm người dùng.
> 	* Phát sinh vấn đề về [[Cache Stampede]]
> * Khó quản lí, hoặc có độ trễ khi dữ liệu invalid. (Cần phải update hoặc clear cache.)

> [!hint] Khi nào nên dùng Cache Aside?
> Dùng trong trường hợp **Read-heavy workloads**, dữ liệu sử dụng nhiều, lặp lại và tốn thời gian/resource để tính toán, xử lý.
> 

### Read through Cache

> [!abstract] Nguyên tắc
> Application chỉ cần giao tiếp với Cache, Cache sẽ tự lấy dữ liệu chính mình hoặc từ DB. (Cache đóng vai trò là DB chính của ứng dụng).

![[Pasted image 20230417115403.png]]

> [!note] Cách hoạt động
> 1. Application sẽ gửi request tới cache để lấy dữ liệu.
> 2. Nếu cache có dữ liệu, nó sẽ trả lại dữ liệu ngay cho application. Nếu cache không có dữ liệu, chuyển sang bước ba.
> 3. Khi cache không chứa dữ liệu mà application cần, cache server sẽ tự động lấy dữ liệu từ database để update chính bản thân mình.
> 4. Trả về dữ liệu cho application.

> [!check] Lợi ích
> Application không cần quân tâm tới trường hợp cache miss, cache server sẽ lo vụ này.

> [!fail] Bất lợi
> * Nếu cache server chết, ứng dụng cũng chết.
> * Phải tìm được dịch vụ cache phù hợp. (lấy dữ liệu từ database từ một/nhiều câu query phức tạp.)
> * Khó control thời gian hết hạn của cache. (phải tuỳ thuộc vào platform sử dụng.)
> * Có nhiều dữ liệu cũ, dữ liệu không đồng nhất với DB trong cache.

> [!hint] Khi nào dùng Read-through Cache?
> Thường dùng trong trường hợp **read-heavy workloads**, mặc dù trong cache chứa nhiều dữ liệu cũ, dữ liệu không dùng tới. Nhìn chung, vẫn đáp ứng được các trường hợp đọc dữ liệu nhiều.

### Write-through Cache
> [!abstract] Nguyên tắc
> Data sẽ được lưu từ application xuống cache, cache sẽ lưu dữ liệu vào DB.

![[Pasted image 20230417152230.png]]

> [!note] Cách hoạt động
> 1. Dữ liệu sẽ được lưu vào cache
> 2. Cache sẽ gửi yêu cầu lưu dữ liệu vào DB ngay lập tức.

> [!check] Lợi ích
> * Không bao h bị cache miss (dữ liệu luôn được lưu vào cache trước khi lưu vào DB)
> * Không xảy ra trường hợp dữ liệu không khớp giữa cache và DB
> * Dữ liệu luôn đồng nhất nếu kết hợp giữa **Read-through Cache** và **Read-through Cache**.

> [!fail] Bất lợi
> * Hầu hết các dữ liệu trong cache là dữ liệu đọc 1 lần -> nhiều dữ liệu trên cache là ko cần thiết
> * Dữ liệu lưu trên cache nhiều tương đuơng với DB -> tốn resource ko cần thiết
> * Quá trình lưu dữ liệu thường sẽ lâu (phải chờ lưu xuống cache và DB)

> [!hint] Khi nào dùng write-though cache?
> * Dùng cho các trường hợp **write-heavy workloads**

### Write back (write behind)
> [!abstract] Nguyên tắc
> Cache không lưu dữ liệu xuống DB ngay khi nhận request từ application. Cache sẽ đồng bộ dữ liệu xuống DB định kì theo thời gian, hoặc theo số lượng dữ liệu được insert/update. (Bất đồng bộ)

![[Pasted image 20230417153523.png]]

> [!note] Cách hoạt động
> 1. Dữ liệu sẽ được lưu vào cache
> 2. Sau một khoảng thời gian, cache sẽ gửi yêu cầu dữ liệu vào DB.

> [!check] Lợi ích
> * Giảm tải áp lực write xuống DB, từ đó sẽ giảm được chi phí và các vấn đề liên quan tới DB 
> * Nếu kết hợp giữa **Write back** và **Read-through cache**, chúng ta sẽ có một hệ thống tốt cho cả Ready-heavy workloads và write-heavy workloads.

> [!fail] Bất lợi
> * Dữ liệu có thể không đồng nhaát giữa cache và DB nếu như cache chưa kịp đồng bộ dữ liệu về DB.
> * Nếu cache server bị chết, hệ thống sẽ bị chết -> mất vĩnh viễn dữ liệu mà cache chưa kịp đồng bộ vào server.

> [!hint] Nên sử dụng Write back khi nào?
> Dành cho Write-heavy workloads.

### Write Around
> [!abstract] Nguyên tắc
> lưu trực tiếp dữ liệu từ application vào DB và đọc dữ liệu theo 1 trong 2 chiến lược: Cache Aside hoặc Read-through cache.

![[Pasted image 20230417154519.png]]
