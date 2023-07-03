## 1. Mẫu và thống kê mô tả
> [!info] Tổng thể 
> Tập hợp các phần tử mang dấu hiệu được quan tâm

Không thể khảo sát được toàn bộ tổng thể, vì:
* Giới hạn về thời gian, tài chính
* Phá vỡ tổng thể nghiên cứu
* Không xác định được chính xác tổng thể
-> Cần lấy ra 1 tập nhỏ của tổng thể để khảo sát và đưa ra quyết định

> [!infor] Tập mẫu
> Là tập con của tổng thể và có tính chất tương tự như tổng thể
> * Số phần tử của tập mẫu được gọi là kích thước mẫu

> [!question] Làm sao để chọn được tập mẫu có tính chất tương tự như tổng thể để các kết luận của tập mẫu có thể dùng cho tổng thể.

### 1.1 Một số cách chọn mẫu

* **Chọn mẫu ngẫu nhiên có hoàn lại**: 
	* Lấy ngẫu nhiên 1 phần tử từ tổng thể vào khảo sát nó
	* Trả phần tử đó về tổng thể trước khi khảo sát 1 phần tử ngẫu nhiên khác
	* Tiếp tục lặp lại n lần, ta có được tập mẫu gồm n phần tử.

* **Chọn ngẫu nhiên không hoàn lại**: tương tự nhưng ko trả lại phần tử về tổng thể

* **Chọn mẫu phân nhóm**: 
	* Chia tập nền thành các nhóm tương đối thuần nhất, từ mỗi nhóm đó chọn ra một mẫu ngẫu nhiên.
	* Tập hợp tất cả các mẫu đó cho ta một mẫu phân nhóm
	* PP áp dụng khi tập nền có những sai khác lớn, phụ thuộc lớn vào việc chia nhóm.

* **Chọn mẫu có suy luận**:
	* Dựa trên ý kiến của chuyên gia về đối tượng nghiên cứu để chọn mẫu

### 1.2 Biểu diễn dữ liệu 

**Dạng liệt kê**:
![[Pasted image 20230606230008.png]]

**Dạng rút gọn**:
![[Pasted image 20230606230046.png]]

**Dạng khoảng**:
* Dữ liệu thu được nhận giá trị trong (a,b). Chia (a,b) ra thành k miền con bởi các điểm chia: $a_0 = a < a_1 < a_2 < a_3 < ... < a_{k-1} < a_k = b$
* Biểu diễn theo tần số:
	![[Pasted image 20230606230348.png]]
* Biểu diễn theo tần suất:
	![[Pasted image 20230606230454.png]]
* Một số lưu ý:
	* k = 5 -> 15
	* Độ dài các khoảng thường chia bằng nhau

* Nếu độ dài các khoảng bằng nhau, ta có thể chuyển về dạng rút gọn, trong đó $x_i$ là đại diện cho khoảng $(a_{i-1}, a_i]$ và được xác định:
$$
x_i = 1/2 * (a_{i-1} + a_i)
$$
> [!note] 
> * Dạng rút gọn thường được thể hiện bằng đồ thị dạng đường hoặc dạng hình tròn.
> * Dạng khoảng thường được thể hiện bằng đồ thị dạng cột

## 2. Mẫu ngẫu nhiên và các đặc trưng mẫu

### 2.1 Mẫu ngẫu nhiên
* Tổng thể được đặc trưng bởi dấu hiệu nghiên cứu X là một biến ngẫu nhiên.
* Trích ra từ tổng thể n phần từ làm 1 tập mẫu. Có 2 loại tập mẫu:
	* Mẫu ngẫu nhiên
	* Mẫu cụ thể

> [!info] Mẫu ngẫu nhiên
> Là vector $W_X = (X_1, X_2, X_3, ..., X_n)$, trong đó mỗi thành phần $X_i$ là một **biến ngẫu nhiên**.
> * Các biến ngẫu nhiên này độc lập và có cùng phân phối xác suất với X

> [!info] Mẫu cụ thể
> Là vector $W_x = (x_1, x_2, x_3, ..., x_n)$ trong đó mỗi thành phần $x_i$ là một giá trị cụ thể

* Một mẫu ngẫu nhiên thì có nhiều mẫu cụ thể ứng với các lần lấy mẫu khác nhau.

> [!example] Ví dụ về mẫu ngẫu nhiên
> ![[Pasted image 20230607090807.png]]
> ![[Pasted image 20230607090835.png]]
> ![[Pasted image 20230607090858.png]]

### 2.2 Các đặc trưng mẫu
> [!note] Thống kê
> Với ($X_1, X_2, ..., X_n$) là một mẫu ngẫu nhiên, thì biến ngẫu nhiên $Y = g(X_1, X_2, ..., X_n)$ với hàm $g$ là một thống kê.

