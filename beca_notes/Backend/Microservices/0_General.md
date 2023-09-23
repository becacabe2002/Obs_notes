### Monolithic Architecture
* Các business logic được thể hiện bởi các khối dịch vụ, đối tượng cho từng vùng nghiệp vụ (domain obj) và các sự kiện (events)
* Trong nhiều trường hợp, các services có thể được xây dựng độc lập nhưng được triển khai chung, đóng gói và cài đặt thành 1 khối duy nhất.

> [!failure] Các bất lợi
> * Phức tạp, kích thước lớn -> khó khăn cho việc bảo trì hay thêm tính năng mới
> * Khó phát triển theo Agile
> * Phải triển khai lại toàn bộ hệ thống mỗi lần cập nhật/nâng cấp dù chỉ 1 service.
> * Các service yêu cầu về tài nguyên khác nhau -> khó khăn trong việc mở rộng
> * Cả hệ thống có thể bị sập đồng thời
> * Khó thay đổi, ứng dụng công nghệ mới.

==👉 **Microservices** khắc phục các nhược điểm này.==

## Microservices
> * Tổng hợp nhiều services nhỏ, được phát triển và triển khai độc lập riêng biệt
> * Mỗi service thực hiện các chức năng riêng biệt, có kết nối với nhau.

* Một số dịch vụ nhỏ lộ ra giao tiếp API cho các services khác, hoặc ứng dụng client gọi tới.
* Mỗi service được chạy trong máy ảo hoặc Docker container riêng.

> [!check] Ưu điểm
> 1. **Cho phép dễ dàng continuous delivery và deployment các ứng dụng lớn, phức tạp**:
> 	* Cải thiện khả năng bảo trì
> 	* Khả năng testing được cải thiện
> 	* Các service được triển khai độc lập -> Khả năng triển khai tốt hơn
> 	* Cho phép các service khác nhau được phát triển bởi các team khác nhau.
> 2. **Giảm thiểu rủi ro:** 
> 	* nếu có lỗi trong một service thì chỉ có service đó bị ảnh hưởng, ko phải toàn bộ hệ thống
> 3. **Dễ dàng thay đổi các công nghệ mới**

> [!failure] Nhược điểm
> 1. **Phức tạp trong việc phát triển một hệ thống phân tán**:
> 	* Cần implement inter-services communication
> 	* Một luồng xử lý đi qua nhiều service -> Khó khăn trong việc handle partial failure
> 	* Cần sự phối hợp giữa các team để handle requests cần sự tham gia nhiều service.
> 	* Khó khăn trong việc đảm bảo toàn vẹn CSDL nếu triển khai theo kiến trúc cơ sở dữ liệu phân vùng.
> 1. **Triển khai và quản lý hệ thống sẽ phức tạp hơn**
> 2. **Cần quan tâm tới rủi ro/lỗi khi gửi thông điệp**

### Các quy chuẩn cần tuân thủ khi phát triển Microservices
* **Single Responsibility Principle (SRP)**:
	* Một service chỉ phục vụ một mục tiêu duy nhất
	* Giúp giảm sự phức tạp và tăng tính linh hoạt

* **High Cohension and Low Coupling**:
	* Một service chỉ nên phục vụ 1 mục đích, và phục vụ tốt mục đích đó -> High Cohension
		* Các functions trong 1 service cần có liên hệ chặt chẽ
	* Các service không nên quá phụ thuộc vào nhau -> Low Coupling
		* Mức độ phụ thuộc được đo lường bằng tri thức của module tới module khác.
		* Khi các service có low Coupling -> giúp kiểm tra ứng dụng theo các thành phần riêng.

* **Discrete Boundaries**:
	* Các microservices có kích thước nhỏ và được triển khai như các khối chức năng độc lập.
	* Trong kiến trúc microservices rời rạc, mỗi service chịu trách nhiệm cho một task nhất định.
	* Khi thiết kế một hệ thống microservices, cần nên tránh có sự phụ thuộc chồng chéo giữa các services.
	
	*VD: Khi có hai service là authentication/authorization và user profile managing -> service user profile managing ko nên gọi tới service còn lại để hoạt động chính xác.*
		
> [!tip] Cách xử lý có thể áp dụng
> Implement một gateway có thể biên dịch requests từ một service thành requests mà service khác có thể hiểu được.
> ```shell
> service1 --[make request]--> API gateway --[translate]--> servie2
> ```

* **Design for Failure**:
	* ***Circuit Breaker Pattern*** là một design pattern được dùng để bảo vệ hệ thống chống lại các cascading failure trong một hệ thống phân tán.
		* Nó cho phép failure của một service xảy ra có kiểm soát, khi service đó thường xuyên gặp lỗi, mà không gây ảnh hưởng tới toàn bộ hệ thống.
	* Cho phép các services khác của hệ thống hoạt động một cách bình thường, kể cả trong trường hợp một service gặp sự cố.
	* Lỗi của một service (memory leak, lỗi kết nối db, ...) sẽ không dẫn tới failure của toàn bộ application.

* **Business Capabilities**:
	* Mỗi service nên chịu trách nhiệm cho một business capability cụ thể. Và tất cả các service sẽ bao quát tất cả các business capability cần thiết.

> [!question] Lý do
> * Dễ hiểu và thay đổi các service nếu cần.
> * Dễ mở rộng cho các service cần thiết mà không cần thay đổi tất cả.
> * Giúp devs có thể thiết kế ứng dụng đàn hồi.
> * Hạn chế ảnh hưởng tới người dùng khi một trong các service bị lỗi.

* **Decentralization**: ko giống các ứng dụng monolithic, trong microservices, mỗi service duy trì bản sao dữ liệu riêng.
	-> Cho phép devs tập trung kiểm soát truy cập, đồng thời thực hiện ghi nhật ký kiểm tra và lưu vào bộ nhớ đệm.

> [!tip] 
> Lý tưởng nhất khi mỗi service có 1-2 bảng trong db.

* **Process Automation**:
	* There are several deployment units need to be managed.
	-> The deployment process should be automated.

> [!tip] 
> Embracing DevOps culture and using **Azure DevOps/ Jenkins**

* **Inter-Service Communication**:
	* Có vài phương pháp có thể sử dụng để implement inter-service communication trong hệ thống microservices.
		* PP tiếp cận dựa trên sự kiện: một service công bố một sự kiện và service khác có thể theo dõi và phản ứng dựa trên sự kiện đó.
		* PP tiếp cận dựa trên thông điệp: sử dụng các messaging protocol (HTTP, AMQP) để trao đổi thông điệp giữa các services.
	* Các service phải được đóng gói về mặt kĩ thuật và chỉ để lộ các APIs cho phép các services khác truy cập thông qua chúng.

* **Monitoring**:
* **Command Query Responsibility Segregation**:



