
[[Chap1 - Tổng quan#Tiến trình và luồng]]
## 1.1 Khái niệm tiến trình
### Tiến trình và trạng thái hệ thống
> Trạng thái hệ thống:
> - Vi xử lý: giá trị các thanh ghi
> - Bộ nhớ: Nội dung các ô nhớ
> - Thiết bị ngoại vi: trạng thái thiết bị

* Thực hiện chương trình -> trạng thái hệ thống thay đổi.
	* Rời rạc, theo từng câu lệnh được thực hiện

![[Pasted image 20221109231740.png]]

### Dịch và thực hiện một chương trình
![[Pasted image 20221110130614.png]]

* HĐH tạo 1 TT và phân phối vùng nhớ cho nó

* Bộ thực hiện (loader/exec)
	* Đọc và dịch (interprets) file thực thi (header file)
	* Thiết lập không gian địa chỉ cho TT để chứa mã lệnh và dữ liệu từ file thực thi
	* Đặt các tham số dòng lệnh, biến môi trường (argc, argv, envp) vào stack
	* Thiết lập các thanh ghi của VXL tới các giá trị thích hợp và gọi hàm `_start()` (hàm của HĐH)

* Chương trình bắt đầu thực hiện tại `_start()`. Hàm gọi tới hàm `main()`.
-> "Tiến trình" đang được thực hiện, ko đề cập đến "chương trình" nữa.

* Khi hàm `main()` kết thúc, OS gọi tới hàm `_exit()` để huỷ bỏ TT và thu hồi tài nguyên hệ thống.

### Trạng thái tiến trình
![[Pasted image 20221110130756.png]]

* ***New***  - TT đang được khởi tạo
* ***Ready*** - TT đang đợi sử dụng VXL vật lý 
* ***Running*** - Các câu lệnh của TT đang được thực hiện 
* ***Waiting***  - TT đang chờ 1 sự kiện (sự hoàn thành thao tác vào/ra) xuất hiện
* ***Terminated*** - TT thực hiện xong 

Hệ thống có 1 VXL:
* Có duy nhất 1 TT ở trạng thái running
* Có thể có nhiều TT ở trạng thái ready/waiting

### Process Control Block - PCB
> Mỗi TT được thể hiện trong hệ thống bởi 1 PCB = 1 PCB là cấu trúc thông tin cho phép xác định duy nhất 1 TT

![[Pasted image 20221110132316.png]]

#### Danh sách tiến trình
![[Pasted image 20221110132605.png]]

### Tiến trình đơn luồng và TT đa luồng
> ***Đơn luồng*** - TT thực hiện chỉ 1 luồng thực thi
> -> Thực hiện chỉ 1 nhiệm vụ tại 1 thời điểm

>***Đa luồng*** - TT có nhiều luồng thực thi
>-> Thực hiện nhiều hơn 1 nhiệm vụ tại 1 thời điểm

## 1.2 Điều phối tiến trình (Process Scheduling)
* Trong hệ thống 1 VXL:
	* Chỉ có 1 TT thực hiện, các tiến trình khác phải ở trạng thái waiting cho tới khi CPU free

* Trong hệ thống đa nhiệm:
	* Tối đa tgian của CPU -> cần có nhiều TT trong hệ thống
	* Luân chuyển CPU giữa các TT -> phải có hàng đợi cho các TT

### Các hàng đợi tiến trình
Hệ thống có nhiều hàng đợi dành cho TT
* ***Job-queue*** - Tập các TT trong hệ thống
* ***Ready-queue*** - tập các TT tồn tại trong bộ nhớ, đang sẵn sàng và chờ đợi để được thực hiện
* ***Device queues*** - tập các TT đang chờ đợi 1 thiết bị vào ra. Phân thành các hàng đợi cho từng thiết bị.

![[Pasted image 20221110134702.png]]

![[Pasted image 20221110134725.png]]

* Các TT di chuyển giữa các queues khác nhau.

![[Pasted image 20221110134937.png]]

* TT mới được tạo, được đặt trong hàng đợi ss, đợi tới khi được lựa chọn.
* TT được chọn và đang thực hiện.
	* TH1: Đưa ra 1 y/c vào ra -> chuyển sang hàng đợi thiết bị.
	* TH2: Tạo 1 TT con và đợi TT con kết thúc
	* Hết tgian sử dụng CPU, quay lại hàng đợi ready.
* Trường hợp chờ đợi TH1 và TH2 sau khi hoàn thành
	* TT sẽ chuyển từ t/thai đợi -> trạng thái sẵn sàng
	* TT quay lại hàng đợi sẵn sàng
* TT tiếp tục chu kì (ready -> running -> waiting) cho tới khi kết thúc
	* Xoá khỏi TT tất cả các hàng đợi
	* PCB và tài nguyên đã cấp được giải phóng

### Bộ điều phối (Schedular)
* Lựa chọn TT trong queue
	* Job schedular/long-term schedular
	* CPU schedular/short-term schedular

#### Job schedular
* Chọn các TT từ hàng đợi vào (đc lưu trong các vùng đệm - disk) đưa vào bộ nhớ để thực hiện.

* Thực hiện **không thường xuyên** (đơn vị giây/phút)

* Điều khiển **mức độ đa chương trình** (số TT trong bộ nhớ).

* Khi mức độ đa chương trình ổn định, điều phối công việc được gọi chỉ khi có TT rời khỏi hệ thống.

* Vấn đề lựa chọn công việc (điều phối)
	* TT **thiên về tính toán**: nhiều tgian CPU
	* TT **thiên về vào/ra**: ít thời gian CPU
=> cần lựa chọn lẫn cả 2 loại TT
- Chọn thiên về I/O: ready queue trống -> lãng phí CPU
- Chọn thiên về tt: device queues trống -> lãng phí thiết bị
![[Pasted image 20221110141617.png]]

* Job scheduler sắp xếp lại vị trí các job rồi gửi sang CPU scheduler
![[Pasted image 20221110141813.png]]

#### CPU schedular
* Lựa chọn 1 TT từ hàng đợi các TT đang sẵn sàng thực hiện và phân phối CPU cho nó

* Được **thực hiện thường xuyên**
	* TT thực hiện vài ms rồi thực hiện vào/ra
	* Lựa chọn TT mới, đang sẵn sàng

* Phải thực hiện **nhanh** 

* Vấn đề luân chuyển CPU từ TT này sang TT khác (hoán đổi TT thực hiện)
	* Lưu t/thai của TT cũ vào PCB và khôi phục t/thai cho TT mới.
	* Thời gian luân chuyển được tính là tgian lãng phí
	* Có thể được hỗ trợ bởi phần cứng
	* Thực hiện khi xuất hiện tín hiệu ngắt (tgian) hoặc TT đưa ra System calls ([[Chap1 - Tổng quan#Lời gọi hệ thống (System calls)]])

![[Pasted image 20221110142916.png]]

#### Hoán chuyển tiến trình (Medium-term schedular)
* Đưa TT ra khỏi bộ nhớ (làm giảm mức độ đa chương trình)

* Đưa TT quay trở lại sau đó (có thể ở vị trí khác) và tiếp tục thực hiện
=> Giải phóng mem, tạo vùng nhớ tự do rộng hơn.
![[Pasted image 20221110143128.png]]

## 1.3 Thao tác trên tiến trình
### Tạo tiến trình
* TT có thể tạo nhiều TT mới cùng hoạt động (CreateProcess(), fork())
	* TT tạo: TT cha
	* TT được tạo: TT con

* TT con có thể TT con khác.

* Vấn đề **phân phối tài nguyên**
	* TT con lấy từ HĐH
	* TT con lấy từ TT cha
		* Tất cả
		* Một phần của TT cha (ngăn ngừa việc tạo quá nhiều TT con)

* Vấn đề thực hiện
	* TT cha tiếp tục thực hiện đồng thời với TT con
	* TT cha đợi  TT con kết thúc.

### Kết thúc tiến trình
* Hoàn thành câu lệnh cuối và yêu cầu HĐH xoá (exit)
	* Gửi trả dữ liệu tới TT cha.
	* Các tài nguyên đã cung cấp được trả lại hệ thống.

* TT cha có thể kết thúc sự thực hiện của TT con.
	* TT cha phải biết định danh TT con => TT con phải gửi định danh cho TT cha khi được khởi tạo.
	* Sử dụng lời gọi hệ thống (abort)

* TT cha kết thúc TT con khi: 
	* TT con sử dụng **vượt quá mức tài nguyên** được cấp.
	* Nhiệm vụ cung cấp cho TT con không còn cần thiết nữa.
	* TT cha kết thúc và HĐh không cho phép TT con tồn tại khi TT cha kết thúc.
=> Cascading termination. 

#### Một số hàm với tiến trình

## 1.4 Hợp tác tiến trình
### Phân loại tiến trình
> ***Các TT tuần tự*** - điểm bắt đầu của TT này nằm sau điểm kết thúc của TT kia

> ***Các TT song song*** - điểm bắt đầu của TT này nằm giữa điểm bắt đầu và kết thúc của tiến trình kia.
> - **Độc lập**: không ảnh hưởng tới hoặc bị ảnh hưởng bởi TT khác đang thực hiện trong hệ thống
> - **Có hợp tác**: ảnh hưởng tới hoặc chịu ảnh hưởng bởi TT khác đang thực hiện trong hệ thống.

### Hợp tác tiến trình
* Mục đích: 
	* Chia sẻ thông tin
	* Tăng tốc độ tính toán 
	* Module hoá
	* Tiện hoá

* Đòi hỏi cơ chế cho phép:
	* Truyền thông giữa các TT
	* Đồng bộ hoá hoạt động của các TT

### Bài toán người sx (producer) - người tiêu thụ (consumer)
![[Pasted image 20221110165150.png]]

* Gồm 2 tiến trình:
	* Producer sản xuất ra các sản phẩm
	* Consumer tiêu thụ các sản phẩm được sx ra.

* ***Producer*** và ***Consumer*** hoạt động đồng thời, sử dụng vùng đệm dùng chung (Buffer), chứa sản phẩm được điền vào bởi Producer và lấy ra bởi Consumer
	* IN - vtri trống kế tiếp trong vùng đệm
	* OUT - vtr đầu tiên trong vùng đệm
	* Counter - số sp trong vùng đệm

* P và C phải **đồng bộ**

* Buffer **dung lượng vô hạn**:
	* Buffer rỗng, Consumer phải đợi
	* Producer khong phải đợi khi đặt sp vào buffer
* Buffer **dung lượng hữu hạn**:
	* Buffer rỗng, Consumer phăỉ đợi
	* Producer phải đợi nếu vùng đệm đầy.

## 1.5 Truyền thông liên tiến trình
### Trao đổi giữa các tiến trình
* ***Mô hình bộ nhớ dùng chung***:
	* Các TT chia sẻ vùng nhớ chính
	* Mã cài đặt được viết bởi người lập trình ứng dụngp
![[Pasted image 20221114131441.png]]

* ***Mô hình bộ nhớ truyền thông liên TT (Interprocess communication)***:
	* Cơ chế cho phép các TT truyền thông và hoạt động đồng bộ
	* Thường được sử dụng trong các hệ phân tán, khi các TT truyền thông nằm trên các máy khác nhau (Các ứng dụng chat)
	* Đảm băỏ bởii **hệ thống truyền thông điệp**
![[Pasted image 20221114131824.png]]

### Hệ thống truyền thông điệp
> Là hệ thống cho phép các TT trao đổi với nhau, không qua sử dụng các biến chung.

* Hai thao tác cơ bản: 
	* ***Send***: gửi các msg có kích thước cố định hoặc thay đổi.
		* Cố định: dễ cài đặt mức hệ thống, nhiệm vụ lập trình khó.
		* Thay đổi: cài đặt mức hệ thống phức tạp, lập trình đơn giản
	* ***Receive***: 

* Nếu 2 TT muốn trao đổi:
	1. Thiết lập 1 liên kế truyền thông (vật lý/logic) giữa chúng
	2. Trao đổi các msg nhờ các thao tác send/receive
![[Pasted image 20221114132551.png]]

### Truyền thông trực tiếp >< gián tiếp

| |<b>Truyền thông trực tiếp</b>|<b>Truyền thông gián tiếp</b>|
|:---|:---|:---|
|*Định nghĩa*|Các TT phải gọi tên TT nhận/gửi **một cách tường minh**|Các thông điệp được gửi/nhận tới/từ các **hòm thư**, **cổng**. <br> Mỗi hòm thư có **định danh duy nhất**. <br> Các TT có thể trao đổi nếu chúng **dùng chung hòm thư**|
|*Các thao tác*|1. `send(P, msg)` - gửi 1 thông báo tới TT P <br> 2. `receive(Q,msg)` - nhận 1 thông báo từ TT Q|1. Tạo hòm thư <br> 2. Gửi nhận thông báo **qua hòm thư**:<br> + `send(A,msg)` - gửi 1 msg tới hòm thư A <br> + `receive(A,msg)` - nhận 1 msg từ hòm thư A <br> 3. Huỷ bỏ hòm thư|
|*Tính chất*|- Được **thiết lập tự động** <br> - 1 liên kết gắn chỉ với **cặp TT truyền thông**<br> - Chỉ tồn tại duy nhất 1 liên kết giữa cặp TT<br> - LK thường là hai chiều|- Được thiết lập chỉ khi các **TT dùng chung hòm thư**<br> - 1 LK có thể được gắn với **nhiều TT**<br> - Mỗi cặp TT có thể dùng chung **nhiều liên kết** truyền thông <br> - LK có thể 1 hay 2 chiều|

### Vấn đề đồng bộ hoá
* Truyền thông điệp có thể phải **chờ đợi (blocking)** hoặc **không chờ đợi (non blocking)**
	* **blocking** - truyền thồng đồng bộ
	* **non-blocking** - truyền thông không đồng bộ

* Các thủ tục `send()` hoặc `receive()` có thể phải chờ đợi:
	* ***Blocking send TT***: gửi thông báo và **đợi cho tới khi msg được nhận** bởi TT nhận hoặc bởi hòm thư
	* ***Non-blocking send TT***: gửi thông báo và **tiếp tục làm việc**
	* ***Blocking receive TT***: nhận phải đợi cho tới khi có thông điệp
	* ***Non-blocking receive TT***: nhận trả về 1 thông điệp có giá trị, hoặc 1 gtr null

### Vùng đệm 
> [!note] 
> Các thông điệp trao đổi giữa các TT được lưu trong ***hàng đợi tạm thời (buffer)***

![[Pasted image 20221117094902.png]]

* Hàng đợi có thể được cài đặt theo **khả năng chứa**:
	* 0 - độ dài hàng đợi là 0
		* Ko tồn tại thông điệp trong đường liên kết -> sender phải đợi cho tới khi thông điệp được nhận
	* Có giới hạn (Bound Capacity)
		* Hàng đợi có độ dài n -> Chứa nhiều nhất n thông điệp
		* Nếu hàng đợi ko đầy, thông điệp sẽ được lưu vào trong vùng đệm và Sender tiếp tục bình thường
		* Nếu hàng đợi đầy, sender đợi cho tới khi có chỗ trống
	* Không giới hạn (Unbound Capacity)
		* Sender không bao h phải đợi.

![[Pasted image 20221117095300.png]]

![[Pasted image 20221117095324.png]]