> [!note] Các tham số đặc trưng
> * Xét tổng thể về **mặt định lượng**: tổng thể được đặc trưng bởi dấu hiệu nghiên cứu X (là một biến ngẫu nhiên). Ta có:
> 	* Trung bình tổng thể: $EX = \mu$
> 	* Phương sai tổng thể: $VX = \sigma^2$
> 	* Độ lệch chuẩn của tổng thể: $\sigma$
> * Xét tổng thề về **mặt định tính**: tổng thể có kích thước N, trong đó có M phần tử có tính chất A. Khi đó $p = M/N$ gọi là tỷ lể xảy ra A của tổng thể.

> [!note] Trung bình mẫu 
> #xstk_fomula 
> Cho ($X_1, X_2, ..., X_n$) là một mẫu ngẫu nhiên.
> * Thống kê - trung bình mẫu ngẫu nhiên:
> $$
> \overline{X} = 1/n * \sum^n_{i = 1} X_i
> $$
> * Mẫu ngẫu nhiên ($X_1, X_2, ..., X_n$) có mẫu cụ thể ($x_1, x_2, ..., x_n$) thì $\overline{X}$ nhận giá trị:
> $$
> \overline{x} = 1/n * \sum^n_{i = 1} x_i
> $$
> ($\overline{x}$ là **trung bình mẫu**)
> Nếu mẫu dạng rút gọn thì: $\overline{x}= 1/k * \sum^n_{i = 1} x_in_i$

> [!note] Phương sai mẫu (chưa hiệu chỉnh)
>  #xstk_fomula 
>  Cho ($X_1, X_2, ..., X_n$) là một mẫu ngẫu nhiên.
>  * Thống kê - Phương sai mẫu ngẫu nhiên:
>  $$
>  S^2 = 1/n \sum^n_{i = 1} (X_i - \overline{X})^2
>  $$
>  * Mẫu ngẫu nhiên ($X_1, X_2, ..., X_n$) có mẫu cụ thể ($x_1, x_2, ..., x_n$) thì $S^2$ nhận giá trị:
>  $$
>  S^2 = 1/n \sum^n_{i = 1} (x_i - \overline{x})^2
>  $$
>  $S^2$ được gọi là **Phương sai mẫu (chưa hiệu chỉnh)**
>  * Vấn đề: $E(S^2) = \frac{n-1}{n}\sigma^2$

> [!note] Phương sai mẫu hiệu chỉnh
> #xstk_fomula 
> Hiệu chỉnh để có được giá trị thay thế giá trị $\sigma ^ 2$ tốt hơn.
> * Thống kê - Phương sai mẫu ngẫu nhiên hiệu chỉnh:
> $$
> s^2 = \frac{1}{n-1} \sum ^n _{i=1}(X_i - \overline X)^2
> $$
> * Mẫu ngẫu nhiên ($X_1, X_2, ..., X_n$) có mẫu cụ thể ($x_1, x_2, ..., x_n$) thì $s^2$ nhận giá trị:
>  $$
> s^2 = 1/n \sum^n_{i = 1} (x_i - \overline{x})^2
>  $$
>  s^2 được gọi là **Phương sai mẫu hiệu chỉnh**
>  * s là **độ lệch chuẩn mẫu hiệu chỉnh**

> [!question] Vì sao cần phương sai mẫu hiệu chỉnh?
> * Vì mẫu dữ liệu chỉ là phần nhỏ của dữ liệu quần thể -> có thể xảy ra hiện tượng bias trong ước lượng do sự không chắc chắn của mẫu. (Cần phương sai hiệu chỉnh để làm giảm hiện tượng sai lệch)
> * Psai mẫu thường < phương sai quần thể (phân bố các giá trị mẫu gần nhau hơn so với phương sai quần thể) -> Hiệu chỉnh phương sai mẫu, chúng ta có thể đảm bảo ước lượng phương sai quần thể chính xác hơn.
> * Trong TH dữ liệu tuân theo pp chuẩn, phương sai mẫu được sử dụng để ước lượng psai quần thể sẽ không tuân theo pp chuẩn. Nếu sử dụng cthuc hiệu chỉnh với kích thước mẫu = n -1, ước lượng phương sai quần thể sẽ tuân theo pp chuẩn.

#### Ước lượng điểm
* Mẫu số liệu thu thập được của X (x1, x2,x3, ... , xn)
	Khi đó $\overline \theta = g(x_1, x_2, x_3 ... , x_n)$ được gọi là **ước lượng điểm của $\theta$**

* Muốn biết ước lượng xấu hay tốt, ta đem đi so sán với $\theta$

> [!note] Ước lượng không lệch
> Thống kê $\overline \theta$ được gọi là ước lượng không lệch của $\theta$ nễu thỏa mãn $E\overline \theta = \theta$

