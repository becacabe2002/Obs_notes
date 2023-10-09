
> **ĐỊNH NGHĨA**: là một nhóm các statement hoặc là một phần tử làm việc.

- Các thao tác với csdl tạo thành 1 transaction có thể được nhúng vào trong chương trình của ứng dụng, hoặc có thể xác định một cách gián tiếp thông qua ngôn ngữ SQL.

* Nếu **TRANSACTION** thành công, các dữ liệu được thay đổi sẽ được lưu lại trong csdl
* Ngược lại, nếu **TRANSACTION** không thành công và được hoàn lại, các thay đổi về dữ liệu sẽ bị xoá (hoàn trả lại về trạng thái trước đó)

## I. Đặc tính ACID của transaction
Gồm 4 đặc tính: (ACID)
- ***Tính nguyên tử*** (Atomicity) - đảm bảo tất các phép toán trong phần tử làm việc đều hoàn thành. Nếu không, transaction sẽ bị huỷ bỏ tại điểm xảy ra lỗi và tất cả các phép toán được thực hiện lúc trước được hoàn trả về trạng thái ban đầu.

- ***Sự nhất quán*** (Consistency) - đảm bảo là csdl thay đổi đúng các trạng thái khi transaction được cam kết thành công.

- ***Cô lập*** (Isolation) - cho phép các transaction được thực hiện một cách độc lập và minh bạch với nhau

- ***Sự bền chắc*** (Durability) - đảm bảo là kết quả hoặc ảnh hưởng của một committed transaction được bảo toàn kể cả khi hệ thống có phát sinh lỗi 

👉 <mark style='background: #D3D3D3'>Dành cho mục đích phục hồi, hệ thống cần phải theo dõi thời điểm transaction <b>bắt đầu</b>, <b>chấm dứt</b> và <b>cam kết</b> hoặc <b>huỷ bỏ</b>.</mark>

## II. Xử lý transaction

