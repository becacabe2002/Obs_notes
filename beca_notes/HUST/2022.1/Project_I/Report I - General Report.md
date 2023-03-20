**Người làm báo cáo** : Ngô Minh Tú 20205226 - K65 Công nghệ Thông tin Việt Pháp
**Nội dung bài báo cáo**: trình bày tổng quát về đề tài tìm hiểu ***"Sử dụng dữ liệu trong phân tích rủi ro của ngành tài chính."***

## Lý do chọn đề tài
* Hậu đại dịch COVID-19, đã có những chuyển biến lớn trong tất cả các mặt của đời sống,  trong đó không thể không kể tới sự ảnh hưởng đã, đang và sẽ diễn ra của nền kinh tế. Mức độ thiệt hại vô vùng to lớn, chạm mốc hàng nghìn tỷ đô.
* Đại dịch cũng đã phơi bày các vấn đề vô cùng nổi cộm, đó chính là khả năng phân tích rủi ro của các công ty.

 > [!question] 
 > Tại sao các công ty có giá trị lớn như các hãng hàng không hay các chuỗi cửa hàng lại có thể nhanh chóng lâm vào tình trạng phá sản chỉ sau một thời gian ngắn, trong khi đó các công ty ngành tài chính, ví dụ như các ngân hàng lại vẫn có thể trụ vững?
 
 => Câu trả lời cho điều đó chính là sự áp dụng của các bài **stress tests**, thành quả của quá trình phân tích dữ liệu rủi ro.

* Phân tích rủi ro trong các chủ thể tài chính (cụ thể hơn là các ngân hàng) vẫn còn rất nhiều dư địa để phát triển và cải tiến.

* Một trong những vấn đề được chú trọng nhất hiện nay là ***"Nhúng các mô hình vào trong các cơ sở dữ liệu, giúp chúng có thể thực hiện thao tác nhận dữ liệu và trả và lưu kết quả vào cùng cơ sở dữ liệu đó ngay lập tức"***

> [!quote] 
> "*... What is missing is the integration of model codes into the database so that the data can be processed in situ with results being generated and stored into the same database.* ...." 

* Trở ngại lớn nhất hiện tại đó chính là khoảng cách giữa lý thuyết (***Concept***) và triển khai (***Deployment***).

> [!warning] Khó khăn của các hướng tiếp cận:
> * Không thể thực hiện được từ phía các chuyên gia kinh tế do thiếu khả năng kỹ thuật
> * Không thể thực hiện được từ phía các kỹ thuật viên IT do thiếu kiến thức chuyên ngành...

> [!check] Sự xuất hiện của các ngôn ngữ mã nguồn mở như Python, R, đem tới khả năng tương tác trực tiếp với cơ sở dữ liệu.

### Các mục nội dung chính
> [!note] Các nội dung tìm hiểu chính trong đề tài
> 1. Các hình thái rủi ro và sự áp dụng dữ liệu
> 	* Phân loại rủi ro
> 	* Các khía cạnh cần quan tâm khi phân tích rủi ro thông qua dữ liệu
> 
> 2. Bối cảnh phân tích rủi ro
> 	* Các bước tiến hành  software acquisition
> 	* Quy trình liên ngành trong việc khai thác dữ liệu
> 	* Dòng chảy dữ liệu
> 
> 3. Kiểm toán dữ liệu
> 	* Tiến hành đánh giá dữ liệu: thiếu, không đáng tin cậy, lỗi thời,...
> 
> 4. Rủi ro của các tổ chức tài chính
> 
> 5. Các mô hình hoá và phân tích rủi ro thường thấy

## I. Các hình thái rủi ro và sự áp dụng dữ liệu
### a. Phân loại rủi ro
> [!warning] Không phải tất cả rủi ro đều giống nhau
> => Việc phân loại giúp chúng ta hiểu ro hơn về rủi ro cần đối phó, từ đó thiết kế và triển khai hệ thống một cách tối ưu hơn.

