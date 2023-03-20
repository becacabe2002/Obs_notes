## 1. Tổng quan
* Tài nguyên TT cần 
	* Bộ xử lý (ảo)[[Chap2.4 - Tài nguyên găng và điều độ tiến trình]]
	* Bộ nhớ [[Chap3 - Quản lý bộ nhớ]]
	* Tập tài nguyên khác

### 1.1 Ví dụ
### 1.2 Bộ nhớ và chương trình
#### Phân cấp bộ nhớ
* Bộ nhớ - tài nguyên quan trọng của hệ thống
	* Chương trình phải nằm trong bộ nhớ để thực hiện

* Đặc trưng của bộ nhớ : **kích thước** và **tốc độ truy cập**

> [!note] Phân cấp theo tốc độ truy cập
> ![[Pasted image 20221219233705.png]]

#### Bộ nhớ  chính
> [!info] Bộ nhớ chính
> Là mảng các ô nhớ kiểu bytes, words với mỗi ô nhớ có một địa chỉ riêng (***Địa chỉ vật lý*** - địa chỉ xuất hiện ở chân VXL).
> Được dùng lưu trữ dữ liệu và chương trình.

![[Pasted image 20221219235512.png]]

![[Pasted image 20221219235521.png]]

#### Chương trình
> [!info] Chương trình
> * Là các file nhị phân thực thi được:
> 	* Vùng tham số file
> 	* Lệnh máy (Mã nhị phân)
> 	* Vùng dữ liệu (Biến toàn cục)
> * Tồn tại trên thiết bị lưu trữ ngoài

> [!info]  Hàng đợi vào (input queue)
> * Tập các tiến trình ở bộ nhớ ngoài (thông thường là disk).
> * Đợi để được đưa vào bộ nhớ trong và thực hiện.

> [!note] CÁC BƯỚC THỰC HIỆN CHƯƠNG TRÌNH
> 1. **Nạp chương trình vào bộ nhớ**
> 	* Đọc và dịch file thực thi (\*.com, \*.exe)
> 	* Xin vùng nhớ để nạp chương trìn từ file trên đĩa
> 	* Thiết lập các tham số, các thanh ghi tới giá trị thích hợp
> 2. **Thực thi chương trình**
> 	* CPU lấy các lệnh trong bộ nhớ tại vị trí được xác định bởi bộ đếm chương trình (PC)
> 	* CPU giải mã lệnh (Có thể lấy thêm toán hạng từ bộ nhớ)
> 	* Thực hiện lệnh với toán hạng
> 	* Lưu kết quả vào bộ nhớ tại một địa chỉ xác định (Nếu cần)
> 3. **Giải phóng vùng không gian nhớ** dành cho chương trình sau khi thực hiện xong.

> [!warning] Vấn đề.
> Chương trình có thể được nạp vào vị trí bất kỳ trong bộ nhớ. Khi thực hiện, CT sinh ra chuỗi địa chỉ bộ nhớ.
> 👉**Truy cập địa chỉ bộ nhớ như thế nào?**

### 1.3 Liên kết địa chỉ
> [!note] Các bước xử lý chương trình ứng dụng
> ![[Pasted image 20221205125234.png]]

#### Các kiểu địa chỉ
> [!info] Địa chỉ biểu tượng (symbolic)
> Tên của đối tượng trong chương trình nguồn

> [!info] Địa chỉ tương đối 
> * Sinh ra từ địa chỉ biểu tượng trong giai đoạn dịch (compiler)
> * Là vị trí tương đối của đối tượng kể từ đầu modul

> [!info] Địa chỉ tuyệt đối
> * Sinh ra từ địa chỉ tương đối trong giai đoạn nạp chương trình thực thi vào bộ nhớ để thực hiện
> > [!example] 
> > Với PC: địa chỉ tương đối \<Seg :Ofs\> -> Seg * 16 + Ofs
> 
> * Là địa chỉ của đối tượng trong bộ nhớ vật lý (địa chỉ vật lý)

