## 1. Các nguyên tắc thiết kế giao diện Norman
> [!abstract] Gồm 6 nguyên tắc
> * **Trực quan**
> * **Phản hồi**
> * **Ràng buộc**
> * **Ánh xạ**
> * **Nhất quán**
> * **Thế chỗ**

### 1.1 Trực quan
* Các chức năng của hệ thống trực quan -> người dùng có khả năng nhận biết việc cần làm và ngược lại
* Các cấp độ của trực quan: 0 (thấp nhất, chức năng bị che khuất) -> 4 (cao nhất, cho xem trước kết quả)

### 1.2 Phản hồi
* Thông tin trả về từ hệ thống về hành động người dùng đã làm và  kết quả công việc hệ thống đã thực hiện
-> Giúp người dùng đánh giá hệ thống để thực hiện công việc tiếp theo

* Phản hồi = âm thanh, hiệu ứng, hình ảnh, các cử chỉ ...

### 1.3 Ràng buộc
* Giới hạn loại tương tác mà người dùng có thể thực hiện tại thời điểm (ngăn chặn sai sót từ người dùng)
* 3 kiểu:
	* Rằng buộc vật lý: dùng các đối tượng vật lý để hạn chế
	* Rằng buộc về văn hóa: quy ước mang tính toàn cầu
	* Rằng buộc về logic thực hiện: dùng các quy ước để hạn chế các thao tác

### 1.4 Ánh xạ
* quan hệ giữa các đk và chuyển động của chúng với kết quả tương tác.
	* Ánh xạ tốt khi tương đồng về bố cục và hành vi

### 1.5 Nhất quán
* Có các thao tác tương tự nhau, sử dụng các phần tử tương tự nhau để thực hiện các nvu tương tự nhau.
-> Dễ dùng, dễ học
* **Nhất quán trong**: các thao tác, phần tử giao diện nhất quán trong phạm vi ứng dụng
* **Nhất quán ngoài**: các thao tác, giao diện tương tự nhau cho các thiết bị và ứng dụng ngoài

### 1.6 Thế chỗ
* thuộc tính cho biết cách thức sử dụng

## 2. Các nguyên tắc thiết kế giao diện Schneiderman
> [!abstract] 
> * Nhận biết sự khác biệt người dùng
> * 8 quy tắc vàng
> * Ngăn chặn lỗi

### 2.1 Nhận biết sự khác biệt người dùng
* Thực hiện trước khi tk
* Các cách sử dụng khác nhau đối với:
	* Đối tượng sử dụng khác nhau (trình độ người dùng)
	* kịch bản sử dụng khác nhau
-> mục tiêu của người dùng,  cách thức tiến hành?

### 2.2 8 nguyên tắc vàng
1. **Hướng tới sự nhất quán**: trình tự các hành động đồng nhất trong các tình huống tương tự
2. **Cung cấp phím tắt cho người dùng**: dành cho những người dùng có chuyên môn, cho các tác vụ sử dụng thường xuyên
3. **Cung cấp thông tin phản hồi**: các hành động thường xuyên cần phản hồi đơn giản, các hành động ít xảy ra cần có phản hồi đáng chú ý hơn
4. **Thiết kế hội thoại đảm bảo tính đóng**: đảm bảo có mở, thân, kết (Có thông báo khi kết thúc)
5. **Cung cấp pthuc xử lý lỗi đơn giản**: thiết kế để người dùng không mắc những lỗi nghiêm trọng, cần phát hiện các nguy cơ mắc lỗi tiềm tàng.
6. **Cho phép dễ dàng hủy bỏ các hành động đã thực hiện**: tất cả các hành động đều có thể undo
7. **Hỗ trợ người dùng tập trung kiểm soát hệ thống**: người dùng nắm quyền chủ động, là người khởi tạo các hành động
8. **Giảm tải bộ nhớ làm việc**: hệ thống xử lý thay phần người dùng

### 2.3 Ngăn chặn lỗi
* Cần có các bước thiết kế để ngăn ngừa nguy cơ xảy ra lỗi
* Tự động sửa những lỗi đã được dự đoán trước của người dùng.