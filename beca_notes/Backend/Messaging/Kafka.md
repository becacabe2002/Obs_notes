> [!note] Nguyên lý hoạt động của Kafka
> Apache Kafka được xây dựng dựa trên mô hình publish/subscriber. Các ứng dụng đóng vai trò như các **producer** gửi các msgs (records) tới một node kafka (**broker**) và khai báo rằng các msgs sẽ được sử dụng bởi các **consumer**. Các msgs được gửi lên **broker** sẽ được lưu trữ trong các **topic**. Consumer có thể subscribe tới các topic đó để lấy các msgs thuộc topic đó.
> 

![[Pasted image 20230709144405.png]]
## Các thuật ngữ/khái niệm trong Kafka
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

## Quy trình thực hiện Publish-Subscribe Messaging
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

## Quy trình Queue Messaging/Consumer Group
1. Kafka Producer gửi msg tới topic
2. Tương tự publish-subscribe messaging, Kafka cũng lưu trữ tất cả các tin nhắn trong các partition được định cấu hình cho topic cụ thể đó.
3. Một single consumer subscribes vào một topic cụ thể.
4. Cũng giống như pub-sub messaging, Kafka tương tác với consumer cho đến khi consumer mới đăng ký vào cùng một chủ đề.
5. Khi consumer mới đến, chế độ chia sẻ bắt đầu trong các hoạt động và chia sẻ dữ liệu giữa hai Kafka consumer. Hơn nữa, cho đến khi số lượng Kafka consumer bằng với số lượng partion được định cấu hình cho topic cụ thể đó, việc chia sẻ sẽ lặp lại.
6. Một khi số lượng Kafka consumer vượt quá số lượng partion, consumer mới ở Kafka sẽ không nhận được bất kỳ message nào nữa. Nó duy trì cho đến khi bất kỳ một trong những consumer hiện tại hủy đăng ký. Điều này phát sinh bởi vì ở Kafka có một điều kiện là mỗi Kafka consumer sẽ có tối thiểu một partion và nếu không có partion nào trống, thì consumer mới sẽ phải chờ.