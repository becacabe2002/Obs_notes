## 1. Nguyên tắc quản lý chung
### Giới thiệu
> [!note] Thiết bị vào ra
> * Trên quan điểm kỹ thuật: các thiết bị với bộ VXL, Monitor, các linh kiện khác
> * Trên quan điểm lập trình: Giao diện như phần mềm để nhận lệnhm thực hiện và trả kết quả về

* Phân loại thiết bị ngoại vi:
	* **Khối** (Đĩa từ, băng từ):
		* Thông tin được lưu trữ có kích thước cố định và địa chỉ riêng
		* Có thể đọc ghi 1 khối độc lập với khối khác:
			* Tồn tại thao tác định vị thông tin (seek)
	* **Ký tự** (Máy in, bàn phím, chuột):
		* Chấp nhận luồng ký tự, không có cấu trúc khối
		* Không có thao tác định vị thông tin
	* Loại khác: Đồng hồ

* Thiết bị ngoại vi (TBNV) đa dạng và nhiều loại -> Không tồn tại tín hiệu riêng cho từng thiết bị
* CPU ko điều khiển trực tiếp thiết bị:
	* TBNV được nối với hệ thống qua thiết bị điều khiển (Device Controller), các mạch điện tử được cắm trên các slot của mainboard máy tính

> [!note] Thiết bị điều khiển
> * Mỗi TBĐK có thể điều khiển được nhiều TBNV, tuỳ theo số giắc cắm có trên TBDK.
> 	* Nếu giao diện điều khiển chuẩn (ANSI, IEEE, ISO, ...) có thể nối tới nhiều thiết bị khác.
> * Mỗi TBĐK có các thanh ghi riêng để làm việc với CPU
> 	* Dùng các không gian địa chỉ đặc biệt cho các thanh ghi: cổng vào ra.

![[Pasted image 20230127213741.png]]

* Nhưng giao diện TBĐK - TBNV là giao diện mức rất thấp

* HĐH chỉ làm việc với các TBĐK:
	* Thông qua các thanh ghi điều khiển của thiết bị
	* Các câu lệnh và tham số sẽ được đưa vào các thanh ghi điều khiển
	* Khi 1 lệnh được bộ điều khiển chấp nhận, CPU sẽ để cho bộ điều khiển hoạt động một mình và nó quay sang làm task khác.
	* Khi thực hiện lệnh xong, bộ điều khiển báo CPU bằng tín hiệu ngắt.
	* CPU sẽ lấy result và trạng thái thiết bị thông qua các thanh ghi điều khiển.

> [!info] Trình điều khiển thiết bị - Device Driver
> Đoạn mã trong nhân của hệ thống cho phép tương tác trực tiếp với phần cứng thiết bị.
> * Cung cấp 1 giao diện chuẩn cho các TBNV khác nhau.

* Các device driver thường được chia làm 2 mức:
	* **Mức cao**: được truy nhập qua các lời gọi hệ thống
		* Cài đặt tập lời gọi chuẩn (`open()`, `close()`,...)
		* Là giao diện của nhân OS với driver
		* Luồng mức cao khởi động thiết bị thực hiện vào/ra và sau đó đặt luồng điều khiển tạm nghỉ

	* **Mức thấp**: được thực hiện như 1 thủ tục ngắt
		* Đọc dữ liệu đầu vào, hoặc đưa khối dữ liệu tiếp theo ra ngoài
		* Đánh thức luồng tạm nghỉ mức trên khi vào/ra dữ liệu

> [!note] Chu kì của một yêu cầu vào ra
> ![[Pasted image 20230127225655.png]]

#### Giao tiếp thiết bị ngoại vi và OS
* Sau khi OS gửi yêu cầu ra TBNV, OS cần phải biết liệu:
	* TBNV hoàn thành yêu cầu vào ra hoặc gặp lỗi
-> Có thể thực hiện bằng 2 pp: ***Ngắt*** hoặc ***thăm dò*** 

* ***Ngắt***:
	* TBNV phát tín hiệu ngắt báo cho CPU biết
	* IRQ - dường dẫn vật lý đến bộ quản lý ngắt
		* Ánh xạ các tín hiệu IRQ thành các vector ngắt
		* Gọi tới chương trình xử lý ngắt
* ***Thăm dò***:
	* OS kiểm tra theo chu kỳ thanh ghi trạng thái của thiết bị

> [!warning] 
> Lãng phí chu kỳ thăm dò nếu thao tác vào ra ko thường xuyên

> [!check] Kết hợp cả 2 pp
> * Ngắt khi gói tin đầu tiên tới
> * Thăm dò với các gói tin tiếp theo cho tới khi vùng đệm rỗng

#### Ngắt và xử lý ngắt
> [!info] Ngắt
> * Hiện tượng dừng đột xuất chương trình để thực hiện sang chương trình khác ứng với một sự kiện nào đó.
> 
>-> Ngắt là phương tiện thông báo cho CPU biết trạng thái của các thiết bị trong hệ thống

