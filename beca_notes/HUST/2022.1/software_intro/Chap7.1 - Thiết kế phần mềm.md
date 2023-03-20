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
> >[!note] Thiết kế phải thực hiện tất cả các yêu cầu rõ ràng
> >chứa trong mô hình phân tích, đáp ứng tất cả các yêu cầu tiềm ẩn khách hàng mong muốn
> ---
> >[!note] Thiết kế phải là một hướng dẫn dễ hiểu dễ đọc
> >cho những người tạo code, những người kiểm thử và hỗ trợ cho phần mềm
> 
> ---
> >[!note] Thiết kế nên cung cấp một bức tranh hoàn chỉnh của phần mềm
> >giải quyết vấn đề dữ liệu, chức năng, và hành vi từ một quan điểm thực thi
> 
> ---
> >[!note] Một thiết kế nên thể hiện một kiến trúc
> > Kiến trúc được tạo ra bằng cách sử dụng phong cách kiến trúc hoặc các pattern được công nhận, bao gồm các thành phần mang những đặc tính thiết kế tốt và có thể được thực hiện một cách tiến hoá.
> ---
> > [!note] Một thiết kế nên môđun hoá
> > Phần mềm nên được phân chia thành các thành phần hợp lý hoặc hệ thống con
> ---
> > [!note] Một thiết kế cần có biểu diễn riêng biệt
> > của dữ liệu, kiến trúc, giao diện và các thành phần.

### 1.3 Nguyên tắc chất lượng
* Một thiết kế nên dẫn đến các cấu trúc dữ liệu thích hợp

* Một thiết kế nên dẫn đến các thành phần mang những đặc tính chức năng độc lập.

* Một thiết kế nên dẫn đến giao diện mà giảm sự phức tạp

* Một thiết kế nên được chuyển hoá bằng cách sử dụng một phương pháp lặp lại

* Một thiết kế nên được đại diện bằng một ký hiệu truyền đạt hiệu quả ý nghĩa của nó

### 1.4 Nguyên tắc thiết kế
* Việc thiết kế nên được cấu trúc:
	* Để thích ứng với thay đổi
	* Để làm suy thoái (degrade) nhẹ nhàng, ngay cả khi đang gặp phải dữ liệu bất thường, các sự kiện, hoặc điều kiện hoạt động.

* Việc thiết kế nên được đánh giá về chất lượng khi nó được tạo ra.

* Việc thiết kế cần được xem xét để giảm thiểu lỗi khái niệm.

## 2. Các khái niệm trong thiết kế phần mềm
### 2.1 Các khái niệm cơ bản trong thiết kế
|Khái niệm|Định nghĩa|
|:---:|:---|
|***Trừu tượng hoá***| Lựa chọn/ xác định các thông tin/ dữ liệu quan trọng thể hiện bản chất của sự vật |
|***Kiến trúc***|Cấu trúc tổng thể của phần mềm|
|***Mẫu thiết kế (Design Patterns)***|Chắt lọc của một giải pháp thiết kế đã được chứng minh|
|***Phân tách mỗi quan tâm </br> (Separation of concerns)***|Chia nhỏ các vấn đề phức tạp thành các mảnh dễ quản lí, có thể đưa ra giải pháp giải quyết nhanh chóng hơn|
|***Mô đun hoá </br> (Modularity)***|Mô đun hoá các dữ liệu và chức năng|
|***Tính ẩn***|giao diện được điều khiển|
|***Độc lập chức năng***|Các hàm đơn mục đích và khớp nối thấp|
|***Sàng lọc***|Xây dựng chi tiết cho tất cả các khái niệm trừu tượng|
|***Các khía cạnh***| cơ chế cho sự hiểu biết các yêu cầu tổng thể ảnh hưởng đến thiết kế như thế nào|
|***Refactoring***| kĩ thuật tái tổ chức nhằm đơn giản hoá thiết kế|
|***OO design concepts***| Các khái niệm về thiết hế hướng đối tượng|
|***Thiết kế lớp***| cung cấp chi tiết thiết kế mà sẽ cho phép các lớp đã phân tích được thực thi|

