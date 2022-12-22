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
> [!abstract] 
> * Đóng gói
> * Địa chỉ hoá
> * Điều khiển truy nhập đường truyền
> * Kiểm soát luồng
> * Kiểm soát lỗi
> * Chế độ truyền

> [!note] Đóng gói
> * Đơn vị dữ liệu: khung tin (frame)
> * Bên gửi: thêm phần đầu cho gói tin nhận được tầng mạng
> * Bên nhận: bỏ phần đầu, chuyển lên tầng mạng

> [!note] Địa chỉ hoá
>* Sử dụng địa chỉ MAC

> [!note] Điều khiển truy cập đường truyền
> * Cần có giao thức điều khiển đa truy nhập với mạng đa truy cập

> [!note] Kiểm soát luồng
> * Đảm bảo bên nhận ko bị quá tải

> [!note] Kiểm soát lỗi
> * Phát hiện và sửa lỗi bit trong các khung tin 

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
> [!info] MAC address
> * Địa chỉ MAC: 48 bit, được quản lý bởi IEEE
> * Mỗi cổng mạng được gán một MAC
> 	* Không thể thay đổi địa chỉ vật lý
> * Không phân cấp, có tính di động
> 	* Không cần thay đổi địa chỉ MAC khi host chuyển sang mạng khác
> * Địa chỉ quảng bá trong mạng LAN: **FF-FF-FF-FF-FF-FF**