**Lưu đồ các trạng thái của quá trình transaction**
![Image](https://media.geeksforgeeks.org/wp-content/uploads/20200501195048/Tt7.png)

* Các lệnh chỉ được sử dụng với DML: `INSERT`, `UPDATE`, `DELETE`

### 2.0 Begin
> Bắt đầu khai báo một transaction
```sql
BEGIN TRANSACTION transName;
```

### 2.1 Commit 
> Dùng để lưu các thay đổi bởi transaction vào csdl

- Chứa các transaction trong csdl từ lệnh `COMMIT` hoặc `ROLLBACK` gần nhất.

```sql
COMMIT;
```

### 2.2 Rollback
> Dùng để quay lại trạng thái mà các thay đổi chưa được lưu vào csdl

- Chỉ có thể dùng để hoàn tác lại transaction từ lệnh `COMMIT` hoặc `ROLLBACK` gần nhất.

```sql
ROLLBACK;
ROLLBACK TO savePointName;
```

### 2.3 Savepoint
> Điểm bên trong transaction, một điểm xác định dùng để hoàn tác lại các lệnh mà không phải hoàn tác lại về trạng thái đầu tiên.

* Create a savepoint
  ```sql
  SAVEPOINT savepointName;
  ```
* Xoá savepoint đã được tạo
  ```sql
  RELEASE SAVEPOINT savepointName;
  ```
(Một khi savepoint đã bị xoá, không thể hoàn tác lại tới savepoint đó)

### 2.4 Set transaction
* Dùng để bắt đầu một transaction và để cấu hình transaction (thành read-only hoặc read-write)

```sql
SET TRANSACTION [READ WRITE | READ ONLY];
```

### (BONUS) Read and write operation , DBMS buffer
* **Read operation** and **Write operation** là hai thao tác chính mà bao hàm trong transaction.

* Đơn vị cơ sở của lượng dữ liệu truyền tải từ ổ cứng tới bộ nhớ chính là **1 khối (block)**.

* Thực hiện thao tác `read_item(X)`:
  + Tìm địa chỉ của khối trong ổ cứng chứa phần tử X
  + Copy khối đó từ ổ cứng sang buffer (bộ nhớ đệm) trong bộ nhớ chính (nếu block đó chưa nằm trong bất cứ buffer nào của bộ nhớ chính).
  + Sao chép phần tử X từ buffer tới biến của chương trình đặt là X

* Thực hiện thao tác `write_item(X)`:
  + Tìm địa chỉ của khối trong ổ cứng chứa phần tử X
  + Copy khối đó từ ổ cứng sang buffer trong bộ nhớ chính (nếu block đó chưa nằm trong bất cứ buffer nào của bộ nhớ chính).
  + Copy phần tử X từ biến X của chương trình vào vị trí hiện tại trong buffer.
  + Lưu khối đã được cập nhật từ buffer vào lại ổ cứng (ngay lập tức hoặc sau đó)

* Một **read-set** của transaction bao gồm tất cả các phần tử mà transaction đó đọc.
* Một **write-set** của transaction bao gồm tất cả các phần tử mà transaction đó viết.

## III. Concurrent control (điều khiển tương tranh) 🎮
> là một procedure in DSMS giúp quản lý hai chương trình chạy đồng thời mà không phát sinh ra lỗi.

### 3.1 Các vấn đề phát sinh

#### 🪲 The Lost Update
* Hai transaction truy cập cùng khoản mục dữ liệu nhưng thao tác xen kẽ, làm cho giá trị của các khoản mục dữ liệu không còn đúng nữa.

![lost_update_image](https://media.geeksforgeeks.org/wp-content/uploads/20190823132655/d32.jpg)

#### 🪲 The Temporary Update (or Dirty Read)
* Xuất hiện khi 1 transaction (T1) update 1 khoản mục dữ liệu (X), nhưng sau đó xảy ra lỗi -> transaction failed -> rollback về giá trị trước đó.

* Nhưng đồng thời một transaction khác (T2) cũng sử dụng khoản mục dữ liệu đó trước khi khoản mục được rollback về giá trị cũ.

![temp_update_img](https://media.geeksforgeeks.org/wp-content/uploads/20190823132421/d110.jpg)

#### 🪲 The Incorrect Summary
* Một transaction tính hàm tích luỹ trên các bản ghi đang được update bởi 1 transaction khác 
-> Hàm có thể tính dựa trên một số **giá trị đã cập nhật** và một **số giá trị chưa cập nhật**.

![incorrect_sum_img](https://media.geeksforgeeks.org/wp-content/uploads/20190823132540/d28.jpg)

*T2 đọc X sau khi X - N, đọc Y trước khi Y + N*

#### 🪲 The Unrepeatable Read
* Một transaction (T2) thực hiện đọc một khoản mục dữ liệu 2 lần, giữa hai lần đó, giá trị của khoản mục bị thay đổi và cập nhật bởi 1 transaction khác (T1)
-> Kết quả hai lần đọc là hai giá trị khác nhau.

![unrepeat_read_img](https://media.geeksforgeeks.org/wp-content/uploads/20190823132817/d41.jpg)

### 3.2 Vì sao cần chế độ hồi phục (Recovery) 🔁
* Vì DBMS không cho phép chỉ áp dụng một vài thao tác trong 1 transaction và không áp dụng các thao tác còn lại.

* Các nguyên nhân dẫn tới lỗi khi đang thực hiện transaction:
  + A computer failure (system crash)
  + A transaction or system error
  + Local errors or exception conditions detected by the
transaction
+ Concurrency control enforcement
+ Disk failure
+ Physical problems and catastrophes

### 3.3 Các kỹ thuật điều khiển tương tranh

#### a, Lock-based Protocols (Khoá) 🔒
* Không transaction nào có thể đọc hoặc ghi dữ liệu cho tới khi nó có được khoá thích hợp.

* 2 loại khoá:
  * **Shared lock**: còn được gọi là Read-only lock. 
    + Phần tử dữ liệu chỉ có thể được đọc bởi transaction.
    + Có thể được chia sẻ giữa các transactions vì nếu một transaction giữ khoá, nó không thể cập nhật dữ liệu của phần tử dữ liệu.

  * **Exclusive lock**:
    * Transaction có thể đọc và ghi dữ liệu của phần tử dữ liệu
    * Khoá này là độc nhất, nhiều transactions không sửa đổi cùng một dữ liệu một cách đồng thời.

**4 loại Lock-based Protocol**
1. Simplistic lock protocol

2. Pre-claming lock protocol

3. Two-phase locking

4. Strict Two-phase locking

[***Tham khảo thêm***](https://www.javatpoint.com/dbms-lock-based-protocol)

#### b, Timestamp-based Protocols (Dán nhãn thời gian) ⏱️
* Use to order the transactions based on their **timestamps**. (Dựa trên thời gian transaction được tạo ra)

* Thứ tự ưu tiên của các transactions được xác định bằng thời gian đi vào hệ thống của từng transactions. (Transaction vào trước sẽ thực hiện trước)

* Lock-based protocols được sử dụng để quản lí thứ tự giữa các cặp xung đột giữa các transactions vào thời điểm thực thi. Nhưng timestamp-based protocols bắt đầu ngay sau khi transaction được tạo ra.

👉 **Quy trình thực thi TS protocol**:

*TS(Ti) - biểu thị timestamp của transaction Ti*
*R_TS(X) - biểu thị Read timestamp của item X*
*W_TS(X) - biểu thị Write timestamp của item X*

1. Kiểm tra điều kiện mỗi khi transaction Ti có ***Read(X)***
  * Nếu *W_TS(X) > TS(Ti)* -> Operation bị từ chối
  * Nếu *W_TS(X) <= TS(Ti)* -> Operation được thực thi
  * Cập nhật timestamps cho tất cả các items

2. kiểm tra điều kiện mỗi khi transaction Ti có ***Write(X)***
  * Nếu *TS(Ti) < R_TS(X)* -> Operation bị từ chối
  * Nếu *TS(Ti) < W_TS(X)* -> Operation bị từ chối, Ti rollback
  * Còn lại, Operation được thực thi

**Ưu điểm ✅ và nhược điểm ❌ của TS protocol**:
* TO protocol đảm bảo khả năng tuần tự hoá bởi biểu đồ ưu tiên như sau:

![img](https://static.javatpoint.com/dbms/images/dbms-timestamp-ordering-protocol.png)

* TS protocol đảm bảo không có sự bế tắc (không transaction nào phải vào tình trạng đợi)

* Nhưng schedule không thể hồi phục, và có thể không cascade-free

### 3.4 Schedule 📅
* Một **schedule của một set transactions** là thứ tự tuyến tính các hành động của chúng.
  + Ex:
  ```latex
  R_1(X) \rightarrow R_2(X) \rightarrow W_1(X) \rightarrow W_2(X)
  ```

* Một **serial schedule** là cái mà tất cả các bước của mỗi transaction xuất hiện một cách liên tiếp. (Tất cả các bước của 1 transaction được hoàn thành trước khi bắt đầu một transaction mới.)

* Một **serializable schedule** là một non-serial schedule nhưng kết quả cho ra giống với khi các transaction được thực hiện tuần tự.


### 3.5 Mức độc lập (Isolation Levels)
```sql
SET ISOLATION LEVEL <level>
```

* **Read Uncommitted** (No lost update)
  - Exclusive locks for write operations are held for the duration of the transactions.
  - No locks for read

* **Read Committed** (No inconsistent retrieval)
  - Shared locks are released as soon as the read operation terminates.

* **Repeatable Read** (No unrepeatable reads)
  - Strict two phase locking

* **Serializable** (No phantoms)
  * Table locking or index locking to avoid phantoms


