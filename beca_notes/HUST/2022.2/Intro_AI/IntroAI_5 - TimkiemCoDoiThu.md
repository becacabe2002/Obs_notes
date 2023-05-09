* Các bài toán IDS và AStar không có tác dụng với các bài toán có 2 tác tử (có mục tiêu đối nghịch nhau)

> [!note] Các vấn đề của tìm kiếm trong trò chơi
> * **Khó dự đoán trước được phản ứng của đối thủ**:
> * **Giới hạn về thời gian (nếu trò chơi có tính giờ)**:
> * **Tìm kiếm đối thủ đòi hỏi tính hiệu quả (chất luợng nước đi/chi phí thời gian)**:
> * **Nguyên tắc trong nhiều trò chơi đối kháng**:

### Biểu diễn bài toán trò chơi đối kháng
* Bao gồm các thông tin:
	* **Trạng thái bắt đầu**: trạng thái của trò chơi + người chơi đi nước đầu tiên 
	* **Hàm chuyển trạng thái** (successor func): trả về thông tin (move, state)
		* Tất cả move hợp lệ từ state hiện tại
		* New state after move
	* **Kiểm tra kết thúc trò chơi** (terminal test)
	* **Hàm tiện ích** (Utility func): đánh giá các trạng thái

Ví dụ về ***Cây biểu diễn trò chơi***

![[Pasted image 20230421090311.png]]

## Các chiến lược tối ưu
> chuỗi các nước đi giúp đưa đến trạng thái đích mong muốn.

* Chiến lược của MAX bị ảnh hưởng (phụ thuộc) vào các nước đi của MIN , và ngược lại.

> [!hint]  
> * MAX cần chọn chiến lược giúp cực đại hóa giá trị hàm mục tiêu (với MIN là các nước đi )
> * MIN cần chọn chiến lược giúp cực tiểu hóa giá trị hàm mục tiêu
> 
> **-> Chiến lược được xác định bằng việc xét giá trị MINIMAX đối với mỗi nút trong game tree**
> 

VD: trong trò chơi cờ vua
* Ở mỗi state, điểm xét sẽ được tính bằng công thức: tổng điểm quân trắng - tổng điểm quan đen
	* Điểm càng lớn -> quân trắng càng có lợi (Hàm MAX)
	* Điểm càng thấp -> quân đen càng có lợi (Hàm MIN)

### Giải thuật MINIMAX
> * MAX chọn nước đi ứng với MINIMAX cực đại (để đạt giá trị cực đại của hàm mục tiêu)
> * MIN chọn nước đi ứng với MINIMAX cực tiểu

![[Pasted image 20230421093253.png]]

**Nhận xét**
* Tính hoàn chỉnh: có (nếu game tree là hữu hạn)
* Tính tối ưu: có (đối với một đối thủ luôn chọn nước đi tối ưu)
* Độ phức tạp về thời gian: O(b^m)
* Đối với trò chơi cờ vua, hệ số phân nhánh b xấp xỉ 35, hệ số mức độ sâu của game tree xấp xỉ 100
	* Chi phí quá cao -> ko thể tìm kiếm chính xác nước đi tối ưu.

> [!check] 
> Cắt tỉa tìm kiếm

### Cắt tỉa tìm kiếm
> cắt bỏ một số nhánh tìm kiếm trong cây biểu diễn trò chơi.

> [!note] PP cắt tìa $\alpha-\beta$ (Alpha-Beta prunning)
> * Nếu một nhánh tìm kiếm nào ko thể cải thiện đối với giá trị (hàm tiện ích) đã có -> ko cần xét đến nhánh tìm kiếm đó nữa.
> 
> *Việc cắt tỉa nhánh tìm kiếm tồi không ảnh hưởng đến kết quả cuối cùng*

* **Alpha** - giá trị của nước đi tốt nhất đối với MAX (gía trị tối đa) tính đến hiện tại đối với nhánh tìm kiếm
* **Beta** - giá trị của nước đi tốt nhất đối với MIN 

![[Pasted image 20230425000550.png]]

![[Pasted image 20230425001807.png]]
![[Pasted image 20230425001842.png]]

**Nhận xét**:
* Đối với các trò chơi có không gian trạng thái lớn, phương pháp cắt tỉa $\alpha - \beta$ vẫn không phù hợp.
	* Không gian tìm kiếm dù kết hợp cắt tỉa vẫn quá lớn.
* Có thể hạn chế không gian tìm kiếm bằng cách sử dụng tri thức cụ thể của bài toán.
	* Tri thức cho phép đánh giá mỗi trạng thái của trò chơi.
	* Tri thức bổ sung (heuristic) đóng vai trò tương tự như hàm h(n) trong AStar