#### Khuôn mẫu thiết kế (Design Patterns)
> [!info] Khuôn mẫu thiết kế (Design Patterns)
> Phương pháp có hệ thống để mô tả các vấn đề và giải pháp, cho phép các cộng đồng công nghệ pm có thể nắm bắt kiến thức thiết kế theo cách tái sử dụng. 

##### Các loại khuôn mẫu
* ***Architectural patterns*** - mẫu kiến trúc mô tả các vấn đề thiết kế trên diện rộng được giải quyết bằng cách tiếp cận cấu trúc

* ***Data patterns*** - mẫu giữ liệu mô tả vấn đề dữ liệu và các giải pháp mô hình dữ liệu có thể được dùng để giải quyết vấn đề trên.

* ***Component patterns*** - mẫu thành phần nhằm đến các vấn đề phát triển hệ thống con và các thành phần, cách thức chúng giao tiếp với nhau, và vị trí của chúng trong kiến trúc bao quát hơn.

* ***Interface design patterns*** - mẫu thiết kế giao diện mô tả các vấn đề giao diện người dùng thông thường và giải pháp (đặc trưng cụ thể của người dùng cuối)

* ***WebApp patterns*** - mẫu giải quyết tập hợp vấn đề có thể gặp phải khi xây dựng ứng dụng web và thường là sự kết hợp của nhiều mô hình phía trên.

> [!info] Gang of Four - GoF
> 23 khuôn mẫu thiết kế với 3 nhóm : 
>*  ***Khuôn mẫu khởi tạo (Creational patterns)*** tập trung vào việc khởi tạo, sáng tác và biểu diễn của các đối tượng, ví dụ:
> 	- Abstract factory pattern
> 	- Factory method pattern
> 
> * ***Khuôn mẫu cấu trúc (Structural patterns)*** tập trung vào các vấn đề và các giải pháp liên quan đến cách các lớp và các đối tượng được tổ chức và tích hợp để xây dựng một cấu trúc lớn hơn, ví dụ:
> 	- Adapter pattern
> 	- Aggregate pattern
> 
> * ***Khuôn mẫu hành vi (Behavioral patterns)*** giải quyết các vấn đề liên quan đến việc phân công trách nhiệm giữa các đối tượng và cách thức mà giao tiếp được thực hiện giữa các đối tượng, ví dụ: 
> 	- Chain of responsibility pattern
> 	- Command pattern

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

#### Khung (Frameworks)
Pattern có thể không đủ để phát triển một thiết kế hoàn chỉnh 
==-> Cần có một cơ sở hạ tầng thực hiện cụ thể==

> [!info] Framework
> Bộ khung, với tập hợp các **plug points** cho phép thích ứng với một miền vấn đề xác định
> * Plug points cho phép tích hợp các lớp vấn đề cụ thể hoặc chức năng trong các bộ khung.

#### Mô đun hoá (Modularity)

* Việc chia thiết kế thành nhiều module sẽ là một cách để đội nhóm có thể hiểu thiết kế một cách dễ dàng và hiệu quả hơn.
-> Giảm chi phí cần thiết để xây dựng các phần mềm

* Sự đánh đổi
![[Pasted image 20221219163552.png]]

#### Ẩn thông tin

```start-multi-column
ID: ID_v66l
Number of Columns: 2
Largest Column: standard
border: off
```

> [!question] Vì sao cần *Ẩn thông tin*
> > [!check] Lí do
> > * Giảm khả năng "tác dụng phụ"
> > * Hạn chế ảnh hưởng chung của quyết định thiết kế cục bộ
> > * Nhấn mạnh truyền thông qua giao diện điều khiển
> > * Không khuyến khích việc sử dụng các dữ liệu toàn cục
> > * Dẫn đến đóng gói, một thuộc tính của thiết kế chất lượng cao
> > * Kết quả tạo ra phần mềm chất lượng cao

--- column-end ---

![[Pasted image 20221219163634.png]]

=== end-multi-column

#### Tái cấu trúc (Refactoring)
> [!info] Refactoring
> Quá trình thay đổi một hệ thống phần mềm trong một cách mà không làm thay đổi hành vi bên ngoài của mã nguồn nhưng cải thiện cấu trúc bên trong của nó.

