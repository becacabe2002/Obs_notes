* k - nearest neighbors (k - NN) là một pp phổ biến trong ML (Còn được gọi là Instance-base learning/lazy learning/Mem-based learning)

> [!tip] Ý tưởng
> * Ko xây dựng một model rõ ràng cho hàm mục tiêu cần học
> * Quá trình học chỉ lưu lại các dữ liệu huấn luyện
> * Việc dự đoán cho một quan sát mới sẽ dựa vào các hàng xóm gần nhất trong tập học.

> [!note] Hai thành phần chính của k - NN
> * **Độ đo tương đồng (similarity measure/distance)** giữa các đối tượng
> * **Các hàng xóm** dùng trong việc phán đoán

* Trong một số điều kiện thì k - NN có thể đạt mức **lỗi tối ưu Bayes** (mức lỗi mong muốn của bất kỳ phương pháp nào)

![[Pasted image 20230702164122.png]]

### Giải thuật k - NN cho phân lớp
* Mỗi ví dụ học $x$ được biểu diễn bởi 2 thành phần:
	* Mô tả của ví dụ: $x = (x_1, x_2, ..., x_n$) trong đó $x_i \in R$
	* Nhãn lớp: $c \in C$ với $C$ là tập các nhãn lớp được xác định trước

* Giai đoạn học:
	* Đơn giản là lưu lại các ví dụ học trong tập học: $D$

* Giai đoạn phân lớp: để phân lớp cho một ví dụ (mới) $z$
	* Với mỗi ví dụ học $x\in D$ tính khoảng cách giữa $x$ và $z$
	* Xác định tập $NB(z)$ - các láng giềng gần nhất với $z$
		-> Gồm $k$ ví dụ học trong $D$ gần nhất với $z$ tính theo một hàm khoảng cách $d$ 
	* Phân $z$ **vào lớp chiếm số đông** trong số các lớp của các ví dụ trong $NB(z)$

### Giải thuật k - NN cho hồi quy
* Mỗi ví dụ học $x$ được biểu diễn bởi 2 thành phần 
	* Mô tả của ví dụ: $x = (x_1, x_2, ..., x_n$) trong đó $x_i \in R$ 
	* Giá trị đầu ra mong muốn: $y_x \in R$ (là một số thực)

* Giai đoạn học:
	* Đơn giản là lưu lại các ví dụ học trong tập học $D$

* Giai đoạn dự đoán: để dự đoán giá trị đầu ra cho ví dụ $z$
	* Đối với mỗi ví dụ học $x \in D$ tính khoảng cách giữa $x$ và $z$
	* Xác định tập $NB(z)$ - các láng giềng gần nhất với $z$
		-> Gồm $k$ ví dụ học trong $D$ gần nhất với $z$ tính theo một hàm khoảng cách $d$ 
	* Dự đoán giá trị đầu ra đối với z: 
	$$
	y_z = \frac{1}{k} \sum_{x \in NB(z)} y_x
	$$

> [!warning] Các vấn đề cốt lõi của k - NN
> * Suy nghĩ của các bên khác nhau -> nhìn nhận vấn đề khác nhau 
> * Hàm khoảng cách
> 	* Mỗi hàm tương ứng một cách nhìn về dữ liệu 
> 	* Vô vạn hàm
> 	* Khó trong quyết định lựa chọn hàm
> * Chọn tập láng giềng NB(z)
> 	* Chọn bao nhiêu láng giềng
> 	* Giới hạn chọn theo vùng 

## k - NN: một hay nhiều láng giềng ?
*1 - NN cũng có thể được coi là một trong số các phương pháp tối ưu*

* k - NN là một pp tối ưu Bayes nếu gặp một số điều kiện
	* y bị chặn
	* cỡ M của tập học lớn
	* hàm hồi quy liên tục
	$$
	k \rightarrow \infty; (k/M) \rightarrow 0; (k/log M) \rightarrow + \infty
	$$

