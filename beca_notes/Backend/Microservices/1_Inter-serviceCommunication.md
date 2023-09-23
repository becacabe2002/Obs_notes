> [!abstract] 
> Phụ thuộc vào tính chất của service, thường có 3 communication style chính:
> * Remote Procedure Invocation
> * Messaging
> * Domain-specific protocol

## I. Remote Procedure Invocation - RPI
> Client sử dụng request/reply-based protocol để gửi requests tới một service.

![[Pasted image 20230923162026.png]]

* Các service có thể kết nối trực tiếp với nhau thông qua API end-point

* Một vài pattern cho RPI:
	* ***REST*** ([[REST]])
	* ***gRPC*** ([[gRPC]])
	* ***Apache Thrift***

> [!check] Lợi ích
> * Đơn giản
> * Request/reply dễ dàng
> * Hệ thống đơn giản, ko cần các message broker phục vụ gửi/nhận request/response

> [!failure] Nhược điểm
> * Ko hỗ trợ notifications, request/async response, publish/subcribe, publish/async response.
> * Client và service luôn active trong suốt thời gian tương tác.

## II. Messaging
> Sử dụng asynchronous messaging để giao tiếp giữa các services. Các services trao đổi message qua các kênh message.

![[Pasted image 20230923162820.png]]
*VD:
* *Order service publish một msg tới msg queue theo một topic nào đó.
* *Payment service và các service sẽ subscribe tới một topic cụ thể.
* *Các service nhận msg được gửi tới topic tương ứng*

* Một vài messaging pattern:
	* ***Apache Kafka*** ([[Kafka]])
	* ***RabbitMQ***

> [!check] Ưu điểm
> * Hỗ trợ nhiều kiểu giao tiếp dạng asynchronous
> * Tách biệt người gửi và người nhận, các tin nhắn sẽ được lưu tới khi người nhận có thể xử lý (hoặc bị tiêu hủy nếu quá timetolive)

> [!failure] Nhược điểm
> * Hệ thống phức tạp hơn vì cần message broker

## III. Domain-specific protocol
* Email protocols: SMTP, IMAP
* Media streaming protocols: RTMP, HLS, HDS