👉 More about [MAC address](https://www.geeksforgeeks.org/introduction-of-mac-address-in-computer-network/)

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

* Phát hiện lỗi trên nhiều bit
$$
\begin{array}{cc}
f_{edc}(P_{send}) \neq f_{edc}(P_{receive}) & \forall P_{send} \neq P_{receive}
\end{array}
$$

### Mã Checksum
* **Gửi**:
	* Chia dữ liệu thành các phần có kích thước n bit
	* Tính tổng các phần. Nếu kết quả tràn quá n bit, cộng các bit tràn vào phần kết quả.
	* Đảo bit kết quả cuối cùng được checksum
	* Truyền checksum kèm theo dữ liệu

* **Nhận**: 
	* Tách dữ liệu và checksum
	* Chia dữ liệu thành các phần có kích thước n bit
	* Tính tổng các phần và checksum. Nếu kết quả tràn quá n bit, cộng các bit tràn vào phần kết quả.
	* Nếu kết quả cuối xuất hiện bit 0 -> ***Dữ liệu bị lỗi***

> [!example] Ví dụ
> Xử lý khi gửi
> ![[Pasted image 20221221100526.png]]
> Xử lý khi nhận
> ![[Pasted image 20221221100553.png]]

### Mã vòng CRC (Cyclic Redundancy Check)
* **Phía gửi**:
	* Chọn 1 đa thức sinh bậc k
	* Biểu diễn đa thức dưới dạng chuỗi bit P [Cách chuyển đa thức thành chuỗi bit ](https://cs.stackexchange.com/questions/71387/converting-polynomials-into-binary-form)
	* Thêm k bit 0 vào frame dữ liệu F được F_k
	* Chia F_k cho P, lấy phần dư R (có kích thước k bit)
	* Ghép phần dư vào chuỗi dữ liệu được FR

* **Phía nhận**: lấy FR chia cho P 
	* Nếu chia hết -> ***Truyền đúng***
	* Nếu chia có dư -> căn cứ vào số dư (syndrom) để phát hiện và sửa lỗi (nếu được)

![[Chương 3 - Tầng liên kết dữ liệu.pptx-17-20.pdf]]

> [!question] Làm gì sau khi phát hiện lỗi ?
> > [!note] Các loại lỗi
> > * Mất khung dữ liệu
> > * Khung dữ liệu bị lõi 
> > * Thông báo lỗi bị mất
> 
> **Làm thế nào để báo cho bên gửi ?**
> * Báo nhận: ***ACK*** (acknowledgements)
> * Báo lỗi : ***NAK*** (negative acknowledgements), báo cho người gửi về một gói tin bị lỗi
> 
> **Phản ứng của bên gửi?**
> * Truyền lại nếu là NAK
> * Nếu không nhận được cả ACK/NAK? Timeout

### Các kỹ thuật báo nhận, phát lại
> [!info] Automatic repeat request - ARQ
> Có 3 phiên bản chuẩn hoá:
> * ***Dừng và chờ (Stop and wait) ARQ***:
> 	* Chỉ phát tiếp khi nhận được ACK của gói đã phát
> 	* Hoặc nếu gặp timeout mà chưa nhận được ACK thì phát lại gói vừa phát.
> * **Quay lại N (Go back N) ARQ**: (Có tại tầng mạng)
> * **Loại bỏ chọn lọc (Selective Reject) ARQ**: (có tại tầng mạng)

![[Chương 3 - Tầng liên kết dữ liệu.pptx-23-28.pdf]]

## 3. Kiểm soát luồng

==**Đảm bảo trạm gửi không làm quá tải trạm nhận**==

> [!note] Trạm đích
> * Lưu trữ các khung dữ liệu trong bộ nhớ đệm
> * Thực hiện một số thao tác trước khi chuyển dữ liệu lên tầng trên
> * Bộ nhớ đệm có thể bị đầy, dẫn tới mất khung dữ liệu

> [!note] Không đặt vấn đề lỗi truyền tin
> * Các khung dữ liệu luôn luôn được truyền chính xác
> * Độ trễ truyền tin không đáng kể

> [!tip] Giải pháp
> * ***Cơ chế dừng và chờ***
> * ***Cơ chế cửa sổ trượt*** (có ở tầng mạng)

### Cơ chế dừng và chờ
> [!abstract] Nguyên tắc
> * Nguồn gửi một khung dữ liệu
> * Đích nhận khung dữ liệu, xử lí, sau đó thông báo sẵn sàng nhận các khung dữ liệu tiếp theo bằng một thông báo báo nhận (ACK)
> * Nguồn phải chờ tới khi nhận được báo nhận mới truyền tiếp khung dữ liệu tiếp theo.
> 
> ![[Pasted image 20221221132432.png]]
> ![[Pasted image 20221221132537.png]]

> [!check] Ưu điểm
> Đơn giản, thích hợp với các khung dữ liệu lớn

> [!failure] Nhược điểm
> * Với các khung dữ liệu nhỏ, thời gian sử dụng đường truyền bị lãng phí
> * Không thể sử dụng các khung dữ liệu lớn một cách phổ biến
> 	* Bộ nhớ đệm có hạn
> 	* Khung dữ liệu dài có khả năng lỗi lớn
> 	* Trong môi trường truyền tin chia sẻ, không cho phép trạm nào chiếm dụng lâu đường truyền.

> [!example]- Bài tập
> ![[Chương 3 - Tầng liên kết dữ liệu.pptx-35-37.pdf]]

## 4. Điều khiển truy nhập đường truyền
> [!note] Các dạng liên kết
> * ***Điểm - điểm (point-point)***: ADSL, Telephone  modem, Leased line ...
> 
> * ***Điểm - đa điểm (point - to - multipoint)***: 
> 	* Mạng LAN có dạng bus, mạng LAN hình sao dùng hub
> 	* Mạng không dây
> 	* Cần giao thức điều khiển truy nhập để tránh xung đột
> 
> ![[Pasted image 20221221133432.png]]

### Phân loại các giao thức đa truy nhập
> [!abstract] Phân loại
> * **Phân loại tài nguyên** sử dụng kỹ thuật chia kênh
> 	* Chia tài nguyên của đường truyền thành nhiều phần nhỏ:
> 		* ***Code division multiple access*** - CDMA
> 		* ***Frequency division multiple access*** - FDMA
> 		* ***Time division multiple access*** - TDMA
> 	* Chia từng phần nhỏ đó cho các nút mạng
> * **Truy cập ngẫu nhiên** 
> 	* Kênh  ko được chia, cho phép đồng thời truy nhập, chấp nhận là có xung đột.
> 	* Cần có cơ chế để phát hiện và tránh xung đột
> 	* ex: Pure Aloha, Slotted Aloha, CSMA/CD, CSMA/CA ...
> * **Lần lượt**: 
> 	* Theo hình thức quay vòng
> 	* Token Ring, Token Bus....

### Các kĩ thuật chia kênh
> [!note] TDMA & FDMA
> ![[Pasted image 20221221161421.png]]

> [!note] CDMA
> ![[Chương 3 - Tầng liên kết dữ liệu.pptx-43-45.pdf]]
### Các cơ chế truy cập ngẫu nhiên
> [!note] Aloha 
> * Khi một nút mạng cần truyền dữ liệu:
> 	* Frame đầu tiên: truyền ngay. Nếu có đụng độ thì truyền lại với sác xuất p.
> 	* Các frame sau: truyền với xác suất là p
> 	* Trong 1 frame-time chỉ được truyền 1 frame
> 
> ![[Pasted image 20221221163345.png]]
> 
> > [!info] Frame-time
> > Thời gian để truyền hết một frame có kích thước lớn nhất (= MTU/R)
> 
> * Xác suất truyền thành công p = $\approx$ 18.4%
> -> **Xác suất sảy ra đụng độ là cao nhất**


> [!note] Slotted Aloha
> * Hoạt động như Aloha với các yêu cầu:
> 	* Frame-time là như nhau với mọi nút
> 	* Tất cả các nút phải đồng bộ về thời gian
> 	* Các trạm đồng bộ time slot & frame chỉ được truyền vào đầu slot
> 	-> Giảm nguy cơ xung đột 
> 
> ![[Pasted image 20221221163543.png]]
> * Xác suất truyền thành công = $\approx$ 36.8%

> [!note] Carrier Sense Multiple Access - CSMA
> * Đa truy cập sử dụng sóng mang
> * Cảm nhận sóng mang để quyết định đường truyền có bận hay không? (Nghe trước khi nói)
> * Đụng độ xảy ra do **trễ trên đường truyền**
> 
> ![[Pasted image 20221221165934.png]]

> [!info] Sóng mang (Carrier)
> * Sóng mang có tần số lớn (năng lượng lớn) để truyền được xa (ko dây lẫn có dây)
> * Sóng mang là giao động tuần hoàn (ko mang thông tin)
> * Tín hiệu/dữ liệu (mang thông tin) cần được truyền đi xa. Thường có tần số rất thấp (năng lượng yếu)
> ***-> Cần dùng sóng mang để chuyển tín hiệu/dữ liệu đầu vào***
> * Phương pháp **AM**, **FM** (đầu vào analog)
> * Phương pháp **mã hoá** (đầu vào digital)

> [!note] CSMA/CA (Collision Avoidance)
> * Dùng trong mạng WIFI 802.11
> * Nếu 2 hay nhiều trạm cùng phát hiện đường truyền bận và cùng chờ thì có khả năng chúng sẽ cùng truyền lại 1 lúc -> Xung đột
> 
> > [!tip] Giải pháp
> > Mỗi tạm chờ một khoảng thời gian được tính ngẫu nhiên 
> > -> Giảm xác suất đụng độ

> [!note] CSMA/CD (Collision Detection)
> * Dùng trong mạng Ethernet
> * Nếu đường truyền bận, chờ rồi truyền với xác suất p
> * Nếu đường truyền rồi, tiến hành truyền
> 	* Nghe đường truyền trong khi truyền.
> 	* Nếu có xung đột, chỉ phát 1 tín hiệu báo xung đột ngắn và dừng ngay (Ko tiếp tục truyền như CSMA)
> 	* Thử truyền lại sau một khoảng thời gian ngẫu nhiên.

#### Thuật toán CSMA
![[Pasted image 20221221173154.png]]

>[!abstract] tóm tắt CSMA/CD
>* Máy trạm nghe trước khi muốn truyền
>	* Bận: chờ, tiếp tục nghe
>	* Rỗi: Bắt đầu truyền, vừa truyền vừa "nghe ngóng"(duy trì việc phát tín hiệu báo đụng độ trên đường truyền trong một khoảng thời gian để tất cả các nút mạng khác cảm nhận được) xem có xung đột gì hay không (nghe trong bao lâu)
>		* Nếu phát hiện xung đột : huỷ bỏ quá trình truyền và quay lại trạng thái chờ, nghe

* Một số biến thể của CSMA:
	* Persistent CSMA
	* Non-persistant CSMA
	* P-persistant CSMA

### So sánh chia kênh vs truy cập ngẫu nhiên
* Chia kênh : 
	* Hiệu quả, công bằng cho đường truyền với lưu lượng lớn
	* Lãng phí nếu chúng ta cấp kênh con cho một nút chỉ cần lưu lượng nhỏ

* Truy cập ngẫu nhiên
	* Hiệu quả khi tải nhỏ vì mỗi nút có thể sử dụng toàn bộ kênh truyền
	* Xung đột tăng lên khi tải lớn.

> [!tip] Có thể dung hoà ưu điểm hai phương pháp trên bằng ***Phương pháp quay vòng***

### Các hình thức quay vòng
> [!note] Token passing
> * Bit trạng thái: rỗi hay bận
> * Chỉ khi nút mạng **nhận được thẻ bài rỗi**, ko mang dữ liệu -> được phép truyền dữ liệu
> 	* Thiết lập trạng thái thẻ bài về trạng thái bận
> 	* Tổ chức dữ liệu để truyền, thẻ bài trở thành tiêu đề của frame
> 	* Sau khi truyền xong dữ liệu: thiết lập trạng thái thẻ bài là rỗi
> 
> > [!warning] Chỉ tồn tại duy nhất 1 thể bài trong mạng để xác định quyền đưa dữ liệu lên đường truyền
> * Nút đích: sao chép dữ liệu trên frame và trả lại frame cho nút nguồn.
> * Token Ring: vòng luân chuyển thẻ bài là vòng vật lý
> * Token Bus: vòng luân chuyển thẻ bài là vòng logic

#### Khuôn dạng thẻ bài và gói tin
> [!info] Thẻ bài trống
> ![[Pasted image 20221222085544.png]]
> * **Starting Delimiter (8 bit)** - bắt đầu frame
> * **Access Control (8 bit)** - điều khiển
> 	* Mức ưu tiên (3 bit): xác lập quyền ưu tiên sử dụng thẻ bài
> 	* Trạng thái thẻ bài (1 bit)
> 	* Giám sát (1 bit)
> * **Ending Delimiter (8 bit)** - kết thúc frame

> [!info] Frame dữ liệu
> ![[Pasted image 20221222085939.png]]
> * **FC (8 bit)** - kiểu frame dữ liệu mang theo trong thẻ bài 
> * **FS (8 bit)** - báo nhận

* Token bus:
![[Pasted image 20221221195057.png]]

* Token Ring - mạng vòng dùng thẻ bài
	* Một thẻ bài luân chuyển lần lượt qua từng nút mạng
	* Nút nào giữ thẻ bài sẽ được gửi dữ liệu
	* Gửi xong phải chuyển thẻ bài đi.

> [!warning]  Một số vấn đề
> Tốn thời gian chuyền thẻ
> Trễ
> Mất thẻ bài

## 5. Chuyển tiếp dữ liệu
### Chuyển tiếp dữ liệu tầng 2
> [!note] Bảng địa chỉ MAC
> Bao gồm:
> * Địa chỉ MAC của host
> * Cổng kết nối vớ host (interface)
> * TTL: thời gian giữ lại thông tin trong bảng
> ![[Pasted image 20221221213802.png]]

### Switch - cơ chế tự học (learning switch)
* Cập nhật địa chỉ MAC nguồn và cổng nhận gói tin vào bảng MAC Table nếu:
	* Địa chỉ nguồn chưa có trong bảng MAC table
	* Địa chỉ nguồn đã có nhưng nhận được gói tin trên cổng khác

![[Pasted image 20221221214634.png]]
![[Pasted image 20221221214644.png]]

### Switch - cơ chế chuyển tiếp ()
Khi nhận được 1 frame: 
1. Tìm được cổng vào (nhờ tự học)
2. Tìm địa chỉ cổng ra dùng bảng chuyển tiếp 
3. 
```shell
if tìm thấy cổng ra
then {
	if cổng ra == cổng vào
	then huỷ bỏ frame
	else chuyển frame đến cổng ra
}
else quảng bá (flooding) frame tới tất cả các cổng
```

![[Pasted image 20221221215149.png]]

### Nối chồng các switch với nhau
* Các switch có thể được nối với nhau, và **dùng cơ chế tự học**
![[Pasted image 20221221215914.png]]
* A -> I, S1 học A, quảng bá: B, C, S4
* S4 học A từ S1, quảng bá: S2, S3
* S3: học A từ S4, quảng bá: G, H, I

### Các chế độ chuyển mạch
* ***Store and forward*** : nhận đầy đủ frame, kiểm tra lỗi và chuyển mạch theo địa chỉ MAC đích

* ***Cut and through*** : chuyển frame ngay lập tức sau khi đã xác định được cổng

* ***Fragment free*** : kiểm tra 64 byte đầu tiên
	* Frame tin bị lỗi do đụng độ có kích thước < 64 byte

* ***Adaptive*** : tự động lựa chọn 1 trong 3 chế độ trên

## 6. Mạng cục bộ (LAN)
### Các thiết bị kết nối trong mạng LAN
> [!info] Repeater, Hub
> * Đảm nhiện chức năng tầng 1 (tầng vật lý)
> * Tăng cường tín hiệu -> **Mở rộng phạm vi kết nối (broadcast zone)**
> * Có ít hơn 4 repeater trên 1 đoạn mạng (đường truyền kết nối 2 nút mạng)

> [!info] Bridge, Switch
> * Đảm nhiệm chức năng L1, L2
> * Cho phép kết nối các loại đường truyền vật lý khác nhau
> * Chia nhỏ miền đụng độ
> * Chuyển mạch cho khung tin dựa trên địa chỉ MAC

### Router vs Switch
```start-multi-column
ID:router&switch
number of columns: 2
```


* **Xử lý gói tin**: lưu và chuyển tiếp (Store-and-forward)
	* Router: thiết bị tầng mạng
	* Switch: thiết bị tầng liên kết dữ liệu
* **Chuyển tiếp gói tin**:
	* Router: sử dụng thuật toán định tuyến tính toán bảng chuyển tiếp (Forwarding Table), chuyển tiếp theo địa chỉ IP đích
	* Switch: sử dụng cơ chế tự học tính toán bảng MAC Table, chuyển tiếp theo địa chỉ MAC đích

--- end-column ---

![[Pasted image 20221222094857.png]]

=== end-multi-column

![[Chương 3 - Tầng liên kết dữ liệu.pptx-69-71.pdf]]

### Hình trạng LAN
> [!note] Mạng trục (Bus)
> * Tất cả các nút mạng sử dụng chung đường truyền - trục (backbone)
> * Mỗi nút mạng kết nối vào trục bằng đầu nối chữ T (T-connector)
> * Terminator hai đầu
> * Phương thức truyền: điểm - đa điểm (point-to-multipoint)
> 	* Dữ liệu truyền theo 2 hướng
> 	* Nút nhận: kiểm tra địa chỉ đích của dữ liệu
> ![[Pasted image 20221222101650.png]]

> [!note] Mạng sao (Star)
> * Một nút mạng đóng vai trò thiết bị trung tâm
> 	* Hub
> 	* Switch
> 	* Router
> * Các nút mạng khác kết nối trực tiếp với thiết bị trung tâm
> * Phương thức truyền
> 	* Điểm - điểm: switch, router
> 	* Điểm - đa điểm: hub
> ![[Pasted image 20221222101853.png]]

> [!note] Mạng hình vòng (Ring)
> * Các nút mạng chung đường truyền khép kín
> * Phương thức truyền: điểm - điểm, điểm - đa điểm
> * Dự phòng: FDDI vòng kép, thường sử dụng cho khu vực mạng xương sống.
> ![[Pasted image 20221222102337.png]]

## 7. Mạng diện rộng (WAN)