#### Xác định địa chỉ
* Xác định địa chỉ câu lệnh và dữ liệu có thể thực hiện ở các giai đoạn khác nhau khi xử lý chương trình ứng dụng
	* **Giai đoạn dịch** :
		* Sử dụng nếu biết chương trình sẽ nằm ở đâu trong bộ nhớ
		* Khi dịch sẽ sinh ra địa chỉ tuyệt đối
		* Phải dịch lại khi vị trí bắt đầu thay đổi
	* **Thời điểm nạp** :
		* Sử dụng khi không biết chương trình sẽ nằm ở đâu trong bộ nhớ
		* Các đối tượng sẽ được dịch ra sẽ mang địa chỉ tương đối
		* Xác định địa chỉ được hoãn lại tới khi nạp chương trình vào bộ nhớ.
	* **Trong khi thực hiện** : 
		* Sử dụng khi các tiến trình có thể thay đổi vị trí trong khi thực hiện
		* Xác định địa chỉ được hoãn lại tới khi thực thi chương trình
		* Được sử dụng trong nhiều hệ điều hành 
![[Pasted image 20221205125753.png]]

> [!info] Địa chỉ logic (Địa chỉ ảo)
> * Được sinh ra trong tiến trình (CPU đưa ra)
> * Được khối quản lý bộ nhớ (MMU) chuyển sang địa chỉ vật lý khi truy cập tới đối trượng trong chương trình.

> [!info] Địa chỉ vật lý
> * Địa chỉ của một phần tử (byte/word) của bộ nhớ
> * Tương ứng với địa chỉ logic được CPU đưa ra

> [!note] Chương trình làm việc với địa chỉ logic

![[Pasted image 20221220084830.png]]

### 1.4 Các cấu trúc chương trình
#### Cấu trúc tuyến tính
* Sau khi biên tập, các module được tập hợp thành một chương trình hoàn thiện
	* Chứa đầy đủ các thông tin để có thể thực hiện được
	* Các biến trỏ ngoài đã thay bằng 1 giá trị cụ thể
	* Để thực hiện, chỉ cần **định vị 1 lần trong bộ nhớ**
![[Pasted image 20221220085112.png]]

> [!check] Ưu điểm
> * Đơn giản, dễ tổ chức biên tập và định vị chương trình
> * Thời gian thực hiện nhanh
> * Tính lưu động cao

> [!failure] Nhược điểm
> * Lãng phí bộ nhớ (ko phải toàn bộ chương trình đều cần thiết cho thực hiện chương trình)
> * Không thực hiện được chương trình có kích thước lớn hơn kích thước bộ nhớ vật lý

#### Cấu trúc nạp động
* Mỗi modul được biên tập riêng
* Khi thực hiện, hệ thống sẽ định vị  modul gốc
* Cần tới modul nào sẽ xin bộ nhớ và giải nạp modul vào
* Khi sử dụng xong một modul, hoặc khi thiếu vùng nhớ sẽ đưa những modul  không cần thiết ra ngoài.

![[Pasted image 20221220091004.png]]

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
* Các liên kết sẽ hoãn lại tới khi thực hiện chương trình
* Một phần của đoạn mã (stub) được sử dụng để tìm kiếm thủ tục tương ứng trong thư viện trong bộ nhớ.
* Khi tìm thấy, stub sẽ được thay thế bởi địa chỉ của thủ tục và thực hiện thủ tục.

> [!check] Hữu ích cho xây dựng thư viện

### Cấu trúc Overlays
* Modul được chia thành các mức
	* **Mức 0** - chứa modul gốc, nạp và định vị chương trình
	* **Mức 1** - chứa các modul được gọi từ những modul ở mức 0 và ko đồng thời tồn tại ...

* Bộ nhớ cũng được chia thành các mức **ứng với mức chương trình**
	* Kích thước bằng kích thước của modul lớn nhất cùng mức

* Cần cung cấp thêm các thông tin:
	* Chương trình bao nhiêu mức?
	* Mỗi mức gồm những modul nào ?
* Thông tin cung cấp được lưu trong file (sơ đồ Overlays)

![[Hệ Điều Hành-Chuong 3-38-45.pdf]]

* Module mức 0 được biên tập thành **file thực thi riêng**

* Khi thực hiện chương trình
	* Nạp module mức 0 như chương trình tuyến tính
	* Các module khác khi cần tới sẽ được nạp vào **mức bộ nhớ tương ứng**
		* Nếu có module đồng mức tồn tại : đưa ra bên ngoài

**NHẬN XÉT**: 
* Cho phép chạy chương trình có kích thước lớn hơn kích thước HĐH dành cho.
* Yêu cầu người sử dụng cung cấp các thông tin phụ
	* Hiệu quả sử dụng phụ thuộc vào các thông tin được cung cấp

