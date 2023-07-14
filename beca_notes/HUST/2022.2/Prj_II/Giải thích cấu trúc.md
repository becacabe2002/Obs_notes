Mục đích: Phân tích các số liệu của một trong thương mại theo thời gian thực.

* Nguồn dữ liệu: ở đây, các dữ liệu có thể lấy được từ các API của trang web (để đơn giản, ta thực hiện sinh dữ liệu từ 3 tập dữ liệu sẵn có)
* Dữ liệu được đưa vào Kafka từ các đầu producer, gửi tới broker, và lấy ra ở đầu consumer (Kafka topic)
> [!note] Nguyên lý hoạt động của Kafka
> Apache Kafka được xây dựng dựa trên mô hình publish/subscriber. Các ứng dụng đóng vai trò như các **producer** gửi các msgs (records) tới một node kafka (**broker**) và khai báo rằng các msgs sẽ được sử dụng bởi các **consumer**. Các msgs được gửi lên **broker** sẽ được lưu trữ trong các **topic**. Consumer có thể subscribe tới các topic đó để lấy các msgs thuộc topic đó.
> 

---
![[Pasted image 20230709144405.png]]
### Các thuật ngữ/khái niệm trong Kafka
**1. Kafka Broker**:
* Xử lý tất cả các yêu cầu từ client (produce, consume, metadata).
* Giữ dữ liệu được sao chép trong cụm (cluster)
* Có thể có 1 hoặc nhiều broker trong 1 cluster.

**2. Kafka Broker Clusters**
* Một máy có thể chạy nhiều server kafka - tương ứng với 1 broker.
* Các broker cùng trỏ chung tới 1 zookeeper thì gọi là 1 cụm broker (clusters)

**3. Kafka Zookeper**
* Chịu trách nhiệm kiểm soát trạng thái của 1 cluster (brokers, topic, users...)

**4. Kafka Topics**
* Kafka duy trì nguồn cấp tin nhắn trong các categories. 
	* Các msgs được lưu trữ và xuất bản trong 1 category/feed name -> **Topic**
* Có thể coi một topic như 1 table trong SQL, với mỗi msg giống như 1 record trong table.
* Vận hành theo cơ chế hàng đợi, một msg mới được đẩy vào, sẽ luôn ở cuối hàng đợi. 
	* Mỗi thông điệp khi đẩy vào topic sẽ luôn được gán 1 offset tương ứng, giúp cho consumer có thể điều khiển quá trình đọc thông điệp
	* Các thông điệp đã cũ (quá time limitation) sẽ bị xóa để tránh tình trạng đầy bộ nhớ.
![[Pasted image 20230709145412.png]]

* Trên thực tế, một topic có rất nhiều partition
	* Khi một thông điệp được đẩy vào topic, mặc định sẽ được gán cho 1 chuỗi số bất kỳ. 
	* Đảm bảo cho số lượng msg trên mỗi partition là tương tự nhau.
	* Tại 1 thời điểm, 1 partition chỉ được đọc bởi 1 consumer, việc tăng số lượng partition sẽ giúp tăng số lượng dữ liệu được đọc lên (song song)
	* Để consumer có thể đọc chính xác thông điệp, cần cung cấp địa chỉ dạng `(topic, partition, offset)`
![[Pasted image 20230709151038.png]]

**5. Kafka Partitions**
* Một topic trong Kafka có thể có kích thước rất lớn, vậy nên không thể lưu trữ tất cả các dữ liệu trên cùng 1 node.
	* Dữ liệu cần phải được phân chia thành nhiều partition sẽ giúp bảo toàn dữ liệu cũng như xử lý dữ liệu dễ dàng hơn.
* Cho phép consumer có thể thực hiện subscribe song song tới 1 topic cụ thể bằng cách phân chia dữ liệu trong 1 topic ra cho nhiều broker khác nhau
	* Mỗi partition có thể được đặt trên 1 máy riêng biệt -> Cho phép nhiều  consumer đọc dữ liệu từ 1 topic 1 cách song song.
![[Pasted image 20230709151433.png]]
* Các partition có thể  là **leader** hoặc **replica** của 1 topic. 
	* Leader partition chịu trách nhiệm cho tất cả các tác vụ đọc ghi của topic. 
	* Nếu leader partition bị hỏng, replica partition sẽ đảm nhận vai trò leader partition mới.
	* Việc làm leader sẽ phụ thuộc vào Zookeeper quyết định.

**6. Kafka Producers**
* Nơi đẩy dữ liệu từ người dùng vào các partition của topic. Tùy vào việc có chỉ định rõ ghi vào phân vùng nào, producer sẽ gửi đến phân vùng đó, hoặc sẽ phân bố đều vào các partition.