* Khi tái cấu trúc, thiết kế hiện tại được kiểm tra:
	* Sự dư thừa
	* Các yếu tố thiết kế không sử dụng
	* Các thuật toán không hiệu quả hoặc không cần thiết
	* Cấu trúc dữ liệu xây dựng kém hoặc không phù hợp
	* Hoặc bất kỳ sự thất bại thiết kế khác có thể được điều chỉnh để mang lại một thiết kế tốt hơn.


### 2.2 Các khái niệm thiết kế  OO
> [!note] Các lớp thiết kế
> * ***Các lớp thiết kế*** là các lớp phân tích được tinh chỉnh trong quá trình thiết kế 
> 
> * ***Các lớp biên*** phát triển trong thiết kế để tạo ra giao diện (màn hình tương tác, báo cáo) mà người dùng thấy và tương tác với phần mềm
> 
> * ***Các lớp điều khiển*** được thiết kế quản lý:
> 	* việc tạo ra hoặc cập nhật các đối tượng thực thể
> 	* Sự tức thời của đối tượng biên khi họ có được thông tin từ các đối tượng thực thể
> 	* Truyền thông phức tạp giữa các tập của các đối tượng
> 	* Xác nhận của dữ liệu trao đổi giữa các đối tượng hoặc giữa người sử dụng với ứng dụng.

### 2.3 Mô hình thiết kế


```start-multi-column
ID: ID_xvl3
Number of Columns: 2
Largest Column: standard
border: off
```

![[Pasted image 20230307164739.png]]

--- column-end ---

* **Các thành phần dữ liệu**:
	* Mô hình dữ liệu -> cấu trúc dữ liệu
	* Mô hình dữ liệu -> kiến trúc cơ sở dữ liệu

* **Các thành phần kiến trúc**:
	* Thông tin về miền ứng dụng cho xây dựng phần mềm
	* Các thành phần mô hình yêu cầu cụ thể (sơ đồ luồng dữ liệu và phân tích lớp, các mối quan hệ và sự hợp tác của chúng.)
	* Sự sẵn có của mô hình kiến trúc và các kiểu

* **Các thành phần giao diện**:
	* Giao diện người dùng (UI)
	* Giao diện bên ngoài đến các hệ thống khác, các thiết bị, mạng, hoặc các nhà sản xuất khác hoặc ngườii dùng thông tin.
	* Giao diện nội bộ giữa các thành phần thiết kế khác nhau.

* **Các yếu tố cấu thành**
* **Các thành phần triển khai**

=== end-multi-column

```start-multi-column
ID: ID_nt38
Number of Columns: 2
Largest Column: standard
border: off
```

![[Pasted image 20230307174202.png]]

Ví dụ về các thành phần giao diện

--- column-end ---

![[Pasted image 20230307174243.png]]

Ví dụ về các thành phần triển khai

=== end-multi-column



## 3. Thiết kế kiến trúc phần mềm
> [!info] Kiến trúc phần mềm
> Mô tả cấu trúc phần mềm ở mức vĩ mô hoặc các cấp độ khác nhau
> * Các thành phần (module)
> * Quan hệ

> [!question] Tại sao cần thiết kế kiến trúc?
> Kiến trúc là **đại diện cho phần mềm** được xây dựng mà thông qua nó người dùng có thể thực hiện nhiều thao tác
> * Đánh giá/ước tính chất lượng
> * Xem xét lựa chọn thay đổi kiến trúc phù hợp
> * Giảm thiểu rủi ro gắn liền với việc xây dựng các phần mềm

* **Đại diện của kiến trúc phần mềm là một tạo khả năng**, cho phép truyền thông giữa tất cả các bên quan tâm đến sự phát triển của một hệ thống dựa trên máy tính.
* **Những kiến trúc làm nổi bật thiết kế quyết định ban đầu** , thứ sẽ có tác động tới tất cả các công việc kỹ thuật phần mềm, và vào sự thành công sau cùng của hệ thống như một thực thể hoạt động
* **Kiến trúc tạo thành một mode minh bạch nhỏ** về cách hệ thống được cấu trúc và cách các thành phần của nó làm việc cùng nhau.