![[Pasted image 20230612081231.png]]

**Cách xác định ước lượng điểm**: 

## 3. Ước lượng khoảng
* Cho biến ngẫu nhiên X có $EX = \mu, VX =  \sigma^2$ và mẫu cụ thể của X là $(x_1, x_2, ... , x_n)$
> [!warning] Nếu cỡ mẫu n $\leq 30$ thì ta phải thêm đk $X\sim N(\mu, \sigma ^2)$

**Bài toán:** Tìm khoảng ước lượng cho $\mu$ với xác suất xảy ra bằng $(1-\alpha)$ cho trước. Tương đương với tìm khoảng (a, b) sao cho $P(a < \mu<b) = 1 - \alpha$
* $(a, b)$ - **khoảng tin cậy** (khoảng ước lượng) của $\mu$
* $(1-\alpha)$ được gọi là **độ tin cậy**

### 3.1 Ước lượng khoảng cho kỳ vọng
> [!note] TH1: $\sigma$ đã biết
* Chọn thống kê: $Z = \frac{\overline X - \mu}{\sigma} \sqrt{n} \sim N(0;1)$ (pp chuẩn)
* Xét cặp số ko âm $\alpha _1, \alpha_2$ thỏa mãn: $\alpha_1 + \alpha_2 = \alpha$ là các phân vị chuẩn tắc $u_{\alpha1}, u_{\alpha2}$: 
	* $P (Z < u_{\alpha1}) = \alpha_1$. Do tính chất của pp chuẩn tắc: $u_{\alpha1} = - u_{1-\alpha1}$ (Do pp chuẩn tắc co tính đối xứng)
	* $P(Z < u_{1- \alpha2}) = 1 - \alpha_2$ 
	-> $P(-u_{1- \alpha_1} < Z < u_{1-\alpha_2}) = P(u_{\alpha_1} < Z < u_{1-\alpha_2})$ $= P(Z < u_{1-\alpha_2}) - P(Z < u_{\alpha_1}) = 1 - \alpha_2 - \alpha_1 = 1 -\alpha$ 
* Mà có $Z = \frac{\overline X - \mu}{\sigma} \sqrt{n}$:
$$
=> 1 - \alpha = P (\overline X - u_{1- \alpha_2}\frac{\sigma}{\sqrt{n}} < \mu < \overline X + u_{1- \alpha_1}\frac{\sigma}{\sqrt{n}})
$$
> [!note] Khoảng ước lượng $\mu$ với độ tin cậy $1 - \alpha$ cho trước 
> #xstk_fomula 
> Với một mẫu cụ thể $(x_1, x_2, x_3, ..., x_n)$:
> $$
> (\overline x - u_{1- \alpha_2}\frac{\sigma}{\sqrt{n}};\overline x + u_{1- \alpha_1}\frac{\sigma}{\sqrt{n}})
> $$
> -> Có **vô số** khoảng ước lượng $\mu$

* **Khoảng ước lượng đối xứng** ($\alpha_1 = \alpha_2 = \alpha/2)$ :
$$
(\overline x - u_{1- \alpha/2}\frac{\sigma}{\sqrt{n}}; \overline x + u_{1- \alpha/2}\frac{\sigma}{\sqrt{n}})
	$$
	- với hàm laplace $\phi(u_{1 - \alpha/2}) = 0.5 - \alpha/2$
	- $\epsilon = u_{1 - \alpha/2}*\frac{\sigma}{\sqrt{n}}$ là **độ chính xác của ước lượng**

* Khoảng ước lượng 1 phía ($\alpha_1 = \alpha$ hoặc $\alpha_2 = \alpha$):
$$
(-\infty; \overline x + u_{1- \alpha}\frac{\sigma}{\sqrt{n}}) \text{ hoặc } (\overline x - u_{1- \alpha}\frac{\sigma}{\sqrt{n}}; \infty)
$$
	- Với  hàm laplace $\phi(u_{1-\alpha}) = 0,5 - \alpha$

VD:
![[Pasted image 20230612095938.png]]

(tra bảng z-table có: $\phi(u_{0.975}) = 0.475$ -> có $u_{0.975} = 1.9 + 0.06 = 1.96$)

> [!note] TH2: $\sigma$ chưa biết
* Sử dụng phân vị Student thay cho phân vị chuẩn

