> [!note] Yêu cầu
> Không gian bài toán (Problem)
> * Xác định yêu cầu
> * Ghi nhận yêu cầu
> **What?**

> [!note] Thiết kế
> Không gian giải pháp (Solution)
> - Các thành phần:
> 	- Kiến trúc: tổng quan, các mối quan hệ
> 	- Chi tiết:
> 		- Module
> 		- Giao diện
> 		- Giữ liệu
> 	
> 	-> Biểu diễn các nội dung thiết kế 
> 	-> Sử dụng mô hình

```shell
Yêu cầu --[Phân tích yêu cầu]--> Thiết kế
```

> [!question] Đánh giá chất lượng/độ tốt của thiết kế ?
> Sử dụng hai tiêu chí ***Tính móc nối (Coupling)*** - ***Tính kết dính (Cohension)***

## 1. Tổng quan thiết kế phần mềm
### 1.1 Khái niệm về thiết kế phần mềm
> [!info] Thiết kế phần mềm
> - Tạo ra các **biểu diễn** và **dữ kiện** của hệ thống phần mềm
> 	- *Input*: Phân tích yêu cầu
> 	- *Output*: Mô hình thiết kế (Đủ chi tiết để thực hiện xây dựng)
> 	

* Đánh giá chất lượng của sản phẩm:
	* User: sử dụng như thế nào
	* Developer: Phát triển, thay đổi, nâng cấp

![[Pasted image 20221219145257.png]]

* Thiết kế xuất phát từ kết quả phân tích yêu cầu, giúp trả lời câu hỏi "Như thế nào?"
> [!note]
> Thiết kế thường mô tả ở một mức trừu tượng nhất định, sử dụng các mô hình (Khác với cài đặt chi tiết khi lập trình)

> [!failure] Thiết kế tồi
> Tăng công sức viết mã chương trình
> Tăng công sức bảo trì
> Khó khăn khi sửa đổi, mở rộng

> [!info] Tuyên ngôn về thiết kế phần mềm
> * **Sự ổn định (Firmness)**: pm ko nên có bất cứ lỗi nào làm hạn chế chức năng của nó
> * **Tiện nghi (Commodity)**: Một chương trình nên phù hợp với mục đích đã định của nó.
> * **Sự hài lòng (Delight)**: trải nghiệm sử dụng chương trình nên làm hài lòng người dùng.

#### Các giai đoạn thiết kế
1. Thiết kế kiến trúc/ thiết kế mức cao (High level design):
	* Mô hình tổng thể của hệ thống
	* Cách thức hệ thống được phân rã thành các mô đun
	* Mối quan hệ giữa các mô đun
	* Cách thức trao đổi thông tin giữa các mô đun
	* Thực hiện bởi nhiều mức trừu tượng

2. Thiết kế chi tiết/ thiết kế mức thấp (Low level design):
	* Thiết kế chi tiết lớp, module, thiết kế thuật toán, thiết kế dữ liệu, thiết kế giao diện, ...

### 1.2 Quan hệ giữa thiết kế và chất lượng của phần mềm
> [!abstract] 
> >[!note]- Thiết kế phải thực hiện tất cả các yêu cầu rõ ràng
> >chứa trong mô hình phân tích, đáp ứng tất cả các yêu cầu tiềm ẩn khách hàng mong muốn
> ---
> >[!note]- Thiết kế phải là một hướng dẫn dễ hiểu dễ đọc
> >cho những người tạo code, những người kiểm thử và hỗ trợ cho phần mềm
> 
> ---
> >[!note]- Thiết kế nên cung cấp một bức tranh hoàn chỉnh của phần mềm
> >giải quyết vấn đề dữ liệu, chức năng, và hành vi từ một quan điểm thực thi
> 
> ---
> >[!note]- Một thiết kế nên thể hiện một kiến trúc
> > Kiến trúc được tạo ra bằng cách sử dụng phong cách kiến trúc hoặc các pattern được công nhận, bao gồm các thành phần mang những đặc tính thiết kế tốt và có thể được thực hiện một cách tiến hoá.
> ---
> > [!note]- Một thiết kế nên môđun hoá
> > Phần mềm nên được phân chia thành các thành phần hợp lý hoặc hệ thống con
> ---
> > [!note]- Một thiết kế cần có biểu diễn riêng biệt
> > của dữ liệu, kiến trúc, giao diện và các thành phần.

### 1.3 Nguyên tắc chất lượng

### 1.4 Nguyên tắc thiết kế

## 2. Các khái niệm trong thiết kế phần mềm
### 2.1 Các khái niệm cơ bản trong thiết kế
|Khái niệm|Định nghĩa|
|:---|:---|
|Trừu tượng hoá | Lựa chọn/ xác định các thông tin/ dữ liệu quan trọng thể hiện bản chất của sự vật |



#### Khuôn mẫu thiết kế (Design Patterns)
> [!info] Khuôn mẫu thiết kế (Design Patterns)
> Phương pháp có hệ thống để mô tả các vấn đề và giải pháp, cho phép các cộng đồng công nghệ pm có thể nắm bắt kiến thức thiết kế theo cách tái sử dụng. 

##### Các loại khuôn mẫu
* ***Architectural patterns*** - mẫu kiến trúc mô tả các vấn đề thiết kế trên diện rộng được giải quyết bằng cách tiếp cận cấu trúc

* ***Data patterns*** - mẫu giữ liệu mô tả vấn đề dữ liệu và các giải pháp mô hình dữ liệu có thể được dùng để giải quyết vấn đề trên.

> [!info] Gang of Four - GoF
> 23 khuôn mẫu thiết kế với 3 nhóm : 
>*  ***Khuôn mẫu khởi tạo (Creational patterns)*** tập trung vào việc khởi tạo, sáng tác và biểu diễn của các đối tượng, ví dụ:
> 	- Abstract factory pattern
> 	- Factory method pattern
> 
> * ***Khuôn mẫu cấu trúc (Structural patterns)*** tập trung vào các vấn đề và các giải pháp liên quan đến cách các l
> 
> * ***Khuôn mẫu hành vi (Behavioral patterns)***

> [!example] VD: Thông tin của một mẫu thiết kế
> - Tên
> - Ý định
> - Tên khác
> - Động lực
> - Khả năng áp dụng
> - Cấu trúc
> - Các thành phần
> - Cộng tác
> - Hệ quả
> - Các pattern liên quan

#### Khung (Framworks)

#### Mô đun hoá (Modularity)

* Sự đánh đổi
![[Pasted image 20221219163552.png]]

#### Ẩn thông tin
![[Pasted image 20221219163634.png]]

#### Tái cấu trúc (Refactoring)

### 2.2 Các khái niệm thiết kế  OO

## 3. Thiết kế kiến trúc phần mềm

## 4. Thiết kế chi tiết phần mềm

## 5. Tính móc nối (Coupling) và tính kết dính (Cohension)