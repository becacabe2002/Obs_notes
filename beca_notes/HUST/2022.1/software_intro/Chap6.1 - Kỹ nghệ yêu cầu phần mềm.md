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
>* Tìm hiểu nhu cầu, cơ hội, ý tưởng
>* Thu thập thông tin

> [!info] Khám phá (Eliciation)  🔍: 
> xác định tất cả các yêu cầu của khách hàng (hỏi đáp, phỏng vấn, phân tích xu hướng, xin ý kiến tham vấn)

> [!info] Xây dựng (Elaboration) ⚒️: 
> phân tích yêu cầu về dữ liệu, chức năng, hành vi
>-> Hiểu rõ về yêu cầu

> [!info] Đàm phán (Negotiation) 🤝

> [!info] Đặc tả (Specification)
> tài liệu ghi nhận đầy đủ yêu cầu (SRS)

* Nhưng sẽ có thể có những thiếu sót trong quá trình đặc tả

> [!info] Đánh giá (Validation)

![[20221121_151400 1.jpg]]

> [!info] Quản lý các Yêu cầu (Requirements management)

## 2. Tầm quan trọng của yêu cầu phần mềm
![[20221121_152456.jpg]]

### Nguồn gốc yêu cầu phần mềm
> [!note] Khách hàng/người sử dụng
> * Khách hàng cung cấp các ***business requirement***: cung cấp các thông tin về cty, về các đặc điểm ở mức độ cao, về mô hình và phạm vi của hệ thống
> * Khách hàng cung cấp các ***user requirement***: Cung cấp các thông tin về từng nhiệm vụ cụ thể mà họ sẽ làm việc với phần mề,.
> ->Cần phối hợp, kết hợp chặt chẽ với hai loại khách hàng trên.

#### Đặc điểm của khách hàng pm
* ý tưởng mơ hồ/chưa rõ ràng về phần mềm
* Hay thay đổi 

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

### Yêu cầu phi chức năng và ràng buộc

![[20221121_162347.jpg]]

## 4. Các hoạt động chính trong kỹ nghệ yêu cầu phần mềm
* **Phát hiện** các yêu cầu pm (Requirements elicitattion)
* **Phân tích** các yêu cầu pm và thương lượng với khách hàng (Requirements analysis and negotiation)
* **Đặc tả** các yêu cầu phần mềm (Requirement specification)
* **Mô hình hoá** hệ thống (System modeling)
* **Kiểm tra tính hợp lý** của các yêu cầu pm (Requirements validation)
* **Quản trị** các yêu cầu pm (Requirements management)

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
 > * **Thẩm định các rủi ro** có thể xảy ra với từng yêu cầu.
 > 
 
### 4.3 Đặc tả yêu cầu phần mềm


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

> [!note] Ký pháp 
> * tập các trạng thái (state) Q hữu hạn: các hình tròn chứa tên trạng thái
> * Dịch chuyển: mũi tên, trên mũi tên chứa hành động
> * Tập hữu hạn các đầu vào I

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

### 4.5 Quản trị các yêu cầu phần mềm