* Trong thực tiễn, ta nên lấy nhiều hàng xóm (k > 1) khi cần phân lớp, dự đoán, nhưng không quá nhiều.
	* Tránh ảnh hưởng của lỗi/nhiễu nếu chỉ dùng 1 hàng xóm.
	* Nếu quá nhiều hàng xóm thì sẽ phá vỡ cấu trúc tiềm ẩn trong dữ liệu

## Hàm tính khoảng cách 

> [!note] Hàm tính khoảng cách $d$
> * Đóng vai trò rất quan trọng trong phương pháp học dựa trên các láng giềng gần nhất.
> * Thường được xác định trước, và không thay đổi trong quá trình học cũng như phân loại/dự đoán

### Lựa chọn hàm khoảng cách $d$

> [!abstract] 
> * **Các hàm khoảng cách hình học** - dành cho các bài toán có các thuộc tính đầu vào là kiểu số thực ($x_i \in R$)
> * **Hàm khoảng cách Hamming** - dành cho các bài toán có các thuộc tính đầu vào là kiểu nhị phân ($x_i \in \{0,1\}$)

* Các hàm tính khoảng cách hình học (Geometry distance funcs)
![[Pasted image 20230702181046.png]]

* Hàm khoảng cách Hamming:
![[Pasted image 20230702181134.png]]

### Chuẩn hoá miền giá trị thuộc tính
![[Pasted image 20230702181314.png]]

* Có thể chuẩn hoá miền giá trị:
	* Khoảng giá trị [0, 1] thường được sử dụng 
	* Đối với mỗi thuộc tính i: $x_i := x_i/max(x_j)$ 

### Trọng số của các thuộc tính

> [!warning] Chú ý 
> Các thuộc tính khác nhau có thể (nên) có mức độ ảnh hưởng khác nhau đối với giá trị khoảng cách.

* Có thể phải tích hợp các giá trị trọng số của các thuộc tính trong hàm tính khoảng cách:
	* $w_i$ là trọng số của thuộc tính $i$ : 
	$$
	d(x, z) = \sqrt{\sum ^n _{i=1}w_i (x_i - z_i)^2}
	$$

> [!question] Làm sao để xác định các giá trị trọng số của các thuộc tính ?
> * Dựa trên các tri thức cụ thể của bài toán
> 	* *Được chỉ định bởi các chuyên gia trong lĩnh vực*
> * Bằng một quá trình tối ưu hoá các giá trị trọng số
> 	* *sử dụng một tập học để học một bộ các giá trị trọng số tối ưu*

## Khoảng cách của các láng giềng
* Xét tập $NB(z)$ - gồm k ví dụ học gần nhất với ví dụ cần phân lớp/dự đoán $z$
	* Mỗi ví dụ này có khoảng cách khác nhau đến $z$
	* Các láng giềng này **Không** ảnh hưởng như nhau đối với việc phân lớp/dự đoán cho $z$.

* Có thể gán các mức độ ảnh hưởng của mỗi láng giềng gần nhất tuỳ theo khoảng cách của nó đến z (cao hơn cho các láng giềng gần)

![[Pasted image 20230702190148.png]]

## Ưu nhược điểm của k - NN
> [!check] Các ưu điểm
> * Chi phí thấp cho quá trình huấn luyện (chỉ việc lưu lại các ví dụ học)
> * Hoạt động tốt với các bài toán phân loại gồm nhiều lớp (ko phải học toàn bộ phân loại cho tất cả các lớp)
> * với k >> 1, k - NN có khả năg xử lý nhiễu cao
> * Linh động trong việc chọn hàm khoảng cách:
> 	* Có thể dùng độ tương tự
> 	* Có thể dùng độ đo khác: Kullback-Leibler divergence, Bregman divergence, …

> [!fail] Các nhược điểm
> * Phải lựa chọn hàm tính khoảng cách (sự khác biệt) thích hợp với bài toán
> * Chi phí tính toán cao tại thời điểm phân loại/dự đoán
> * Có thể cho kết quả kém/sai khác với các thuộc tính ko liên quan.