**7. Kafka Consumers**
* Mỗi consumer phụ trách 1 vài partition của topic. 
* Nhiều consumer có thể sử dụng chung 1 nhóm để hỗ trợ cho việc xử lý nhanh các dữ liệu.
![[Pasted image 20230709153325.png]]
* Consumer có thể được tổ chức thành các **consumer group** cho 1 topic cụ thể bằng cách thêm thuộc tính `Group.id` vào mỗi consumer
	* Mỗi consumer sẽ phụ trách đọc msg từ 1 partition.
		* Nếu số consumer > số partition: một số consumer sẽ ở chế độ rảnh rỗi vì không có partition để xử lý
		* Nếu số partition > số consumer: consumer sẽ nhận các msg từ nhiều partition
		* Nếu số partition = số consumer: mỗi consumer sẽ đọc msg theo thứ tự từ 1 partition.
	* Mỗi khi consumer được xóa khỏi group, mức tiêu thụ sẽ được cân bằng lại giữa các consumer trong nhóm.

### Quy trình thực hiện Publish-Subscribe Messaging
1. Kafka Producer gửi  msg tới topic
2. Kafka Broker lưu trữ tất cả các msg trong các partition được định cấu hình topic cụ thể, đảm bảo các msg được phân phối cân bằng giữa các partition. 
3. Kafka Consumer subscribes 1 topic cụ thể. 
4. Sau khi Consumer subscribe vào 1 topic, Kafka cung cấp offset hiện tại của topic cho consumer và lưu nó vào trong Zookeeper
5. Consumer liên tục gửi request đến Kafka để pull về các msg mới.
6. Kafka sẽ chuyển tiếp tin nhắn đến consumer ngay sau khi nhận được từ Producer.
7. Consumer sẽ nhận được msg và xử lý nó.
8. Kafka Broker nhận được xác nhận về việc msg đã được xử lý.
9. Kafka cập nhật giá trị offset hiện tại ngay khi nhận được xác nhận. Ngay cả trong máy khi máy chủ outrages, consumer có thể đọc được message tiếp theo một cách chính xác. (Zookeeper quản lí các offset)
10. Quy trình dừng lại cho đến khi consumer dừng việc subscribe lại.

### Quy trình Queue Messaging/Consumer Group
1. Kafka Producer gửi msg tới topic
2. Tương tự publish-subscribe messaging, Kafka cũng lưu trữ tất cả các tin nhắn trong các partition được định cấu hình cho topic cụ thể đó.
3. Một single consumer subscribes vào một topic cụ thể.
4. Cũng giống như pub-sub messaging, Kafka tương tác với consumer cho đến khi consumer mới đăng ký vào cùng một chủ đề.
5. Khi consumer mới đến, chế độ chia sẻ bắt đầu trong các hoạt động và chia sẻ dữ liệu giữa hai Kafka consumer. Hơn nữa, cho đến khi số lượng Kafka consumer bằng với số lượng partion được định cấu hình cho topic cụ thể đó, việc chia sẻ sẽ lặp lại.
6. Một khi số lượng Kafka consumer vượt quá số lượng partion, consumer mới ở Kafka sẽ không nhận được bất kỳ message nào nữa. Nó duy trì cho đến khi bất kỳ một trong những consumer hiện tại hủy đăng ký. Điều này phát sinh bởi vì ở Kafka có một điều kiện là mỗi Kafka consumer sẽ có tối thiểu một partion và nếu không có partion nào trống, thì consumer mới sẽ phải chờ.
---

* Hệ thống truyền tải dữ liệu (Streaming System): lấy dữ liệu từ kafka topic

* Data Storage: 
	* Sẽ được lưu vào 2 hệ csdl:
		* Cassandra: lưu dữ liệu chưa qua xử lý (raw data)
		* MySQL: lưu dữ liệu đã qua xử lý

---
> [!note] Spark Streaming 
> Là hệ thống xử lý luồng có khả năng chịu lỗi và khả năng mở rộng, hỗ trợ native cho cả xử lý thông tin dạng luồng, hoặc dạng batch.
> * Là một extension của Spark Core, cho phép người dùng  có thể xử lý dữ liệu real-time từ các nguồn đa dạng như Kafka ...
> * Các thông tin đã được xử lý có thể được lưu trữ vào các hệ thống file, CSDL hoặc bảng biểu diễn trực tiếp.
> * Cơ chế của việc xử lý luồng: 
> 	* Coi stream như các mini-batches 
> 	* Thực hiện kĩ thuật RDD transformation đối với các mini-batches này.
> 	-> Tận dụng được các đoạn code sử dụng cho xử lý batch để xử lý stream.

> [!info] Resilient Distributed Dataset - RDD (Tập dữ liệu phân tán đàn hồi)
> Là dạng dữ liệu nền tảng cho Apache Spark. 
> Là một tập các thành phần bất biến, có khả năng chống chịu lỗi và được xử lý song song trong các cụm máy.

