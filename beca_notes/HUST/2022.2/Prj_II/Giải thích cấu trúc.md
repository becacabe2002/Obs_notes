Mục đích: Phân tích các số liệu của một trong thương mại theo thời gian thực.

* Nguồn dữ liệu: ở đây, các dữ liệu có thể lấy được từ các API của trang web (để đơn giản, ta thực hiện sinh dữ liệu từ 3 tập dữ liệu sẵn có)
* Dữ liệu được đưa vào Kafka từ các đầu producer, gửi tới broker, và lấy ra ở đầu consumer (Kafka topic)
[ ] Kafka topics là gì
[ ] Nguyên lý hoạt động của Kafka
[ ] Vì sao Kafka lại có tốc độ nhanh

* Hệ thống truyền tải dữ liệu (Streaming System): lấy dữ liệu từ kafka topic

* Data Storage: 
	* Sẽ được lưu vào 2 hệ csdl:
		* Cassandra: lưu dữ liệu chưa qua xử lý (raw data)
		* MySQL: lưu dữ liệu đã qua xử lý
[ ] Spark Streaming là gì

* Các file dữ liệu tĩnh (static data file) được lưu trữ trong hệ thống HDFS của Apache Hadoop
[ ] Cấu trúc file HDFS là ntn?
[ ] Tại sao sử dụng HDFS để lưu dữ liệu tĩnh

* Dữ liệu sẽ ở dạng Data Frame, vì sử dụng cơ chế Structure Streaming
[ ] Cơ chế Structure Streaming từ Kafka

* Các dữ liệu đã qua xử lý (được lưu trữ tại MySQL) sẽ được biểu diễn bằng Superset.