* Việc phân loại các rủi ro theo nguồn gốc của chúng như rủi ro vận hành, rủi ro tự nhiên, rủi ro về mặt công nghệ ... không giúp cho việc phân tích và quản lý chúng.
**=> Cần có một hướng tiếp cận khác trong việc phân loại rủi ro, nhằm đem lại hiệu quả cao hơn**

#### Mô hình "Xà lan chở hàng"
> Sử dụng mô hình một chiếc xà lan chở hàng trên biển để thể hiện các rủi ro có thể trong quá trình vận chuyển.

![[Pasted image 20230108092951.png]]
*Các phân loại sẽ được giữ nguyên bằng tiếng Anh*
* ***Inherent Risk***: liên quan tới nội tại của sự vật 
	* Ex: Quá trình tàu được xây dựng
* ***Single Exposure Risk*** : có một hay nhiều mặt phơi nhiễm lớn có thể gây ra sự sụp đổ của tổ chức
	* Ex: một kiện hàng chứa chất gây cháy nổ có thể phá huỷ cả xà lan
* ***Concentration Risk*** : manh tính tập trung, định hướng theo một chiều hơn Single Exposure Risk (theo một nhóm nhất định)
	* Ex: tàu bị nghiêng về một bên do các kiện hàng xếp lệch, dễ dẫn tới lật tàu
* ***Marginal Risk*** : các rủi ro cận biên
	* Ex: các kiện hàng được vận chuyển lên xuống ở các cảng mà tàu neo đậu, có khả năng gây ảnh hưởng tới tàu
* **Environmental Risk** : các yếu tố ngoại vi liên quan tới tự nhiên
	* Ex: Các điều kiện thời tiết xấu có thể ảnh hưởng tới tàu
* ***Forward Risk*** : Các ảnh hưởng vẫn có thể xảy ra, cho dù có sự chuẩn bị trước
	* Ex: Dù các tàu được trang bị cảm biến băng trôi, vẫn có khả năng va chạm với chúng 

#### Bảng phân loại rủi ro của các dịch vụ tài chính

|Phân loại|Ánh xạ tới các danh mục|Ví dụ|
|---|---|---|
|Inherit|Vận hành,Pháp lý|Xung đột lợi ích|
|Single Exposure|Tín dụng, thị trường|Nghĩa vụ nhà nước|
|Concentration|Tínd dụng, thị trường|Phân bố địa lí|
|Marginal|Tín dụng, thị trường, mô hình|Ứng viên tín dụng|
|Environmental|Tất cả|Các yếu tố kinh tế vĩ mô|
|Forward|Tài chính, thị trường, mô hình, Pháp lý, Quốc gia|Sản phẩm hoặc thị trường mới|

* Trong việc phân tích các loại rủi ro, có **2 yếu tố** quan trọng cần quan tâm
là **Dữ liệu** và **Việc sử dụng dữ liệu**

* Ví dụ về việc sử dụng dữ liệu: rủi ro tín dụng trong các ngân hàng
	* Các ứng viên tín dụng sẽ được yêu cầu cung cấp thông tin để dành cho việc thẩm định
	* Các thông tin đó được hệ thống tiếp nhận và sau đó được chiết xuất để chuyển hoá thành đánh giá tín dụng.
	* Các vấn đề xuất hiện trong quá trình đánh giá:
		* Thông tin của ứng viên không được kiểm tra trong hệ thống của ngân hàng -> dẫn tới tình trạng một ứng viên có thể có nhiều lần đánh giá tín dụng
		* Các thông tin của thực thể không được cập nhật, một khi trở thành khách hàng ...

> [!check] Giải pháp 
> Chú trọng vào nguồn gốc của dữ liệu, và cách lưu trữ dữ liệu hợp lý.

* Không chỉ các dữ liệu ngoài (***external data***) được thu thập và lưu trữ, và còn cần phải có sự liên hệ với các dữ liệu trong hệ thống (***internal data***).

