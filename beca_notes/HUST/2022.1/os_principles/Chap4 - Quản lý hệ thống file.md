## 1. Hệ thống file
* Thông tin lưu trữ trên nhiều phương tiện/ thiết bị lưu trữ khác nhau. Các thiết bị lưu trữ được mô hình như 1 mảng của các khối nhớ.

> [!info] File
> Tập thông tin ghi trên thiết bị lưu trữ
> * Là đơn vị lưu trữ của OS trên bộ nhớ ngoài
> * Bao gồm dãy các bits, bytes, dòng, bản ghi, ... mang ý nghĩa và được định nghĩa bởi người dùng.

* **Cấu trúc file** được định nghĩa theo loại file
	* **File văn bản**: Chuỗi ký tự tổ chức thành dòng
	* **File đối tượng**: Bytes được tổ chức thành khối để chương trình liên kết (linker) hiểu được
	* **File thực thi**: Chuỗi các mã lệnh có thể thực hiện trong bộ nhớ

#### Các thuộc tính file
> [!abstract] 
> * **Tên file**: Chuỗi ký tự phân biệt giữa các file
> * **Định danh (Identifier)**: thẻ xác định duy nhất 1 file
> * **Kiểu (Type)**: dùng cho hệ thống hỗ trợ nhiều kiểu file
> * **Vị trí (Position)**: trỏ tới thiết bị và vị trí của file trên đó
> * **Kích thước (Size)**: Kích thước hiện thời/tối đa của file
> * **Bảo vệ (Protection)**: Điều khiển truy nhập (quyền của các người dùng)
> * **Thời gian (Time)**: Thời điểm tạo, sửa đổi, sử dụng cuối...

* Tên file:
	* Thông tin lưu dưới dạng người dùng có thể đọc được
	* Có thể phân biệt Capital
	* Đảm bảo tính độc lập của file với TT, người dùng ...

* Kiểu: 
	* Có thể xác định kiểu file dựa trên một phần của tên file
	* Dựa trên kiểu, HĐH sẽ thao tác trên tập tin phù hợp

> [!info] Bản ghi file
> Cấu trúc dữ liệu lưu trữ thuộc tính file
> * Có thể chỉ chứa tên file và định danh file, định danh file xác dịnh các thông tin còn lại
> * Kích thước từ vài bytes lên tới kilobytes

> [!info] Thư mục file
> Lưu trữ các bản ghi file
> * Thường được lưu trữ trên thiết bị nhớ ngoài
> * Được đưa từng phần vào bộ nhớ khi cần thiết
> * Kích thước có thể đạt tới Megabytes

![[Pasted image 20230116102350.png]]

#### Các thao tác cơ bản
> [!abstract] 
> * Tạo file (Create)
> * Ghi file (Write)
> * Đọc file (Read)
> * Thay đổi vị trí trong file (Seek)
> * Xoá file (Delete)
> * Thu gọn file (Truncate)

> [!note] Tạo file
> * Tìm vùng tự do trong không gian lưu trữ của hệ thống file
> * Tạo một phần tử mới trong thư mục file
> * Lưu tên, vị trí của file và các thông tin khác
> ![[Pasted image 20230116224942.png]]

> [!note] Ghi file
> * Lời gọi hệ thống Write() yêu cầu tên file và dữ liệu được ghi
> * Dùng tên file, tìm kiếm file trong thư mục file.
> * Dựa vào vị trường vị trí, tìm vị trí của file trên thiết bị lưu trữ.
> * Hệ thống lưu con trỏ ghi (Write pointer) để chỉ ra vị trí ghi
> 	* Con trỏ ghi thay đổi sau mỗi thao tác ghi.
> ![[Pasted image 20230116225232.png]]

> [!note] Đọc file
> * Lời gọi hệ thống Read() yêu cầu tên file và vùng đệm ghi KQ
> * Dùng tên file để tìm kiếm trong thư mục file
> * Dựa vào trường vị trí, tìm vị trí của file trên thiết bị lưu trữ
> * Hệ thống lưu con trỏ đọc (read pointer) chỉ ra vị trí được đọc
> 	* Vị trí của con trỏ đọc thay đổi sau mỗi thao tác đọc dữ liệu
> ![[Pasted image 20230116225317.png]]

* Có thể dùng một con trỏ cho cả thao tác đọc và ghi: ***Con trỏ file***

