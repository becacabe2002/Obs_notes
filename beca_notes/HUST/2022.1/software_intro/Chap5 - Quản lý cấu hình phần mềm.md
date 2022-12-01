## 1. Khái niệm quản lý cấu hình phần mềm 
* Quá trình phần mềm:
	* Khó khăn: "Sự thay đổi"
		* **Lý tưởng**: hạn chế sự thay đổi -> Sự ổn định: các yêu cầu
		* **Thực tế:** ko tồn tại các yêu cầu ổn định
> [!caution] Bất cự dự án pm nào cũng cần phải có chiến lược để <b>giải quyết vấn đề THAY ĐỔI</b>

### Sự tiến hoá của phần mềm
* PM phát triển theo tgian:
	* Nhiều yếu tố khác nhau đc tạo trong suốt tgian dự án
	* Nhiều phiên bản khác nhau
	* Các nhóm làm việc song song để đưa ra sp cuối cùng

-> Hệ thống có thể **Thay đổi liên tục**

* ***Nguồn thay đổi***:
	* Bên ngoài: từ các yêu cầu đầu vào cho quá trình phát triển
	* Bên trong: sự phát triển của các sản phẩm
![[Pasted image 20221114143641.png]]

### Cấu hình phần mềm
 > [!check] Các kết quả/sản phẩm:
 > + Chương trình
 > + Dữ liệu
 > + Tài liệu

> [!note] Các mục cấu hình phần mềm (software configuration items - SCIs)
> * Có thể ở các mức nhỏ: một biểu đồ UML
> * Có thể ở mức to: một thành phần phần mềm (software component)

**-> Sự thay đổi là tất yếu**

> [!info] Quản lý cấu hình phần mềm (Software configuration Management - SCM)
> * Quản lý các hệ thống phần mềm đang phát triển
> * Kiểm soát chi phí liên quan đến việc thực hiện các thay đổi đối với hệ thống.

### Thay đổi và Kiểm soát
* Nếu những thay đổi **không được kiểm soát** -> vượt khỏi tầm tay

* Vấn đề quản lý thay đổi là cần thiết trong dự án được thực hiện bởi nhiều người.

> [!caution] 
> Nếu không có các chiến lược và cơ chế thích hợp để kiếm soát các thay đổi không thể khôi phục về **bản sao cũ ổn định hơn** của pm, do bởi mọi thay đổi dều dẫn đến rủi ro.

### 1.2 Quản lý cấu hình phần mềm
> [!info]
> Bao gồm các:
>- **Nguyên tắc**
>- **Kỹ thuật**
>
> => Đánh giá và kiểm soát **sự thay đổi** của các sản phẩm PM trong và sau quá trình kỹ thuật PM

* Các tiêu chuẩn: IEEE 828, IEEE 1042

* Áp dụng một cách tiếp cận nghiêm ngặt để đảm bảo:
	* **Các chi tiết** trong hệ thống phần mềm đều được xác định
	* **Các thay đổi** với các mục khác nhau được ghi lại và thay đổi
	* **Tích hợp** thích hợp tất cả các mô-đun khác nhau.

![[20221114_145823.jpg]]

* SCM có thể **giúp xác định tác động của thay đổi** cũng như **kiểm soát sự phát triển**
 
*  SCM có thể theo dõi và kiểm soát các thay đổi trong tất cả các khía cạnh của phát triển PM (yêu cầu, thiết kế, mã hoá, kiểm thử, làm tài liệu...)

> [!note] Sự cần thiết của SCM
> - Ngăn ngừa các lỗi có thể tránh được phát sinh từ các thay đổi xung đột khi nhiều tài nguyên hệ thống thay đổi cùng với sự phát triển phần mềm.
> 
> - Thông thường nhiều phiên bản của phần mềm được phát hành và cần đến sự hỗ trợ
> 	- SCM cho phép 1 nhóm **hỗ trợ nhiều phiên bản**
> 	- SCM cho phép các **thay đổi trong các phiên bản tuần tự** được **truyền bá**
> 
> - Cho phép các nhà phát triển theo dõi các thay đổi và **khôi phục bất kỳ thay đổi** nào để đưa hệ thống phần mềm **về trạng thái an toàn** gần nhất


