## 2.1 Giới thiệu
[[Chap1 - Tổng quan#Tiến trình và luồng]]
> [!info] Luồng
> Là đơn vị sử dụng CPU cơ bản, gồm:
> * ID Thread
> * Program Counter
> * Registers
> * Không gian Stack

* Chia sẻ cùng các luồng khác trong cùng 1 TT
	* Đoạn mã lệnh
	* Đoạn dữ liệu (đối tượng toàn cục)
	* Các tài nguyên HĐH khác (file đang mở)

> [!note]
> Các luồng có thể thực hiện **cùng đoạn mã** nhưng với **ngữ cảnh** (Registers, PC, Stack) **khác nhau**.

> ***TT nhẹ (Lightweight Process)*** - TT có ít nhất là 1 luồng

### Tiến trình >< Luồng
|Tiến trình|Luồng|
|:---|:---|
|TT có đoạn mã/dữ liệu/heap và các đoạn khác nhau|Luồng không có đoạn dữ liệu hay heap riêng|
|Phải có ít nhất 1 luồng trong mỗi TT|Luồng không đứng riêng mà nằm trong 1 TT|
|Các luồng trong phạm vi 1 TT chia sẻ mã/dữ liệu/heap, vào/ra nhưng có stack và tập thanh ghi riêng|Có thể tồn tại nhiều luồng trong mỗi TT. <br>Luồng đầu là luồng chính và sở hữu không gian stack của TT|
|Thao tác khởi tạo, luân chuyển TT tốn kém|Thao tác khởi tạo, luân chuyển luồng ko tốn kém|
|Bảo vệ tốt do có không gian địa chỉ riêng|Không gian địa chỉ chung, cần phải bảo vệ|
|Khi TT kết thúc, các tài nguyên được đòi lại, các luồng phải kết thúc theo nó.|Luồng kết thúc, Stack được thu lại.|

> [!check]- Lợi ích của lập trình đa luồng
> - **Tăng tính đáp ứng với người dùng**
> 	- Cho phép  TT vẫn thực hiện ngay khi 1 phần đang chờ đợi (block) hoặc đang thực hiện tính toán tăng cường (lengthy operation)
> - **Chia sẻ tài nguyên**
> 	- Các luồng chia sẻ bộ nhớ và tài nguyên của TT chứa nó
> 		- Tốt cho các thuật toán song song (sử dụng chung các CTDL)
> 		- Trao đổi giữa các luồng thông qua bộ nhớ dùng chung
> - **Tính kinh tế**
> 	- Các thao tác khởi tạo, huỷ bỏ và luân chuyển luồng ít tốn kém
> 	- Minh hoạ được tính song song trên bộ đơn VXL do thời gian luân chuyển CPU nhanh 
> - **Sử dụng kiến trúc nhiều vi xử lý**
> 	- Các luồng chạy song song thực sự trên các bộ VXL khác nhau.

### Cài đặt luồng
#### Luồng người dùng (User - level threads)
![[Pasted image 20221117101921.png]]

> [!note]
> - Quản lý các luồng được thực hiện bởi **chương trình ứng dụng**
> 
> - Nhân hệ thống không biết gì về sự tồn tại luồng
> 	- Điều phối TT như 1 đơn vị duy nhất
> 	- Gán cho mỗi TT 1 tr/thai duy nhất (Ready - Waiting - Running)
> 
> - Chương trình ứng dụng được lập trình theo mô hình đa luồng được hỗ trợ bởi **thư viện luồng**.

* Thư viện: POSIX Pthreads, Mach C-threads, Solaris 2 UI-threads, Win32 threads

> [!check] Advantages
> Nhanh chóng trong việc tạo và quản lý luồng

> [!failure]  Disadvantages
> * Khi một luồng rơi vào tr/thai chờ đợi, tất cả các luồng trong cùng 1 TT cũng bị chờ đợi theo.
> * Không tận dụng được ưu điểm của mô hình tập trung đa luồng.

#### Luồng mức hệ thống (Kernel - level threads)
![[Pasted image 20221117103641.png]]

> [!note] 
> * Nhân duy trì thông tin về TT và các luồng
> * Quản lý luồng được thực hiện bởi nhân
> 	* Không tồn tại các mã quản lý luồng trong ứng dụng
> 	* Điều phối luồng được thực hiện bởi nhân, dựa trên các luồng

* HĐH: Windows NT/2000/XP, Linux, OS/2,..

> [!check] Advantages
> * Một luồng chờ đợi vào ra, không ảnh hưởng tới luồng khác
> * Trong môi trường đa VXL, nhân có thể điều phối các luồng cho các VXL khác nhau.

> [!failure] Disadvantage
> Chậm trong tạo và quản lý luồng

## 2.2 Mô hình đa luồng
*Nhiều hệ thống hỗ trợ cả luồng mức người dùng và luồng mức hệ thống -> có nhiều mô hình đa luồng khác nhau*
![[Pasted image 20221117121625.png]]

### Mô hình nhiều - một
> [!info] 
> Ánh xạ nhiều luồng mức người dùng -> 1 luồng mức hệ thống

* Quản lý luồng được thực hiện trong không gian người dùng
	* Hiệu quả
	* Cho phép tạo nhiều luồng tuỳ ý
	* Toàn bộ TT sẽ bị khoá nếu 1 luồng bị khoá

* Không thể chạy song song trên các máy nhiều VXL ( **Chỉ 1 luồng có thể truy cập nhân tại 1 thời điểm**)

* Dùng trong HĐH không hỗ trợ luồng hệ thống

![[Pasted image 20221118084435.png]]

### Mô hình một - một
![[Pasted image 20221118084536.png]]

> [!info]
> Ánh xạ mỗi luồng mức người dùng -> 1 luồng hệ thống

* Cho phép **thực hiện luồng khác** khi **1 luồng bị chờ đợi**.

* Cho phép **chạy song song đa luồng** trên máy tính nhiều vi xử lý

> [!caution] 
> Tạo luồng mức người dùng đòi hỏi tạo 1 luồng mức hệ thống tương ứng
> * Ảnh hưởng tới hiệu năng của ứng dụng 
> * Chi phí cao => Giới hạn số luồng được hệ thống hỗ trợ.

### Mô hình nhiều - nhiều
![[Pasted image 20221118085834.png]]
> [!info]
> Nhiều luồng mức người dùng ánh xạ tới một số nhỏ luồng mức hệ thống.

* Số lượng luồn nhân có thể được xác định theo máy hoặc theo ứng dụng. (*VD: được cấp nhiều luồng nhân hơn trên hệ thống nhiều VXL*)

> [!check] Có được ưu điểm của 2 mô hình trên
> * Cho phép tạo nhiều luồng mức ứng dụng theo yêu cầu
> * Các luồng nhân tương ứng có thể chạy song song trên hệ nhiề VXL
> * 1 luồng bị khoá, nhân có thể cho phép luồng khác thực hiện.

### Cơ chế kích hoạt bộ điều phối (Schedular activation)
> [!note]
> Cách thức để **kernel** liên lạc với trình quản lý luồng mức user để **duy trì số lượng luồng mức nhân** hợp lý được phân phối cho TT

![[Pasted image 20221118092119.png]]

### Mô hình 2 mức (two-level)
* Kết hợp nhiều - nhiều và một - một

* Ưu tiên một số luồng cần được phục vụ nhiều hơn.
![[Pasted image 20221118092223.png]]

## 2.3 Cài đặt luồng với Windows
## 2.4 Vấn đề đa luồng

![[Hệ Điều Hành-Chuong 2-88-95.pdf]]
