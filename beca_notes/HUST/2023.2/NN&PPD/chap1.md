Chương trình nguồn (NNLTBC) -- [Compiler] --> Chương trình đích
                            (Thông báo lỗi)

* Chương trình có thể cần liên kết đến các thư viện để thực hiện chương trình.

* Thông dịch (Interpreter): giải thích chương trình nguồn, lần lượt trực tiếp theo từng lệnh
    - Size <<
    - Run Speed <<

```shell
[Source program]
| (Compiler)
v
[Intermediate program]
| (Interpreter)
v
[Result]
```
_Thông dịch mã trung gian_

$T_M^{S -> T}$: 
- Chương trình dịch trên máy có cài ngôn ngữ M

- Chương trình đầu vào viết bằng S --(dịch)--> chương trình đầu ra bằng T

### Bootstrapping
> Sử dụng đầu vào chương trình chính là nó

**Yêu cầu** viết $T_M^{L -> M}$ (dịch từ ngôn ngữ L ra ngôn ngữ máy)
- Dùng mã máy M viết L' là tập con của L
    -> Viết ra $T_M^{L' -> M}$

- Dùng L' để viết CTD L -> M 

- Dùng L' làm đầu vào của $T_M^{L' -> M}$, từ đó có thể dịch L -> M qua ngôn ngữ cài đặt M

### Cross Compiling
> Xây dựng chương trình dịch cho ngôn ngữ đã tồn tại, trên loại máy tính mới. Không sử dụng mã máy

**Yêu cầu** xây dựng CTD $T_{BK}^{C -> BK}$ nhưng BK là loại máy, chưa có.
Đã có $T_{PC}^{C -> PC}$
-> Xây dựng $T_{PC}^{C -> BK}$
- B1: Dùng Bootstrapping xây dựng CTD $T_{PC}^{C -> BK}$
- B2: Dùng Bootstrapping xây dựng CTD $T_{BK}^{C -> BK}$

## 2. Các thế hệ programming language

(Gần NN máy) Thấp --> Cao (gần NN tự nhiên)

**Các thành phần của NNLTCC**:
1. Từ vựng và cú pháp
2. Kiểu dữ liệu
3. Các đại lượng
4. Các tóan tử và biểu thức
5. Các câu lệnh
6. Chương trình con

### 2.1 Từ vựng và cú pháp
* **Từ vựng**:
    - Chữ cái: A..Z, a..z
    - Chữ số: 0 .. 9
    - Dấu: đơn (+ - * / { }), kép (<= >=)
    - Từ khóa: riêng cho từng ngôn ngữ để khai báo, ra lệnh
* **Cú pháp**: các quy tắc để viết ra các đại lượng và các câu lệnh

### 2.2 Kiểu dữ liệu
* **Kiểu cơ bản**: int, float, char, boolean
 
* **Kiểu dữ liệu có cấu trúc**: arr, str, file, pt*

### 2.3 Các đại lượng
* **Hằng**: số nguyên, thực, chuỗi

* **Tên**: nguyên tăc đặt, độ dài

### 2.4 Các tóan tử và biểu thức
* **Tóan tử**:
    - Số học: cộng trừ nhân chia
    - Logic: OR, AND, XOR, \==, != , >, <

* **Biểu thức**: kết hợp toán hạng với tóan tử
    - Số học: trả về con số
    - Logic: trả về giá trị boolean
    - Xâu: trả về string
### 2.5 Các câu lệnh
* **Câu lệnh tuần tự**: gán, vào ra, gọi hàm, begin - end

* **Câu lệnh rẽ nhánh**: if, else, switch

* **Câu lệnh lặp**: for, while, do while

### 2.6 Chương trình con
* Các dạng: trả về giá trị (return), void

* Truyền params: theo trị (không đổi), theo địa chỉ (có đổi)

* Địa phương/toàn cục

## 3. Các giai đọan chính của CTD
```shell
[Phân tích từ vựng] --> [Phân tích cú pháp (ngữ nghĩa)] --> [Sinh mã] 
```

```shell
Bảng ký hiệu : --> {*} <-- Xử lý lỗi
*:
_Chương trình nguồn_
|
v
Phân tích từ vựng
|
v
Phân tích cú pháp
|
v
Phân tích ngữ nghĩa
|
v
Sinh mã trung gian
|
v
Tối ưu mã
|
v
Sinh mã máy
|
v
_Chương trình đích_

```

### 3.1 Bảng kí hiệu
> **Bảng kí hiệu** - ctdl chứa tên và thuộc tính cần thiết (vị trí, kiểu, phạm vi)

* Khi chỉ ra được tên:
    - Đưa tên và thuộc tính vào bảng
    - Lấy thông tin của tên trong bảng ký hiệu

### 3.2 Phân tích từ vựng (Lexical Analysis)

* Duyệt từng ký tự của chương trình nguồn
    - Loại bỏ ký tự thừa
* Xây dựng các từ vựng từ các ký tự đọc được
* Nhận dạng các **token** các từ vựng
---
> **Token (Từ tố)** - đơn vị cú pháp không thể chia nhỏ hơn nữa
* Các từ tố có thể do người viết CTD tự đặt ra để dễ dàng trong việc mã hóa chương trình 