### Mô tả kiến trúc
> [!info] Mô tả kiến trúc
> Tập hợp các sản phẩm để tài liệu hoá một kiến trúc.

* Thường sử dụng :
	* Sơ đồ lớp
	* Sơ đồ gói
	* Sơ đồ thành phần 

> [!info] Thể loại kiến trúc
> Ngụ ý một phân loại cụ thể trong lĩnh vực phần mềm tổng thể
> 	* Trong mỗi thể loại, sẽ lại có một số tiểu phân loại.

### Kiểu kiến trúc
> [!abstract] Kiểu kiến trúc
> 1. Tập hợp các thành phần với chức năng cụ thể
> 2. Kết nối giữa các thành phần
> 	* Truyền thông
> 	* Phối hợp
> 	* Hợp tác
> 3. Sự tích hợp hình thành hệ thống
> 4. Các mô hình ngữ nghĩa kèm theo

* Một số kiểu kiến trúc hệ thống
	* Kiến trúc lấy dữ liệu làm trung tâm
	* Kiến trúc luồng dữ liệu
	* Kiến trúc gọi và trả về
	* Kiến trúc phân lớp
	* Kiến trúc hướng đối tượng

#### Kiến trúc lấy dữ liệu làm trung tâm
![[Pasted image 20221226143730.png]]
* **Đặc tả**: kho dữ liệu trung tâm, các client software xung quanh
 
 > [!check] Ưu điểm
 > * Dữ liệu được quản lý và duy trì tập trung -> đảm bảo tính nhất quán và sự chính xác của dữ liệu
 > * Dữ liệu được truy cập và chia sẻ dễ dàng giữa các thành phần trong hệ thống -> giúp việc phát triển và bảo trì hệ thống dễ dàng hơn
 > * Kiểm soát quyền truy cập và bảo mật dữ liệu dễ dàng hơn
 > * Tăng hiệu suất hệ thống khi các thành phần không cần phải truy vấn và lưu trữ dữ liệu nhiều lần.
 
 > [!failure] Nhược điểm
 > * Khó bảo trì nếu hệ thống phải xử lý nhiều loại dữ liệu khác nhau
 > * Nếu điểm chết (điểmmà tất cả các thành phần phụ thuộc vào để truy nhập dữ liệu) bị hỏng -> gây ra gián đoạn toàn bộ hệ thống
 > * Hiệu suất có thể bị ảnh hưởng nếu dữ liệu phải truy xuất và truyền tải qua mạng (đặc biệt khi có nhiều thành phần cùng thực hiện)
 > * Không phù hợp với các ứng dụng có tính độc lập cao.
 
* **Tình huống áp dụng**:

#### Kiến trúc luồng dữ liệu:
##### a. Kiến trúc lô tuần tự (batch sequential)
![[Pasted image 20221226144459.png]]
* **Đặc tả**: gồm nhiều thành phần độc lập, hoạt động theo cơ chế tuần tự

> [!info] Filter
> Xử lý dữ liệu đầu vào theo một định dạng xác định, tạo kết quả đầu ra cũng theo một định dạng xác định

 > [!check] Ưu điểm
 > * Tăng tính chính xác, tin cậy của hệ thống khi các tác vụ được thực hiện một cách tuần tự, cụ thể
 > * Dễ thay đổi các thành phần do tính độc lập của chúng (thay thế, nâng cấp)
 > * Tự động hoá quy trình -> giảm thiểu lỗi do con người và tăng hiệu quả công việc.
 
 > [!failure] Nhược điểm
 > * Kiến trúc không phù hợp với các ứng dụng có tính tương tác cao.
 > * Độ trễ và thời gian xử lí tỉ lệ thuận với độ lớn dữ liệu
 > * Ràng buộc giữa các filter khiến cho kiến trúc thiếu sự linh hoạt trong việc thay đổi hoặc cập nhật quy trình xử lý.
 
* **Tình huống áp dụng**: các ứng dụng xử lý có thể chia ra thành các công đoạn xử lý độc lập với nhau, các ứng dụng có dữ liệu lớn và tính đơn điệu, không yêu cầu tương tác ngườii dùng.

