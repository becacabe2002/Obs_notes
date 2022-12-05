	## 1. Khái niệm
>[!info] Yêu cầu phần mềm (Software requirement)
> Mong muốn/nhu cầu: khách hàng, người dùng mong đợi.
> 
> ***Yêu cầu*** - đơn giản là phát biểu cái mà phần mềm, hệ thống phải làm hoặc dặc tính mà phần mềm/ hệ thống phải có.

> [!note] Yêu cầu có nhiều mức độ:
>* Lĩnh vực/nghiệp vụ mà nó phải thoả mãn
>* Bài toán của khách hàng
>* Nhu cầu/ràng buộc của các bên liên quan

### Kỹ nghệ yêu cầu phần mềm (Software requirement engineering - SRE)
> [!info] Khởi đầu (Inception) 🏁: 
>* Vấn đề cần giải quyết
>* Đối tượng cần giải pháp
>* Loại giải pháp mong muốn
>* Mức độ hiệu quả ban đầu của việc trao đổi thông tin giữa hai bên.

> [!info] Khám phá (Eliciation)  🔍: 
> xác định tất cả các yêu cầu của khách hàng (hỏi đáp, phỏng vấn, phân tích xu hướng, xin ý kiến tham vấn)

> [!info] Xây dựng (Elaboration) ⚒️: 
> phân tích yêu cầu về dữ liệu, chức năng, hành vi
>-> Hiểu rõ về yêu cầu

> [!info] Đàm phán (Negotiation) 🤝
> Đồng ý với một hệ thống có thể bàn giao một cách thực tế đối với cả 2 bên.

> [!info] Đặc tả (Specification)
> tài liệu ghi nhận đầy đủ yêu cầu (SRS), có thể là một hoặc nhiều thứ sau:
> * Một tài liệu được viết 
> * Một tập hợp các mô hình
> * Một hình thức biểu diễn toán học
> * Một tập các use-case
> * Một prototype
> 

* Nhưng sẽ có thể có những thiếu sót trong quá trình đặc tả, vậy nên cần có sự đánh giá.

> [!info] Đánh giá (Validation)
> Tạo cơ chế xem xét các vấn đề
> * Sai sót trong nội dung hoặc giải thích
> * Phần được yêu cầu làm rõ
> * Thông tin bị thiếu
> * Mâu thuẫn
> * Yêu cầu không thực tế, không thể đạt được

![[20221121_151400 1.jpg]]

> [!info] Quản lý các Yêu cầu (Requirements management)

## 2. Tầm quan trọng của yêu cầu phần mềm
![[20221121_152456.jpg]]

### Nguồn gốc yêu cầu phần mềm
> [!note] Khách hàng/người sử dụng
> * Khách hàng cung cấp các ***business requirement***: cung cấp các thông tin về cty, về các đặc điểm ở mức độ cao, về mô hình và phạm vi của hệ thống
> * Khách hàng cung cấp các ***user requirement***: Cung cấp các thông tin về từng nhiệm vụ cụ thể mà họ sẽ làm việc với phần mềm.
> 
> **->Cần phối hợp, kết hợp chặt chẽ với hai loại khách hàng trên.**

#### Đặc điểm của khách hàng pm
* ý tưởng mơ hồ/chưa rõ ràng về phần mềm
* Hay thay đổi -> cần nắm bắt để sửa đổi các mô tả hợp lý

> [!warning] Các thách thức của kỹ nghệ yêu cầu PM
> * Sự tham gia quá mức của NSD
> * Có quá nhiều yêu cầu trong yêu cầu phần mềm
> * Yêu cầu mơ hồ, nhập nhằng
> * Không lưu ý tới người sử dụng phần mềm
> * Các đặc tính thừa
> * Đặc tả quá ít
> * Kế hoạch sai

## 3. Yêu cầu chức năng và yêu cầu phi chức năng
>[!abstract] Phân loại yêu cầu
>* Theo thành phần của phần mềm: 
>	* Software
>	* Hardware
>	* Data
>	* Users
>* Theo cách đặc tả phần mềm:
>	* Các yêu cầu chức năng
>	* Các yêu cầu ngoài chức năng
>	* Các ràng buộc khác

