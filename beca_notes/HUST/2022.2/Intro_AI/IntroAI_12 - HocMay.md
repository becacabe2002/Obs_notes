* Học máy là một quá trình nhờ đó một hệ thống cải thiện hiệu suất 
* Là việc lập trình các máy tính để tối ưu hoá một tiêu chí hiệu suất dựa trên dữ liệu hoặc kinh nghiệm trong quá khứ.

> [!info] Một máy học
> Một máy tính có khả năng tự học khi nó tự cải thiện hiệu suất hoạt động `P` cho một công việc `T` cụ thể, dựa vào kinh nghiệm `E` của nó.
> * Một bài toán học máy có thể biểu diễn bằng 1 bộ `(T, P, E)`: 
> 	* **T** - một công việc
> 	* **P** - tiêu chí đánh giá hiệu năng 
> 	* **E** - kinh nghiệm

![[Pasted image 20230702091742.png]]

> [!note] Học ?
> Là một ánh xạ:
> $$
> f: x \rightarrow y
> $$
> * `x` - quan sát, kinh nghiệm
> * `y` - phán đoán, tri thức mới, kinh nghiệm mới

* Với y là một số thực -> **Hồi quy**
* Với y thuộc một tập rời rạc -> **Phân loại**

> [!note] Quy trình học
> * Học từ các quan sát trong quá khứ (tập học): {$x_1, x_2, ..., x_N$}{$y_1, y_2, ..., y_M$}
> * Thu được một mô hình, kinh nghiệm, tri thức mới
> * Dùng các điều đó để **suy diễn (phán đoán)** cho quan sát trong tương lai: $Y = f(x)$

## Hai bài toán học cơ bản
> [!abstract] 
> * Học có giám sát (supervised learning)
> * Học không giám sát (unsupervised learning)

### Học có giám sát
* Cần học một hàm $y = f(x)$ từ tập học  {$x_1, x_2, ..., x_N$}{$y_1, y_2, ..., y_N$} sao cho $y_i = f(x_i)$
	* Phân loại :  nếu y chỉ nhận giá trị từ một tập rời rạc
	* Hồi quy: nếu y nhận được giá trị số thực

![[Pasted image 20230702094507.png]]

### Học không giám sát
* Cần học một hàm $y=f(x)$ từ tập học  cho trước {$x_1, x_2, x_3, ..., x_N$}
	* Y có thể là các cụm dữ liệu
	* Y có thể là các cấu trúc ẩn

![[Pasted image 20230702094550.png]]

## Quá trình học máy
* Toàn diện:
![[Pasted image 20230702094718.png]]

## Thiết kế một hệ thống học
1. Lựa chọn các ví dụ học
	* Các thông tin hướng dẫn quá trình học được chứa ngay trong các ví dụ học, hoặc được cung cấp gián tiếp
	* Các ví dụ học, theo kiểu có giám sát/không giám sát
	* Các ví dụ học trên tương thích với các ví dụ sẽ được làm việc bởi hệ thống trong tương lai (future examples)

2. Xác định hàm mục tiêu (giả thiết, khái niệm) cần học
	* $F: X \rightarrow {0,1}$
	* $F: X \rightarrow$ một tập các nhãn lớp
	* $F: X \rightarrow R^+$

3. Lựa chọn cách biểu diễn cho hàm mục tiêu cần học
	* Hàm đa thức
	* Tập các luật
	* Cây quyết định
	* Mạng nơ-ron nhân tạo

4. Lựa chọn giải thuật học máy có thể học (xấp xỉ) được hàm mục tiêu
	* Pp học hồi quy
	* Pp quy nạp luật
	* Pp học cây quyết định
	* Pp học lan truyền ngược

## Các vấn đề trong Học máy 
> [!warning] Các vấn đề
> * **Giải thuật học máy:**
> 	* Những gth nào có thể học xấp xỉ
> 	* Với những đk nào thì gth học máy hội tụ hàm mục tiêu cần học
> 	* Đối với một lĩnh vực bài toán cụ thể và đối với cách biểu diễn các ví dụ cụ thể, gth học máy nào thực hiện tốt nhất?
> * **Các ví dụ học máy:**
> 	* Bao nhiêu là đủ
> 	* Kích thước của tập học ảnh hưởng ntn đối với độ chính xác của hàm mục tiêu được chọn
> 	* Các ví dụ lỗi hoặc các ví dụ thiếu giá trị thuộc tính sẽ ảnh hưởng thế nào đối với độ chính xác ?
> * **Quá trình học :**
> 	* Chiến lược tối ưu cho việc lựa chọn thứ tự sử dụng các ví dụ học
> 	* Các chiến lược lựa chọn làm thay đổi mức độ phức tạp của bài toán học máy ntn?
> 	* Các tri thức cụ thể của bài toán (ngoài các ví dụ học) có thể đóng góp thế nào đối với quá trình học
> * **Khả năng/ giới hạn học :**
> 	* Hàm mục tiêu nào mà hệ thống cần học
> 		* Khả năng biểu diễn và độ phức tạp của giải thuật và quá trình học
> 	* Các giới hạn đối với khả năng học của các giải thuật học máy?
> 	* Khả năng ***Khái quát hoá (generalization)*** của hệ thống
> 		* Để tránh vấn đề ***Over-fitting***
> 	* Khả năng tự thay đổi cấu trúc bên trong của hệ thống
> 		* Cải thiện khả năng của hệ thống đối với việc biểu diễn và học hàm mục tiêu.

### Overfitting
> Đạt độ chính xác cao trên tập học, nhưng đạt độ chính xác thấp trên tập thử nghiệm.

> [!note] Các nguyên nhân gây ra Overfitting
> * Hàm học tập quá phức tạp
> * Lỗi (nhiễu) trong tập huấn luyện (Do quá trình thu thập/xây dựng tập dữ liệu)
> * Số lượng các ví dụ học quá nhỏ, ko đại diện cho toàn bộ tập của các ví dụ của bài toán học.

![[Pasted image 20230702122930.png]]

* Tổng quát hoá là mục tiêu chính của ML <=> Khả năng phán đoán tốt với dữ liệu tương lai

![[Pasted image 20230702142827.png]]
*(Đường màu xanh là đường tối ưu nhất)*