> [!note] Xoá file
> * Dùng tên file, tìm kiếm file trong thư mục file
> * Vùng nhớ được xác định bởi 2 trường vị trí và kích thước được giải phóng để có thể sử dụng lại bởi các file khác
> * Xoá  phần tử tương ứng trong thư mục file
> * Xoá logic/xoá vật lý
> ![[Pasted image 20230116225923.png]]

> [!note] Thay đổi vị trí trong file
> * Duyệt thư mục để tìm phần tử tương ứng
> * Con trỏ file được thay bằng giá trị thích hợp
> * Thao tác này không yêu cầu một hoạt động vào/ra

> [!note] Thu gọn file
> * Được sử dụng khi người sử dụng muốn xoá nội dung file nhưng vẫn giữ nguyên các thuộc tính
> * Tìm kiếm file trong thư mục file
> * Đặt kích thước file về 0
> * Giải phóng vùng nhớ dành cho file

* Các thao tác file phải duyệt thư mục file -> **Lãng phí thời gian**

> [!check] 
> Để giải quyết, các TT phải thực hiện mở file trước khi thao tác với file.


 * Thao tác mở file: 
	* tìm kiếm **file** trong **thư mục file**
	* Chép phần tử tương ứng vào **bảng file mở**
	* Chứa thông tin về các file đang được mở
	* Trả lại con trỏ của phần tử tương ứng trong bản file mở

 * Khi có yêu cầu, OS tìm kiếm trong bảng file mở
	* Dùng con trỏ trả về của thao tác mở file

![[Pasted image 20230116231048.png]]

* Khi không sử dụng file nữa, cần phải đóng file
	* OS loại bỏ phần tử tương ứng trong bảng file mở.

> [!note] Thao tác đóng mở file trong môi trường đa người dùng
> * Dùng 2 loại bảng file mở: cho từng TT và cho hệ thống
> * Ghi lại số TT đang mở file bằng File Open Counter 
> 	* Tăng/giảm bộ đếm khi có TT mở/đóng file
> 	* Xoá p/tử tương ứng trong bảng file mở ở mức OS khi FOC = 0

![[Pasted image 20230116231348.png]]

### Cấu trúc thư mục
* Đĩa được chia thành nhiều phân vùng Partitions, Minidisks, Volumes
	* Mỗi phân vùng được xử lý như 1 **vùng lưu trữ riêng biệt**
	* Có thể chứa một HĐH riêng trong mỗi phân vùng
* Có thể kết hợp một vài đĩa thành 1 cấu trúc logic lớn:
	* Người dùng chỉ quan tâm tới **cấu trúc file** và **thư mục logic**
	* Người dùng ko quan tâm tới cách phân phối vật lý không gian đĩa cho files

* Mỗi một phân khu lưu các thông tin về file trong nó
	* Các thông tin file được lưu trữ trong thư mục thiết bị (**Thư mục**)

> [!info] Thư mục
> Bảng chuyển cho phép ánh xạ từ 1 tên (file) --> 1 phần tử trong thư mục

> [!abstract] Các thao tác với thư mục
> * Tìm kiếm file
> * Tạo file
> * Xoá file
> * Liệt kê thư mục
> * Đổi tên file
> * Duyệt hệ thống file (thường dùng để backup dữ liệu)

* Thư mục có thể được cài đặt bằng nhiều cách khác nhau

#### Thư mục 1 mức
* Có cấu trúc đơn giản nhất, các file nằm trong **cùng 1 thư mục**

![[Pasted image 20230117002430.png]]

* Mỗi người dùng có 1 thư mục riêng
	* Chỉ duyệt file trong thư mục riêng
	* Khi login, hệ thống sẽ kiểm tra và cho phép user làm việc với thư mục riêng của họ

* Khi muốn thêm user:
	* Hệ thống tạo phần tử mới trong master file directory
	* Tạo User file directory

> [!check] Ưu điểm
> * Giải quyết vấn đề trùng tên
> * Hiệu quả khi người dùng độc lập

> [!failure] Nhược điểm
> Khó khăn khi muốn dùng chung file

#### Thư mục cấu trúc cây
* Tồn tại 1 đường dẫn (tương đối hoặc tuyệt đối) tới 1 file
* Thư mục con là file được xử lý đặc biệt (bit đánh dấu)
* Các thao tác với thư mục được thực hiện trên thư mục hiện thời
	* Xoá thư mục con đồng nghĩa với việc xoá hết các cây con của nó.

