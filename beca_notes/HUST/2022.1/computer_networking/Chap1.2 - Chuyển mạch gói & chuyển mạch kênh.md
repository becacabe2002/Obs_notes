## Vấn đề
* Xét kết nối điểm - điểm giữa 2 host, có các thông số:
	* ***Băng thông*** (Bandwith): lượng dữ liệu truyền tối đa trong 1 đơn vị thời gian (bps)
	* ***Trễ*** (Latency): thời gian truyền liệu từ A -> B

*  Xét kết nối điểm - đa điểm: sử dụng 1 đường truyền chung cho tất cả (truyền quảng bá - broadcast)

### 👉Giải pháp: mạng chuyển mạch (switch)
* Mỗi host kế nối với ***1 thiết bị chuyển mạch***

* Thiết bị chuyển mạch kết nối điểm-điểm và thực hiện chuyển tiếp dữ liệu tới đích

* Chia sẻ tài nguyên đường truyền

![[chap1_switch.png]]

## Chuyển mạch kênh
> Cấp phát tài nguyên đường truyền (kênh) dành riêng cho từng kết nối logic giữa 2 nút mạng

![[chap1_circuit_switching.png]]

![[chap1_gian_do.png]]

### 🟢 Ưu điểm
* Kênh được thiết lập sẵn -> **Trễ khi chuyển mạch thấp**

* Tài nguyên dành riêng cho kênh và không đổi trong quá trình truyền -> **Đảm bảo chất lượng dịch vụ**

### 🔴 Nhược điểm

***Kênh 'trắng'***

![[Pasted image 20221027164628.png]]

***Kênh 'bé'***

![[Pasted image 20221027164643.png]]

***Lỗi kênh truyền***
* Bắt đầu lại toàn bộ quá trình thiết lập kênh truyền nếu có lỗi xảy ra trên thiết bị chuyển mạch khi truyền.

![[Pasted image 20221027164800.png]]

### Ghép kênh/Phân kênh
*Muốn nhiều kênh truyền dữ liệu trên 1 kênh liên kết vật lý*

 ![[Chap1_multiplexing_demultiplexing.png]]
 ***Ghép kênh*** (Multiplexing)
 > Gửi dữ liệu của nhiều kênh khác nhau trên cùng 1 liên kết vật lý
 
 ***Phân kênh*** (Demultiplexing)
 > Phân dữ liệu nhận được trên liên kết vật lý vào các kênh tương ứng và chuyển đến đúng đích 

### Một số kỹ thuật ghép kênh
* ***Ghép kênh theo thời gian*** (TDM): mỗi kết nối sử dụng tài nguyên  trong khe thời gian được phân

* ***Ghép kênh theo tần số*** (FDM): mỗi kết nối sử dụng một băng tần tín hiệu riêng

![[Pasted image 20221027165855.png]]

## Chuyển mạch gói
> Chia dữ liệu thành các gói:
> - **Header**: địa chỉ, số thứ tự
> - **Payload data**

* Thiết bị chuyển mạch chuyển tiếp gói tin dựa trên tiêu đề

* Mỗi gói tin có thể được **xử lý độc lập**
	* Các gói tin có thể tới đích theo các đường khác nhau, ko còn đúng thứ tự

* Tài nguyên **dùng chung** cho tất cả các kết nối, nếu còn thì bất cứ nút nào cũng có thể sử dụng.

![[Chap1.2_chuyen_mach_goi.png]]


### Giản đồ thời gian

![[Pasted image 20221030233544.png]]

* Thiết bị chuyển mạch chỉ chuyển tiếp khi nhận được đầy đủ gói tin. (Store and forward)

* Thiết bị chuyển mạch cần thời gian để xử lý gói tin (d_proc):
	* Kiểm tra lỗi trên gói tin
	* Quyết định gói tin gửi đến đâu
	* d_proc thường rất nhỏ so với trễ truyền tin
![[Chương 1 - Tổng quan.pptx-66-73.pdf]]

### Ưu điểm
* Không mất tgian thiết lập kênh truyền
* Hiệu suất sử dụng đường truyền cao hơn