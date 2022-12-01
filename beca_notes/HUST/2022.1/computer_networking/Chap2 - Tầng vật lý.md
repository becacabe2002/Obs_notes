> [!abstract] TỔNG QUAN
> Đảm nhận việc truyền dòng bit
> * Đặt dòng bit từ máy trạm lên đường truyền
> * Lấy dòng bit từ đường truyền vào máy trạm

### Từ tín hiệu tới gói tin

![[Pasted image 20221124085030.png]]

## I. Đường truyền có dây
### 1.1 Cáp xoắn đôi
![[Pasted image 20221124085108.png]]

> [!note] Cấu tạo
> Gồm nhiều cặp dây đồng xoắn với nhau
> 2 loại:
> * Có bọ kim chống nhiễu (STP): ít phổ biến
> * Không bọc kim chống nhiễu (UTP): phổ biến

> [!check] Ưu điểm
> * Đơn giản
> * Rẻ tiền
> * Được sử dụng rộng rãi

> [!failure] Nhược điểm
> * Khả năng chống nhiễu kém (STP chống nhiễu tốt hơn UTP)
> * Khoảng cách nhỏ (hạn chế 100m đối với mạng Ethernet)
> * Giải thông hạn chế (x1MHz)
> * Tốc độ hạn chế (100MHz)

### 1.2 Cáp đồng trụ

![[Pasted image 20221124085445.png]]

> [!note] Cấu tạo
> * Lõi dẫn điện được bọc bởi 1 lớp điện môi không dẫn điện
> * Quấn thêm 1 lớp bện kim loại
> * Ngoài cùng có vỏ bọc cách điện

> [!tip] Ứng dụng
> * Truyền bá TV
> * Truyền các cuộc gọi điện thoại đường dài
> 	* 10000 cuộc gọi cùng lúc
> 	* Nhưng đang dần bị thay thế bởi cáp quang (phần sau)
> * Liên kết các máy tính khoảng cách ngắn
> * Mạng cục bộ  10BaseT, 100BaseT...
> * Khoảng cách triển khai thực tế ~500m

### 1.3 Cáp sợi quang (Optical fiber)

![[Pasted image 20221124085939.png]]

![[Pasted image 20221124085944.png]]

> [!note] Cấu tạo
> * ***Core*** - lớp lõi là sợi thuỷ tinh hoặc sợi plastic để truyền tín hiệu ánh sáng
> * ***Cladding*** - vật chất quang bên ngoài bao bọc lõi mà phản xạ ánh sáng trở lại vào lõi
> * ***Jacket*** - vỏ bọc ngoài

* Các sợi quang có thể được bó với nhau trong 1 đường cáp quang, được gia cố bằng sợi dây gia cường

![[Pasted image 20221124090203.png]]

> [!note] Multimode stepped index (Chiết suất liên tục)
> * Nhiều tia sáng đi theo nhiều đường
> * Tại điểm đến sẽ nhận các chùm tia riêng lẻ
> * Xung dễ bị **méo dạng**.

> [!note] Multimode graded index (Chiết suất bước)
> * Chỉ số khúc xạ của lõi giảm dần từ trong ra ngoài cladding
> * Các tia gần trục truyền chậm hơn các tia gần cladding.
> * Các tia truyền theo đường cong
> * Xung **ít bị méo dạng**

> [!note] Single mode
> * Hệ số khúc xạ thay đổi từ lõi ra cladding ít hơn multimode
> * Các tia truyền theo phương song song trục
> * Xung nhận được hội tụ tốt, ít méo dạng.

> [!check] Ưu điểm
>* Thông lượng cao hơn
>* Nhỏ, nhẹ hơn
>* Suy hao ít hơn
>* Cách ly điện từ tốt
>* Khoảng cách phải lặp tín hiệu lớn hơn (10km)

> [!tip] Ứng dụng
> * Đường truyền khoảng cách xa
> * Đường truyền trong thành phố
> * Đường truyền giữa các router của Công ty viễn thông
> * Xương sống của LAN

## II. Đường truyền không dây
>[!info] Truyền thông tin trên các dải tần khác nhau của sóng điện từ