### Các đặc trưng của RDDs
**1. Distributed (Phân tán)**:
* một RDD được phân bố trong nhiều nodes của một cụm máy -> cho phép xử lý song song.
* Mỗi partition giữ một tập con của tập dữ liệu.

**2. Resilient (Đàn hồi):**
* Có khả năng phục hồi từ thất bại.
* Nếu một partition bị mất, nó có thể được tính toán lại dựa trên các dữ liệu lineage lưu trữ trong RDD

**3. Immutable (Bất biến):**
* RDD chỉ cho phép đọc dữ liệu, không cho phép chỉnh sửa chúng.
* Transformation RDD sẽ được thực hiện bằng việc tạo nên một RDD mới.

**4. Lazy Evaluated**:
* RDD Transformation không được thực hiện ngay lập tức.
* Transformation xây dựng một biểu đồ lineage, thể hiện thứ tự các hoạt động sẽ được tiến hành.
![[Pasted image 20230709210851.png]]
* Những tính toán sẽ được thực hiện một khi các hành động được thực hiện trên RDD. (Ex: thu thập dữ liệu hoặc lưu trữ dữ liệu vào file)

### Các Operations được hỗ trợ
**Transformation (Biến đổi):** 
* Tạo một RDD mới từ một RDD đã có sẵn, cho phép các thao tác với dữ liệu và biến đổi theo hướng phân tán và chịu lỗi. 
* Bao gồm các hoạt động: `map`, `filter` hoặc `join`. 
* Các loại Transformation:
	* **Narrow Transformation**: 
		* Là kết quả của `map()` và `filter()` 
		* Các dữ liệu được tính toán tồn tại trên partition duy nhất (Ko có sự dịch chuyển data giữa các partitions)
		![[Pasted image 20230709211737.png]]
	* **Wider Transformation**:
		* Là kết quả của `groupByKey()` và `reduceByKey()`
		* Các dữ liệu tính toán được giữ trong nhiều partitions
		![[Pasted image 20230709212714.png]]

**Actions**: 
* Các hành động kích hoạt các hoạt động tính toán và trả về kết quả hoặc thực hiện một side effect.
* Bao gồm `count`, `collect`, `save`.

---
* Các file dữ liệu tĩnh (static data file) được lưu trữ trong hệ thống HDFS của Apache Hadoop
---
### Map Reduce
> Mô hình thiết kế độc quyền bởi Google, có khả năng xử lý các tập dữ liệu lớn song song và phân tán tren 1 cụm máy tính.

![[Pasted image 20230709221213.png]]

* Bao gồm các thủ tục `Map()` và `Reduce()`:
	* Thủ tục `Map()` bao gồm **filter** và **sort** trên dữ liệu
		* Nhận input cho các cặp key-value và output chính là là những cặp key-value trung gian.
		* Ghi xuống hard disk và thông báo cho các hàm `Reduce()` để tiếp nhận dữ liệu.
	* Thủ tục `Reduce()` thực hiện quá trình tổng hợp dữ liệu
		* Tiếp nhận key-value trung gian
		* Ghép lại tạo thành một tập khóa khác nhau.
		* Các cặp key-value được đưa vào hàm Reduce thông qua con trỏ vị trí.

> [!tip] Nguyên tắc "Chia để trị"
> * Phân chia các dữ liệu cần xử lý thành nhiều phần nhỏ trước khi thực hiện
> * Xử lý các vấn đề nhỏ theo phương thức song song trên các máy tính rồi phân tán hoạt động theo hướng độc lập.
> * Tiến hành tổng hợp những kết quả thu được để đề ra những kết quả sau cùng.

### Hadoop Distributed File System - HDFS
> Hệ thống lưu trữ dữ liệu sử dụng bởi Hadoop, có thể mở rộng một Hadoop Cluster tới hàng trăm nghìn nodes.

* HDFS tạo ra các mảnh nhỏ hơn của dữi liệu lớn rồi phân tán chúng lên các node khác nhau. Từ đó, sao chép mỗi miếng dữ liệu nhỏ hơn lên nhiều nodes khác nhau.
-> Khi có một node bị lỗi, hệ thống sẽ sử dụng dữ liệu từ một node khác để tiếp tục xử lý. 