---

* Chuyển các token cho pha kế tiếp

### 3.2 Phân tích cú pháp (Syntax Analysis)
* Phân tích ct nguồn dựa vào các từ tố nhận được
    - Thể hiện dưới dạng: đệ quy, BNF, sơ đồ
* Kiểm tra các từ tố có tuân theo nguyên tắc cú pháp (syntax)

--> Kết quả: 
- Cây phân tích cú pháp (chương trình đã đúng syntax)
- Thông báo lỗi

![[chap1-20240514142535307.webp]]

![[chap1-20240514142634992.webp]]

---
>**Cây cú pháp (Syntax tree)**: các nút trong là các tóan từ, các tóan hạng là các nút lá

![[chap1-20240514142730779.webp]]

---

### 3.3 Phân tích ngữ nghĩa (Semantic Analysis)
* Kiểm tra lỗi ngữ nghĩa của chương trình

Ex: nếu hằng số được gán giá trị khác -> sai ngữ nghĩa

* Kiểm tra kiểu tóan hạng có phù hợp tóan tử

Ex: % đòi hỏi toán hạng nguyên
_Tuy nhiên, cũng sẽ có các trường hợp tóan tử chấp nhận tóan hạng khác kiểu, nhờ có chuyển kiểu tự động_

* Lấy thông tin về kiểu của danh biểu, dùng cho giai đọan sinh mã

### 3.4 Sinh mã
#### 3.4.1 Sinh mã trung gian
* Mã nguồn --> Ctr trong NN trung gian
    - Thuận lợi khi cần thay đổi cách biểu diễn
    - Tối ưu hóa mã độc lập cho máy đích cho dạng biểu diễn trung gian
    - Giảm thời gian thực thi chương trình (mã trung gian được tối ưu)

* Ngôn ngữ trung gian thường được dùng: mã 3 địa chỉ

---
> **Mã 3 địa chỉ** - mỗi câu lệnh có nhiều nhất 3 toán hạng, 2 tóan tử (1 trong đó là tóan tử gán)

* CTD sinh ra biến tạm chứa giá trị tính tóan sau mỗi lệnh
---

#### 3.4.2 Tối ưu mã
* Tối ưu về kích thước, tốc độ

Ex: `Int2Real()` được thay bằng số thực tại tđ dịch ...

#### 3.4.3 Sinh mã đích
* Tạo chương trình thực thi:

Trình tự:
1. Các biến được cấp ô nhớ cụ thể
2. Các câu lệnh trung gian được thay bằng mã máy tương đương
3. Các biến được ấn định cho các thanh ghi

### 3.5 Xử lý lỗi
* Lỗi có thể gặp trong mọi pha của CTD

* Khi gặp lỗi, CTD cần thông báo: kiểu lỗi, vị trí gây lỗi

* Cần hồi phục sau khi gặp lỗi
    - Tiến hành tiếp tục phân tích
    - (Có thể) Thông báo không chính xác

## 4. Khái niệm ngôn ngữ
> Là tập hợp các câu có cấu trúc, với các câu là tập hợp các từ có cấu trúc quy định cách thức tạo thành câu

### 4.1 Kiến thức toán học liên quan
* **Tập hợp**: tập các phần tử không lặp lại
    * **Tập lũy thừa**: tập các tập con của 1 tập

Ex: tập lũy thừa 2 của A = $2^A$

* Các phép tóan: hợp, giao, hiệu, tích descarter

* **Quan hệ**: tập con `|R` của tích descarter các tập
    - Quan hệ 2 ngôi: tập con của tích descarter 2 tập

Ex: a $\in$ A, b $\in$ B => $(a,b)\in A x B$ là quan hệ 2 ngôi.
(a,b) in R -> `a |R b`

* **Hàm**: mối quan hệ trên tích descarter $DxR$
    - $\forall d \in D$, $\exists$ nhiều nhất 1 cặp $(d,r) \in DxR$
    - _D_ - miền xác định
    - _R_ - miền giá trị
    -> $f(d) = r$

- Hàm xác định khi D và R là những tập xác định và có thể biểu diễn bằng bảng các cặp $\{(d,r)\}$
- Hàm n biến vào, m biến ra
    + Miền xác định là tích descarter của n tập
    + Miền giá trị là tích descarter của m tập

* **Đồ thị**:

* **Cây**:

### 4.2 Bộ chữ và xâu kí hiệu
#### 4.2.1 Bộ chữ
> **Bộ chữ** - tập hợp các thành phần được gọi là ký hiệu

Ex: bảng chữ cái, bộ điển, keywords của nnlt

#### 4.2.2 Xâu ký hiệu
> Dãy liên tiếp các kỹ hiệu của một bộ chữ

Ex: $\alpha$ : Madam
    $\beta$ : Hom_nay_troi_dep  _xâu trong tiếng việt_
    $\gamma$ : while (a > b) a = a -b _xâu trong NNLT_

