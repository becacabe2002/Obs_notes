> [!info] Biến ngẫu nhiên
> Một đại lượng mà giá trị của nó là ngẫu nhiên, phụ thuộc vào kết quả phép thử.
> * Thường kí hiệu bằng các chữ in hoa: X, Y, Z, X_1 ...
> * Các giá trị mà biến ngẫu nhiên nhận được: a, b, c, d ....

* Phân loại biến ngẫu nhiên:
	* ***Biến ngẫu nhiên rời rạc*** : nếu tập giá trị của nó là tập hữu hạn hoặc vô hạn đếm được các phần tử.
	* ***Biến ngẫu nhiên liên tục*** : nếu tập giá trị của nó lấp kín một khoảng hoặc một số khoảng của trục số hoặc cả trục số.

## 1. Biến ngẫu nhiên rời rạc
### 1.1 Bảng phân phối xác suất
> [!info] Bảng phân phối xác suất
> ![[Pasted image 20230424080350.png]]
> * x_n là các giá trị của biến ngẫu nhiên X
> * p_n là xác suất để biến ngẫu nhiên X nhận giá trị x_n

* $\sum_i p_i = 1$

> [!note] Hàm phân phối xs của biến ngẫu nhiên rời rạc X
> #xstk_fomula 
> $$
> F(x) = P(X < x) = \sum _{i: x_i < x} P(X = x_i) = \sum _{i: x_i < x} p_i 
> $$

### 1.2 Các tham số đặc trưng
> [!info] Kỳ vọng
> #xstk_fomula 
> Đại lượng đặc trưng cho giá trị trung bình. (Trong một vài trường hợp đặc biệt, có thể được coi là giá trị trung bình)
> * Với X rời rạc có: $EX = \sum _i(x_i*p_i)$
 
> [!hint] Các tính chất của kỳ vọng
> * $Ec = c$ với c là hằng số
> * $E(aX) = a.EX$
> * $E(X+b) = EX + b$
> 	->  $E(aX +b) = aEX + b$
> * $E(X+Y) = EX + EY$
> 
> **Tổng quát với X là biến ngẫu nhiên rời rạc:**
>  $$
>  Eg(X) = \sum_ig(x_i).p_i
> $$
 
Ví dụ: $E(X^2) = \sum_i(x_i)^2.p_i$ 

> [!info] Phương sai
> #xstk_fomula 
> Trung bình của bình phương sai số
> * Kí hiệu: $V(X)$ hoặc $VX$
> * Công thức:
> $$
> VX = E(X - EX)^2 = E(X^2) - (EX)^2
> $$
> *với X - EX là sai số (độ lệch) khỏi giá trị trung bình, X là biến ngẫu nhiên rời rạc*
> * $EX = \sum^n_{i=1}x_i.p_i$
> * $E(X^2)=\sum^n_{i=1}x_i^2.p_i$

**Ý nghĩa của phương sai**:
* Phương sai thể hiện mức độ phân tán dữ liệu xung quanh giá trị EX
	-> Phương sai càng lớn, độ phân tán dữ liệu càng cao và ngược lại.

Ví dụ:
- Với X là kích cỡ của sản phẩn -> VX biểu thị độ chính xác của các sản phẩm.
* Với X là kích thước và cân nặng của vật nuôi -> VX biểu thị độ tăng trưởng đồng đều của vật nuôi.
* Với X là năng suất của giống cây trồng -> VX biểu thị mức độ ổn định của năng suất giống cây trồng.
* Với X là lãi suất của khoản đầu tư -> VX biểu thị cho mức độ rủi ro của đầu tư.

> [!hint] Các tính chất của phương sai
> * $Vc = 0$ với c = const
> * $V(aX) = a^2.VX$
> * $V(X +b) = VX$
> 
> **Tổng quát**:
> $$
> V(aX + b) = a^2VX
> $$

> [!info] Độ lệch chuẩn
> #xstk_fomula 
> Dùng để đo độ phân tán dữ liệu xung quanh gía trị EX ($\sigma(X)$ hoặc $\sigma$)
> * Công thức tính: $\sigma = \sqrt{VX}$