* Broadcast, bán song công: tại 1 thời điểm chỉ nhận hoặc gửi

> [!warning] Ảnh hưởng của môi trường
> * Phản xạ
> * Nhiễu/giao thoa
> * Tán xạ do vật cản

> [!info] Sóng radio
> * Bước sóng: 1mm - 100.000km
> * Tần số: 3Hz - 300GHz
> 
> > [!example] 
> > Bluetooth, WIFI

> [!info] Sóng vi ba (microwave)
> * Bước sóng: 1mm - 1m
> * Tần số: 300 MHz - 300 GHz
> 
> > [!tip] Ứng dụng
> > Vi ba mặt đất: Kết nối nội thị, hệ thống điện thoại di động
> > VI ba vệ tinh: TV, điện thoại đường dài

> [!info] Hồng ngoại
> * Bước sóng 700 nm - 1mm
> * Tần số: 300 Ghz - 430 THz
> * Phạm vi nhỏ, ko xuyên tường
> > [!tip] Ứng dụng
> > Dùng trong các bộ điều khiển từ xa

* ***Free Space Optics*** - có các bước sóng: 850nm, 1300nm, 1500nm

### 2.1 Dải tần các kênh truyền thông

![[Pasted image 20221124093313.png]]

### 2.2 Phương thức truyền

> [!info] Đơn công - Simplex
> Dữ liệu chỉ được truyền theo 1 chiều 

> [!info] Song công - Duplex
> Dữ liệu có thể được truyền theo cả hai chiều tại cùng 1 thời điểm

> [!info] Bán song công - Half duplex
> Dữ liệu có thể truyền theo cả 2 chiều nhưng tại 1 thời điểm thì chỉ có thể truyền theo 1 chiều

### 2.3 Hình thức truyền
* ***Truyền nối tiếp*** - truyền 1 bit tại 1 thời điểm (trên 1 dây)
* ***Truyền song song*** - truyền đồng thời nhiều bit tại cùng 1 thời điểm (trên nhiều dây dẫn)
![[Pasted image 20221124093927.png]]