### 1.3 Các khái niệm trong SCM
#### Mục cấu hình (Configuarion Item - CI)
> [!info]
>các thực thể (cả phần cứng và phần mềm) được coi như là duy nhất được chỉ định để quản lý cấu hình

* Xác định: 
	* Định dạng duy nhất
	* Thời điểm bắt đầu quản lý cấu hình

* Các mục cấu hình phần mềm còn là tất cả các loại tài liệu cho sự phát triển của pm
	* tệp mã
	* Trình điều khiển cho các test case
	* Tài liệu phân tích hoặc thiết kế
	* TL hướng dẫn user
	* Cấu hình hệ thống

***Tìm kiếm các mục cấu hình***
*Các dự án lớn tạo ra rất nhiều thục thể cần phải được xác định duy nhất, nhưng ko phải tất cả đều cần được định cấu hình -> nên quản lí những gì, quản lí khi nào ?*

* Một số thực thể phải được duy trì kể cả sau khi giai đoạn phát triển kết thúc, để hỗ trợ khách hàng.

> [!note] 
> **Lược đồ đặt tên thực thể** được xác định để định danh cho các tài liệu liên quan.
> - Rất giống với mô hình đối tượng
> - Sử dụng các kỹ thuật tương tự mô hình hoá đối tượng để tìm CIs


![[Pasted image 20221114151958.png]]

#### Đường cơ sở (Baseline)
> [!info]
> Đặc tả kỹ thuật hoặc sản phẩm đã được thống nhất chính thức.
> -> được sử dụng như một cơ sở để tiếp tục phát triển, có thể thay đổi chỉ thông qua thủ tục kiểm soát thay đổi chính thức.

* Một **mốc quan trọng** trong sự phát triển của phần mềm được đánh dấu bằng việc **cung cấp một hoặc nhiều mục cấu hình phần mềm** và **sự chấp thuận của các SCIs** thu được thông qua đánh giá kỹ thuật chính thức.

* Có thể được định nghĩa ở **bất kỳ mức chi tiết nào**.

> [!example]-
> * Baseline A: API của một chương trình được xác định hoàn toàn, phần thân các phương thức trống
> * Baseline B: tất cả các phương thức truy cập dữ liệu được thực hiện và kiểm thử; bắt đầu lập trình GUI
> * Baseline C: GUI được triển khai, giai đoạn thử nghiệm bắt đầu.

* Các SCI đã xác định đường cơ sở và cơ sở dữ liệu dự án:
![[Pasted image 20221114152928.png]]

#### Kho lưu trữ SCM (SCM Repository)
> [!info] SCM Repository
> Tập các **cơ chế hoạt động** và **cấu trúc dữ liệu** cho phép một nhóm phát triển phần mềm có thể **quản lý thay đổi, phát triển, bảo trì phần mềm** một cách hiệu quả.

![[Pasted image 20221114153541.png]]

* Một kho lưu trữ (repository) dữ liệu có các đặc trưng: 
	* ***Phiên bản*** - lưu trữ tất cả các phiên bản để cho phép quản lý các phiên bản đã đóng gói của SP
	* ***Theo dõi sự phục thuộc và quản lý thay đổi*** - các kho quản lý lưu trữ mối quan hệ giữa các yếu tố được lưu trữ 
	* ***Yêu cầu tìm kiếm*** - cung cấp để có thể theo dõi tất cả các bản thiết kế và các thành phần xây dựng và các sản phảm mà kết quả từ một đặc tả cụ thể
	* ***Quản lý cấu hình*** - lưu trữ những cấu hình cụ thể đại diện cho sự quan trọng và các sản phẩm đã đóng gói.
	* ***Thông tin tác giả*** - thông tin về thời gian bắt đầu/kết thúc, người thực hiện theo từng phiên bản

### Thự mục SCM (SCM Directory)
![[Pasted image 20221121112328.png]]

> [!note]- Programmer's Directory
> * IEEE: Dynamic Library
> * Chứa các thực thể của pm mới được tạo hoặc sửa đổi
> * Không gian làm việc của lập trình viên chỉ do ltv kiểm soát

>[!note]- Master Directory
>* IEEE: Controlled Library
>* Quản lý, kiểm soát các thay đổi với baselines
>* Mục nhập được kiểm soát, thường sau khi xác minh
>* Các thay đổi phải được cho phép