> [!check] Các ưu điểm nổi bật của HDFS
> * **Cho phép dữ liệu có thể phân tán:** nếu cho một cụm Hadoop mà trong đó có 20 máy tính. Khi đưa 1 file dữ liệu vào HDFS, file sẽ tự động được chia nhỏ thành nhiều phần rồi lưu trữ ở 20 máy đó
> * **Cho phép tính toán và phân tán song song:** thay vì xử dụng 1 máy để xử lý dữ liệu, các máy trong HDFS sẽ hoạt động song song để xử lý chung 1 công việc.
> * **Cho phép nhân bản các file:** để phòng trường hợp một máy trong cụm Hadoop phát sinh sự cố, dữ liệu sẽ được backup lại
> * **Có thể mở rộng theo chiều dọc và chiều ngang:** cho phép nâng cấp các hệ thống bằng cách nâng cấu hình máy, hoặc tăng số lượng máy.

**KIẾN TRÚC HDFS (HDFS ARCHITECTURE)**
* HDFS là một **master/slave** architecture. 
![[Pasted image 20230710061914.png]]

* Một HDFS Cluster sẽ luôn bao gồm 1 **NameNode**, đóng vai trò làm master server.
	* Quản lý hệ thống tập tin
	* Điều chỉnh các truy cập đến các tập tin khác từ client.
* Bên cạnh đó sẽ có nhiều **DataNode**, thường sẽ là 1 đối với mỗi node trong cluster và thực hiện vai trò quản lý kho dữ liệu gắn liền với node hiện tại của chúng. 
* HDFS sẽ expose file system namespace và cho phép dữ liệu của người dùng được lưu trữ trong các file.
* Một file thường được tách thành nhiều khối, các khối sau đó được lưu trữ trong một tập các DataNodes.
* **NameNode**:
	* Đóng, mở, đổi tên cho các tập tin, thư mục.
	* Điều chỉnh cho các truy cập đến hệ thống của tập tin
* **DataNode:**
	* Ghi, đọc vào hệ thống tập tin.
	* Tạo, xóa, nhân rộng các dữ liệu dựa trên chỉ dẫn của NameNode.

> [!note] Quá trình hoạt động của NameNode và DateNode
> * NameNode có trách nhiệm điều phối cho các thao tác truy cập của client với hệ thống HDFS. NameNode thực hiện nhiệm vụ thông qua các daemon `namenode` chạy trên port 8021.
> * DataNode Server sẽ chạy một daemon `datanode` trên port 8022, theo định kì mỗi DataNode có nhiệm vụ báo cáo cho NameNode danh sách tất cả các block nó đang lưu trữ. NameNode dựa vào đó để cập nhật các metadata trong nó.
> * Sau mỗi lần cập nhật thì metadata trên NameNode đều sẽ đạt được các trạng thái thống nhất dữ liệu trên các DataNode. Tất cả trạng thái của metadata khi đang ở tình trạng hệ thống này sẽ được gọi là **checkpoint**.
> * Mỗi một metadata ở trạng thái checkpoint đều sẽ được sử dụng cho mục đích nhân bản metadata với mục đích phục hồi lại NameNode nếu như NameNode gặp phải lỗi.
> ---
> * **Quá trình xử lý yêu cầu đọc file**:
> 	* NameNode nhận yêu cầu từ Client (Yêu cầu chứa thông tin về tệp tin hoặc thư mục cần đọc)
> 	* NameNode kiểm tra quyền truy cập của client đối với tệp tin hoặc thư mục được yêu cầu. Nếu client ko có quyền truy cập, NameNode từ chối yêu cầu.
> 	* NameNode sử dụng metadata được lưu trữ trong bộ nhớ để tra cứu thông tin về tệp tin hoặc thư mục được yêu cầu. (Metadata bao gồm cấu trúc thư mục, tên tệp tin, vị trí của các khối dữ liệu và các bản sao của khối dữ liệu.)
> 	* Dựa trên thông tin trong metadata, NameNode xác định vị trí các khối dữ liệu cần thiết để đáp ứng yêu cầu đọc. NameNode trả về danh sách các DataNode lưu trữ các bản sao của các khối dữ liệu.
> 	* Client tiếp tục liên lạc trực tiếp với các DataNode được chỉ định để yêu cầu dữ liệu. Client gửi yêu cầu đọc đến các DataNode và yêu cầu chúng truyền dữ liệu khối tương ứng.
> 	* Các DataNode nhận yêu cầu đọc và truyền dữ liệu khối dữ liệu cho client. Dữ liệu được truyền trực tiếp từ DataNode đến client qua giao thức mạng.
> 	* Sau khi client nhận được dữ liệu từ các DataNode, yêu cầu đọc được coi là hoàn thành. Client sử dụng dữ liệu nhận được để thực hiện các giao thức xử lý tiếp theo. 
> ---
> * **Quá trình xử lý yêu cầu ghi file:**
> 	* NameNode nhận yêu cầu ghi từ client. Yêu cầu này chứa thông tin về tệp tin cần ghi và dữ liệu cần được ghi vào tệp tin đó.
> 	* NameNode kiểm tra quyền truy cập của client đối với tệp tin. Nếu client không có quyền ghi, NameNode từ chối yêu cầu.
> 	* NameNode tạo mới một khối dữ liệu để lưu trữ dữ liệu ghi vào tệp tin. Khối dữ liệu này được chia thành các phân đoạn nhỏ hơn và được gửi đến các DataNode để lưu trữ.
> 	* NameNode xác định các DataNode để lưu trữ bản sao của khối dữ liệu. Việc chọn DataNode được dựa trên các yếu tố như tải công việc hiện tại của DataNode và sự phân tán dữ liệu trong cụm.
> 	* NameNode liên lạc với các DataNode được chọn và yêu cầu chúng lưu trữ bản sao của khối dữ liệu. NameNode gửi thông tin về vị trí và nội dung của khối dữ liệu cho các DataNode.
> 	* Các DataNode nhận yêu cầu ghi và lưu trữ bản sao của khối dữ liệu. Sau khi các DataNode xác nhận việc ghi bàn thành công, NameNode được thông báo về việc hoàn thành ghi dữ liệu.
> 	* NameNode cập nhật metadata để phản ánh việc thêm một khối dữ liệu mới và vị trí của các bản sao khối dữ liệu.
> 	* Sau khi dữ liệu được ghi thành công, yêu cầu ghi được coi là hoàn thành. Client nhận được thông báo về việc ghi thành công và có thể tiếp tục thực hiện các thao tác khác  trên tập tin.