* Phân loại:
	* Nguồn gốc: Trong - ngoài
	* Thiết bị: cứng - mềm
	* Khả năng quản lý: Che được - Ko che được
	* Thời điểm ngắt: yêu cầu - báo cáo

> [!note] Xử lý ngắt
> 1. Ghi nhận đặc trung sự kiện gây ngắt vào ô nhớ cố định
> 
> 3. Ghi nhận trạng thái của tiến trình bị ngắt
> 4. Chuyển địa chỉ của prog xử lý ngắt vào thanh ghi PC
> 5. Thực hiện chương trình xử lý ngắt
> 6. Khôi phục lại tiến trình bị ngắt

## 2. Dịch vụ vào ra của hệ thống
### Vùng đệm - Buffer
> [!bug] Vấn đề đặt ra 
> * TBNV hoạt động chậm:
> 	* Khi kích hoạt thiết bị
> 	* Khi chờ đợi thiết bị đạt được trạng thái hđ thích hợp
> 	* Chờ đợi các thao tác vào ra được thực hiện


 * Để đảm bảo hiệu năng của toàn hệ thống, cần:
	* Giảm số lượng thao tác vào ra, làm việc với từng khối dữ liệu
	* Thực hiện song song thao tác vào ra với các thao tác khác
	* Thực hiện trước khác phép truy nhập

> [!check] Vùng đệm
> là vùng nhớ trung gian, lưu trữ thông tin các thao tác vào ra.

#### Phân loại
* Trạng thái vào ra:
	* Vùng đệm **vào**:
		* Có thể thực hiện ngay phép truy nhập dữ liệu
	* Vùng đệm **ra**:
		* Thông tin được đưa ra vùng đệm, khi vào vùng đệm đầy sẽ đưa vào thiết bị
* Đối tượng:
	* Vùng đệm **gắn với thiết bị**:
		* Được xây dựng khi mở TB hoặc file
		* Phục vụ riêng cho TB
		* Bị xoá khi đóng TB
		* *Thích hợp khi các TB có cấu trúc bản ghi vật lý khác nhau*
	* Vùng đệm **gắn với hệ thống**:
		* Xây dựng khi khởi tạo hệ thống, ko gắn với TB cụ thể
		* Tồn tại trong suốt quá trình hoạt động của hệ thống
		* Một vùng đệm có sẵn sẽ được gán khi mở file hoặc TB 
		* Vùng đệm được trả lại khi đóng file hoặc thiết bị
		* *Thích hợp khi các TB có cấu trúc bản ghi vật lý chung*
		* Tránh được việc phải xoá vùng đệm nhiều lần
		* Nhưng khi đó, vùng đệm sẽ trở thành **tài nguyên găng** và cần phải được điều độ
* Phân cấp:
	* Vùng đệm trung chuyển = vùng đệm vào + vùng đệm ra
	* Vùng đệm xử lý
	* Vùng đệm vòng tròn = vùng đệm trung chuyển + vùng đệm xử lý

### Quản lý lỗi vào ra
> [!warning] 
> Lỗi luôn có thể xảy ra tại mọi bộ phận của hệ thống, và việc xử lý lõi là trách nhiệm của hệ thống.

* Khi phát hiện lỗi, hệ thống khắc phục bằng cách thực hiện lại nhiều lần.

* Nếu lỗi ổn định -> Khôi phục lại thông tin ban đầu.

* Trường hợp lưu trữ, để đảm bảo chất lượng thông tin
	* TBĐK đọc kết quả vừa lưu trữ:
		* So sánh với thông tin gốc/so sánh 2 tổng kiểm tra
		* Kết quả báo cho hệ thống để có thể xử lý tương ứng
		=> Lặp lại thao tác hoặc thông báo lỗi

* Phân tích và đánh giá dựa trên mã trả về của TB vào ra

### Kỹ thuật SPOOL
* Trên phương diện lập trình, TB vào ra là trạm nhận các yêu cầu từ chương trình và thực hiện chúng. Chúng trả các mã trạng thái để hệ thóng phân tích.
-> Có thể dùng phần mềm để mô phỏng các TB vào ra.

* TB vào ra có thể coi như tiến trình, được điều độ theo quy tắc quản lý TT

> [!note] Mục đích
> * Mô phỏng quá trình điều khiển, quản lý thiết bị ngoại vi
> 	* Kiểm tra hoạt động của các thiết bị đang chế tạo
> * Tạo hiệu ứng sử dụng song song cho các thiết bị truy nhập tuần tự

![[Pasted image 20230128004423.png]]

