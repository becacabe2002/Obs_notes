> [!question] Làm thế nào để duy trì tính nhất quán dữ liệu trong kiến trúc Microservices.

> [!important] Yêu cầu khi xây dựng DB cho hệ thống microservices.
> * Các services cần đảm bảo loose coupling để việc deploy, development và scale được độc lập.
> * Một số Business Transactions cần thực thi tính nhất quán và bất biến trên nhiều services, trong khi một số BT khác phải cập nhật data thuộc sở hữu của nhiều services khác nhau.
> * Một số queries cần join data thuộc sở hữu của các services khác nhau.
> * DB đôi khi phải được nhân rộng hoặc phân chia để mở rộng quy mô.
> * Các services khác nhau có yêu cầu lưu trữ dữ liệu khác nhau. (Có thể là SQL hoặc No-SQL)

## Shared Database
* Một db được chia sẻ cho nhiều services.
* Các services được tự do truy cập các bảng của nhau để đảm bảo [[C9 (old)- TRANSACTION#I. Đặc tính ACID của transaction]]
![[Pasted image 20230923165444.png]]

> [!check] Lợi ích
> * Đơn giản 
> * Devs có thể sử dụng ACID transactions để thực thi tính nhất quán dữ liệu.

> [!failure] Hạn chế
> * **Development time coupling**: thay đổi schema của DB gây ảnh hưởn tới nhiều services -> làm chậm quá trình phát triển của các nhóm phát triển khác.
> * **Runtime coupling**: các services có khả năng can thiệp lẫn nhau (cùng truy cập tới 1 bảng) -> tăng tgian truy vấn.
> * Khó đáp ứng đủ yêu cầu về lưu trữ và truy cập dữ liệu đối với một hệ thống lớn.

## Database per service
> Mỗi service có một db riêng. Các services khác nếu muốn thao tác với DB này cần phải thông qua API của service quản lý DB đó.

![[Pasted image 20230923170257.png]]

* CSDL của service cũng là một phần của việc triển khai service đó.
* Tuy nhiên, không cần phải cung cấp một máy chủ csdl riêng cho mỗi service để giữ cho mỗi service db là private.

> [!note] Một số cách thức để cung cấp private DB
> * **Private-tables-per-service**: mỗi service sở hữu một tập các tables chỉ được truy cập bởi services đó.
> * **Schema-per-service**: mỗi service có một schema riêng tư với service đó. 
> * **Database-server-per-service**: mỗi service có một database server riêng.

* `private-tables-per-service` và `Schema-per-service` có chi phí thấp nhất.
* `Schema-per-service` sẽ làm rõ việc sở hữu.
* `database-server-per-service` phù hợp khi service có lượng truy cập cao

> [!check] Lợi ích
> * Giúp đảm bảo rằng các services được kết nối lỏng lẻo -> việc thay đổi db của một services ko làm ảnh hưởng đến bất kỳ services nào khác.
> * Mỗi dịch vụ có thể sử dụng loại cơ sở phù hợp nhất với nhu cầu của nó. (ElasticSearch cho việc tìm kiếm ...)

> [!fail] Hạn chế
> * Việc thực hiện các transaction trải rộng trên nhiều services không đơn giản -> các transaction phân tán nên được hạn chế vì [[CAP Theory]]. Nhiều NoSQL ko hỗ trợ.
> * Khó khăn trong việc thực hiện các queries cần join data trong nhiều csdl.
> * Sự phức tạp trong việc quản lý nhiều csdl

* Có nhiều patterns/solutions khác nhau để giải quyết bài toán query và transaction trên nhiều services.
	* Để thực hiện transaction trên nhiều services -> [[Saga Pattern]]
	* Để thực hiện query trên nhiều services -> [[API Composition]] hoặc [[Command Query Responsibility Segregation]]

