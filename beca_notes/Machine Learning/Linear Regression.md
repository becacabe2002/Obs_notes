> [!note] 
> * Các kí hiệu số vô hướng: $x_1,y,z,N$
> * Các kí hiệu vector: $\textbf{y},\textbf{x}_1$

* vector chứa thông tin input: $\textbf{x}=[x_1, x_2, x_3]$ 
* $y$ là một số vô hướng thể hiện giá trị đầu ra của $f(x)$

$$
\begin{gather*} 
y \approx f(x) = \hat{y}
\end{gather*}
$$
$$
\begin{equation}
f(x) = w_1x_1 + w_2x_2 + w_3x_3 + w_0 \tag{1}
\end{equation}
$$
trong đó $w_1, w_2, w_3, w_0$ là các hằng số (gọi là **bias**)

* Bài toán ở đây cần tìm các hệ số bias tối ưu ${w_1, w_2, w_3, w_0}$

> [!note] 
> $y$ là giá trị thực outcome, trong khi $\hat{y}$ là giá trị dự đoán bởi mô hình. Ta mong muốn hai giá trị này sát nhau nhất có thể.

## Phân tích
### Dạng của Linear Regression
* Nếu coi trong $(1)$, nếu đặt $\textbf{w} = [w_0, w_1, w_2, w_3]^T$ là một column vector, $\overline{\textbf{x}} = [1, x_1, x_2, x_3]$ là row vector, ta có thể viết lại phương trình
$$
y \approx \textbf{w} \overline{\textbf{x}} = \hat{y}
$$
### Sai số dự đoán
* Mong muốn sai khác $e$ giữa $y$ và $\hat{y}$ là nhỏ nhất.
$$
\frac{1}{2}e^2 = \frac{1}{2}(y - \hat{y})^2 = 1/2(y - \textbf{w} \overline{\textbf{x}})^2
$$

(1/2 để thuận tiện trong tính toán, sẽ bị triệt tiêu khi đạo hàm)

### Cost Function
* Tính toán tương tự với các cặp (input, outcome) khác $(x_i,y_i), i = 1,2,3,...,N$, yêu cầu tìm $\textbf{w}$ sao cho hàm sau đạt giá trị min:
$$
\mathcal{L}(\textbf{w}) = \frac{1}{2}\sum^N_{i=1}(y_i - \overline{\textbf{x}}_i\textbf{w})^2 \tag{2}
$$

* Giá trị của $\textbf{w}$ để cost function min được gọi là **điểm tối ưu**: $\textbf{w}^* = \text{arg } \underset{\textbf{w}}{min} \mathcal{L}(\textbf{w})$ 
* Đặt:
	* $\textbf{y}=[y_1, y_2, ..., y_N]$ là một column vector chứa tất cả các output của tập training data
	* $\overline{\textbf{X}} = [\overline{\textbf{x}}_1,\overline{\textbf{x}}_2, \overline{\textbf{x}}_3, ..., \overline{\textbf{x}}_N]$ là ma trận dữ liệu đầu vào mà mỗi row làm một điểm dữ liệu.  
* từ đó viết lại cost func:
$$
\begin{align}
\mathcal{L}(\textbf{w}) & = & 1/2 \sum^N_{i=1}(y_i - \overline{\textbf{x}}_i\textbf{w})^2\\
& = & \frac{1}{2} ||\textbf{y} - \overline{\textbf{X}}\textbf{w}||^2_2 \tag{3}
\end{align}
$$

Với $||\textbf{z}||_2$ là chuẩn Euclid (Euclidean norm, hay khoảng cách Euclid), nói cách khác $||\textbf{z}||_2^2$ là tổng của bình phương mỗi phần tử của vector $\textbf{z}$.

### Cách tìm nghiệm cho bài toán Linear Regression

* Có thể triển khai theo hướng giải đạo hàm (gradient descent) = 0;

> [!warning] 
> Chỉ nên áp dụng với các phương trình đạo hàm không quá phức tạp. (VD: mô hình tuyến tính)

* Đạo hàm theo $\text{w}$ của cost function
$$
\frac{\partial \mathcal{L}(\textbf{w})}{\partial \textbf{w}} = \overline{\textbf{X}}^T (\overline{\textbf{X}}\textbf{w} - \textbf{y})
$$
Ptr đạo hàm = 0 tương đương:
Đặt $\textbf{b}$ bằng $\overline{\textbf{X}}^T.\textbf{y}$
$$
\overline{\textbf{X}}^T.\overline{\textbf{X}}.\textbf{w}= b \tag{4}
$$  
> [!note] 
> Nếu đặt ma trận $\textbf{A}=\overline{\textbf{X}}^T.\overline{\textbf{X}}$, và là ma trận khả nghịch (Tồn tại ma trận $\textbf{A}^{-1}$ sao cho $\textbf{A}.\textbf{A}^{-1} =\textbf{I}$ - ma trận đơn vị chứa 1 ở đường chéo, 0 ở các chỗ khác), thì ma trận có nghiệm duy nhất 
> $$
> \textbf{w} = \textbf{A}^{-1}\textbf{b}
> $$

(trong trường hợp A là ma trận không khả nghịch --> dùng giả nghịch đảo (pseudo inverse))

$$
\textbf{w} = A^{\dagger} \textbf{b} = (\overline{\textbf{X}}^T.\overline{\textbf{X}})^{\dagger} \overline{\textbf{X}}^T \textbf{y} \tag{5}
$$

## Các thuật toán có thể sử dụng Linear Regression

* có thể áp dụng cho các mô hình mà hàm số $y \approx f(\textbf{x} = \textbf{w}^T\textbf{x})$ là một hàm tuyến tính theo w hoặc cả w và x.

* **Hạn chế**: 
	* nhạy cảm với giá trị nhiễu (noise) - chỉ cần một giá trị outliner lệch đi nhiều, thì LR sẽ sai khác nhiều