## 1. Tổng quan
* Tài nguyên TT cần 
	* Bộ xử lý (ảo)[[Chap2.4 - Tài nguyên găng và điều độ tiến trình]]
	* Bộ nhớ [[Chap3 - Quản lý bộ nhớ]]
	* Tập tài nguyên khác

### 1.1 Ví dụ
### 1.2 Bộ nhớ và chương trình
### 1.3 Liên kết địa chỉ
> [!note] Các bước xử lý chương trình ứng dụng
> ![[Pasted image 20221205125234.png]]

#### Các kiểu địa chỉ
> [!info] Địa chỉ biểu tượng (symbolic)
> Tên của đối tượng trong chương trình nguồn

> [!info] Địa chỉ tương đối 

> [!info] Địa chỉ tuyệt đối

#### Xác định địa chỉ
![[Pasted image 20221205125753.png]]

### 1.4 Các cấu trúc chương trình
#### Cấu trúc tuyến tính

#### Cấu trúc nạp động
* Mỗi modul được biên tập riêng
* Khi thực hiện, hệ thống sẽ định vị  modul gốc
* Cần tới modul nào sẽ xin bộ nhớ và giải nạp modul vào
* Khi sử dụng xong một modul, hoặc khi thiếu vùng nhớ sẽ đưa những modul  không cần thiết ra ngoài.

> [!check] Ưu điểm
> * Có thể sử dụng vùng nhớ nhiều hơn phần dành cho CT
> * Hiệu quả sử dụng bộ nhớ cao nếu quản lý tốt

> [!failure] Nhược điểm
> * Tốc độ thực hiện chậm
> * Sai lầm sẽ dẫn tới lãng phí bộ nhớ và tăng thời gian thực hiện
> * Yêu cầu người sử dụng phải nạp và xoá các modul
> 	* Người dùng phải nắm rõ hệ thống
> 	* Giảm tính lưu động

#### Cấu trúc  liên kết động

### Cấu trúc Overlays

## 2. Các chiến lược quản lý bộ nhớ
### 2.1 Chiến lược phân chương cố định
> [!abstract] Nguyên tắc
> * Bộ nhớ được chia thành n phần
> * Mỗi phần gọi là 1 chương (partition)
> 	* Kích thước: ko nhất thiết phải bằng nhau
> 	* Được sử dụng như 1 vùng nhớ độc lập
> 		* Tại 1 thời điểm chỉ cho phép 1 CT tồn tại
> 		* Các CT nằm trong vùng nhớ cho tới khi kết thúc

> [!info] Phân mảnh trong
> Phân mảnh ở bên trong phân vùng, không gian dư thừa trong mỗi phân vùng.

> [!check] Ưu điểm
> * Đơn giản, dễ tổ chức bảo vệ
> 	* CT và vùng nhớ có một khoá bảo vệ
> 	* So sánh 2 khoá với nhau khi nạp CT
> * Giảm thời gian tìm kiếm

> [!failure] Nhược điểm
> * Phải sao lưu modul  điều khiển ra làm nhiều bản và lưu ở nhiều nơi
> * Hệ số song song không thể vượt quá n
> * Bị phân đoạn bộ nhớ
> 	* Kích thước CT lớn hơn kích thước chương lớn nhất
> 	* Tổng bộ nhớ tự do còn lớn, nhưng không dùng để nạp các CT khác
> => Sửa lại cấu trúc chương, kết hợp một số chương kề nhau

* Thường dùng để quản lý các đĩa dung lượng lớn.

### 2.2 Chiến lược phân chương động

### 2.3 Chiến lược phân đoạn

### 2.4 Chiến lược phân trang

### 2.5 Chiến lược kết hợp phân đoạn - phân trạng

## 3. Bộ nhớ ảo
### 3.1 Giới thiệu
### 3.2 Các chiến lược đổi trang

## 4. Quản lý bộ nhớ trong VXL họ intel