## 3. Hệ thống vào ra của đĩa
### 3.1 Cấu trúc đĩa từ
> [!note] Cấu trúc của đĩa từ
> ![[Pasted image 20230128004533.png]]
> * Mô hình hoá như mảng một chiều các khối logic
> 	* Khối logic là đơn vị trao đổi nhỏ nhất
> * Ánh xạ liên tiếp các khối logic tới các sector của đĩa
> 	* Khối 0 là sector đầu 0 rãnh/Cylinder ngoài cùng
> 		* Ánh xạ theo trật tự: Sector -> Header -> Track/Cylinder
> 	* Ít phải dịch chuyển đầu từ khi đọc các sector kế tiếp nhau

#### Vấn đề truy nhập đĩa
* OS phải sử dụng hiệu quả phần cứng
	* Ở đây, đĩa phải được truy cập nhanh và có băng thông cao

> [!note] Băng thông
> $= Exchanged\_bytes/time$

> [!note] Thời gian truy nhập
> $= Seek\_time + Rotational\_latency$
>* ***Seek time*** - tgian dịch chuyển đầu từ tới cylinders chứa sector cần truy nhập
> *  ***Rotational latency*** - tgian chờ đợi để đĩa quay tới sector cần truy nhập

=> Giảm thiểu tới mức tối đa thời gian định vị (tương đương với khoảng cách dịch chuyển)

### 3.2 Điều phối truy nhập đĩa
> [!bug] Vấn đề đặt ra
> Hàng đợi các yêu cầu truy nhập
> * Khi đĩa và bộ điều khiển:
> 	* Sẵn sàng -> yêu cầu được thực hiện
> 	* Chưa ss -> yêu cầu được đặt trong hàng đợi
> * Khi hoàn thành 1 y/c truy nhập -> yêu cầu tiếp theo ?

> [!check] Giải pháp
> Các thuật toán điều phối dịch vụ yêu cầu vào ra đĩa:
> * First Come First Served - FCFS
> * Shortest Seek Time First - SSTF
> * SCAN
> * C-SCAN (Circular SCAN)
> * LOOK/C-LOOK

* Đầu đọc ở Cylinder 53:
* Theo FCFS:
![[Pasted image 20230128011433.png]]

=>Quá tốn tgian

> [!note] Shortest Seek Time First
> Chọn truy nhập có tgian định vị từ vị trí hiện tại nhỏ nhất.

![[Pasted image 20230128011508.png]]

> [!warning] 
> Có thể tồn tại yêu cầu phải đợi vô hạn do y/c mới xuất hiện gần đầu đọc hơn.

> [!note] SCAN
> Đầu từ dịch chuyển từ Cylinder ngoài cùng đến Cylinder trong cùng và quay ngược lại, các yêu cầu được bắt gặp trên đường đi được phục vụ

![[Pasted image 20230128011705.png]]

> [!note] C-SCAN
> Xử lý các cylinders như một danh sách nối vòng: Cylinder ngoài cùng nối tiếp với cylinder trong cùng

* Đầu từ d/chuyển từ cylinder ngoài cùng -> cylinder trong cùng
	* Phục vụ cho các y cầu gặp trên đường đi
* Khi tới Cylinder trong cùng, quay ngược lại Cylinder ngoài cùng
	* Không phục vụ cho các y cầu gặp trên đường đi

![[Pasted image 20230128011845.png]]

* Thu được thời gian đợi **đồng nhất hơn** SCAN
* Khi đầu đọc đạt tới 1 phía của đĩa (Cylinder trong cùng hoặc ngoài cùng), mật độ các yêu cầu xuất hiện ở phía đối diện lớn hơn vị trí hiện tại
* Các yêu cầu ở phía đối diện cũng có tgian đợi lâu hơn, cần quay về lập tức.

> [!note] LOOK/C-LOOK
> Tương tự SCAN/C-SCAN nhưng thay vì đi tới Cylinder ngoài cùng, đầu từ chỉ đi tới các yêu cầu xa nhất về 2 phía

![[Pasted image 20230128012142.png]]

#### Vấn đề lựa chọn thuật toán
* SSTF phổ biến và hiệu quả hơn FCFS

* SCAN/C-SCAN hoạt động tốt hơn trên hệ thống có nhiều yêu cầu truy nhập đĩa, tránh được tình trạng đói (starvation)

* Hiệu quả của các thuật toán phụ thuộc vào số lượng và các kiểu yêu cầu.

* Các pp phân phối đĩa cho file có ảnh hưởng tới yêu cầu truy xuất đĩa ([[Chap4 - Quản lý hệ thống file]])
	* PP liên tục: đưa ra các yêu cầu truy xuất lân cận nhau
	* PP liên kết/chỉ mục: có thể đưa ra các yêu cầu truy xuất phân bố khắp đĩa

* Thuật toán điều phối truy nhập đĩa có thể được viết như những modul riêng việt của OS cho phép có thể thay thế bởi các thuật toán khác khi cần thiết.

* Cả SSTF và LOOK đều hợp lý cho việc lựa chọn thuật toán mặc định.