* Độ dài xâu: $|\alpha|$ hoặc $|(\alpha)$

* Đảo ngược xâu: $\alpha^R$

* Xâu con

* Ghép xâu: $\alpha$ `concat` $\beta$

* Xâu lũy thừa: lũy thừa n = ghép n xâu ($\alpha^n$)

---
**Tính tóan trên tập xâu**
A, B là tập xâu trên 1 bộ chữ

* _Hợp_: A $\cup$ B (hoặc)

* _Giao_: A $\cap$ B (và) 

* _Tích/Ghép_: $AB = \{x = \alpha * \beta | \alpha \in A \text{ và } \beta \in B\}$

* _Tích descarter_: $A x B = \{<\alpha, \beta> | \alpha \in A \text{ và } \beta \in B\}$

* _Lũy thừa_:

* _Bao đóng_: bao gồm $A^0$ (kí hiệu $A^*$)
    * Bao đóng dương: không bao gồm $A^0$ ($A^+$)


---

### 4.3 Văn phạm (Grammar) 
$$
G = (V_T, V_N, P, S)
$$

- $V_T$: tập các kí hiệu kết thúc của một bảng chữ (kí hiệu a,b,c)
- $V_N$: tập các kí hiệu không kết thúc của bảng chữ (kí hiệu A,B,C)
$$
    V_T \cap V_N = \oslash
$$
$$
    V = V_T \cup V_N: \text{bộ chữ của văn phạm}
$$
- $S$: kí hiệu bắt đầu
    $S \in V_N$
- $P$: tập hữu hạn các cặp ($\alpha, \beta$) được gọi là các **quy tắc (sản xuất)** (kí hiệu $\alpha \rightarrow \beta$)
    $\alpha \in V^* V_N V^*$ (*có ít nhất 1 ký hiệu không kết thúc*)
    \beta thuộc V* (*có thể chứa sâu rỗng*)

Ex: $G_1 = (V_T, V_N, P, S)$
$V_T = \{a, b, c\}$
$V_N = \{S, A\}$
$P = {S \rightarrow aSA, S \rightarrow b, A \rightarrow bA, A \rightarrow c}$

### 4.4 Suy dẫn
Cho văn phạm G

> $\gamma$ viết ra (suy dẫn trực tiếp ra) $\delta$ (Kí hiệu $\gamma => \delta$)
> nếu tồn tại các sâu $\alpha, \beta, v, w$ thỏa mãn các điều kiện

$$
    \gamma = \alpha v \beta
$$
$$
    \delta = \alpha w \beta
$$
/‌‌‌‌‌‌/ Do $v \rightarrow w$ là một sản xuất của P.
$$
(v,w) \in P \text{ (có thể viết v -> w thuộc P)}
$$
$$
    \alpha, \beta \in V^*, v \in V^* V_N V^*, w \in V^*
$$

Ex: với văn phạm $G_1: aSc => abc$
$\alpha = a$
$\beta = c$
$v = S$
$w = b$
lại có $S \rightarrow b \in P$

* Cho văn phạm G, \delta được suy dẫn từ \gamma nếu tồn tại dãy các sâu $\alpha_0, \alpha_1,\alpha_2 ... \alpha_n$ thỏa mãn:
$$
    \gamma = \alpha_0 => \alpha_1 => \alpha_2 ... => \alpha_n = \delta
$$
- n >= 1: áp dụng ít nhất 1 bước suy dẫn, $\gamma =>^+ \delta$
- n >= 0: có thể không áp dụng suy dẫn, $\gamma =>^* \delta$

![[chap1-20240514131521734.webp|598]]

### 4.5 Câu
Cho văn phạm G
	* Xâu được suy ra từ S -> dạng câu, dạng cú pháp
	* Dạng cú pháp toàn ký hiệu kết thúc -> một câu

$$
S =>^* \delta \text{ và } \delta \in V_T^*
$$

![[chap1-20240514133836581.webp]]

### 4.6 Ngôn ngữ
> là tập (các xâu) của một bộ chữ

* Tập rỗng (\epsilon) là ngôn ngữ trên mọi bộ chữ

=> Có thể tạo ngôn ngữ mới từ các nn đã có bởi sử dụng toán tử tập

* Một số tính chất:
    - $L^+ = L L^* = L^* L$
    - $L* = L^+ \cup \{\epsilon\}$

#### Ngôn ngữ sản sinh
* Ngôn ngữ L được sinh ra từ G ($L(G)$):
$$
L(G) = \{\gamma | \gamma \in V_T^* \text{ và } S =>^* \gamma \}
$$

![[chap1-20240514135141621.webp]]

#### Quy ước:???

Ex:
![[chap1-20240514135647055.webp]]

### 4.7 Đệ quy

### 4.8 Phân loại văn phạm
> [!abstract] 
> - Văn phạm ngữ cấu
> - Văn phạm ngữ cảnh
> - Văn phạm phi ngữ cảnh
> -  Văn phạm chính quy 

## 5. Văn phạm phi ngữ cảnh

## 6. PL/0 mở rộng