![[Pasted image 20230117002934.png]]

#### Thư mục dùng chung
* Người dùng có thể link đến 1 file của người dùng khác
* Khi duyệt thư mục (backup) file có thể duyệt nhiều lần
* Xoá file: có thể là xoá liên kết nếu người dùng chung, hoặc xoá file hoàn toàn nếu đó là người dùng có liên kết cuối.

![[Pasted image 20230117003139.png]]

## 2. Cài đặt hệ thống file
### Cài đặt thư mục
> [!note] DS tuyến tính với con trỏ tới các khối dữ liệu
> ![[Pasted image 20230117003636.png]]
> * Đơn giản khi lập trình
> * Tốn thời gian khi thực hiện các thao tác với thư mục (Như duyệt toàn bộ)

> [!note] Bảng băm/Bảng băm với DS tuyến tính
> ![[tinywow_Screenshot 2023-01-17 003914_11697080.png]]
> * Giảm thời gian duyệt thư mục (tốc độ nhanh)
> * Đòi hỏi có một hàm băm hiệu quả
> ![[Pasted image 20230117004119.png]]
> * Hàm băm trả về cùng 1 kết quả với hai tên file khác nhau -> **đụng độ**
> * Khi tăng kích thước cần tính toán lại những phần đã tồn tại -> **vấn đề kích thước cố định**

### Các pp phân phối vùng lưu trữ
> [!question] Tại sao cần phân phối vùng lưu trữ?
> * Tăng hiệu năng truy nhập tuần tự 
> * Dễ dàng truy nhập ngẫu nhiên tới file
> * Dễ dàng quản lý file