> [!info] Mode
> Mode của biến ngẫu nhiên X (mod(X)) là giá trị của biến X có khả năng xuất hiện lớn nhất trong 1 lân cận nào đó của nó.
> * Với biến ngẫu nhiên rời rạc,  mod(X) là giá trị ứng với xác suất lớn nhất.
> * Với biến ngẫu nhiên liên tục, có thể có nhiều mod(X)

> [!info] Phân vị mức p
> là giá trị $z_p$ sao cho:
> $$F(z_p)= P(X<z_p)=p$$
> 
> * Một số phân vị đặc biệt: Phân vị mức 25% (tứ phân vị 1st), Trung vị 50%, Phân vị mức 75% (tứ phân vị 3rd)
> 	* ***Trung vị (med)***: giá trị tốt hơn EX, nhất là trong trường hợp số liệu có nhiều sai sót hoặc sai sót thái quá.
> 
> $$
> P(X < med(X)) = P(X \geq med(X)) = 0.5
> $$
> (*Có thể tìm trung vị med(X) bằng cách giải F(x) = 0.5*)

## 2. Biến ngẫu nhiên liên tục

### 2.1 Hàm mật độ xác suất

> [!info] Hàm mật độ xác suất
> #xstk_fomula 
> Hàm mật độ xác suất của biến ngẫu nhiên liên tục X là hàm f(x) xác định trên R:
> * $f(x)\geq \forall x \in R$
> * $P(X \in (a,b)) = \int _a^b f(x)dx$

> [!warning] Chú ý
> Vì hàm mật độ xác suất f(x) của biến ngẫu nhiên liên tục X thể hiện mức độ tập trung xác suất của X xung quanh điểm x. Tức là với $\Delta_x$ đủ nhỏ:
> $$
> P(x \leq X \leq x + \Delta_x) \approx f(x).\Delta_x
> $$
> -> Xác xuất để để X nhận giá trị lân cận bé tỉ lệ thuận với f(x)

> [!hint] Tính chất
> #xstk_fomula 
> * $\int^{+ inf} _{- inf} f(x)dx = 1$
> 
> * $P(a \leq X < b) = P(a < X < b) = P(a < X \leq b) = P(a \leq X \leq b) = \int^{b} _{a} f(x)dx$
> * Hàm phân phối xác suất : $F(x) = P(X < x) =\int^{x} _{- inf} f(t)dt$ -> $f(x) = F'(x)$

### 2.2 Các tham số đặc trưng của biến ngẫu nhiên liên tục

> [!info] Kỳ vọng của biến nn liên tục
> #xstk_fomula 
> * Công thức:
> $$
> EX = \int^{+ inf}_{- inf}x.f(x)dx
> $$
> * Tính chất:
> 	* $E(aX +b) = a.EX +b$
> 	* $E g(X) = \int^{+ inf} _{- inf} g(x).f(x).dx$

Ví dụ: 
![[Pasted image 20230425232306.png]]

> [!info] Phương sai của biến nn liên tục
> * Công thức: $VX = E(X - EX)^2 = E(X^2) - (EX)^2$
> 	* $EX = \int^{+ inf} _{- inf} x.f(x).dx$
> 
> 	* $E(X^2) = \int^{+ inf} _{- inf} x^2.f(x).dx$
> * Tính chất: $V(aX + b) = a^2VX$

* Độ lệch chuẩn (tương tự rời rạc)

> [!info] Mode
> Mod của biến ngẫu nhiên liên tục là giá trị của X ứng với f(x) đạt cực đại địa phương.

* Phân vị mức p (tương tự rời rạc)

## 3. Một số phân phối xác suất thông dụng
> [!abstract] 
> * Với biến ngẫu nhiên rời rạc:
> 	* Luật phân phối nhị thức (Binomial Distribution)
> 	* Luật phân phối Poisson
> * Với biến ngẫu nhiên liên tục:
> 	* Phân phối đều liên tục
> 	* Phân phối chuẩn
> 	* Phân phối mũ
> 	* Phân phối khi bình phương
> 	* Phân phối Student