* Hiệu quả sử dụng bộ nhớ phụ thuộc vào cách tổ chức các module  trong chương trình

> [!warning]
> Nếu tồn tại một module có kích thước lớn hơn các modul khác cùng mức rất nhiều 
> -> **Hiệu quả giảm rõ rệt**

* Quá trình nạp các module là động, nhưng chương trình có tính chất tĩnh 
 **=> Không thay đổi trong các lần thực hiện**

* Cung cấp thêm bộ nhớ tự do, hiệu quả vẫn không đổi.

## 2. Các chiến lược quản lý bộ nhớ
### 2.1 Chiến lược phân chương cố định
> [!abstract] Nguyên tắc
> * Bộ nhớ được chia thành n phần
> * Mỗi phần gọi là 1 chương (partition)
> 	* Kích thước: ko nhất thiết phải bằng nhau
> 	* Được sử dụng như 1 vùng nhớ độc lập
> 		* Tại 1 thời điểm chỉ cho phép 1 CT tồn tại
> 		* Các CT nằm trong vùng nhớ cho tới khi kết thúc

![[Pasted image 20221220095742.png]]

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
> [!abstract] Nguyên tắc
> Chỉ có **1 danh sách** quản lý bộ nhớ tự do
> * Thời điểm ban đầu, toàn bộ bộ nhớ là **tự do** với các tiến trình => Vùng trống lớn nhất (hole)
> 
> * Khi tiến trình yêu cầu bộ nhớ:
> 	* Tìm trong DS vùng trống một **phần tử đủ lớn** cho yêu cầu
> 	* Nếu tìm thấy:
> 		* Vùng trống được chia làm hai phần
> 		* 1 phần cung cấp cho TT
> 		* 1 phần trả lại danh sách vùng trống tự do
> 	* Nếu ko tìm thấy:
> 		* Chờ tới khi tìm được vùng trống thoả mãn
> 		* Cho phép tiến trình khác trong hàng đợi thực hiện (nếu **độ ưu tiên** đảm bảo)
> 
> * Khi tiến trình kết thúc:
> 	* Vùng nhớ được trả về DS quản lý ban đầu
> 	* Kết hợp với các vùng trống khác liền kề nếu cần

![[Pasted image 20221220100613.png]]

> [!note] Các chiến lược chọn vùng trống cho yêu cầu
> * ***First Fit*** - vùng trống đầu tiên thoả mãn
> * ***Best Fit*** - vùng trống vừa vặn nhất
> * **Worst Fit** - vùng trống kích thước lớn nhất

#### Buddy Allocation
> [!note] Cung cấp nhớ
> Chia đôi liên tiếp vùng trống tự do cho tới khi thu được vùng trống nhỏ nhất thoả mãn

> [!example] Ví dụ
> Cung cấp cho yêu cầu n bytes
> * Chia vùng trống tìm được thành 2 khối bằng nhau (buddies)
> * Tiếp tục chia vùng trống trên thành 2 phần cho tới khi đạt vùng trống nhỏ nhất có kích thước lớn hơn n. 
> * Đối với yêu cầu 800 bytes thì cần vùng trống 1k Bytes
> ![[Pasted image 20221220160240.png]]

* Hệ thống duy trì các danh sách vùng trống kích thước 1,2,..., 2^n bytes
* Với yêu cầu K -> tìm phần tử nhỏ nhất có kích thước lớn hơn K
* Nếu phần tử nhỏ nhất có kích thước > 2K -> tiến hành chia liên tiếp cho tới khi được vùng nhỏ nhất có kích thước lớn hơn  K

> [!check] Có tốc độ duyệt nhanh ( với bộ kích thước n, chỉ cần duyệt $\log _2 n$ danh sách)

> [!note] Thu hồi vùng nhớ
> * Kết hợp 2 vùng kề nhau có cùng kích thước
> * Tiếp tục kết hợp liên tiếp cho tới khi tạo ra **vùng trống lớn nhất** có thể

> [!example] Ví dụ
> ![[Pasted image 20221220161727.png]]
> * Giải phóng vùng nhớ thứ nhất (1K)
> 	* 2 * 1K = 2K
> * Giải phóng vùng nhớ thứ hai (2K)
> 	* 2 * 2K = 4K
> * Giải phóng vùng nhớ thứ ba (2K)
> 	* Kết hợp 2 vùng 2K thành vùng 4K
> 	* Kết hợp 2 vùng 4K thành vùng 8K
> 	* Kết hợp 2 vùng 8K thành vùng 16K