### Yêu cầu chức năng
> [!info] Yêu cầu chức năng
> Miêu tả các chức năng của hệ thống, phụ thuộc vào kiểu phần mềm và mong đợi của người dùng
> 

* Giữa phần mềm và môi trường, độc lập với việc cài đặt

#### Các công cụ đặc tả yêu cầu chức năng 
* [[Chap6.1 - Kỹ nghệ yêu cầu phần mềm#Biểu đồ luồng dữ liệu - Data Flow Diagram (DFD)]]
* [[Chap6.1 - Kỹ nghệ yêu cầu phần mềm#Máy trạng thái - Finite State Machine]]
* Mạng Petri

* Tuy nhiên, ko bắt buộc và có thể dùng ngôn ngữ tự nhiên

### Yêu cầu phi chức năng và ràng buộc
> [!info] Yêu cầu phi chức năng
> Định nghĩa các khía cạnh sử dụng phần mềm, ko liên quan trực tiếp tới các hành vi chức năng (độ tin cậy, response time, memory ...)

> [!info] Ràng buộc
> Các ràng buộc do khách hàng hay môi trường thực thi phần mềm đặt ra

* Các yêu cầu do tổ chức qui định chuẩn về quá trình tiến hành, chuẩn tài
* Các yêu cầu từ bên ngoài

#### Các công cụ đặc tả yêu cầu phi chức năng
* [[Chap6.1 - Kỹ nghệ yêu cầu phần mềm#Sơ đồ thực thể liên kết - Entity Relation Diagram (ERD)]]
* Đặc tả Logic (Logic Specifications)
* Đặc tả đại số

> [!warning] Khó phát biểu chính xác, khó kiểm tra

![[20221121_162347.jpg]]

## 4. Các hoạt động chính trong kỹ nghệ yêu cầu phần mềm
* [[Chap6.1 - Kỹ nghệ yêu cầu phần mềm#4.1 Phát hiện yêu cầu phần mềm]]
* [[Chap6.1 - Kỹ nghệ yêu cầu phần mềm#4.2 Phân tích các yêu cầu của pm và thương lượng với khách hàng]]
* [[Chap6.1 - Kỹ nghệ yêu cầu phần mềm#4.3 Đặc tả yêu cầu phần mềm]]
* [[Chap6.1 - Kỹ nghệ yêu cầu phần mềm#4.4 Một số mô hình hoá hệ thống]]
* **Kiểm tra tính hợp lý** của các yêu cầu pm (Requirements validation)
* [[Chap6.1 - Kỹ nghệ yêu cầu phần mềm#4.5 Quản trị các yêu cầu phần mềm]]

![[Pasted image 20221128142618.png]]
* Cần xây dựng mô hình nguyên mẫu khi khách hàng chưa xác định rõ được yêu cầu
* Xây dựng mô hình phân tích khi khách hàng đã xác định được yêu cầu đối với pm

### 4.1 Phát hiện yêu cầu phần mềm
> [!abstract] 
> * **Đánh giá tính khả thi** về kỹ thuật và nghiệp vụ của phần mềm định phát triển
> * **Tìm kiếm nhân sự** những chuyên gia, người sử dụng có những hiểu biết sâu sắc và chi tiết nhất về hệ thống giúp chúng ta  xác định yêu cầu pm.
> * **Xác định môi trường kỹ thuật** mà trong đó sẽ triển khai phần mềm
>  * **Xác định các ràng buộc** về lĩnh vực ứng dụng của phần mềm (giới hạn về chức năng/hiệu năng phần mềm)

> [!note] Phương pháp phát hiện các yêu cầu pm
> * Phỏng vấn
> * Làm việc nhóm
> * Các buổi họp
> * Gặp gỡ đối tác

> [!note] Đầu ra của bước phát hiện hiệu cầu pm
> * Bảng kê các đòi hỏi và chức năng khả thi của pm
> * Bảng kê phạm vi ứng dụng của phần mềm
> * Mô tả môi trường kỹ thuật của phần mềm
> * Bảng kê tập hợp các use case của pm
> * Các prototypes xây dựng, phát triển hay sử dụng trong phần mềm (nếu có)
> * Ds nhân sự tham gia vào quá trình phát hiện các yêu cầu phần mềm 

### 4.2 Phân tích các yêu cầu của pm và thương lượng với khách hàng

![[Pasted image 20221128144222.png]]

 > [!abstract] 
 > * **Phân loại các yêu cầu** pm và sắp xếp chúng theo các nhóm liên quan
 > * **Khảo sát** tỉ mỉ từng yêu cầu phần mềm trong mối qua hệ của nó với các yêu cầu pm khác
 > * **Thẩm định** từng yêu cầu pm theo các t/c: phù hợp, đầy đủ, rõ ràng, không trùng lặp
 > * **Phân cấp** các yêu cầu pm dựa tren nhu cầu và đòi hỏi khách hàng/người sử dụng
 > * Thẩm định từng yêu cầu về khả năng thực hiện
 > * **Thẩm định các rủi ro** có thể xảy ra với từng yêu cầu.
 > * **Đánh giá thô** về giá thành và thời gian thực hiện của từng yêu cầu pm 
 > * Giải quyết các bất đồng giữa hai bên bằng thảo luận và thương lượng
 
### 4.3 Đặc tả yêu cầu phần mềm
> [!info] Đặc tả các yêu cầu phần mềm
> Xây dựng các tài liệu đặc tả , có thể sử dụng các công cụ : mô hình hoá, mô hình toán học hình thức, tập hợp các kịch bản sử dụng, các prototype hoặc tổ hợp các công cụ nói trên.

#### Các phương pháp đặc tả
 * ***Phi hình thức (Informal Specifications)*** - viết bằng ngôn ngữ tự nhiên
 
 * ***Hình thức (Formal Specifications)*** - viết bằng tập hợp các ký pháp có các quy định syntax và sematic chặt chẽ 

> [!important] Tiêu chí đánh giá chất lượng
> * Tính rõ ràng, chính xác
> * Tính phù hợp
> * Tính đầy đủ, hoàn thiện

#### Các thành phần của hồ sơ đặc tả
* ***Đặc tả vận hành (Operational Specifications)***: 
	* Đặc tả chức năng
	* Mô tả các hoạt động của hệ thống phần mềm sẽ xây dựng
		* Các dịch vụ mà hệ thống phải cung cấp
		* Hệ thống sẽ phản ứng với đầu vào cụ thể ra sao
		* Hành vi của hệ thống trong các tình huống đặc biệt

* ***Đặc tả mô tả (Descriptive specifications)***:
	* Đặc tả phi chức năng
	* Đặc tả các đặc tính, đặc trưng của phần mềm
		* Các ràng buộc về dịch vụ hay các chức năng hệ thống cung cấp như thời gian
		* Ràng buộc về quá trình phát triển 
		* Các chuẩn

* Ngoài ra có các yêu cầu đặc trưng về lĩnh vực của ứng dụng hệ thống

#### Tài liệu yêu cầu
> [!info] Tài liệu yêu cầu
> Các phát biểu chính thức về cái được yêu cầu bởi các nhà phát triển hệ thống, bao gồm:  
> * Định nghĩa
> * Đặc tả yêu cầu 


> [!warning] Không phải là tài liệu thiết kế
> Chỉ là tập các điều mà hệ thống phải làm, ko phải làm như thế nào.

![[Pasted image 20221202235333.png]]

### 4.4 Một số mô hình hoá hệ thống
#### Biểu đồ phân cấp chức năng - Work Break down Structure (WBS)
👉 Nhắc lại bài [[Chap4 - Quản lý dự án#Work Breakdown Structure - WBS]]

#### Biểu đồ luồng dữ liệu - Data Flow Diagram (DFD)
> [!info]
> - Biểu diễn hệ thống sự biến đối của dữ liệu qua các chức năng xử lý

> [!note] Ký pháp
> ![[Pasted image 20221128153034.png]]
> * Các chức năng còn có thể được biểu diễn bằng hình chữ nhật bo góc tròn
> * Kho dữ liệu còn có thể được biểu diễn dạng
> ![[Pasted image 20221128160558.png]]



![[Pasted image 20221128153222.png]]

> [!failure] Các hạn chế của DFD
> * Không xác định rõ các hướng thực hiện (control aspects)
> * Không chỉ rõ đầu vào là gì để thực hiện chức năng và đầu ra là gì sau khi thực hiện chức năng
> * Không xác định sự đồng bộ giữa các chức năng/module
> 
> > [!warning] Cần có buffer để ngăn chặn tình trạng mất dữ liệu

#### Máy trạng thái - Finite State Machine
> [!info] 
> Biểu diễn tập trung trạng thái hữu hạn của hệ thống và các dịch chuyển giữa các trạng thái

> 	[!note] Ký pháp 
> 	* tập các trạng thái (state) Q hữu hạn: các hình tròn chứa tên trạng thái
> 	* Dịch chuyển: mũi tên, trên mũi tên chứa hành động
> 	* Tập hữu hạn các đầu vào I

![[Pasted image 20221128160910.png]]

#### Sơ đồ thực thể liên kết - Entity Relation Diagram (ERD)
👉 Ôn lại bài cũ [[W6 - RELATIONAL DATABASE DESIGN]]

>[!info] 
>Biểu diễn sự logic của hệ thống về dữ liệu

> [!note] Ký pháp
> * Thực thể (kiểu thực thể): hình chữ nhật chứa tên thực thể (ngoài ra còn có thể hình chữ nhật lồng chứa tên thực thể dữ liệu)
> * Quan hệ (min,max): ![[Pasted image 20221128163222.png]]
> 	* min - sự bắt buộc của quan hệ:
> 		* = 0 : tuỳ ý
> 		* $\neq$ 0 : bắt buộc
> 	* max:
> 		* 1 - N
> 		* 1 - 1
> 		* N - N
> * Thuộc tính: ![[Pasted image 20221128163513.png]]

> [!note] Các bước xây dựng hệ cơ sở dữ liệu
> 1. Thiết kế mức khái niệm (ERD)
> 
> 2. Thiết kế logic
> 	* Quan tâm tới mô hình dữ liệu:
> 		* Quan hệ (table) 
> 		* Phi quan hệ (document, record) MongoDB
> 	* Độ  tốt của thiết kế : các dạng chuẩn 
> 
> 3. Thiết kế vật lý
> 	* Chọn kiểu dữ liệu cho đúng
> 	* Lưu trữ
> 	* Index

![[Pasted image 20221128164057.png]]

|DFD|FSM|ERD|
|---|---|---|
|Đơn giản, dễ hiểu|Có thể phức tạp với số lượng trạng thái lớn|Đơn giản, dễ hiểu|
|Mô tả luồng dữ liệu|Mô tả trạng thái của thực thể|Mô tả trừu tượng cơ sở dữ liệu|
|Không xác định rõ hướng thực hiện|Xác định rõ hướng thực hiện|Không xác đjnh rõ hướng thực hiện|
|Không thể hiện tính tuần tự hay song song của tiến trình|Thể hiện tốt tính song song và tuần tự|Không thể hiện tính tuần tự hay song song|

> [!question]  Thế nào là một đặc tả tốt ?
> - Dễ hiểu với người dùng
> - Ít điều nhập nhằng
> - Có ít quy ước khi mô tả, đơn giản để tạo
> - Topdown
> - Dễ triển khai cho những pha sau của vòng đời

![[Pasted image 20221203005110.png]]

### 4.5 Quản trị các yêu cầu phần mềm
> [!check] Lợi ích
> * Chi phí phát triển thấp hơn trong suốt vòng đời pm 
> * Ít sai sót hơn
> * Giảm thiểu rủi ro đối với các sản phẩm quan trọng về an toàn
> * Giao hàng nhanh hơn
> * Khả năng tái sử dụng 
> * Truy xuất nguồn gốc
> * Các yêu cầu gắn liền với các trường hợp thử nghiệm 

#### Quản lý thay đổi và vấn đề phát sinh
> [!info] Thay đổi
> Bất cứ hđ nào thay đổi phạm vi, kết quả bàn giao, kiến trúc cơ bản, chí phí, lịch trình của một dự án.

=> Cần quản lý vì thay đổi và vấn đề phát sinh là 2 lý do thường làm dự án thất bại

* Giảm rủi ro dự án nhờ quy trình hiệu quả quản lý thayđổi và vấnđề
* Các thành viên nhóm hiểu được quy trình quản lý thay đổi và vấn đề
* Ghi chép đầy đủ về các yêu cầu thay đổi/vấn đề

#### Kiểm soát nguồn thay đổi tiềm năng
![[Pasted image 20221203005821.png]]