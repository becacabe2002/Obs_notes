## Internet & Lịch sử phát triển

## Các khái niệm mạng máy tính
### Mạng máy tính
> Tập hợp các "máy tính" kết nối với nhau dựa trên 1 kiến trúc để có thể trao đổi dữ liệu

### Giao thức mạng (Protocol)
>Quy tắc để truyền thông 
> - Gửi một yêu cầu hoặc thông tin
> - Nhận một thông tin hoặc yêu cầu hành động
> - Các yêu cầu, thông tin được gửi dưới dạng các thông điệp

* Định nghĩa
	* Khuôn dạng dữ liệu, thông điệp
	* Thứ tự truyền, nhận thông điệp giữa các thực thể trên mạng
	* Các hành động tương ứng khi nhận được thông điệp

VD: TCP, UDP, IP, HTTP, Telnet, SSH, ...

### Đường truyền vật lý
> Các phương tiện vật lý có khả năng truyền dẫn tín hiệu

* **Phân loại**:
	* Hữu tuyến: Cáp xoắn, cáp đồng trục ...
	* Vô tuyến: các loại sóng điện (radio, hồng ngoại)

* Thông số đặc trưng:
	* ***Băng tần***: độ rộng tần số tín hiệu có thể truyền đi
		* = Tần số lớn nhất (f_max) - Tần số bé nhất (f_min)
	
	* ***Tỉ lệ lỗi khi truyền*** (BER - Bit Error Rate/Ratio)
	
	* ***Độ suy hao***: mức suy giảm tín hiệu khi truyền

### Kiến trúc mạng
> Định nghĩa các nút mạng kết nối với nhau ntn (Hình trạng - Topology) và trao đổi dữ liệu với nhau ntn ([[Chap1.1 - Cơ bản về mạng máy tính#Giao thức mạng (Protocol)]] - Protocol)

* ***Topology vật lý***: hịnh trạng dựa trên cáp kết nối

![[chap1_topology.png]]

* ***Topology logic***: hình trạng dựa trên cách thức truyền tín hiệu
	* Điểm - Điểm
	* Điểm - Đa điểm

### Phân loại mạng máy tính
* ***Cá nhân*** (PAN - Personal Area Network)
	* Vài chục mét
	* Một vài người dùng
	* Phục vụ cá nhân

* ***Cục bộ*** (LAN - Local Area Network)
	* vài kilomét
	* Một vài tới hàng trăm nghìn người dùng
	* Phục vụ cá nhân, hộ gđ, tổ chức 

* ***Đô thị*** (MAN - Metropolitian Area Network)
	* hàng trăm km
	* hàng triệu người dùng
	* Phục vụ thành phố, khu vực

* ***Diện rộng***
	* Vài nghìn km
	* hàng tỉ người dùng
	* Phạm vi toàn cầu (Internet)

## Kiến trúc mạng
### Kiến trúc Internet

![[chap1_internet.png]]

* Kết nối mỗi mạng vào một ***trạm chuyển tiếp*** của một nhà cung cấp toàn cầu (global ISP)
* Các ISP được kết nối bằng các ***Trạm trung chuyển Internet*** (IXP), và được coi là các **kết nối ngang hàng**
* Các mạng khu vực (regional net) kết nối vào các ISP

***Mạng biên*** (Network edge)
* Nút mạng đầu cuối (end-system, host): PC, điện thoại, máy chủ, máy tính nhúng
*  Mạng truy cập (access network): đường truyền, thiết bị kết nối (Router, switch, hub, ...)

***Mạng lõi*** (Network core):
> Đường truyền, thiết bị kết nối

* Mạng của các mạng