* Địa chỉ của hai khối nhớ chỉ khác nhau ở bit thứ **k**
![[Pasted image 20221220162129.png]]

#### Vấn đề bố trí lại bộ nhớ
* Sau một thời gian hoạt động, các vùng trống nằm rải rác khắp nơi gây ra hiện tượng thiếu bộ nhớ.
> [!warning] Cần bố trí lại bộ nhớ

> [!note] Dịch chuyển các tiến trình
> * Vấn đề không đơn giản vì các đối tượng bên trong khi chuyển sang vị trí mới sẽ có địa chỉ khác.
> 	* Sử dụng thanh ghi dịch chuyển (relocatiopn register) chứa giá trị bằng độ dịch chuyển của tiến trình
> * Vấn đề lựa chọn phương pháp để chi phí nhỏ nhất
> 	* Tất cả về một phía -> **Vùng trống lớn nhất**
> 	* Dịch chuyển để tạo ra ngay lập tức một vùng trống vừa vặn

> [!note] Phương pháp tráo đổi (swapping)
> * Lựa chọn thời điểm dừng tiến trình đang thực hiện
> * Đưa tiến trình và trạng thái tương ứng ra bên ngoài
> 	* Giải phóng vùng nhớ để kết hợp với các phần tử liền kề
> * Tái định vị vào vị trí cũ và khôi phục trạng thái cũ
> 	* Dùng thanh ghi dịch chuyển nếu đưa vào vị trí khác

> [!check] Ưu điểm
> * Không phải sao lưu modul điều khiển ra nhiều nơi
> * Tăng/giảm hệ số song tuỳ theo số lượng và kích thước chương trình

> [!failure] Nhược điểm
> * Không thực hiện được chương trình có kích thước **lớn hơn** kích thước bộ nhớ vật lý
> * Gây ra hiện tượng **rác** 
> >Bộ nhớ ko được sử dụng, cũng ko nằm trong DS quản lý bộ nhớ tự do, do lỗi HĐH hoặc do phần mềm phá hoại
> * Gây ra hiện tượng **phân đoạn ngoài** 
> > Vùng nhớ tự do được quản lý đầy đủ, nhưng nằm rải rác nên không sử dụng được
> * Gây ra hiện tượng **phân đoạn trong**
> > Vùng nhớ dành cho chương trình nhưng không được chương trình sử dụng tới.

### 2.3 Chiến lược phân đoạn
#### Chương trình
> [!note] Chương trình thường gồm các modul
> * 1 CT chính (main prog)
> * Tập các chương trình con
> * Các biến, các cấu trúc dữ liệu ...

* Các modul, đối tượng trong c/trình được **xác định bằng tên**
	* Hàm `sqrt()`, thủ tục `printf()`
	* x, y, counter, Buffer ...

* Các phần tử trong modul được xác định theo độ lệch với vị trí ban đầu
	* Câu lệnh thứ 10 của hàm `sqrt()` ...
	* Phần tử thứ 2 của mảng Buffer ....

> [!note] Không quan tâm tới việc chương trình được tổ chức ntn trong bộ nhớ.

#### Quan điểm người dùng
* Khi đưa ctrinh vào bộ nhớ để thực hiện, ctrình có **nhiều đoạn khác nhau**
* Mỗi đoạn là 1 **khối logic**, ứng với một module
	* Mã lệnh: `main()`, thủ tục, hàm ...
	* Dữ liệu: đối tượng toàn cục, cục bộ
	* Các đoạn khác: stack, mảng

* Mỗi đoạn chiếm **một vùng liên tục**
	* Có vị trí bắt đầu và kích thước
	* Có thể nằm tại bất cứ đâu trong bộ nhớ

* Mỗi đối tượng trong đoạn được xác định bởi **vị trí tương đối** so với đầu đoạn
![[Hệ Điều Hành-Chuong 3-77-79.pdf]]

