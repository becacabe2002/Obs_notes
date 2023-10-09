* Đối với việc lựa chọn mô hình **Database per Service**, mỗi service sẽ có một db riêng -> xuất hiện các transaction trải rộng trên nhiều services.
	-> Cần thiết phải có cơ chế để đảm bảo tính thống nhất của dữ liệu trên các services. (Không thể sử dụng cơ chế **2PC**)

> [!info]- Two-phase commit protocol - 2PC
> Thuật toán đảm bảo các nút khác nhau của một hệ thống phân tán xác nhận một transaction.
> * Trong quá trình xác nhận, nếu một trong các nút của hệ thống phủ nhận transaction, toàn bộ transaction sẽ bị hủy bỏ. (Transaction chỉ thành công nếu tất cả các node của hệ thống chấp nhận).
> * Quá trình xác nhận bao gồm 2 phases:
> 	* **Gửi yêu cầu**: nút điều phối (coordinator) gửi câu truy vấn, yêu cầu xác nhận giao dịch tới tất cả các nút tham gia, sau đó đợi trả lời từ các nút đó.
> 	* **Xác nhận giao dịch:** 
> 		* khi nút điều phối nhận được trả lời đồng ý của tất cả các nút tham gia, gửi lại thông điệp xác nhận tới tất cả các nút tham gia một lần nữa để hoàn tất việc giao dịch, và giao dịch đó được xác nhận thành công.
> 		* Trong trường hợp có 1 nút trả lời phủ định giao dịch, hoặc nếu sau khoảng tgian nhất định vẫn chưa nhận được toàn bộ trả lời từ các nút tham gia. Nút điều phối sẽ gửi thông điệp hủy bỏ việc xác nhận tới tất cả các nút tham gia, và việc xác nhận giao dịch thất bại.

> [!check] Solution
> * Coi mỗi một transaction trải rộng trên nhiều services là một ***Saga***. (Saga = chuỗi các transaction cục bộ trên các services khác nhau.)
> * Nếu một local transaction thất bại, Saga sẽ thực hiện 1 loạt các transactions để **rollback** lại các thay đổi đã thực hiện trước đó.

![[Pasted image 20230924152947.png]]

> [!abstract] Các cách triển khai Saga
> * Events/Choregraphy-based saga
> * Command/Orchestration-based saga

## Events/Choregraphy-based saga
* Service đầu tiên thực hiện transaction và sau đó publish 1 event.
* Event được lắng nghe bởi một/nhiều services.
	* Các services đó thực hiện transaction cục bộ và publish các event mới (hoặc ko)
* Transaction phân tán kết thúc khi service cuối cùng thực hiện transaction cục bộ của nó và ko publish bất kì event nào hoặc event được publish ko được nghe bởi bất kỳ services nào của saga.

![[Pasted image 20230924155827.png]]
*VD:*
- *`Order Service` sẽ tạo ra một đơn hàng ở trạng thái pending và gửi đi `ORDER_CREATED_EVENT`.
- *`Payment Service` lắng nghe `ORDER_CREATED_EVENT`, trừ tiền của khách hàng và gửi đi `BILLED_ORDER_EVENT`.*
- *`Stock Service` lắng nghe `BILLED_ORDER_EVENT`, cập nhật lại stock, chuẩn bị các sản phẩm và gửi đi `ORDER_PREPARED_EVENT`*.
- *`Delivery Service` lắng nghe `ORDER_PREPARED_EVENT`, sau đó nhận và giao sản phẩm. Cuối cùng nó gửi đi `ORDER_DELIVERED_EVENT`
- *`Order Service` lắng nghe `ORDER_DELIVERED_EVENT` và đặt lại trạng thái của đơn hàng*.

* Khi có lỗi xảy ra trong chuỗi transaction cục bộ -> Rollback các thay đổi.

![[Pasted image 20230924160000.png]]
* *`Stock Service` sẽ gửi đi `PRODUCT_OUT_OF_STOCK_EVENT`.*
* *`Order Service` và `Payment Service` lắng nghe `PRODUCT_OUT_OF_STOCK_EVENT`: Payment Service hoàn trả tiền cho khách hàng còn Order Service cập nhật trạng thái đơn hàng là không thành công.*

> [!check] Ưu điểm
> * Dễ hiểu
> * Các service có loose coupling

> [!fail] Nhược điểm
> * Khó khăn khi muốn mở rộng transaction.
> * Khó khăn khi testing (phải chạy tất cả các services.)

## Command/Orchestration-based saga
* Một service chịu trách nhiệm riêng biệt (**Orchestrator**) điều phối các logic của Saga.
	* Orchestrator sẽ giao tiếp với service theo dạng **command/reply** để cho chúng biết thực hiện thao tác nào.

![[Pasted image 20230924160838.png]]
*VD:*
* *`Order Service` tạo ra một đơn hàng ở trạng thái pending và yêu cầu `Order Saga Orchestrator (OSO)` bắt đầu một order transaction.*
* *`OSO` gửi lệnh Execute Payment đến `Payment Service`, và `Payment Service` trả lời bằng tin nhắn Payment Executed đối với `Oder Saga Reply Channel`.*
* *`OSO` gửi lệnh Prepare Order đến `Stock Service`, và `Stock Service` trả lời bằng message Order Prepared.*
* *`OSO `gửi lệnh `Deliver Order` đến `Delivery Service`, và nhận lại Order Delivered message.*

Khi cẩn cũng thuận tiện hơn trong việc rollback
![[Pasted image 20230924161206.png]]

* *`Stock Service` gửi cho `OSO` một Out-Of-Stock message;*
* *`OSO` nhận ra rằng transaction thất bại và bắt đầu rollback. Trong trường hợp này chỉ một thao tác duy nhất được thực hiện thành công trước khi thất bại, nên `OSO `sẽ gửi lệnh Refund Client đến `Payment Service` và đặt trạng thái của đơn hàng là không thành công.*

> [!check] Ưu điểm của việc có OSO
> * Giảm sự phức tạp của các services (chỉ cần quan tâm tới việc execute/reply lệnh)
> * giảm độ phức tạp khi thêm các steps mới vào transaction.