##### b. Kiến trúc ống và lọc
![[Pasted image 20221226145149.png]]
* **Đặc tả**: sự mở rộng của kiến trúc tuần tự, cho phép các bộ lọc có thể thực hiện song hành với nhau (pipes)
 
 > [!check] Ưu điểm
 > * Cho phép chia nhỏ các tác vụ thành các bộ lọc độc lập, giúp tăng tính tái sử dụng và linh hoạt hơn trong việc sửa đổi và cập nhật hệ thống.
 > * Các bộ lọc có thể được xây dựng và kiểm thử độc lập -> giảm thiểu lỗi hệ thống.
 > * Giúp tách rời việc xử lý dữ liệu với cách trình bày kết quả -> tăng tính hiệu quả và tái sử dụng
 > * Các pipes giúp giảm tải hệ thống
 
 > [!failure] Nhược điểm
 > * Kiến trúc có thể trở nên phức tạp nếu số lượng pipes và filters quá lớn
 > * Các bộ lọc phải đáp ứng được định dạng của dữ liệu truyền trong pipes -> gặp khó khăn khi dạng dữ liệu phức tạp
 > * Việc xử lý lỗi có thể khó kkhăn vì các bộ lọc độc lập -> khó xác định lỗi
 > * Việc triển khai có thể mất nhiều tgian và tài nguyên.
 
* **Tình huống áp dụng**:

#### Kiến trúc gọi và trả về (chương trình chính và các thủ tục)
![[Pasted image 20221226145522.png]]
* **Đặc tả**: thể hiện dưới dạng cây phân cấp
	* Càng sâu, độ phức tạp càng lớn
	* Càng rộng, quy mô càng lớn
	* 

 
 > [!check] Ưu điểm
 > * Cho phép các thành phần được phân tán và tương tác với nhau một cách hiệu quả
 > * Tính độc lập giữa các thầnh phần -> tăng khả năng sửa đổi, cập nhật và tái sử dụng
 > * Giúp giảm thiểu hệ thống bằng cách chia nhỏ quá trình xử lý thành các yêu cầu và trả về kết quả
 > * Giúp các ứng khác khác nhau giao tiếp với nhau một cách linh hoạt -> tăng tính tương thích
 
 > [!failure] Nhược điểm
 > * Yêu cầu một quá trình mạng -> hiệu suất thấp nếu kết nối mạng ko ổn định
 > * Có thể trở nên quá phức tạp nếu có quá nhiều thành phần phần mềm được kết nối với nhau
 > * Việc phân tách có thể giảm tính toàn vẹn của dữ liệu hoặc thông tin
 > * Kiến trúc yêu cầu các thành phần phần mềm cần phải được chuẩn hoá để đảm bảo tính tương thích.
 
* **Tình huống áp dụng**:

#### Kiến trúc phân lớp
![[Pasted image 20221226151645.png]]

* **Đặc tả**: hệ thống bao gồm các lớp chức năng đặt chồng lên nhau.
	* Mỗi lớp (layer) có chức năng cụ thể, rõ ràng.
	* Layer dưới cung cấp dịch vụ cho layer phía trên.
 
 > [!check] Ưu điểm
 > * Giảm thiểu sự phụ thuộc giữa các lớp, tăng tính tái sử dụng của mã nguồn
 > * Bảo trì, sửa đổi hệ thống đơn giản và dễ dàng hơn
 > * Các lớp có thể được phát triển và triển khai độc lập, giúp tăng tính linh hoạt của kiến trúc
 > * Tính bảo mật cao
 
 > [!failure] Nhược điểm
 > * Khó tách bạch các layer
 > * Chia quá nhiều layer có thể làm giảm sút hiệu năng của hệ thống
 
* **Tình huống áp dụng**: 
	* Phát triển hệ thống có sẵn -> xây dựng các lớp báo quanh các lớp đã có sẵn
	* Yêu cầu bảo mật ở nhiều mức khác nhau

### Thiết kế kiến trúc
> [!info] Thiết kế kiến trúc
> Là quá trình xác định và tinh chỉnh các thành phần phần mềm thực hiện từng nguyên mẫu.