#### Cấu trúc phân đoạn
> [!note] Cấu trúc phân đoạn
> * Chương trình là tập hợp các đoạn (modul, segment)
> 	* Tên đoạn (**số hiệu đoạn**), **độ dài** của đoạn
> 	* Mỗi đoạn có thể được **biên tập riêng**
> * Khi dịch và biên tập chương trình tạo ra ***Bảng quản lý đoạn (Segement Control Block - SCB)***
> 	* Mỗi phần tử của bảng ứng với một đoạn của chương trình
> 	![[Pasted image 20221220174709.png]]
> 	* ***Dấu hiệu (Mark)*** - mang giá trị 0/1 dựa trên sự tồn tại của đoạn trong bộ nhớ
> 	* ***Địa chỉ (Address)*** - vị trí cơ sở của đoạn trong bộ nhớ
> 	* ***Độ dài (Length)*** - độ dài của đoạn
> * ***Địa chỉ truy cập*** = <`tên(số hiệu đoạn)`, `độ lệch trong đoạn`>

^f33fe2

> [!example] 
> ![[Hệ Điều Hành-Chuong 3-81-88.pdf]]

#### Chuyển đổi địa chỉ
Khi thực hiện chương trình
* Bảng quản lý đoạn được nạp vào bộ nhớ
	* ***Segment-table base register (STBR)***: Vị trí SCB trong bộ nhớ
	* ***Segment-table length register (STLR)***: số phần tử của SCB

![[Pasted image 20221220201453.png]]

> [!note] Khi truy cập tới địa chỉ logic <s,d>
> 1. s $\geq$ STLR: lỗi
> 2. STBR + s * K: vị trí phần tử s trong SCB
> 3. Kiểm tra trường dấu hiệu M của phần tử SCBs
> 	* **M = 0**: đoạn s chưa tồn tại trong bộ nhớ => lỗi truy nhập => HĐH phải nạp đoạn
> 		* Xin vùng nhớ có kích thước được ghi trong L
> 		* Tìm module tương ứng ở bộ nhớ ngoài và nạp và định vị vào vùng nhớ xin được
> 		* Sửa lại trường địa chỉ A và trường dấu hiệu M (M=1)
> 		* Truy nhập bộ nhớ như trường hợp M = 1
> 	* **M = 1**: đoạn đã tồn tại trong bộ nhớ
> 		* d $beq$ Ls: lỗi  truy nhập (vượt quá kích thước đoạn)
> 		* d + As: Địa chỉ vật lý cần tìm

> [!check] Ưu điểm
> * Sơ đồ nạp Module không cần sự tham gia của người sử dụng
> * Dễ dàng thực hiện nhiệm vụ bảo vệ đoạn
> 	* Kiểm tra lỗi truy nhập bộ nhớ
> 		* Địa chỉ không hợp lệ: vượt quá kích thước đoạn
> 	* Kiểm tra tính chất truy nhập
> 		* Đoạn mã: chỉ đọc 
> 		-> *Viết vào đoạn mã: lỗi truy nhập*
> 	* Kiểm tra quyền truy nhập module
> 		* Thêm trường quyền truy nhập (user/system) vào SCB
> * Cho phép sử dụng **chung đoạn**
> 	* VD: soạn thảo văn bản
> 	![[Pasted image 20221220203946.png]]

> [!warning] Vấn đề chính của việc dùng chung đoạn
> * Đoạn dùng chung phải cùng
> 	* Số hiệu trong SCB
> * Giải quyết bằng cách truy nhập gián tiếp
> 	* JMP +08
> 	* Thanh ghi đoạn chứa số hiệu đoạn

> [!failure] Nhược điểm
> * Hiệu quả sử dụng phụ thuộc vào cấu trúc chương trình
> * Bị phân mảnh bộ nhớ
> 	* Phân phối vùng nhớ theo các chiến lược First fit/ best fit 
> 	* Cần phải bố trí lại bố nhớ (dịch chuyển, swapping)
> 		* Có thể dựa vào bảng SCB
> 			* M = 0: đoạn chưa nhập vào
> 			* Vùng nhớ được xác định bởi A và L được trả về Danh sách tự do
> 		* Vấn đề lựa chọn module cần đưa ra 
> 			* Module tồn tại lâu nhất
> 			* Module có lần sử dụng cuối cách xa nhất
> 			* Module có tần xuất sử dụng thấp nhất
> 		=> Cần phương tiện ghi lại số lần và thời điểm truy nhập đoạn

> [!tip] Giải pháp:
> Phân phối bộ nhớ theo các đoạn bằng nhau (page)

