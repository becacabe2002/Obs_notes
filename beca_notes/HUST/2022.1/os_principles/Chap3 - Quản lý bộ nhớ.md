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

### 2.5 Chiến lược kết hợp phân đoạn - phân trạng

## 3. Bộ nhớ ảo
### 3.1 Giới thiệu
### 3.2 Các chiến lược đổi trang

## 4. Quản lý bộ nhớ trong VXL họ intel