> [!note] Các bước thiết kế kiến trúc
> 1. Thu thập các kịch bản
> 2. Gợi ý các yêu cầu, ràng buộc và đặc tả môi trường
> 3. Mô tả các phong cách/ mô hình kiến trúc đã được lựa chọn để giải quyết  các tình huống và yêu cầu:
> 	* Quan điểm module
> 	* Góc nhìn quá trình
> 	* Quan điểm dòng dữ liệu
> 4. Đánh giá chất lượng thuộc tính bằng cách quan sát chúng khi bị cô lập
> 5. Xác định mức độ nhạy cảm của các thuộc tính chất lượng vs thuộc tính kiến trúc khác nhau trong một phong cách kiến trúc nhất định.
> 6. Kiến trúc ứng cử 

## 4. Thiết kế chi tiết phần mềm
> [!info] Thiết kế chi tiết
> Chỉ ra chi tiết và đầy đủ về thành phần
> -> tạo điều kiện xây dựng phần mềm ở các pha phía sau 

> [!note] Thế nào là một thành phần?
> * Có tính module: có thể phân chia
> * Đóng gói thực thi: 
> 	* Có thể triển khai được
> 	* Có thể thay thế được
> * Có một tập các interface


```start-multi-column
ID: ID_jmec
Number of Columns: 2
Largest Column: right
border: off
```


* Theo góc nhìn **hướng đối tượng**: một thành phần bao gồm một tập các lớp cộng tác 

--- column-end ---

![[Pasted image 20221226153649.png]]


=== end-multi-column

```start-multi-column
ID: ID_359m
Number of Columns: 2
Largest Column: right
border: off
```


* Theo góc nhìn **quy ước**: một thành phần bao gồm:
	* Logic xử lý
	* Cấu trúc dữ liệu bên trong để triển khai logic
	* Giao diện cho phép gọi thành phần và truyền dữ liệu cho nó

--- column-end ---

![[Pasted image 20221226153703.png]]


=== end-multi-column

### Các nguyên lý thiết kế cơ bản
|Nguyên lý|Định nghĩa|
|---|:---|
|Nguyên lý mở-đóng (OCP)| Một mô-đun (thành phần) nên được mở cho việc mở rộng nhưng nên đóng cho việc hiệu chỉnh.|
|Nguyên lý thay thế Liskov (LSP)|Các lớp con nên thay thế được các lớp cha|
|Nguyên lý tráo đổi phụ thuộc (DIP)|Phụ thuộc vào trừu tượng hóa, không phụ thuộc vào kết cấu.
|Nguyên lý tách biệt giao diện (ISP)|Nhiều giao diện client cụ thể thì tốt hơn một giao diện mục đích chung.|
|Nguyên lý phát hành và tái sử dụng tương đương (REP)|"Nguyên tắc tái sử dụng là nguyên tắc phát hành".</br>Nói cách khác, nếu một thành phần được coi là có thể tái sử dụng thì nó phải là một đơn vị có thể thay thế được.|
|Nguyên lý đóng chung (CCP)|Các lớp thay đổi cùng nhau thì thuộc về nhau|
|Nguyên lý tái sử dụng chung (CRP)|Các lớp không được tái sử dụng cùng nhau thì không nên nhóm lại với nhau|

### Hướng dẫn thiết kế
* **Thành phần**:
	* Quy ước đặt tên nên được thiết lập cho các thành phần được xác định như là một phần của mô hình kiến trúc rồi sau đó tinh chỉnh và xây dựng như là một phần của mô hình mức thành phần

* **Giao diện**:
	* Giao diện cung cấp thông tin quan trọng về sự giao tiếp và cộng tác (đồng thời cũng giúp chúng ta đạt được OPC)

* **Phụ thuộc và kế thừa**:
	* Việc mô hình hóa sự phụ thuộc từ trái sang phải và sự kế thừa từ dưới lên trên.

#### Thiết kế mức thành phần 

