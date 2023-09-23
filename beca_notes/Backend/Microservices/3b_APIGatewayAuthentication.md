![[Pasted image 20230923213755.png]]

> [!abstract] Roles of API Gateway
> * Managing API request traffic as a single point of entry.
> * Managing API authentication/authorization

* **Managing API request traffic**:
	* Gateway đứng giữa các APIs và người dùng muốn sử dụng các APIs đó.
	* Người dùng muốn truy cập tới các đầu APIs đó chỉ cần thông qua việc tương tác với Gateway, nó sẽ chuyển hướng request tới API phù hợp và trả về kết quả cho người dùng.
	-> Phù hợp với hệ thống nhiều ứng dụng, bao gồm nhiều microservices.

* **Managing API authen/author**:
	* Sử dụng các authentication services (Okta, OAuth-based authentication ...) để có thể xác minh và phân quyền cho người dùng ngoại vi.
		* Áp dụng giới hạn volume
		* Kiểm soát truy cập đối với các request của clients. (read-only, role-based access ...)
	* Gateway cũng có thể tự quản lí authen/author bằng các công nghệ như Basic Auth, API Key Authentication, LDAP...

> [!question] Vì sao cần có API Authentication/Authorization?
> * Bảo vệ khỏi các lỗi lầm, vi phạm dữ liệu, malicious hack cũng như các vấn đề về truy cập khác. Đảm bảo user chỉ có khả năng truy cập tới các thông tin và điều khiển hệ thống đúng thẩm quyền
> * Cho phép giới hạn lưu lượng dữ liệu được truyền phát, nhằm ngăn chặn các cuộc tấn công, hoặc người dùng API làm quá tải hệ thống.
> * Cho phép ngừng truy cập tới các dịch vụ sau khi subscription hết hạn.
> * Cho phép điều khiển các xác minh thất bại (điều hướng, cho phép tiếp cận giới hạn ...)

## Ưu điểm của API Gateway Authentication
1. Bỏ qua việc phát triển phương thức xác minh từ đầu, mà thay vào đó có thể sử dụng các dịch vụ được cung cấp ngoài.
2. Thuận tiện cho người dùng cuối. 
	* Có thể sử dụng các tài khoản có sẵn để đăng nhập (Facebook, Google, ...) -> giảm tải thời gian đăng kí tk của user
	* Admin có thể nhanh chóng phân quyền cho user (administrator, manager, read-only access), một team hoặc thành viên của team 

## Phân loại các phương pháp API Gateway Authentication
### 1. Basic Authentication

### 2. API Key Authentication

### 3. LDAP Authentication

### 4. OAuth 2.0 Authentication

### 5. OpenID Connect