### 2.4 Chiến lược phân trang
> [!abstract] Nguyên tắc
> * Chia bộ nhớ vật lý được chia thành từng khối có kích thước bằng nhau, gọi là ***frame***.
> 	* Trang vật lý được đánh số 0,1,2 -> địa chỉ vật lý của trang
> 	* Trang được dùng làm **đơn vị phân phối nhớ**
> * Bộ nhớ logic (chương trình) được chia thành từng khối có kích thước bằng trang vật lý, gọi là ***page***.

> [!info] Lỗi trang - Page fault
> **Nếu trang nhớ đó chưa nằm trong bộ nhớ chính**, hiện tượng này chúng ta gọi là lỗi trang (Page fault), khối MMU sẽ báo cho hệ điều hành để hệ điều hành tiến hành nạp trang tương ứng từ bộ nhớ ngoài (ví dụ: ổ cứng) và tiến hành thực thi lại lệnh trước đó.

* Khi thực hiện chương trình:
	* Nạp trang logic từ bộ nhớ ngoài vào trang vật lý
	* Xây dựng một ***bảng quản lý trang*** (Page Control Block - PCB) để xác định mối quan hệ giữa trang vật lý và trang logic.
	* Mỗi phần tử của PCB ứng với một trang CT
		* Cho biết trang vật lý chứa trang logic tương ứng.
	* Địa chỉ truy nhập được chia thành:
		* **Số hiệu trang - p**: chỉ số trong PCB để tìm địa chỉ cơ sở trang
		* **Độ lệch trong trang - d**: kết hợp địa chỉ cơ sở của trang để tìm ra địa chỉ vật lý.