> [!note] Tính năng Data Replication trong HDFS
> Mỗi khối dữ liệu được chia thành các bản sao và lưu trữ trên nhiều DataNode khác nhau trong cụm.
> ![[Pasted image 20230710173059.png]]
> 1. **Replication factor:** có thể hiểu là số lượng bản sao của mỗi khối dữ liệu.
> 2. **Block placement**: khi một tập tin mới được ghi vào HDFS, NameNode sẽ xác định các DataNode để lưu trữ các bản sao của khối dữ liệu. Cần đảm bảo sao cho các bản sao được đặt ở các máy chủ vật lý khác nhau trong cụm để tránh mất mát dữ liệu khi có sự cố xảy ra.
> 3. **Replica Placement Policy:** HDFS cung cấp một số chính sách đặt bản sao để quyết định vị trí lưu trữ các bản sao khối dữ liệu. Một số chính sách:
> 	* **Default:** bản sao được đặt trên các DataNode ngẫu nhiên trong cụm
> 	* **Rack-awareness:** bản sao được đặt trên các DataNode nằm trên các rack khác nhau, nhằm tối ưu khóa độ tin caajjy và hiệu suất mạng trong cụm
> 	* **Node-group-awareness:** bản sao được đặt trên các DataNode nằm trong cùng 1 nhóm nút để tận dụng băng thông nội bộ trong nhóm.
> 4. **Replication and Maintenance:** khi một DataNode gặp sự cố hoặc mất kết nối, HDFS sẽ tự động sao chép lại các bản  sao khối dữ liệu từ các DataNode khác để đảm bảo đủ số bản sao được duy trì. Nếu một bản sao không khả dụng, DataNode sẽ đánh dấu nó là  "Corrupt" và yêu cầu sao chép lại.

> [!question] Tại sao sử dụng HDFS để lưu dữ liệu tĩnh
> * **Tính tin cậy**: HDFS được thiết kế để có tính tin cậy cao (sao chép dữ liệu -> đảm bảo tính toàn vẹn và khả năng phục hồi dữ liệu)
> * **Khả năng mở rộng**: HDFS có khả năng mở rộng với việc phân tán dữ liệu trên nhiều nút trong cụm. Điều này cho phép lưu trữ lượng dữ liệu lớn mà không gặp hạn chế về dung lượng đĩa hoặc tốc độ truy xuất
> * **Hiệu suất đọc:** HDFS được tối ưu cho việc đọc dữ liệu lớn.
> * **Đồng bộ hóa dữ liệu:** HDFS hỗ trợ cho việc đồng bộ hóa dữ liệu giữa các nút trong cụm. Khi một tập tin mới được ghi vào trong HDFS, dữ liệu sẽ được sao chép và lưu trữ trên các DataNode -> đảm bảo các bản sao khối dữ liệu là nhất quán và đồng bộ.
> * **Tính linh hoạt:** dữ liệu trong HDFS có thể được truy cập từ nhiều ứng dụng khác nhau thông quá giao thức Hadoop. HDFS ko chỉ hỗ trợ lưu trữ dữ liệu tĩnh mà còn phù hợp cho các ứng dụng phân tích dữ liệu, xử lý dữ liệu lớn và truy vấn dữ liệu theo mô hình MapReduce.

