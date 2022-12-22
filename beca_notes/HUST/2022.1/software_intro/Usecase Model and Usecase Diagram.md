## Mô hình Usecase
Bao gồm:
* **Usecase diagram**: 

* **Usecase Specification**: mô tả chi tiết trình tự tương tác giữa các tác nhân và hệ thống trong kịch bản usecase. Có thể sử dụng kết hợp thêm các biểu đồ.
	* Biểu đồ tuần tự (Sequence Diagram)
	* Biểu đồ tương tác ()

* **Supplementary specification (Đặc tả phụ trợ)**: các đặc tả bổ sung về các yêu cầu phần mềm mà các đặc tả usecase chưa mô tả.
> [!example] Ví dụ
> Các yêu cầu chung cho các chức năng
> Các yêu cầu phi chức năng

* **Glossary (Bảng chú giải)**: danh sách các từ vựng/thuật ngữ và giải nghĩa kèm theo

## Biểu đồ Usecase
Bao gồm: 
* **System Boundary (Một đường bao)**: ranh giới giữa bên trong và bên ngoài hệ thống.

* **Actor (Tác nhân)**: Một tác nhân là một người hoặc một vật thể có tương tác với hệ thống. Có trao đổi thông tin với hệ thống, hay hưởng lợi từ hệ thống và phải có sự tự trị trong quyết định. Tác nhân mô tả một thực thể tham gia tương tác với vai trò cụ thể:
	* Tác nhân có thể là người, các thiết bị, các hệ thống khác tương tác với hệ thống  đang xét.

* **Usecase**: tập hợp chuỗi hành động dẫn dến một kết quả cụ thể.

* **Relationship (Quan hệ)**:
	* ***Asociation*** - Quan hệ kết hợp: Quan hệ kết hợp cho biết tác nhân nào tham gia vào ca sử dụng nào. Biểu diễn bằng đường thẳng nối giữa tác nhân và ca sử dụng (có thể sử dụng mũi tên để nhấn mạnh vào hướng của ca sử dụng)
	* ***Generalization*** - Quan hệ tổng quát hoá: actor hoặc usecase con kế thừa tính chất và hành vi của tác nhân hoặc parent usecase
	* ***Include***: biểu diễn một usecase chứa hành vi định nghĩa trong một usecase khác (luôn gọi đến)
	* ***Extend***: một usecase tuỳ ý mở rộng chức năng do usecase khác cung cấp. Chỉ chèn khi điều kiện extend là đúng tại điểm phát sinh (extension point) 