*👉 Liên hệ tới bảng phân đoạn [[Chap3 - Quản lý bộ nhớ#^f33fe2]]*
![[Hệ Điều Hành-Chuong 3_Reduced-105-108.pdf]]

> [!note] 
> * **Dung lượng** trang luôn là **luỹ thừa 2** ( cho phép ghép giữa số hiệu trang vật lý và độ lệch trang)
> 	* VD: bộ nhớ n bit, kích thước trang 2^k 
> 	![[Pasted image 20230115211834.png]]
> * **Không cần nạp toàn bộ** trang logic vào
> 	* Số frame phụ thuộc vào kích thước bộ nhớ, trong khi đó số page tuỳ ý
> 	* PCB cần **Mark** để nhận biết trang đã được nạp vào bộ nhớ hay chưa
> 		* 0 - trang chưa được lưu vào bộ nhớ vật lý
> 		* 1 - trang đã được đưa vào 

|Phân trang|Phân đoạn|
|---|---|
|Các modul phụ thuộc cấu trúc logic của CT|Các khối có kích thước độc lập kích thước CT </br> nhưng phụ thuộc vào phần cứng|

![[Pasted image 20230115213457.png]]

#### Nạp CT vào bộ nhớ
![[Pasted image 20230115213704.png]]

> [!note]
> * Nếu đủ trang vật lý tự do -> **Nạp toàn bộ**
> * Nếu không đủ trang vật lý tự do -> **Nạp từng phần**

#### Truy nhập bộ nhớ

![[Pasted image 20230115213846.png]]
* Nạp CT:
	* Xây dựng bảng quản lý trang và luôn giữ trong bộ nhớ
		* **Page-table base register - PTBR** trỏ tới PCB
		* **Page-table length register - PTLR** kích thước PCB
* Thực hiện truy nhập
	* Địa chỉ truy nhập được chia thành dạng <p,d>
	* $PTBR + p * K$ = địa chỉ phần tử p của PCB trong bộ nhớ (K là kích thước 1 phần tử của PCB)
* Kiểm tra Mp (Mark of p):
	* Mp = 0 -> Lỗi trang, sinh ra ngắt để tiến hành nạp trang
		* Xin trang vật lý tự do
		* Tìm kiếm trang logic ở bộ nhớ ngoài và nạp trang
		* Sửa lại trường địa chỉ A (address) và dấu hiệu M
	* Mp = 1 -> trang đã tồn tại
		* Lấy Ap  ghép với d ra địa chỉ cần tìm

#### Nạp trang và thay thế trang
> [!warning] 
> * TH số trang vật lý dành cho CT lớn
> 	* Thực hiện nhanh, nhưng hệ số song song giảm
> * TH số trang vật lý dành cho CT bé
> 	* Hệ số song song cao nhưng thực hiện chậm do hay thiếu trang
> 
> **=> Hiệu quả phụ thuộc nhiều vào các chiến lược nạp trang và thay thế trang**

* Các chiến lược nạp trang:
	* **Nạp tất cả** - nạp toàn bộ CT
	* **Nạp trước** - dự báo trang cần thiết tiếp theo
	* **Nạp theo yêu cầu** - chỉ nạp khi cần thiết

* Các chiến lược thay thế trang:
	* FIFO
	* LRU - Least Recently Used
	* LFU - Least Frequently Used

> [!check] Ưu điểm của chiến lược phân trang
> * Tăng tốc độ truy nhập 
> * Không tồn tại hiện tượng phân đoạn ngoài
> * Hệ số song song cao
> * Dễ dàng thực hiện nhiệm vụ bảo vệ
> * Cho phép sử dụng chung trang

> [!note] Dùng chung trang - Soạn thảo văn bản 
> ![[Pasted image 20230115232705.png]]
> * Cần thiết trong môi trường hoạt động có sự chia sẻ -> giảm kích thước vùng nhớ cho tất cả các tiến trình
> * Phần mã dùng chung:
> 	* Chỉ có 1 phiên bản chia sẻ giữa các TT trong bộ nhớ
> 	* Vấn đề nảy sinh: mã dùng chung ko đổi -> Trang dùng chung phải cùng vị trí trong không gian logic của tất cả các TT -> Cùng số hiệu trong bảng quản lý trang
> * Phần mã và dữ liệu riêng biệt cho các TT có thể nằm ở bất cứ đầu trong bộ nhớ logic của TT

> [!failure] Nhược điểm của chiến lược phân trang
> * Tồn tại hiện tượng phân đoạn trong
> 	* Luôn xuất hiện ở trang cuối 
> 	* Có thể giảm kích thước trang để giảm hiện tượng phân đoạn ?
> 		* Ko vì sẽ tăng khả năng gặp lỗi trang
> 		* Và làm tăng kích thước của bảng quản lý trang
> * Đòi hỏi hỗ trợ của phần cứng (chi phí lớn)
> * Khi CT lớn, PCB có nhiều phần tử -> tốn bộ nhớ lưu trữ PCB
> 
> ✅Solution : Dùng ***Trang nhiều mức***

> [!info] Trang nhiều mức
> Bảng quản lý được phân trang
> ![[Hệ Điều Hành-Chuong 3_Reduced-122-126.pdf]]

### 2.5 Chiến lược kết hợp phân đoạn - phân trạng
> [!abstract] Nguyên tắc
> * CT được biên tập theo chế độ **phân đoạn**
> 	* Tạo ra bảng quản lý đoạn SCB
> 	* Mõi phần tử của bảng quản lý đoạn ứng với 1 đoạn (<M,A,L>)
> * Mỗi đoạn được biên tập riêng theo chế độ **phân trang**
> 	* Tạo ra bảng quản lý trang cho từng đoạn
> * Địa chỉ truy nhập: **<s,p,d>**
> * Thực hiện truy nhập địa chỉ:
> 	* $STBR + s = As$ - địa chỉ phần tử s
> 	* Kiểm tra Ms, nạp PCBs nếu cần
> 	* $As + p = Ap$ - Địa chỉ phần tử p của PCBs
> 	* Kiểm tra Mp, nạp trang p nếu cần
> 	* Ghép Ap với d ra được địa chỉ cần tìm 

![[Pasted image 20230115234403.png]]

![[Pasted image 20230115234521.png]]

## 3. Bộ nhớ ảo
### 3.1 Giới thiệu
> [!question] Vì sao cần tới bộ nhớ ảo?
> ![[Pasted image 20230115234942.png]]
> * CT trong 1 không gian địa chỉ ảo có thể lớn tuỳ ý
> * Có thể có nhiều CT cùng tồn tại -> Tăng hiệu suất sử dụng CPU
> * Giảm yêu cầu vào/ra cho việc nạp và hoán đổi CT -> kích thước swap nhỏ hơn

![[Pasted image 20230115234956.png]]

> [!info]
> * Dùng bộ nhớ thứ cấp (HardDisk) lưu trữ phần CT chưa đưa vào bộ nhớ vật lý
> * Phân tách bộ nhớ logic của người dùng với bộ nhớ vật lý
> * VM ánh xạ địa chỉ trong CT tới địa chỉ vật lý
> * Cho phép thẻ ánh xạ vùng nhớ logic lớn vào bộ nhớ vật lý nhỏ
> * Cài đặt theo:
> 	* Phân trang
> 	* Phân đoạn
> 
> ![[Pasted image 20230115235331.png]]

* Nạp từng phần của trang CT vào bộ nhớ
	* Trang của TT có thể nằm trên bộ nhớ vật lý cũng như nằm trên bộ nhớ ảo
	* Biểu diễn nhờ 1 bit trong bảng quản lý trang (page table)
	* Khi yêu cầu trang, trang sẽ được đưa từ bộ nhớ thứ cấp (bộ nhớ ảo) -> bộ nhớ vật lý (RAM)
	[[Pasted image 20230115235639.png]]

* Xử lý lỗi trang:
	* Tiến hành đổi trang khi không có frames tự do
	[[Pasted image 20230115235830.png]]

> [!note] Đổi trang
> 1. Xác định vị trí trang logic trên đĩa
> 2. Lựa chọn trang vật lý
> 	* Ghi ra đĩa
> 	* Sửa lại bit valid - invalid trong page table
> 3. Nạp trang logic vào trang vật lý được chọn
> 4. Restart TT
> ![[Pasted image 20230116000137.png]]

### 3.2 Các chiến lược đổi trang
> [!note] FIFO - First In First Out
> ![[Pasted image 20230116000300.png]]
> 
> > **Đưa ra trang theo thứ tự vào, trang vào sớm nhất ra đầu tiên**
> 
> * Hiệu quả chỉ khi CT có cấu trúc tuyến tính
> * Kém hiệu quả khi CT theo nguyên tắc lập trình cấu trúc
> * Đơn giản, dễ thực hiện
> * Tăng trang vật lý, không đảm bảo giảm số lần gặp lỗi trang

> [!note] OPT/MIN - Thuật toán thay thế trang tối ưu
> ![[Pasted image 20230116000839.png]]
> > **Đưa ra trang có lần sử dụng tiếp theo cách xa nhất**
> 
> * Số lần gặp lỗi trang ít nhất
> * Khó dự báo được diễn biễn của CT

> [!note] LRU - Least Recently Used
> ![[Pasted image 20230116001124.png]]
> 
> > Đưa ra trang có lần sử dụng cuối cách xa nhất
> 
> * Hiệu quả cho chiến lược thay trang
> * Đảm bảo giảm số lỗi trang khi tăng số trang vật lý
> 	* Tập các trang trong bộ nhớ có n frames luôn là tập con của các trang trong bộ nhớ có n+1 frames
> * Yêu cầu sự trợ giúp kỹ thuật để chỉ ra thời điểm truy cập cuối

* Cài đặt LRU:
	* Dùng dãy số ghi trang
		* Truy cập tới 1 trang, cho phần tử tương ứng lên đầu
		* Thay thế trang, cho phân tử xuống cuối dãy
		* Thường cài đặt dưới dạng Double Linked-List (tuy vậy tốn thời gian trong việc gán con trỏ)
	* Bộ đếm
		* Thêm 1 trường ghi thời điểm truy nhập vào mỗi phần tử của PCB
		* Thêm vào khối điều khiển (C.U) đồng hồ/bộ đếm
		* Khi có yêu cầu truy nhập trang
			* Tăng bộ đếm
			* Chép nội dung bộ đếm vào trường thời điểm truy nhập tại phần tử tương ứng trong PCB
		* Cần có thủ tục cập nhật PCB (ghi vào trường thời điểm) và thủ tục tìm kiếm trang có giá trị trường thời điểm nhỏ nhất
		* Hiện tượng tràn số !?

#### Các thuật toán dựa trên bộ đếm
* Sử dụng bộ đếm (1 trường của PCB) ghi nhận số lần truy nhập tới trang

> [!note] LFU - Least Frequently Used
> > Trang có bộ đếm nhỏ nhất bị thay thế
> 
> * Trang được truy nhập nhiều đến -> là trang quan trọng -> hợp lý
> * Trang được dùng nhiều, nhưng chỉ ở giai đoạn đầu (trang mới tạo) -> cần dịch bộ đếm 1 bit theo thời gian


> [!note] MFU - Most Frequently Used
> > Trang có bộ đếm lớn nhất bị thay thế
> 
> * Trang có bộ đếm nhỏ nhất có thể là trang vừa được nạp vào và chưa được sử dụng nhiều
> -> có thể cần sử dụng trong tương lai

## 4. Quản lý bộ nhớ trong VXL họ intel