### 2.4 Topology
👉 *nhắc lại bài cũ*: [[Chap1.1 - Cơ bản về mạng máy tính#Kiến trúc mạng]]
#### Điểm - Điểm
![[Pasted image 20221124094333.png]]

> [!abstract] Một đường truyền chỉ kết nối 2 thiết bị
> * 1 đường truyền (bán song công)
> * 2 đường truyền (song công)
> 
> > [!warning] 
> > Trường hợp bán song công có thể có xung đột xảy ra khi 2 thiết bị trên cùng 1 kết nối cùng truyền dữ liệu

#### Điểm - nhiều điểm
![[Pasted image 20221124094354.png]]

> [!abstract] Một đường truyền duy nhất kết nối nhiều thiết bị đầu cuối
> * Dữ liệu được quảng bá (broadcast)
> 
> > [!warning] Xung đột
> > Khi hai trạm cùng phát tín hiệu -> Hai tín hiệu ngược chiều nhau gặp nhau trên đường truyền
> 
> > [!check] Cần có các phương pháp điều khiển **đa truy cập (multi access)** 

### 2.5 Giao diện đường truyền
* **Thiết bị đầu cuối dữ liệu** (data terminal equipment - DTE)
	* Không có các tính năng truyền thông
	* Cần có các thiết bị bổ sung để truy cập đường truyền

* **Thiết bị cuối kênh dữ liệu** (data circuit terminating equipment - DCE) 
	* Truyền các  bít trên đường truyền
	* Trao đổi dữ liệu và các thông tin điều khiển với DCE qua các dây nối

>[!warning] Cần các giao diện chuẩn, rõ ràng giữa DTE, DCE
>

#### DTE - DCE
![[Pasted image 20221124101911.png]]

📚[<b>Differences between DTE and DCE</b>](https://www.geeksforgeeks.org/difference-between-dte-and-dce/)

> [!abstract] Giao diện đường truyền
> > [!note] Cơ
> > Hình dạng giác cắm, số lượng chân, đảm bảo cắm được lẫn nhau
> ---
> > [!note]  Điện
> > * Mức điẹn áp sử dụng
> > * Chiều dài xung (tần số xung nhịp)
> > * Phương pháp mã hoá
> ---
> > [!note] Chức năng
> > * Dây dẫn nào dùng làm gì?
> > * Có 4 nhóm chính:
> > 	* Dữ liệu
> > 	* Điều khiển
> > 	* Đồng bộ
> > 	* Nối đất
> ---
> > [!note] Thủ tục
> > Các thủ tục, chuỗi các sự kiện để thực hiện việc truyền tin

![[Pasted image 20221124141730.png]]
![[Pasted image 20221124141733.png]]

## III. Mã hoá thông tin
> [!info] Mã hoá thông tin
> Biến đổi bit nhị phân thành dạng tín hiệu vật lý thích hợp để truyền trên đường truyền vật lý
> > [!example] 
> > **Mã hoá** - sử dụng các tín hiệu rời rạc có mức điện áp khác nhau để biểu diễn bit 1 và 0
> > **Điều chế** - sử dụng tín hiệu tương tự (sóng) để biểu diễn các bit 1 và 0
> 
> >[!caution] Việc truyền phải được đồng bộ giữa hai bên
> 
> Có nhiều cách biểu diễn khác nhau = các phương pháp mã hoá
### 3.1 Các PP mã hoá dữ liệu số - tín hiệu số
#### NRZ-L Non Return to Zero level
> [!note]
> * Trong thời gian của 1 bit, tín hiệu không trở về mức 0
> * Không có chuyển mức trong khoảng thời gian của một bit
> 
> ![[Pasted image 20221124142245.png]]

#### NRZ-I Non Return to Zero invert
> [!note]
> * Bit 0 tương ứng với không chuyển mức ở đầu thời gian bit
> * Bit 1 tương ứng với chuyển mức ở đầu tgian bit
> * Là một **phương pháp điều chế vi sai**
> 	* 0, 1 tương ứng với chuyển mức, ko phải với mức giá trị
> 	* Tin cậy, đơn giản hơn điều chế theo mức
> 	* Không phụ thuộc vào cực của tín hiệu
> 	
> ![[Pasted image 20221124142245.png]]

### 3.2 Một số yếu tố cần xem xét đánh giá một mã
> [!abstract]
> >[!note]- Đồng bộ đồng hồ bên gửi và bên nhận
> >* Nếu đồng hồ bên gửi và nhận ko đồng bộ -> bên nhận có thể xác định sai thời gian 1 bit
> >-> Giải mã sai -> tăng tỉ lệ lỗi dữ liệu
> >* Một số mã có yếu tố giúp đồng bộ trong mã
> 
> > [!note]- Thành phần một chiều trong tín hiệu
> > * Thành phần một chiều xuất hiện khi tín hiệu ở một mức quá lâu (âm/dương)
> > 	* Làm cho bên nhận xác định sai mức tín hiệu cơ sở
> > 	* Giải mã sai dữ liệu
> > * Phương pháp mã hoá cần tránh thành phần một chiều bằng cách duy trì giá trị trung bình của tín hiệu ở mức 0.

#### Đánh giá NRZ
> [!check] Ưu điểm
> * Đơn giản, sử dụng tối đa đường truyền
> * Giải tần số tập trung từ 0 đến 1/2 tốc độ dữ liệu (VD: 9600bps -> 4800kHz)

> [!failure] Nhược điểm
> * Khó đồng bộ bằng tín hiệu
> 	* Với NRZ-L khi có nhiều 0 hoặc 1 liên tiếp, tín hiệu giữ một mức trong khoảng thời gian dài -> dễ mất đồng bộ.
> 	* Với NRZ-I có một chuỗi 0, tình trạng tương tự cũng xảy ra
> * Có thành phần một chiều khi truyền toàn 1

> [!tip] Ứng dụng
> * Lưu trữ dữ liệu trên vật liệu từ tính
> * Ít dùng trong truyền số liệu

### 3.3 Mã nhị phân đa mức
> [!info]
> * Lưỡng cực xen kẽ đổi dấu 
> * Sử dụng nhiều hơn 2 mức tín hiệu cho 1 bit
> * **Lưỡng cực đảo mức 1 (Bipolar - AMI)**
> 	* 0 - ko có tín hiệu
> 	* 1 - có tín hiệu, tín hiệu đảo cực giữa hai bit 1 liên tiếp.
> * **Giả tam phân (pseudoternary)**
> 	* 1 - ko có tín hiệu
> 	* 0 - có tín hiệu, tín hiệu đảo cực giữa hai bit 0 liên tiếp

![[Pasted image 20221124213113.png]]

* Thành phần một chiều = 0
* Có khả năng phát hiện lỗi
* Đồng bộ khi có nhiều bit 1(0), ko đồng bộ khi có nhiều bit 0(1)
* **Giải thông thấp** hơn
* 3 mức tín hiệu cho một bit
	* Ko sử dụng tối ưu đường truyền
	* Tăng tỉ lệ lỗi (đích cần phân biệt 3 mức tín hiệu)

### 3.4 Mã hai pha: Manchester
> [!abstract] Cơ chế
> Luôn luôn chuyển mức ở giữa thời gian của 1 bit
> * Thấp lên cao: 0, cao xuống thấp 1
> * Chuyển mức cung cấp cơ chế đồng bộ

> [!note] Manchester
> * Luôn có chuyển mức ở giữa bit
> * Bit 0 : sườn âm (chuyển từ +V sang -V )
> * Bit 1: sườn dương (chuyển từ -V sang +V)
> * **dùng trong mạng Ethernet**

> [!note] Manchester visai
> * 0 - có chuyển mức ở đầu bit
> * 1 - ko có chuyển mức
> * Chuyển mức ở giữa bit chỉ phục vụ cho đồng bộ
> * Luôn có chuyển mức tín hiệu ở giữa bit

![[Pasted image 20221124222017.png]]

### 3.5 Tốc độ tín hiệu/tốc độ điều chế

![[Pasted image 20221124222130.png]]

### Tổng hợp các phương pháp mã hoá
![[Pasted image 20221124222211.png]]

## IV. Điều chế dữ liệu số - tín hiệu liên tục
### 4.1 Điều chế khoá dịch biên độ (ASK)
> [!info]
> * Biên độ của sóng mang biến đổi theo thông tin cần truyền
$$
s(t) =
\left \{
\begin{array}{cl}
A\cos(2\pi ft) & cho 1 \\
0 & cho 0
\end{array}
\right .
$$

* 0 và 1 tương ứng với hai biên độ tín hiệu, thông thường một trong hai biên độ = 0

![[Pasted image 20221124223846.png]]

> [!warning] 
> * Dễ bị ảnh hưởng bởi nhiễu (1200bps cho đường thoại)
> * Khó đồng bộ 

> [!tip] Ứng dụng 
> Thường được dùng trong cáp quang (LED hoặc laser)

#### Mã On-Off Keying (OOK)
* dùng trong **cáp quang**
> [!note] Là 1 loại điều chế dịch biên độ
> * 1 - có xung ánh sáng trong thời gian bit (bật nguồn sáng). 
> * 0 - không có xung ánh sáng trong thời gian bit (tắt nguồn sáng).

> [!note] Có thể dùng nhiều định dạng tín hiệu khác nhau
> * NRZ - xung ánh sáng chiếm toàn bộ độ dài  bit 1
> * RZ (return to zero) - chỉ phát xung ánh sáng trong 1 phần thời gian của bit 1

![[Pasted image 20221124234821.png]]

### 4.2 Điều chế khoá dịch tần số (Frequency Shift Keying - FSK)
> [!info]
> Hai giá trị nhị phân được biểu diễn bởi hai tín hiệu tần số khác nhau 


$$
s(t) =
\left \{
\begin{array}{c}
A\cos(2\pi f_1t) \\
A\cos(2\pi f_2t)
\end{array}
\right .
$$
> [!check] Tỷ suất lỗi thấp hơn

> [!tip] Ứng dụng
> Dùng trong truyền số liệu qua đường điện thoại (tần số thấp), hoặc trong mạng ko dây (tần số cao)

### 4.3 Điều chế khoá dịch pha (Phase Shift Keying - PSK)
* 0,1 tương ứng với hai độ lệch pha khác nhau
* 0,1 tương ứng với chuyển pha (vi sai)

$$
s(t) =
\left \{
\begin{array}{cc}
A\cos(2\pi f_ct + \pi) & Binary 1 \\
A\cos(2\pi f_ct) & Binary 0
\end{array}
\right .
$$
$$
s(t) =
\left \{
\begin{array}{cc}
A\cos(2\pi f_ct + 45\degree) & 11 \\
A\cos(2\pi f_ct + 135\degree) & 10 \\
A\cos(2\pi f_ct + 225\degree) & 00 \\
A\cos(2\pi f_ct + 315\degree) & 01
\end{array}
\right .
$$

> [!note] 
> * Có thể sử dụng giải thông một cách hiệu quả hơn khi mã hoá cùng lúc nhiều bit
> * Có thể kết hợp với điều biên

### 4.4 Kết hợp với điều biên
> [!note]
> Các tổ hợp được biểu diễn trên bản đồ sao, mỗi tia ứng với 1 mã
> * Độ dài tia ứng với biên độ
> * Góc lệch với pha tham chiếu ứng với góc pha

![[Pasted image 20221125001452.png]]

### 4.5 Tổng hợp điều chế số/liên tục

![[Chương 2 - Tầng vật lý.jpg]]

## V. Điều chế dữ liệu liên tục - số
> [!info] 
> * Điều chế dữ liệu liên tục thành dữ liệu số
> * Sau đó:
> 	* Điều chế thành tín hiệu số
> 		* Trực tiếp bằng [[Chap2 - Tầng vật lý#NRZ-L Non Return to Zero level]]
> 		* Các pp mã hoá tín hiệu số khác
> 	* Điều chế thành tín hiệu liên tục
> 		* Sử dụng các biện pháp điều số chế - liên tục [[Chap2 - Tầng vật lý#IV. Điều chế dữ liệu số - tín hiệu liên tục]]

* Có hai pp chính đièu chế dữ liệu lt thành dl số:
	* Điều chế mã xung
	* Điều chế Delta 

### 5.1 Điều chế mã xung (Pulse Code Modulation - PCM)
> [!note]
> Lấy mẫu tín hiệu dựa trên định luật lấy mẫu của Shannon
* Nếu tần số lấy mẫu >= 2 lần tần số (có ý nghĩa) cao nhất của tín hiệu, phép lấy mẫu bảo toàn thông tin của tín hiệu

> [!note] Hai bước
> * Lấy mẫu (PAM)
> * Lượng tử hoá

![[Pasted image 20221125003809.png]]

### 5.2 Điều chế delta (Delta Modulation)
* Sử dụng hàm bậc thang
	* Khi hàm số tăng, xung=1
	* Khi hàm số giảm, xung=0
* Tổng quát
	* Biểu diễn giá trị của đạo hàm theo bít
* Tham số
	* Bậc thang
	* Tốc độ lấy mẫu
* Sai số
	* Khi tín hiệu thay đổi chậm: nhiễu lượng tử
	* Khi tín hiệu thay đổi nhanh: nhiễu tràn
![[Pasted image 20221125004056.png]]

### 5.3 Dữ liệu liên tục, tín hiệu liên tục
* Kết hợp tín hiệu m(t) và sóng mang có tần số Fc thành một tín hiệu tập trung xung quanh Fc

* Cho phép chuyển tín hiệu trên một tần số khác phù hợp với kênh truyền

* Cho phép dồn kênh bằng các tần số sóng mang khác nhau

* 3 phương pháp chính dựa vào đặc điểm của tín hiệu
	* Điều biên
	* Điều tần
	* Điều chế góc pha

![[Pasted image 20221125004304.png]]

### 5.4 Điều biên
* Biến đổi biên độ sóng mang theo đầu vào

* Nếu đầu vào cũng là hình sin
	* Tín hiệu đầu ra sẽ có hai thành phần lệch với tần số sóng mang một khoảng bằng tần số đầu vào
	* Na<1 điều biên hợp lệ
	* Na>1 mất thông tin

* Giải thông=2 lần giải thông đầu vào

* Điều biên một chiều: 1 lần giải thông

![[Pasted image 20221125004524.png]]