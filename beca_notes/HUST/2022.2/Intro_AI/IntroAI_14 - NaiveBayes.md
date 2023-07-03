> [!info] Phân lớp Naive Bayes
> * Là các pp học phân lớp có giám sát và dựa trên xác suất
> 	* Phân loại dựa trên các giá trị xác suất của các khả năng xảy ra của các giả thiết
> * Dựa trên một mô hình (hàm) xác suất dựa trên ***định lý Bayes***

* Là một trong các pp ML thường được sử dụng trong các bài toán thực tế.

> [!note] Định lý Bayes
> $$
> P(h|D) = \frac{P(D|h).P(h)}{P(D)}
> $$
> * $P(D)$ - xác suất trước của việc quan sát dữ liệu D
> * $P(h)$ - xác suất trước của giả thiết h
> * $P(D|h)$ - xác suất xảy ra của D, biết rằng giả thiết h là đúng
> * $P(h|D)$ - xác suất (hậu nghiệm) của giả thiết h là đúng, nếu quan sát được D
> 
> **-> Nhiều pp phân loại dựa trên xác suất sẽ sử dụng xác suất hậu nghiệm (posterior probability)**

VD:
![[Pasted image 20230702205810.png]]

* Dữ liệu $D$. Ngoài trời là nắng và Gió là mạnh
* Giả thiết (phân loại) $h$. Anh ta chơi tennis
* Xác suất trước $P(h)$. Xác suất rằng anh ta chơi tennis (bất kể Ngoài trời như thế nào và Gió ra sao)
* Xác suất trước $P(D)$. Xác suất rằng Ngoài trời là nắng và Gió là mạnh
* $P(D|h)$. Xác suất Ngoài trời là nắng và Gió là mạnh, nếu biết rằng anh ta chơi tennis
* $P(h|D)$. Xác suất anh ta chơi tennis, nếu biết rằng Ngoài trời là nắng và Gió là mạnh

## Xác suất hậu nghiệm cực đại
> [!info] Maximum a posteriori - MAP
> Là giả thiết $h$ ($\in H$, tập các giả thiết) có thể xảy ra nhất đối với các dữ liệu quan sát được $D$

$$
h_{MAP} = arg_{h \in H} max P(h|D)$$
theo định lý Bayes, có :
$$
h_{MAP} = arg_{h\in H}max\frac{P(D|h).P(h)}{P(D)}
$$
P(D) là như nhau đối với các giả thiết :
$$
h_{MAP} = arg_{h\in H}maxP(D|h).P(h)
$$

![[Pasted image 20230702211409.png]]

### Đánh giá khả năng có thể nhất
* PP MAP: với một tập các giả thiết có thể H, cần tìm một giả thiết cực đại hoá giá trị: $P(D|h). P(h)$ 

* Giả sử trong pp đánh giá **khả năng có thể nhất (Maximum likelihood estimation - MLE)**, tất cả các giả thiết đều có giá trị xác suất trước như nhau: $P(h_i) = P(h_j), \forall h_i, h_j \in H$ 
* MLE tìm giả thiết cực đại hoá giá trị $P(D|h)$, trong đó $P(D|h)$ là khả năng có thể của dữ liệu D đối với h.
* Giả thiết có khả năng nhất (maximum likelihood hypothesis)
$$
h_{ML} = arg _{h \in H} max P(D|h)
$$
![[Pasted image 20230702214839.png]]

## Phân loại Naive Bayes

> [!note] Biểu diễn bài toán phân loại (classification problem)
> * Một tập học $D_{train}$, trong đó mỗi ví dụ học $x$ sẽ được biểu diễn là một vector $n$ chiều: $(x_1, x_2, ..., x_n)$
> * Một tập xác định các nhãn lớp: $C = {c_1, c_2, c_3, ..., c_n}$
> * Với mỗi ví dụ $z$ mới, $z$ sẽ được phân vào lớp nào?
> 
> **Mục tiêu:** Xác định phân lớp nào phù hợp nhất với z

$$
C_{MAP} = arg_{c_i \in C} max P(c_i|z) = arg_{c_i \in C} max P(c_i|z_1, z_2, ..., z_n)
$$
$$
= arg_{c_i \in C} max \frac{P(z_1, z_2, ... , z_n| c_i).P(c_i)}{P(z_1, z_2, ..., z_n)}
$$
*(Theo định lý Bayes)*
* $P(z_1, z_2, z_3, ..., z_n)$ là như nhau với các lớp

* Giả thuyết trong phương pháp phân loại Naive Bayes: *Các thuộc tính là độc lập có điều kiện đối với các lớp*
$$
P(z_1, z_2, ... , z_n| c_i) = \Pi ^n _{j = 1} P(z_j | c_i)
$$
* Phân loại Naive Bayes tìm phân lớp phù hợp nhất đối với z
$$
C_{NB} = arg _{c_i \in C}maxP(c_i).\Pi ^n _{j = 1} P(z_j | c_i)
$$
> [!note] Giải thuật phân loại Naive Bayes
> * **Giai đoạn học (training phase)**: sử dụng một tập học, đối với mỗi phân lớp có thể $c_i \in C$:
> 	* Tính giá trị xác suất tiên nghiệm: $P(c_i)$
> 	* Đối với mỗi giá trị thuộc tính $x_j$:
> 		* Tính giá trị xác suất xảy ra của giá trị thuộc tính đó đối với một phân lớp $c_i: P(x_j|c_i)$
> 
> * **Giai đoạn phân lớp (classification phase)**: đối với một ví dụ mới