### Apache Hive
> [!question] Apache Hive 
> Là một cơ sở dữ liệu dựa trên Hadoop, được thiết kế để cung cấp một giao diện truy vấn SQL-like cho phép phân tích và truy vấn dữ liệu lớn. Hive giúp người dùng tận dụng khả năng lưu trữ và xử lý dữ liệu phân tán của Hadoop để thực hiện các tác vụ phân tích dữ liệu và truy vấn dữ liệu phức tạp.
> * 3 chức năng quan trọng nhất khi triển khai Hive: **data summarization**, **data analysis** và **data query**. Hive sử dụng HiveQL để tiến hành query
> 	* HiveQL sẽ chuyển đổi các câu lệnh dưới dạng SQL thành các MapReduce jobs để rồi triển khai trên Hadoop. 
> * Các hệ thống file được hỗ trợ bởi Hive:
> 	* Flat file hoặc text files
> 	* Sequence Files chứa các cặp khóa - giá trị dưới dạng binary
> 	* RCFiles chứa các cột của bảng

**CẤU TRÚC CỦA HIVE**
![[Pasted image 20230711013942.png]] 
* **Hive Metastore:** thành phần quản lý metadata trong Hive. Metadata bao gồm dữ liệu cho mỗi bảng như vị trí  và schema của nó. Nó cũng chứa thông tin về metadata phân vùng, cho phép theo dõi tiến trình dữ liệu phân tán trong cụm. Thông tin này thường được lưu trữ trong cơ sở dữ liệu quan hệ. Metadata theo dõi dữ liệu, sao chép dữ liệu và cung cấp bản sao lưu trong trường hợp mất dữ liệu.

* **Driver:** nhận các câu lệnh HiveQL và hoạt động như một bộ điều khiển. Nó giám sát tiến tình và vòng đời của các execution khác nhau bằng cách tạo ra các sessions. Khi một câu lệnh HiveQL được thực thi, Driver lưu trữ metadata được tạo ra trong quá trình thực thi câu lệnh. Khi hoạt động reducing hoàn tất bởi MapReduce, Driver thu thập các điểm dữ liệu và kết quả truy vấn. 

* **Compiler:** chuyển đổi truy vấn HiveSQL thành đầu vào cho MapReduce. Bao gồm một phương pháp để thực hiện các bước và công việc cần thiết cho để giúp đầu ra HiveQL như yêu cầu của MapReduce.

* **Parser**: Parser là thành phần của Hive được sử dụng để phân tích câu lệnh truy vấn HiveQL và chuyển đổi nó thành cấu trúc dữ liệu phù hợp để thực thi. Nhiệm vụ chính của Parser là kiểm tra tính hợp lệ cú pháp của câu lệnh truy vấn và xây dựng cây cú pháp (parse tree) tương ứng.

* **Planner**: Planner (hoặc Query Planner) là thành phần trong Hive có nhiệm vụ tạo kế hoạch thực thi cho câu truy vấn HiveQL dựa trên cây cú pháp đã được xây dựng bởi Parser. Planner sẽ xác định các bước cần thiết để thực hiện câu truy vấn và tạo ra kế hoạch thực thi tối ưu.

* ***Optimizer:** thực hiện các bước biến đổi để tổng hợp, pipeline conversion bằng single join cho multiple join. Nó cũng được giao nhiệm vụ chia công việc trong quá trình biến đổi dữ liệu trước khi tiến hành reduce operations để tăng hiệu suất và khả năng mở rộng.

* **Executor**: Executor thực thi các tác vụ sau các bước biên dịch và tối ưu hóa. Executor tương tác trực tiếp với Hadoop Job Tracker để lên lịch cho các tác vụ chạy.

* **CLI, UI và Thrift Server**: Command Line Interface và User Interface gửi các truy vấn, giám sát quá trình và cung cấp hướng dẫn để người dùng bên ngoài có thể tương tác với Hive. Thrift cho phép các client khác tương tác với Hive.

