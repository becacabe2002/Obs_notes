1. **Mô hình hóa dữ liệu là gì?**:
    - Một mô hình dữ liệu sắp đặt các yếu tố dữ liệu khác nhau và tiêu chuẩn hóa cách chúng liên quan đến nhau và các thuộc tính thực thể trong thế giới thực.
    - Là quá trình tạo ra các mô hình dữ liệu, bao gồm các *Thực thể* - đối tượng/khái niệm mà dữ liệu muốn theo dõi.
        + Mỗi thực thể có các thuộc tính chi tiết mà user muốn theo dõi.

2.

3. **Table (Bảng) là gì?**:
    - Dữ liệu được lưu trữ trong các hàng và cột.
        + Các *cột* hiển thị dữ liệu theo liên kết dọc
        + Các *hàng* đại diện cho các bản ghi

4. **Normalize (Bình thường hóa) là gì?**:
    - quá trình thiết kế csdl theo cách giảm dư thừa dữ liệu mà không phải hi sinh tính toàn vẹn.

5. **Vì sao cần Normalize cho mô hình dữ liệu**:
    - Xóa dữ liệu dư thừa
    - Giảm độ phức tạp dữ liệu
    - Đảm bảo mối quan hệ giữa các bảng ngoài dữ liệu nằm trong các bảng.
    - Đảm bảo phụ thuộc dữ liệu và dữ liệu được lưu trữ hợp lý.

6. **Denormalization (biến đổi) là gì?**:
    - Dữ liệu dư được thêm vào giữ liệu đã được chuẩn hóa.
    - Hy sinh hiệu suất ghi để tăng cường hiệu suất đọc.
