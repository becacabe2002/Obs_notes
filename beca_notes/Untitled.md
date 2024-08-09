## 1. Data Architecture
**Nhận xét - Anh Hiếu**:
* _Nói rõ hơn mối quan hệ giữa data governance và data management_.
**Câu trả lời**: ở mỗi thành phần trong data management đều có governance.

* _slide 9_: anh Hiếu mong muốn hỏi đối chiếu bản kiến trúc phân tích dữ liệu với kiến trúc dữ liệu hiện tại của VtNet, **không có gì mới** ? 
    - Trong một architecture thì có bao nhiêu level: SID ()
    - Data services/app có gì mới (chia sẻ API cho external user)
    - Billing cho việc sử dụng các services
    - Threshold (hạn mức cho việc xử lý dữ liệu)
    - VtNet có msg ko có định dạng --> Không dùng Schema Registry
    - Với mỗi architecture level sẽ có các quy chuẩn gì khi vẽ mô hình
    - Có scale up cho dịch vụ cloud?
    - Kiến trúc hiện tại có còn phù hợp với các mô hình NLP không?
    - **Chưa thể hiện cơ chế tự bảo vệ dữ liệu** (Ex: ko đáp ứng đc thì hi sinh cái gì để duy trì hoạt động)
    - Alert có mũi tên thể hiện luồng dữ liệu?
    
**Các vấn đề hiện tại hệ thống VtNet đang gặp phải**:
- Query dữ liệu tốn nhiều thời gian
- Dữ liệu thiếu nhiều
- Khi có lỗi xảy ra, thời gian recovery tốn nhiều ngày
==> Kì vọng thiết kế kiến trúc phải thể hiện được solution cho các pain point

**Bổ sung**: 
* kế hoạch khôi phục sau thảm họa
* Cơ chế chống quá tải, chống chịu lỗi
* Cần thiết lập mindset khi thể hiện kiến trúc: khả năng chống chịu lỗi phải được thể hiện ngang hàng với các phần khác

**Nhận xét - Anh Minh**: 
* Cần thể hiện đủ 11 phần trong DAMA Book trong sơ đồ kiến trúc
* Có thể có các thành phần phù hợp với các xu hướng hiện tại: Multi-layer Perception - MLP, Mô hình ngôn ngữ lớn - LLM (trend)
* Việc triển khai on-prem có focus vào điều gì mới không?

### 1.1 Enterprise Data Model (EDM)
* Sản phẩm đầu ra của EDM là gì? phạm vi và level là ntn? (vẽ cho cả VtNet)
    - thể hiện ntn, lưu trữ, quản trị, update ntn

* Ai sẽ là người phụ trách mảng này
(Bổ sung đầu ra mẫu cho quá trình thiết kế EDM)

### 1.2 Data Flow Diagram
* Các thành phần giao tiếp bằng API có thuộc trong luồng dữ liệu?

### 1.3 Chuỗi giá trị dữ liệu
* Phương pháp làm rõ ràng, cần phân công người phụ trách (bên khách hàng cùng làm với DE??)
Ex: DS đặt yêu cầu để DE làm

* Liệu có tools hay quy trình để update các tài liệu??

* Bỏ qua slide 19 kiến trúc hiện tại

---

**Lộ trình triển khai cho các phần đề xuất**
* Ranking sự yêu tiên cho các đề xuất của mỗi phần:
    - Nên làm hiện tại
    - Nên làm nhưng có thể lùi lại
    - Có thể lựa chọn làm hoặc ko
* Các công cụ sử dụng
* Cách thức triển khai con người
---