> [!note] Quá trình làm việc với HDFS của Apache Hive
> 1. **Tạo bảng**: người dùng sử dụng HiveQL để tạo bảng trong Hive. Hive sẽ sử dụng Hive Metastore để lưu trữ metadata của bảng, bao gồm tên bảng, cấu trúc dữ liệu, vị trí lưu trữ và các thông tin khác.
> 2. **Lưu trữ dữ liệu:** khi dữ liệu được ghi vào Hive, Hive sẽ tạo ra các tệp tin dữ liệu trong HDFS. Các tệp tin này được lưu trữ trong các thư mục trên HDFS, được quản lý bởi HDFS NameNode.
> 3. **Đọc dữ liệu:** khi người dùng truy vấn dữ liệu từ bảng trong Hive, Hive sẽ tạo ra một kế hoạch thực thi dựa trên câu truy vấn HiveQL. Kế hoạch thực thi bao gồm các bước xử lý dữ liệu và truy vấn từ các tệp tin lưu trữ trên HDFS.
> 4. **Tối ưu hóa và thực thi:** kế hoạch thực thi của Hive được tối ưu hóa để cải thiện hiệu suấ truy vấn. Hive sử dụng Planner và Optimizer để xác định các phép `join`, sắp xếp dữ liệu và phân bố công việc trên cụm Hadoop. Kế hoạch thực thi cuối cùng được chuyển cho Hive Execution Engine để thực thi trên cụm Hadoop.
> 5. **Đồng bộ hóa metadata:** khi dữ liệu được thay đổi trong Hive (thêm mới, xóa ...) Hive sẽ cập nhật metadata tương ứng trong Hive Metastore. Điều này đảm bảo rằng thông tin về dữ liệu và cấu trúc của bảng được duy trì đồng bộ với dữ liệu trên HDFS.

---
* Dữ liệu sẽ ở dạng Data Frame, vì sử dụng cơ chế Structure Streaming

---
## Structure Streaming trong Spark
> Là một thành phần quan trọng trong Apache Spark, được sử dụng để xử lý dữ liệu dạng luồng với structured data. Thay vì xử lý dữ liệu theo batch, Structured Streaming xử lý dữ liệu dạng luồng như một chuỗi sự kiện liên tục. (micro-batch)

> [!note] Các đặc điểm và khái niệm quan trọng
> * **Micro-batch Processing:** luồng dữ liệu được chia thành các "micro-batch" và được xử lý  theo cách tương tự như xử lý dữ liệu theo batch truyền thống. Mỗi micro-batch là một tập hợp nhỏ các sự kiện dữ liệu được xử lý cùng nhau.
> * **Data Source** và **Data Sinks**: structured streaming hỗ trợ nhiều nguồn dữ liệu đầu vào (data sources) và đích đến dữ liệu (data sinks), bao gồm Kafka, Flume, HDFS ... Người dùng có thể định nghĩa các nguồn và đích dữ liệu thông qua API để thực hiện xử lý dữ liệu luồng.
> * **Continuous Processing:** với structured Streaming, người dùng có thể thực hiện các phép biến đổi và phân tích liên tục trên dữ liệu luồng. Các thao tác như  lọc, biến đổi, phép kết hợp và tính toán có thể được áp dụng liên tục trong quá trình xử lý dữ liệu.
> * **Khả năng chịu lỗi:** tích hợp tính năng chống chịu lỗi của Spark, cho phép xử lý dữ liệu luồng một cách an toàn và đảm bảo. Nếu lỗi xảy ra trong quá trình xử lý, Spark sẽ tự động khôi phục và tiếp tục xử lý từ vị trí lỗi.

### Programming Model
* Ý tưởng chính của Structured Streaming là coi luồng dữ liệu trực tiếp như một bảng được liên tục thêm hàng. 
-> tạo nên mô hình xử lý tương tự như batch processing.
* Các phép tính xử lý luồng sẽ được thể hiện như query batch trên bảng tĩnh
	* Spark sẽ chạy phép truy vấn tăng dần trên bảng đầu vào không có giới hạn.
![[Pasted image 20230711145642.png]]
* Coi luồng dữ liệu như "bảng đầu vào". Mỗi mục dữ liệu đến như một hàng mới được thêm vào bảng đầu vào.
* Truy vấn trên bảng đầu vào sẽ tạo ra "bảng kết quả". Mỗi khoảng thời gian kích hoạt (ex: 1s), hàng mới được bổ sung vào bảng đầu vào, từ đó cập nhật bảng kết quả. Khi bảng kết quả được cập nhật, user muốn ghi các hàng kết quả thay đổi vào đích dữ liệu bên ngoài.
![[Pasted image 20230711155634.png]]
* "Đầu ra" được định nghĩa là những gì được ghi ra lưu trữ bên ngoài. Có các chế độ khác nhau:
	* **Complete Mode**: toàn bộ bảng kết quả được cập nhật sẽ được ghi vào lưu trữ bên ngoài. Việc xử lý việc viết toàn bộ bảng này do các kết nối tới kho lưu trữ.
	* **Append Mode:** chỉ các hàng mới được bổ sung trong bảng kết quả kể từ lần kích hoạt trước đó sẽ được ghi vào lưu trữ bên ngoài. Điều này chỉ áp dụng cho các truy vấn mà các hàng tồn tại trong bảng kết quả không đổi.
	* **Update Mode**: chỉ các hàng được cập nhật trong bảng kết quả kể từ lần kích hoạt gần nhất sẽ được ghi vào lưu trữ ngoài. 
		* Khác với complete mode ở chỗ chỉ xuất các hàng đã được thay đổi kể từ lần kích hoạt trước đó. Nếu truy vấn không chứa các phép tổng hợp, chế độ sẽ tương tự với append mode