### 3.1 Phân phối nhị thức
> [!info] PP nhị thức
> Biến nn X nhận gía trị trong tập {0, 1, 2, 3, ..., n} với xác suất được tính theo Bernoulli:
> $P(X = k) = C^k_n.p^k.(1-p)^{n - k}$ với k thuộc (0:n) và p thuộc [0;1]
> được gọi là **tuân theo phân phối nhị thức** với các tham số n và p. ($X\sim B(n;p)$)

* Các tham số đặc trưng:
	* $EX = np$
	* $V X = np(1 − p) = npq$  với $q = 1 − p$
	* $(n + 1)p − 1 ≤ mod(X) ≤ (n + 1)p$

> [!hint] Ứng dụng
> Thực hiện n phép thử độc lập cùng điều kiện. Trong mỗi phép thử xác suất xảy ra sự kiện A luôn là p. X là số phép thử xảy ra A.
> -> $X\sim B(n;p)$

### 3.2 Phân phối Poisson
> [!info] PP Poisson
> Biến nn X nhận giá trị trong tập {0, 1, 2, .., n, ..} với xác suất:
> $$
> P(X = k) = e^{-\lambda}\frac{\lambda^k}{k!}
> $$
> với k = 0, 1, 2, ...
> được gọi là **tuân theo phân phối Poisson** với tham số $\lambda$ ($X\sim P(\lambda)$)

* Các tham số đặc trưng:
	* $EX = λ$ 
	* $VX =λ$
	* $λ − 1 ≤ mod(X) ≤ λ$

> [!warning] Chú ý
> Khi n lớn và p nhỏ (n > 50; p < 0,1) thì $X\sim B(n;p)$ có thể chuyển thành $X\sim P(\lambda)$ với $\lambda = np$

### 3.3 Phân phối chuẩn
> [!info] PP chuẩn
> Biến ngẫu nhiên X được gọi là tuân theo pp chuẩn với hai tham số  $\mu$ và $\sigma^2$ với $\sigma > 0$ ($X\sim N(\mu, \sigma^2)$)
> $$
> f(x) = \frac{1}{\sigma \sqrt{2\pi}}.e^{-\frac{(x-\mu)^2}{2\sigma^2}}
> $$

* Các tham số đặc trưng:
	* $EX = µ$
	* $V X = σ^2$
	* $mod(X) = med(X) = µ$

> [!hint] Mục tiêu
> Tính xác suất dạng $P(a < X < b)$

#### 3.3.1 Phân phối chuẩn tắc
Với $X \sim N(0;1)$ ($\mu = 0, \sigma = 1$) -> PP chuẩn tắc (hay chuẩn hóa)

> [!note] Phân phối chuẩn tắc 
> #xstk_fomula 
> * **Hàm mật độ xác suất (hàm mật độ Gauss)**:
> $$
> \varphi(x) = \frac{1}{\sqrt{2\pi}}* e^{- \frac{1}{2}*x^2}
> $$
> * **Hàm Laplace**: (để tính xác suất)
> $$
> \phi(x) = \int^x_0 \varphi(t)dt
> $$

**Tính chất:**
* $\phi(x)$ là hàm lẻ, tăng thực sự.
* $\phi(inf) = 0,5$
* $X \sim N(0;1)$ có $P(a < X < b) = \phi(b) - \phi(a)$
* Giá trị của hàm Laplace  được tính sẵn thành bảng số liệu

#### 3.3.2 Phân phối chuẩn tổng quát

> [!note] Phân phối chuẩn tổng quát
> #xstk_fomula 
> Nếu  $X \sim N(\mu;\sigma^2)$ $(Z = \frac{X - \mu}{\sigma} \sim N(0;1))$
> * $P(X < a) = 0,5 + \phi(\frac{a - \mu}{\sigma})$
> 
> * $P(X > a) = 0,5 - \phi(\frac{a - \mu}{\sigma})$
> * $P(a \leq X < b) = \phi(\frac{b - \mu}{\sigma})- \phi(\frac{a - \mu}{\sigma})$
> * $P(|X - \mu| < \varepsilon) = 2\phi(\frac{\varepsilon}{\sigma})$

