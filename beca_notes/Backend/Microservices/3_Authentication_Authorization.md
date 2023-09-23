> [!question] Làm sao để xác thực và phân quyền một cách linh hoạt, an toàn và hiệu quả?

## 1. Nhắc lại với Monolithic
![[Pasted image 20230923173916.png]]

* Trong kiến trúc Monolithic, toàn bộ ứng dụng là một quá trình.
	* Một module bảo mật sẽ được sử dụng để thực hiện Authen/Author cho user.
	* Khi Client đăng nhập, module sẽ xác thực danh tính người dùng và tạo ra **sessionID** trả lại cho Client.

![[Pasted image 20230923174232.png]]

* Khi client tạo request đến server nó sẽ gửi kèm **sessionID**, server kiểm tra tính xác thực và quyền mà user được phân.

## 2. Vấn đề về Authen/Author của Microservice.
* Mỗi hệ thống con cũng cần được xác thực/phân quyền.

Nếu áp dụng theo hướng của Monolithic:
* Mỗi service có nhu cầu cần phải tự thực hiện việc xác thực và phân quyền. Tuy có thể sử dụng các thư viện giống nhau, việc bảo trì thư viện chung đối với nhiều nền tảng ngôn ngữ khác nhau rất tốn kém. 
	* Các services bị phụ thuộc vào một thư viện cụ thể cùng phiên bản cụ thể -> Ảnh hưởng đến tính linh hoạt của lựa chọn công nghệ thực hiện.

* Giảm tốc độ của việc phát triển mỗi service, ảnh hưởng tới thời gian đầu tư xây dựng nghiệp vụ chính.

* Các service thông thường sẽ cung cấp interface dưới dạng **RESTful API** (sử dụng giao thức HTTP). Các request đi qua nhiều thành phần của hệ thống. Nếu duy trì trạng thái **stateful** 
	-> Khó khăn cho việc mở rộng hệ thống chiều ngang. 

* Service có thể được truy cập từ nhiều dạng Client, từ đó việc xác định identity và authorization ở nhiều context khác nhau sẽ phức tạp.

## 3. Giải pháp cho xác thực và phân quyền của Microservices.
### 3.1 Distributed Session Management
* **Sticky Session** - đảm bảo tất cả request từ một user sẽ luôn gửi tới server đã xử lý request đầu tiên
	* Yêu cầu load balancer, nhưng khi load balancer gửi request của user tới server khác thì tất cả session của user đó sẽ bị mất.
	* Chỉ đáp ứng được horizontally scaling cluster.

* **Session Replication** - mỗi server lưu hết session, đồng bộ thông qua mạng.
	* Tuy nhiên sau mỗi lần session bị thay đổi, dữ liệu lại phải đồng bộ tới tất cả các server -> Có thể dẫn tới nghẽn băng thông

* **Centralized Sessio Storage** - dữ liệu user được lưu trữ chung, đảm bảo các microservices đọc được dữ liệu giống nhau.
	* Tuy nhiên, sẽ cần một cơ chế bảo mật riêng biệt cho kho lưu trữ session.
![[Pasted image 20230923211900.png]]

==👉 Sử dụng Session gây trở ngại cho việc mở rộng theo chiều ngang của server.==
### 3.2 Client Token
* Trong khi Session được lưu trữ tập trung tại server, Token lại được giữ bởi user (thường lưu trữ ở trình duyệt dưới dạng cookie).

* Token lưu trữ **thông tin nhận dạng** của user
	* Mỗi khi user gửi request tới server, token được gửi kèm nhằm xác định authen/author của user đó.

* Thông tin nội dung của Token thường được mã hóa để tránh làm sai lệch (bởi user/3rd party application).
	* Thường sử dụng chuẩn ***Json Web Token (JWT)***
![[Pasted image 20230923212632.png]]

> [!check] Lợi ích của Token
> * Trạng thái kết nối stateless, thông tin không được lưu trữ trên server
> * Dễ phát triển, mở rộng
> * Performance tốt hơn do thông tin cần đọc có ở trong request.

#### Client Token with API Gateway
![[Pasted image 20230923213411.png]]