![[Pasted image 20230711160659.png]]
> [!warning] Lưu ý
> Structured Streaming không tạo ra toàn bộ bảng. Nó đọc dữ liệu mới nhất có sẵn từ nguồn dữ liệu luồng, xử lý một cách tăng dần để cập nhật kết quả, sau đó loại bỏ dữ liệu nguồn. Chỉ có dữ liệu trạng thái trung gian tối thiểu cần thiết để cập nhật kết quả.

* Mô hình này khác biệt với các mô hình xử lý dữ liệu luồng khác ở việc Spark sẽ phụ trách việc cập nhật bảng kết quả mỗi khi có dữ liệu mới (giải thoát người dùng khỏi nỗi lo về việc tự duy trì sự tổng hợp)

### Đối phó với Event-time và dữ liệu tới trễ
* Event-time là thời gian được gắn trực tiếp trong dữ liệu.
* Đối với nhiều ứng dụng, người dùng yêu cầu các hoạt động dựa trên thời gian này.
Ex: user muốn biết số sự kiện tạo ra bởi các thiết bị IoT/phút, cần sử dụng thời gian khi dữ liệu được tạo ra chứ ko phải thời gian mà Spark nhận được chúng.
* Event-time ở đây được thể hiện như một giá trị cột trong mỗi hàng có trong bảng.
	* Điều này cho phép tổng hợp theo dạng window-based (ex: số sự kiện mỗi phút) chỉ là một kiểu đặc biệt của nhóm và tổng hợp dựa trên cột thời gian sự kiện. (Mỗi time window là một nhóm và mỗi hàng có thể thuộc về nhiều window/nhóm)
		-> Các truy vấn tổng hợp dạng Event-time-window-based có thể được định nghĩa một cách nhất quán trên cả tập dữ liệu tĩnh và trên dữ liệu luồng

### Fault tolerance Semantics
* Việc đảm bảo tính toàn vẹn từ đầu tới cuối (end-to-end) là một trong những mục tiêu chính trong thiết kế Structured Streaming.
* Để đạt được điều đó, các nguồn dữ liệu cho Structured Streaming, các đích đến và execution engine được thiết kế để theo dõi một cách chính xác tiến trình của quá trình xử lý để có thể xử lý bất kỳ loại lỗi nào bằng tái khởi động/hoặc xử lý lại. 
* Mỗi streaming source được cho là có các offsets (tương tự như các offsets Kafka) để theo dõi vị trí đọc trong luồng. Engine sử dụng checkpointing và write-ahead logs để ghi lại phạm vi offsets của dữ liệu đang được xử lý trong mỗi kích hoạt. 
* Các streaming sinks được thiết kế để có khả năng kiểm soát việc xử lý lại. 
* Kết hợp sử dụng replayable sources và idempotent sinks, Structured Streaming có thể đảm bảo tính toàn vẹn chính xác từ đầu đến cuối trong bất kỳ tình huống nào.

> [!note] Structured Streaming + Kafka (input) + HDFS (state store)
> Xây dựng structured streaming với đầu vào là Kafka và các trạng thái sẽ được lưu trữ trong HDFS.
> 1. **Thiết lập kết nối với Kafka**: thiết lập kết nối tới Apache Kafka và đọc dữ liệu từ topics của Kafka. (API được cung cấp có thể tự động theo dõi và đọc các sự kiện mới nhất)
> 2. **Xử lý dữ liệu luồng**: xác định các phép biến đổi và phân tích dữ liệu sẽ được áp dụng trên dữ liệu luồng từ Kafka. Các phép biến đổi có thể bao gồm phép lọc, biến đổi cấu trúc, phép tổng hợp và tính toán (Có thể sử dụng các hàm có sẵn trong API)
> 3. **Lưu trữ trạng thái trên HDFS:** lưu trữ các trạng thái của ứng dụng trong quá trình xử lý dữ liệu luồng, để sử dụng trong các phép biến đổi tiếp theo hoặc để phục hồi sau khi ứng dụng khởi động lại. 
> 	* Có thể lưu trữ và truy xuất trạng thái thông qua API của Spark: `mapGroupsWithState` hoặc `flatMapGroupsWithState`
> 4. **Ghi kết quả vào HDFS:** sau khi hoàn thành xử lý dữ liệu luồng và có kết quả cuối cùng, có thể ghi vào HDFS để lưu trữ hoặc phân tích tiếp (Ở đây sẽ được lưu vào Cassandra và MySQL)


---
* Các dữ liệu đã qua xử lý (được lưu trữ tại MySQL) sẽ được biểu diễn bằng Superset.