### Dữ liệu cần thiết
![[Pasted image 20230108113653.png]]

* Các dữ liệu Internal có thể được thu thập, hoặc sinh ra.
	* Các dữ liệu được thu thập thường không có thiết kế tốt
	* Các dữ liệu được sinh ra có thể không có ảnh hưởng tới sự vận hành, nhưng có thể gây ra lỗi trong quá trình mô hình hoá nếu người dùng không được hiểu rõ cách thức sinh ra của chúng.
* Các dữ liệu external được cung cấp bởi các tổ chức bên ngoài và có thể có những sự thiếu sót như internal

* Các dữ liệu của một đơn vị kinh doanh (Business Unit) thường được thu thập hoặc mua lại cho mục đích sử dụng của chính họ. Khác với thông tin của một Enterprise thường được công bố rộng rãi và ai cũng có thể sử dụng, các dữ liệu được các BU mua lại thường sẽ không được chia sẻ, kể cả với các BU cùng trực thuộc một Enterprise.
	* Các thông tin của Enterprise không được quản lý sẽ dẫn tới sự gãy đổ (corrupted) và sẽ trở thành không còn tác dụng

* Primary data là các dữ liệu được thu thập, trong khi đó Derived là kết quả đầu ra dựa trên Primary data.

### Sự quản lý dữ liệu
* Không giống như các yêu cầu vận hành (Operational requirements), việc phân tích dữ liệu là không bắt buộc. Và một khi không có dữ liệu phù hợp, công đoạn này có thể bỏ qua.

> [!note] 
> Nhưng trong một thế giới nơi phân tích dựa big data là yếu tố then chốt quyết định cạnh tranh, việc quản lý dữ liệu một cách chặt chẽ đã trở thành một yếu tố then chốt.

* Dữ liệu thường chỉ được phản ánh lại khi chúng đã trở nên "unbearable" với người cần sử dụng (không có sự chủ động).

* Quyền quản lý đơn lẻ (single stewardship) thường tốt hơn là quyền quản lý chung (shared stewardship). Nhưng trong một số trường hợp, khi có nhiều tổ chức muốn sử dụng chung 1 tập dữ liệu, quyền quản lý chung sẽ có lợi hơn.

* Ví dụ về vấn đề chia sẻ quyền quản lý dữ liệu: giữa bên nhận tiền gửi (deposit-taking) và bên cho vay (lending).
	* Nếu một khách mới thực hiện dịch vụ gửi tiền, thông tin của họ sẽ được lưu trữ bởi hệ thống nhận tiền gửi.
	* Nếu cùng một người khách hàng đó đi thực hiện vay tiền, bên bộ phận tín dụng sẽ có thể không truy nhập được vào phần thông tin khách hàng đã được lưu trữ của bộ phận nhận tiền gửi, mà sẽ tiến hành tạo mới.
	* Kể cả khi nếu hai bên có thể truy cập thông tin lưu trữ của nhau, việc cập nhật thông tin có thể là vấn đề. Khi khách hàng thay đổi thông tin từ phía bộ phận tín dụng, thông tin có thể không được thông báo cho bộ phận nhận tiền gửi. (Trừ khi hai bên có quyền quản lý chung)

* Quyền quản lý thường là một thách thức lớn đối với Enterprise data, và thường bị nhầm bộ phận kỹ thuật IT nên là người quản lý tất cả dữ liệu.

### Triển khai sử dụng
* Sau cùng, việc dữ liệu sẽ được sử dụng như thế nào đang được quan tâm hơn bao giờ hết.
* Cho đến hiện tại, dấu hiệu nhận biết rõ rệt nhất chính là ở hệ thống đánh giá nội bộ (***Internal rating system - IRS***) của các ngân hàng. (*Hiểu đơn giản là hệ thống đánh giá, xếp hạng tín dụng của các ngân hàng*)