Hình ảnh minh họa cho tính đối xứng của pp chuẩn
![[Pasted image 20230606214458.png]]

![[Pasted image 20230430164642.png]]

#### 3.3.3 Xấp xỉ phân phối nhị thức bằng phân phối chuẩn
Với $X \sim B(n;p)$ thỏa mãn đk $VX = np(1-p) > 20$
Khi đó: $X \sim N(\mu,\sigma^2)$ ($\mu = np, \sigma^2 = np(1-p)$)

  > [!warning]
  > Vì xấp xỉ một phân phối rời rạc bằng một phân phối liên tục.
  > -> **Cần sự hiệu chỉnh để giảm sai số.**

> [!note] Giảm sai số xấp xỉ pp nhị thức -> pp chuẩn
> #xstk_fomula 
> $$
> P(X = k) = \phi(\frac{k + 0,5 -\mu}{\sigma}) - \phi(\frac{k + 0,5 -\mu}{\sigma})
> $$
> $$
> P(k_1\leq X \leq k_2) = \phi(\frac{k_2 + 0,5 -\mu}{\sigma}) - \phi(\frac{k_1 - 0,5 -\mu}{\sigma})
> $$

![[Pasted image 20230430171144.png]]

### 3.4 Phân phối mũ
> [!info] PP mũ
> #xstk_fomula 
> Biến ngẫu nhiên X tuân theo pp mũ với tham số $\lambda > 0$ nếu có hàm mật độ xác suất có dạng:
> * $f(x) = \lambda e ^{- \lambda x}$ với $x >0$
> * $f(x) = 0$ với $x \leq 0$
> 
> Kí hiệu: $X \sim \varepsilon (\lambda)$

Các tham số đặc trưng:
* $EX = \frac{1}{\lambda}$
* $VX = \frac{1}{\lambda^2}$

> [!note] Tính chất: không nhớ
> * Nếu một biến ngẫu nhiên T có pp mũ, xác suất điều kiện phải thỏa mãn 
> $$
> P(T > s + t|T> t) = P(T>s) \text{ for all s, t > 0}
> $$

*Ví dụ: Ta cần đợi 10 phút nữa trước khi cú điện thoại tiếp theo được gọi đến, biết rằng ta đã đợi 30p. Không khác gì ta cần đợi 10 phút nữa cho đến khi cú điện thoại tiếp theo được gọi đến, biết rằng ta vừa bắt đầu quá trình đợi.*

> [!note] Bổ sung
> ![[Pasted image 20230523233755.png]]

### 3.5 Phân phối Khi bình phương
> [!info] PP Khi bình phương
> Giả sử $X_i,(i =1,2,3,...n)$ là các biến ngẫu nhiên độc lập cùng phân phối chuẩn tắc. Biến ngẫu nhiên $Y = \sum ^n _{i =1}X_i^2$ được gọi là tuân theo phân phối Khi bình phương với n bậc tự do. ($Y\sim \chi^2(n)$)

Các tham số đặc trưng:
* $EY = n$
* $VY = 2n$

### 3.6 Phân phối Student
> [!info] PP Student
> #xstk_fomula 
> Giả sử $X \sim N(0;1)$ và $Y\sim \chi^2(n)$ là hai biến ngẫu nhiên độc lập. Khi đó:
> $$
> T = \frac{X}{\sqrt{\frac{Y}{n}}}
> $$
> được gọi là tuân theo phân phối Student với n bậc tự do. ($T\sim T(n)$)

Các tham số đặc trưng:
* $ET = 0$
* $VT = \frac{n}{n-2}$

> [!caution] Về việc sử dụng pp Student
> * PP Student có cùng dạng và tính đối xứng như pp chuẩn nhưng nó phản ánh tính biến đổi của phân phối sâu sắc hơn. PP chuẩn không thể dùng để xấp xỉ phân phối khi mẫu có kích thước nhỏ. Trong TH này, ta sử dụng pp Student.
> * Khi bậc tự do n tăng lên (n > 30) thì phân phối Student tiến nhanh về phân phối chuẩn. Do đó khi n > 30 thì ta có thể dùng phân phối chuẩn thay cho phân phối Student.