> [!abstract] Các phương pháp phân phối vùng lưu trữ
> * [[Chap4 - Quản lý hệ thống file#Phân phối liên tục (Continuous Allocation)]]
> * [[Chap4 - Quản lý hệ thống file#Phân phối liên kết (Linked List Allocation)]]
> * [[Chap4 - Quản lý hệ thống file#Phân phối chỉ mục (Indexed Allocation)]]

#### Phân phối liên tục (Continuous Allocation)
> [!tip] Nguyên tắc
>  File được phân phối các khối nhớ liên tiếp nhau
  
![[Pasted image 20230117004808.png]]
* File có độ dài n và bắt đầu ở khối b sẽ chiếm các khối từ b -> (b + n-1)
	* Do các khối liên tiếp nhau -> không phải dịch chuyển đầu từ khi đọc (trừ sector cuối) -> **Tốc độ truy cập nhanh**
	* Cho phép truy cập trực tiếp khối i của file -> **Truy nhập khối b + i - 1** trên thiết bị lưu trữ
* Lựa chọn vùng trống khi có yêu cầu lưu trữ:
	* Các chiến lược First-Fit, Worst-Fit, Best-Fit
	* Khả năng xảy ra hiện tượng phân đoạn ngoài

> [!fail] Nhược điểm
> Khó khăn khi muốn tăng kích thước của file

#### Phân phối liên kết (Linked List Allocation)
> [!tip] Nguyên tắc
> File được phân phối các khối nhớ không liên tục. Cuối mỗi khối là con trỏ, trỏ tới khối tiếp theo

![[Pasted image 20230117210543.png]]
File abc gồm 7 khối: 12, 10, 7, 14, 15, 2, 3
File def gồm 5 khối: 5, 6, 8, 9, 11

* Chỉ áp dụng hiệu quả cho các file **truy nhập tuần tự**
> [!note] Các hạn chế
> * Để truy nhập khối thứ n, phải duyệt qua (n -1) khối trước đó
> 	* Nếu các khối không liên tục, phải định vị từ đầu
> 	-> **Tốc độ truy nhập chậm**
> * Các khối trong file được liên kết bởi con trỏ, khi con trỏ bị lỗi:
> -> Bị **mất dữ liệu** do mất liên kết tới khối
> -> Liên kết tới **khối không có dữ liệu** hoặc khối của file khác

* Có thể sử dụng nhiều con trỏ trong mỗi khối **-> Tốn bộ nhớ**

#### Phân phối chỉ mục (Indexed Allocation)
> [!tip] Nguyên tắc
> Mỗi file có một khối chỉ mục đích (index block) chứa danh sách các khối dữ liệu của file.
> 

![[Pasted image 20230118235452.png]]
* File abc có index block là 5, chứa ds các khối dữ liệu: 2, 4, 8, 9, 11,  15
* File def có index block là 12, chứa ds các khối dữ liệu 10, 13

* Phần tử thứ i của khối chỉ mục trỏ tới khối thứ i của file
	* Đọc khối i dùng con trỏ được ghi tại phần tử i của khối chỉ mục
* Khi tạo file, các phần tử của khối chỉ mục có giá trị null (-1)
* Khi cần thêm khối i, đưa địa chỉ khối được cấp vào phần tử i

> [!check] Ưu điểm
> * Không gây hiện tượng phân đoạn ngoài
> * Cho phép truy nhập trực tiếp

> [!fail] Nhược điểm 
> * Luôn cần khối chỉ mục: file có kích thức nhỏ vẫn cần 2 khối (Khối cho dữ liệu và khối chứa ds chỉ mục)

> [!warning] Vấn đề về kích thước file có thể lưu trữ
> **=> ✅Giải pháp:**
> * ***Sơ đồ liên kết***:
> 	* Liên kết các khối chỉ mục lại: phần tử cuối của khối chỉ mục trỏ tới khối chỉ mục khác nếu cần
> * ***Index nhiều mức***: 
> 	* Dùng một khối chỉ mục trỏ tới các khối chỉ mục khác.

![[Pasted image 20230119000704.png]]
	
### Quản lý vùng lưu trữ tự do
> [!note] Bit vector
> * Mỗi block thể hiện bởi 1 bit (1: free, 0: allocated)
> * Dễ dàng tìm ra n khối nhớ liên tục
> * Cần có lệnh cho phép làm việc với bit

> [!note] DS liên kết (Link List)
> * Lưu giữ con trỏ tới khối đĩa trống đầu tiên
> * Khối nhớ này chứa con trỏ trỏ tới khối đĩa trống tiếp theo
> * Không hiệu quả khi duyệt danh sách

> [!note] Nhóm (Grouping)
> * Lưu trữ địa chỉ n khối tự do trong khối tự do đầu tiên
> * n -1 khối đầu tự do, khối n chứa địa chỉ của n khối tự do tiếp
> * Có khả năng tìm vùng nhớ tự do nhanh chóng

> [!note] Bộ đếm (Counting)
> * Do các khối nhớ liên tục được cung cấp và giải phóng đồng thời
> * Lưu địa chỉ khối nhớ tự do đầu tiên và kích thước vùng nhớ liên tục trong DS quản lý vùng trống
> * Hiệu quả khi bô đếm lớn hơn 1

## 3. Tổ chức thông tin trên đĩa từ 
*Chỉ học phần đĩa cứng*
### 3.1 Cấu trúc vật lý của đĩa

### 3.2 Cấu trúc logic của đĩa
> [!note] Đĩa cứng - dung lượng lớn 
> * Được chia thành nhiều phân vùng (Partitions, Volumes ...)
> 	* Mỗi vùng là tập hợp các Cylinder liên tiếp nhau
> 	* Người dùng ấn định kích thước (dùng `fdisk`)
> * Mỗi phân vùng có thể được quản lý bởi 1 HĐH riêng
> 	* HĐH format phân vùng theo định dạng được sử dụng
> 	* Tồn tại nhiều hệ thống khác nhau: FAT, NTFS, EXT3
> * Trước tất cả các phân vùng là các sector bị che
>	* ***Master Boot Record - MBR***: Sector đầu tiên của đĩa.
>
>![[Pasted image 20230127211910.png]]

> [!info] Master Boot Record
> * là Sector quan trọng nhất
> * Là sector đầu tiên trên đĩa (địa chỉ = <0,0,1>)
> * Cấu trúc gồm 3 phần:
> 	* CT nhận biết
> 	* Bảng phân chương
> 	* Chữ ký hệ thống (luôn là 55AA)

## 4. Hệ thống FAT (File Allocation Table)

> [!note] Cấu trúc phân vùng cho FAT
> * FAT 12/16:
> 	* Số cluster lớn nhất: FAT12 (2^12 - 18), FAT16 (2^16 - 18)
> 	* Kích thước max: FAT12 - 32MB; FAT16 - 2GB/4GB (32K/64K Cluster)
> * FAT32:
> 	* Chỉ dùng 28 bit => Số cluster 2^28 - 18

### 4.1 Boot Sector

### 4.2 File Allocation Table

### 4.3 Thư mục gốc