> [!note]- Software Repository
> * IEEE: Static Library
> * Lưu trữ các baseline khác nhau được phát hành để sử dụng chung
> * Cung cấp bản sao baseline cho các tổ chức yêu cầu.

#### Version vs Revision vs Release
* Version: 1.0
* Revision: 1.0.156
>[!info] Version
>Bản phát hành **ban đầu** hoặc tái phát hành một mục cấu hình (SCI) được liên kết với bản biên dịch hoặc biên dịch lại **hoàn chỉnh** của mục đó. Các phiên bản khác nhau có chức năng khác nhau.

> [!info] Revision
> Thay đổi thành phiên bản chỉ **sửa các lỗi trong thiết kế/mã**, nhưng ko ảnh hưởng đến chức năng đã được lập thành tài liệu.

> [!info] Release
> Việc **phân phối chính thức** phiên bản đã được phê duyệt

[Doc them](https://cloudgeeks.net/tim-hieu-ve-cach-danh-version-phien-ban-phan-mem/)

#### Các thành phần của một hệ thống quản lý cấu hình
* **Các yếu tố cấu phần** - tập công cụ trong một hệ thống quản lý tập tin, cho phép truy cập và quản lý mỗi mục cấu hình phần mềm.

* **Các yếu tố xử lý** - tập các thủ tục và nhiệm vụ xác định một phương pháp hiệu quả quản lý sự thay đổi cho tất cả các cử tri liên quan về quản lý, kĩ thuật và sử dụng pm máy tính. 

* **Các yếu tổ xây dựng** - một tập hợp các công cụ tự động hoá việc xây dựng các pm bằng cách đảm bảo rằng các thiết lập thích hợp của các thành phần được phê duyệt  đã được lắp ráp

* **Các yếu tố con người** - để thực thi SCM hiệu quả, nhóm nghiêm cứu phần mềm sử dụng 1 tập hợp các công cụ và tính năng quá trình (bao gồm các yếu tố khác ngoài SCM)

## 2. Quy trình quản lý cấu hình phần mềm
### 2.1 Quy trình SCM
* 5 nhiệm vụ của SCM:
![[Pasted image 20221114154921.png]]

* Cung cấp một **kho chứa an toàn** đối với các kết quả bàn giao

* Cho phép việc kiểm soát và tiết lộ có nguyên tắc các kết quả bàn giao thông qua vòng đời của nó, với đầy đủ các dấu tích lịch sử, đảm bảo phiên bản đúng và cập nhật, đã được kiểm tra và phát hành.

* Kiểm soát thay đổi của các kết quả bàn giao, đảm bảo các kết quả này được lưu theo đúng thứ tự.

* Cung cấp việc lập báo cáo về hiện trạng của các kết quả bàn giao và những thay đổi của chúng.

### 2.2 Các hoạt động trong SCM
* ***Quản lý phiên bản:***
	* Sự tăng trưởng: tạo ra các phiên bản cho các nhà phát triển khác
	* Phát hành: việc tạp ra các phiên bản cho khách hàng và người dùng
	* Nhánh: sự phát triển đồng thời
	* Biến thể: các phiên bản dự định cùng tồn tại

* ***Quản lý thay đổi:*** 
	* Xem xét, xử lý các thay đổi
	* Xét duyệt các thay đổi
	* Theo dõi các thay đổi

* **Kiểm toán cấu hình:** Đánh giá cấu hình phần mềm bổ sung cho việc xét duyệt kỹ thuật

* ***Báo cáo trạng thái:*** Cung cấp thông tin về trạng thái (Điều gì đã xảy ra? Ai làm nó? Nó xảy ra khi nào?Những gì sẽ bị ảnh hưởng?)

### 2.3 Các vai trò trong SCM
> [!info] Người quản lý cấu hình
> Xác định các CI
> Xác định các thủ tục để tạo các sự tăng trưởng và các bản phát hành

> [!info] Thành viên ban kiểm soát thay đổi
> Phê duyệt hoặc từ chối các yêu cầu thay đổi

 > [!info] Lập trình viên
 > Tạo các thay đổi được kích hoạt bởi các yêu cầu.
 > Kiểm tra các thay đổi
 > Giải quyết xung đột
 
> [!info] Kiểm soát viên
> Lựa chọn, đánh giá các thay đổi để phát hành.
> Đảm bảo tính nhấtq quán và đầy đủ của bản phát hành

## 3. Quản lý phiên bản (Version Control)
[[Git advanced - Tools and Concepts]]
### 3.1 Khái niệm quản lý phiên bản
> [!info] Version Control
> Quá trình theo dõi các phiên bản khác nhau của phần mềm hoặc CSI và hệ thống mà các thành phần này sử dụng
> * Quản lý baseline
> * Chỉ định các phiên bản thành phần được bao gồm trong hệ thống cụ thể

* Đảm bảo các thay đổi do các nhà phát triển khác nhau không ảnh hưởng lẫn nhau

### 3.2 Hệ thống kiểm soát phiên bản
* Kết hợp các **thủ tục** và **công cụ** để quản lý các phiên bản khác nhau của các đối tượng cấu hình được tạo ra.

> [!note] Chức năng của hệ thống kiểm soát phiên bản
> * **Cơ sở dữ liệu dự án** - lưu trữ tất cả các CI
> 
> * **Quản lý phiên bản** - lưu trữ tát cả các phiên bản của đối tượng cấu hình
> 
> * **Make facility** - cho phép kỹ sư pm thu thập tất cả các đối tượng cấu hình có liên quan, xây dựng một phiên bản đặc biệt của phần mềm.
> 
> * **Theo dõi vấn đề** - cho phép các nhóm ghi lại, theo dõi tình trạng của tất cả các vấn nổi bật liên quan đến từng đối tượng cấu hình.

#### Public repository (PR), Private workspaces (PW)
1. PR duy trì **phiên bản chính**
2. Các nhà phát triển sao chép (check-out) phiên bản về PW và sửa đổi bản sao.
3. Các thành phần thay đổi sau khi hoàn thành sẽ được trả lại vào PR (check-in)

#### Kiểm soát phiên bản tập trung
> [!info]
> Có một kho lưu trữ chính duy nhất duy trì tất cả các phiên bản của các thành phần pm đang được phát triển.
> > [!example] Subversion

* Nếu nhiều người đang làm việc trên cùng 1 thành phần cùng lúc, mỗi người check-out từ kho lưu trữ
-> Hệ thống sẽ cảnh báo rằng nó đã được người khác check-out

![[Pasted image 20221121135016.png]]

#### Kiểm soát phiên bản phân tán
> [!info]
> Tồn tại nhiều phiên bản của kho thành phần cùng một lúc.
> > [!example] Git

* Kho lưu trữ ***Master*** được tạo trên máy chủ duy trì source code
* Thay vì check-out các tệp cần dùng, nhà phát triển tạo bản sao của kho lưu trữ dự án xuống PW
* Các nhà phát triển làm việc trên các tệp được yêu cầu và **duy trì các phiên bản mới** trên kho lưu trữ riêng trên máy tính của mình.
* Khi các thay đổi được thực hiện, nhà ptr commit những thay đổi và cập nhật kho lưu trữ riêng.
	* Sau đó các thay đổi được push vào kho dự án.

![[Pasted image 20221121135427.png]]

> [!note] Branching & Merging
> * Thay vì chuỗi phiên bản tuyến tính phản ánh các thay đổi đối với các thành phần theo tgian, có chuỗi độc lập (***Branching***)
> 
> * Ở một số giai đoạn, có thể cần hợp nhất các nhánh dòng mã để tạo phiên bản mới của thành phần bao gồm tất cả các thay đổi đã được thực hiện. (***Merging***)
> ![[Pasted image 20221121140642.png]]

> [!check] Lợi ích
> * Cung cấp một số cơ chế sao lưu cho kho lưu trữ
> * Cho phép hoạt động ngoại tuyến để các nhà phát triển có thể thực hiện các thay đổi nếu không có kết nối mạng
> * Các nhà phát triển có thể biên dịch và kiểm tra toàn bộ hệ thống trên máy cục bộ và kiểm tra những thay đổi đã thực hiện.

### 3.3 Đánh số phiên bản

## 4. Quản lý thay đổi
![[CNPM05 - Quan ly cau hinh PM-55-67.pdf]]
