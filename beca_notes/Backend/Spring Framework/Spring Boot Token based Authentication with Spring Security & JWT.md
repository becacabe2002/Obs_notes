**Hình ảnh tổng quát hệ thống**
![[Pasted image 20230402154828.png]]

> [!note]- Các APIs sẽ được cung cấp
> ![[Pasted image 20230402163037.png]]

> [!note]- Mô hình cho các thao tác như Đăng kí tài khoản, Login, Truy cập vào tài nguyên
> ![[Pasted image 20230402163111.png]]
> * Khi Token bị quá hạn (expired), gửi request làm mới token
> ![[Pasted image 20230402163241.png]]

## Các thành phần chi tiết của hệ thống
### Spring Security 
> ==Thành phần **quan trọng nhất** trong hệ thống==

- `WebSecurityConfig` là một class cho phép cấu hình các yếu tố như: **CORS**, **CSRF**, **Session**, rules cho các tài nguyên được bảo vệ.

> [!info] CORS (Cross-Origin Resource Sharing)
> cho phép hoặc từ chối webApp có thể tiếp cận tài nguyên nếu từ domains khác. (Mặc định là từ chối tất cả các cross-origin requests)

> [!info] CSRF (Cross-Site Request Forgery (giả mạo)) 
> là loại tấn công mà các trang web độc, trên danh nghĩa người dùng đã được xác thực, thực hiện request tới trang web khác.
>+ Spring Security cung cấp **built-in CSRF Protection** bằng cách sử dụng tokens để xác thực requests. 
	
- Spring Sec cho phép quản lý session bằng các phương thức khác nhau (in-memory, JDBC-based, Redis-based ...)
	+ Cần thiết để tránh các trường hợp ***session hijacking*** hoặc CSRF  

- `WebSecurityConfig` cho phép người dùng có thể tùy chọn phương thức xác thực và phân quyền.
	+ Có thể cấu hình access rules cho các tài nguyên được bảo vệ dựa trên vai trò hoặc sự cho phép.

> [!info] JSON Web Token - JWT 
> * Thường được sử dụng trong truyền tin bảo mật giữa các thành phần theo một cách gọn nhẹ và có thể sửa đổi được.
> * Là một chuỗi kí tự bao gồm 3 phần, phân cách bằng các dấu chấm (các phần được mã hóa theo dạng Base64)
> 	* **Header**: chứa các thông tin liên quan tới định dạng của token và hàm được sử dụng trong **signature**
> 	* **Payload**: chứa đựng thông tin được truyền đi. (UserID, email, ...)
> 	* **Signature**: được tạo ra bởi việc kết hợp encoded **header** và **payload** với khóa bí mật được ghi trong header. 
> 		* Được sử dụng để xác minh tính xác thực của token.

#### UserDetailService
> giao diện có phương thức để nạp người dùng bằng **username** và trả về **`UserDetails`**

* **`UserDetails`** : obj mà Spring Sec có thể sử dụng cho việc xác thực và thẩm định, bao gồm các thông tin như **username**, **password**, **authorities**

#### AuthenticationManager
* có **`DaoAuthenticationProvider`** (với sự giúp sức của **`UserDetailService`** và **`PasswordEncoder`**) để có thể xác thực đối tượng **`UsernamePasswordAuthenticationToken`**.
	* **`UsernamePasswordAuthenticationToken`** lấy các trường {username, password} từ login request
	* Nếu xác thực thành công, **AuthenticationManager** trả về một đối tượng xác thực đầy đủ (bao gồm phân quyền).

#### OncePerRequestFilter
* single execution cho mỗi  request tới API. 
* cung cấp hàm `doFilterInternal()` mà sẽ được sử dụng để:
	* Rà soát và thẩm định JWT
	* Load thông tin người dùng (sử dụng **`UserDetailService`**)
	* Kiểm tra phân quyền (sử dụng **`UsernamePasswordAuthenticationToken`**)

#### AuthenticationEntryPoint 
> được sử dụng để xử lý các lỗi xác thực 

#### Repository
* Chứa các repo như **UserRepository** và **RoleRepository** để làm với DB
* Sẽ đuợc import vào **Controller**

#### Controller
> Tiếp nhận và xử lý các request sau khi đã đuợc lọc bởi `OncePerRequestFilter`

* **`AuthController`** xử lý các signup/login requests
* **`TestController`** có các phương thức truy nhập vào tài nguyên được bảo vệ với thẩm định phân quyền 