> [!question] Vì sao khi tính ước lượng khoảng cho khoảng kì vọng với $\sigma$ chưa biết, ta sử dụng phân vị Student thay cho phân vị chuẩn ?
> * Khi làm việc với mẫu nhỏ mà ko biết độ lệch chuẩn của quần thể, chúng ta sử dụng ước lượng sai số chuẩn (standard error) để tính toán khoảng kỳ vọng.
> 	* Ước lượng sai số chuẩn là một ước lượng của độ lệch chuẩn trong quần thể dựa trên mẫu.
> 	-> Khi sử dụng ước lượng sai số chuẩn, phân phối của ước lượng ko còn là phân phối chuẩn mà là phân phối Student.
> * Phân phối Student được sử dụng vì nó có dạng chuông như pp chuẩn, nhưng có phần đuôi dày hơn. Điều này phản ánh sự không chắc chắn trong ước lượng khi mẫu nhỏ và độ lệch chuẩn của quần thể không biết trước.

* Chọn thống kê: $Z = \frac{\overline X - \mu}{s}\sqrt{n} \sim T(n-1)$ (bậc tự do n - 1)

* Tương tự như trường hợp 1, thay phân vị chuẩn bằng phân vị Student.

> [!note] khoảng ước lượng với $\sigma$ ko cho trước 
> #xstk_fomula 
> Với mẫu cụ thể $(x_1, x_2, x_3, ..., x_n)$, ta có khoảng ước lượng cho $\mu$ với độ tin cậy $1-\alpha$ là:
> $$
> (\overline x - t(n-1, 1-\alpha _2)*\frac{s}{\sqrt{n}}; \overline x + t(n-1, 1-\alpha _1)*\frac{s}{\sqrt{n}})
> $$

> [!warning] n > 30 : pp chuẩn tắc và pp Student bậc tự do n - 1 có thể coi là 1

* Khi đó, ta có thể chọn thống kê: $Z = \frac{\overline X -\mu}{s} \sqrt{n} \sim N(0;1)$ 
* Khoảng ước lượng cho $\mu$ với độ tin cậy $1-\alpha$ là:
$$
(\overline x - u_{1-\alpha_2}*\frac{s}{\sqrt{n}}; \overline x + u_{1- \alpha_1}*\frac{s}{\sqrt{n}})
$$

* **Khoảng ước lượng đối xứng** $(\alpha_1 = \alpha_2 = \alpha/2)$:
$$
(\overline x - t(n-1, 1-\alpha/2)*\frac{s}{\sqrt{n}}; \overline x + t(n-1, 1-\alpha/2)*\frac{s}{\sqrt{n}})
$$

* **Khoảng ước lượng một phía**: $(\alpha_1 = \alpha \text{ hoặc } \alpha_2 = \alpha)$ 
$$
(-\infty; \overline x + t(n-1, 1-\alpha)*\frac{s}{\sqrt{n}})
$$
hoặc:
$$
(\overline x - t(n-1, 1-\alpha)*\frac{s}{\sqrt{n}}; \infty)
$$
VD:
![[Pasted image 20230612155940.png]]

> [!caution] Cần phân biệt giữa **độ lệch chuẩn mẫu hiệu chỉnh (standard error)** và **độ lệch chuẩn (standard deviation)**

### 3.2 Ước lượng khoảng cho tỷ lệ
* Xác suất xảy ra sự kiện A là p.
* Thực hiện n phép thử độc lập, cùng điều kiện trong đó có m phép thử xảy ra A.
	* $f = m/n$ là ước lượng điểm không chệch cho p.

> [!question] Với độ tin cậy $(1-\alpha)$, hãy ước lượng cho $p$.

* Chọn thống kê: $Z = \frac{f-p}{\sqrt{p(1-p)}}\sqrt{n} \sim N(0;1)$ 
* Thay p -> f để thuận tiện cho việc tính toán:
$$
=> Z = \frac{f-p}{\sqrt{f(1-f)}} \sqrt{n} \sim N(0;1)
$$

> [!note] Khoảng ước lượng $p$ với độ tin cậy $1-\alpha$
> Với mẫu cụ thể $(x_1, x_2, ..., x_n)$ :
> $$
> (f - u_{1-\alpha_2}\sqrt{\frac{f(1-f)}{n}};f + u_{1-\alpha_1}\sqrt{\frac{f(1-f)}{n}})
> $$

* **Khoảng ước lượng đối xứng** $(\alpha_1 = \alpha_2 = \alpha/2)$ :
$$
(f - u_{1-\alpha/2}\sqrt{\frac{f(1-f)}{n}};f + u_{1-\alpha/2}\sqrt{\frac{f(1-f)}{n}})
$$
* **Khoảng ước lượng 1 phía** $(\alpha_1 = \alpha \text{ hoặc } \alpha_2 = \alpha)$ :
$$
(-\infty;f + u_{1-\alpha}\sqrt{\frac{f(1-f)}{n}})
$$
hoặc :
$$
(f - u_{1-\alpha}\sqrt{\frac{f(1-f)}{n}};\infty)
$$
VD: ![[Pasted image 20230612163218.png]]