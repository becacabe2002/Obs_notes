## 1. Tổng quát về tầng liên kết dữ liệu
### Tầng liên kết dữ liệu trên mô hình TCP/IP
![[Pasted image 20221117152208.png]]
### Triển khai trên hệ thống mạng
* Điều khiển truyền dữ liệu trên liên kết vật lý giữa 2 nút mạng kế tiếp

* Triển khai trên mọi nút mạng

* Các thức triển khai và cung cấp dịch vụ phụ thuộc vào đường truyền (WiFi, Wimax, 3G, cáp quang, cáp đồng...)

* Truyền thông tin cậy (cơ chế giống TCP nhưng đơn giản hơn) hoặc ko

* Đơn vị truyền: frame (khung tin)
![[Pasted image 20221117152529.png]]

### Triển khai trên các nút mạng
> [!note] 
> Tầng LK dữ liệu được đặt trên **NIC (Network Interface Card)** hoặc trên chip tích hợp

* Cùng với tầng vật lý

* NIC được kết nối với hệ thống bus

### Các chức năng chính
**Đóng gói**
 * Đơn vị dữ liệu: khung tin (frame)
 * Bên gửi: thêm phần đầu cho gói tin nhận được tầng mạng
 * Bên nhận: bỏ phần đầu, chuyển lên tầng mạng

**Địa chỉ hoá**
* Sử dụng địa chỉ MAC

**Điều khiển truy cập đường truyền**
* Cần có giao thức điều khiển đa truy nhập với mạng đa truy cập

**Kiểm soát luồng**
* Đảm bảo bên nhận ko bị quá tải

**Kiểm soát lỗi**
* Phát hiện và sửa lỗi bit trong các khung tin 

> [!note] Chế độ truyền
> * ***Simplex (Đơn công)***
> 	* Mỗi thiết bị trên liên kết vật lý chỉ thực hiện 1 chức năng (Phát tín hiệu hoặc thu tín hiệu).
> 	* Ví dụ: hệ thống truyền hình tương tự, truyền thanh
> * ***Half-duplex (Bán song công)***
> 	* Mỗi thiết bị bên liên kết vật lý có 2 chức năng **phát** và **thu**, nhưng chỉ thực hiện 1 chức năng tại mỗi thời điểm.
> 	* Ví dụ: truyền thông bằng bộ đàm.
> * ***Full-duplex (Song công đầy đủ)***
> 	* Mỗi thiết bị trên liên kết vật lý có thể phát và thu đồng thời.
> 	* Ví dụ: truyền thông trong hệ thống mạng, hệ thống điện thoại.

### Định danh: địa chỉ MAC
* Địa chỉ MAC: 48 bit, được quản lý bởi IEEE
* Mỗi cổng mạng được gán một MAC
	* Không thể thay đổi địa chỉ vật lý
* Không phân cấp, có tính di động
	* Không cần thay đổi địa chỉ MAC khi host chuyển sang mạng khác
* Địa chỉ quảng bá trong mạng LAN:
FF-FF-FF-FF-FF-FF

## 2. Kiểm soát lỗi
### Nguyên lý phát hiện lỗi
![[Pasted image 20221117162050.png]]

### Mã chẵn lẻ (parity)
* **Mã đơn**: 
	* Phát hiện lỗi bít đơn 
	* Không phát hiện nếu nhiều hơn 1 bit lỗi
	![[Pasted image 20221117163507.png]]

* **Mã hai chiều**:
	* Phát hiện và sửa lỗi bit đơn
![[Pasted image 20221117163710.png]]

### Mã Checksum

## 3. Kiểm soát luồng

## 4. Điều khiển truy nhập đường truyền

## 5. Chuyển tiếp dữ liệu

## 6. Mạng cục bộ (LAN)

## 7. Mạng diện rộng (WAN)