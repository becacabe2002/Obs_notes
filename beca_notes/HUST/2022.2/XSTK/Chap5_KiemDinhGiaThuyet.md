> **Kiểm định giả thuyết** - bài toán đi xác định có nên chấp nhận hay bác bỏ một khẳng định về giá trị của một tham số của tổng thể 


## 1. Kiểm định giả thuyết một mẫu
**Bài toán**
![[Pasted image 20230626072209.png]]

> [!check] Cách giải quyết 
> * Từ bộ số dữ liệu đã cho $x_1, x_2, x_3 ..., x_n$, tính được giá trị quan sát k. 
> * Chia được trục số thành 2 phần, 1 phần trong đó là $W_\alpha$ 
> 	* Nếu $X \in W_\alpha$, bác bỏ $H_0$ và chấp nhận $H_1$
> 	* Nếu $X \notin W_\alpha$, không có cơ sở bác bỏ $H_0$

> [!warning] Hai sai lầm có thể mắc phải
> * **Sai lầm 1:** bác bỏ $H_0$ trong khi $H_0$ đúng. 
> 	* Xác suất xảy ra sai lầm: $\alpha = P(k \in W_\alpha | H_o \text{ đúng})$ -> **Mức ý nghĩa**
> * **Sai lầm 2:** Chấp nhận $H_0$ trong khi $H_0$ sai.
> 	* Xác suất xảy ra sai lầm: $\beta = P(k \notin W_\alpha | H_o \text{ sai})$ 

* Mục tiêu là **cực tiểu** cả hai sai lầm -> khó
	* Chọn cách cố định sai lầm loại 1 và cực tiểu sai lầm loại 2

![[Pasted image 20230703102137.png]]

> [!abstract] Các bước làm bài kiểm định
> B1. Gọi biến ngẫu nhiên, xây dựng cặp giả thuyết - đối thuyết
> 
> B2. Chọn tiêu chuẩn kiểm định. Tính giá trị quan sát $k$
> 
> B3. Xác định miền bác bỏ $H_0: W_\alpha$ 
> 
> B4. Kiểm tra xem giá trị quan sát có nằm trong miền bác bỏ hay ko ($k \in W_\alpha ?$) để đưa ra quyết định loại bỏ giả thuyết hay không


### 1.1 Kiểm định cho kỳ vọng - $\sigma^2$ đã biết

### 1.2 Kiểm định cho kỳ vọng - $\sigma^2$ chưa biết

### 1.3 Kiểm định cho tỷ lệ

### 1.4 Kiểm định cho phương sai