* Bước 1. Xác định tất cả các lớp thiết kế tương ứng với miền vấn đề.
* Bước 2. Xác định tất cả các lớp thiết kế tương ứng với kết cấu hạ tầng.
* Bước 3. Xây dựng tất cả các lớp không có được như là thành phần tái sử dụng.
	* Bước 3a. Xác định chi tiết thông điệp khi các lớp hoặc các thành phần cộng tác.
	* Bước 3b. Xác định các giao diện thích hợp cho mỗi thành phần.
	* Step 3c. Xây dựng các thuộc tính và xác định kiểu dữ liệu và cấu trúc dữ liệu cần thiết để thực hiện chúng.
	* Step 3d. Mô tả luồng xử lý trong từng hoạt động cụ thể.
* Step 4. Mô tả các nguồn dữ liệu bền vững (cơ sở dữ liệu và các tập tin) và xác định các lớp cần thiết để quản lý chúng.
* Step 5. Phát triển và xây dựng biểu diễn hành vi cho một lớp hoặc một thành phần.
* Step 6. Xây dựng sơ đồ triển khai để cung cấp thêm thông tin về chi tiết thực hiện.
* ``Step 7. Nhân tố hóa mỗi thể hiện thiết kế mức thành phần và luôn luôn xem xét phương án thay thế.

> [!note] Thiết kế thành phần quy ước

> [!note] Thiết kế thuật toán

### Thiết kế dữ liệu
1. Yêu cầu về dữ liệu
2. Thiết kế/phân tích dữ liệu mức khái niệm (Mô hình thực thể liên kết)
3. Thiết kế logic (Mô hình quan hệ với SQL)
4. Thiết kế dữ liệu vật lý (Bảng, kiểu dữ liệu, ràng buộc, index)

> [!note] Nguyên tắc thiết kế dữ liệu
> * Nhận diện cả cấu trúc dữ liệu và tác vụ truy xuất
> * Chú ý sử dụng từ điển dữ liệu
> * Trì hoãn thiết kế dữ liệu mức thấp cho đến cuối đoạn này
> * Che giấu biểu diễn bên trong của cấu trúc dữ liệu 
> * Nên áp dụng kiểu ADT trong thiết kế cũng như trong lập trình.

## 5. Tính móc nối (Coupling) và tính kết dính (Cohension) 
> [!question] Thế nào là một thiết kế tốt?
> * Dễ đọc hiểu, phát triển
> * Dễ giao tiếp
> * Dễ mở rộng (thêm chức năng mới)
> * Dễ cho việc bảo trì

### Chất lượng của thiết kế
* Mỗi module có tính **cố kết cao (high cohension)**
	* Mỗi module là một đơn vị logic
	* Toàn module cùng đóng góp thực hiện một mục tiêu
* **Liên kết lỏng lẻo (loose coupling)** giữa các module
	* Ít ràng buộc, ít phụ thuộc lẫn nhau
* Dễ hiểu
* Định nghĩa rõ ràng
	* Các module và quan hệ giữa chúng

> [!info] Sự gắn kết - Cohension
> Mức độ mà các **phần tủ của một module** thuộc về nhau. Tính gắn kết là thước đo mức độ liên quan hoặc tập trung của các trách nhiệm của một module đơn lẻ

* Góc nhìn **hướng đối tượng**: sự gắn kết = một thành phần hoặc 1 lớp chỉ đóng gói các thuộc tính và hoạt động liên quan chặt chẽ với nhau và với bản thân thành phần hoặc lớp đó

* Góc nhìn **quy ước**: "tư duy đơn lẻ" của module một module nên giải quyết một nhóm mỗi quan tâm duy nhất

* Các mức của sự gắn kết:
	* Chức năng
	* Tầng
	* Truyền thông
	* Liên tục
	* Thủ tục
	* Phụ thuộc thời gian
	* Lợi ích

> [!note] Ghép nối - Coupling
> Mức độ mà mỗi module phụ thuộc vào từng module khác.

* Góc nhìn **hướng đối tượng**: một thước đo chất lượng mức độ kết nối của các lớp với lớp khác.

* Góc nhìn **quy ước**: mức độ mà một thành phần kết nối với các thành phần khác và với thế giới bên ngoài

* Các mức của ghép nối:
	* Nội dung
	* Chung
	* Điều khiển
	* Đánhh dấu
	* Dữ liệu
	* Lời gọi công thức
	* Loại sử dụng
	* Sự lồng ghép và bao hàm
	* Bên ngoài