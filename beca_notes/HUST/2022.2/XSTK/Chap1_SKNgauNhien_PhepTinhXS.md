BT: 
$$
\begin{eqnarray}
x = f(t,u)\\
x = v*t + n*u
\end{eqnarray}
$$
* Xây dựng mô hình `v`, `n` sao cho x gần với đáp án nhất
-> ***Ước lượng tham số***

* Để tìm được tuyến tính của pt $x = f(t)$ -> cực tiểu hoá
$$
\begin{eqnarray}
\sum_{i = 1}^{n}(x_i - v*t)^2 \rightarrow min \\
<=>\sum2(x_i - v*t) = 0\\
<=> \sum x_i - (\sum t_i)*v = 0
\end{eqnarray}
$$

* Trong trường hợp **không tuyến tính**

* ***Kiểm định***:
	* Mô hình
	* Tham số

**-> Kết quả đầu ra phụ thuộc rất nhiều vào dữ liệu đầu vào.**

## I. Giải tích kết hợp

> [!note] Quy tắc cộng
> #xstk_fomula
> Một cv có thể chia là **k TH**: $k_1$ có $n_1$ cách giải quyết, $k_2$ - $n_2$ , ...
> -> Có $n_1 + n_2 + ... n_k$ cách giải quyết công việc trên

> [!note] Quy tắc nhân
> #xstk_fomula 
> Một cv có thể chia là **k giai đoạn**: $p_1$ có $n_1$ cách giải quyết, $p_2$ - $n_2$ ...
> ->  Có $n_1*n_2* ... *n_k$ cách giải quyết cv

* BT: cần lấy ra k phần tử từ n phần tử
	* Có thứ tự:
		* Có lặp -> Chỉnh hợp lặp
		* Không lặp: -> chỉnh hợp ( $n\neq k$ ) || Hoán vị ($n=k$)
	* Không có thứ tự:
		* Không lặp -> tổ hợp 

> [!note] Chỉnh hợp lặp
> #xstk_fomula 
> Một tập hợp có n phần tử, có bao nhiêu cách chọn để có được dãy k phần tử (có thứ tự, có thể lặp lại)
> = A~k_n = n^k

> [!note] Chỉnh hợp
> #xstk_fomula 
> Chập k của n phần tử (k $\leq$ n) là số cách chọn k phần tử:
> * Có thứ tự
> * Không lặp lại 
> $$
> A^k_n = \frac{n!}{(n-k)!}
> $$

> [!note] Hoán vị
> #xstk_fomula 
> Số cách sắp xếp n phần tử đã cho theo một thứ tự nhất định
> $P_n = n!$

> [!note] Tổ hợp
> #xstk_fomula 
> Tổ hợp chập k của n phần tử (n $\geq$ k)
> * Không có thứ tự
> * Không lặp lại
> $$
> C^k_n = \frac{A^k_n}{k!} = \frac{n!}{(n-k)!*k!}
> $$

> [!example] 
> *Có một tập hợp có n phần tử, có bao nhiêu cách để chia thành k nhóm với n1, n2, ... nk phần tử*
> -> có $\frac{n!}{(n+1-k)!}$ (Sai)
> Đáp án thầy: $\frac{n!}{n_1!*n_2!...*n_k!}$ (Đúng)

*Ex: Sắp xếp 5 quyển sách khác nhau vào 3 ngăn sao cho mỗi ngăn có ít nhất 1 quyển sách
B1. Đếm số cách đưa 5 quyển sách vào 3 ngăn
B2. Đếm số cách đưa 5 quyển sách sao cho có đúng 1 ngăn trống
b2.1 chọn 1 ngăn trống
b2.2 xếp 5 quyển sách vào 2 ngăn sao cho mỗi ngăn có ít nhất 1 quyển
b2.2.a Đếm số cách xếp 5 q vào 2 ngăn 
b2.2.b Trừ số cách xếp 5 q sách vào 1 ngăn
B3. Đếm số cách đưa 5 quyển sách sao cho có đúng 2 ngăn trống*

==-> Quá dài dòng==


## II. Sự kiện và các phép toán

> [!info] Định nghĩa
> * ***Phép thử*** - Việc thực hiện một nhóm các điều kiện cơ bản để quan sát một hiện tượng nào đó.
> * ***Kết cục*** - Kết quả của phép thử mà không thể chia nhỏ hơn
> * ***Không gian mẫu*** ($\ohm$)- tập gồm tất cả các kết cục
> * ***Sự kiện*** (A,B,C ...) - tập con của không gian mẫu

* **Sự kiện sơ cấp** - sự kiện không thể phân tích được nữa
* **Sự kiện chắc chắn** - sự kiện luôn xảy ra trong phép thử ($\ohm$)
* **Sự kiện không thể** - sự kiện không bh xảy ra khi thực hiện phép thử ($\emptyset$)
* **Sự kiện ngẫu nhiên** - Sự kiện có thể xảyg ra hoặc không khi thực hiện phép thử
* **Phép thử ngẫu nhiên** - phép thử mà các kết quả là các sự kiện ngẫu nhiên.

### Quan hệ của các SK
> [!note] Quan hệ kéo theo
> #xstk_fomula 
> Nếu A xảy ra thì B xảy ra: $A\subset B$ hoặc $A => B$
> ![[Pasted image 20230327003334.png]]

> [!note] Quan hệ tương đương
> #xstk_fomula 
> Nếu $A => B$ && $B => A$: $A <=> B$ hoặc $A = B$ 

> [!note] Sự kiện TỔNG
> #xstk_fomula 
> C là tổng A và B khi C xảy ra, khi và chỉ khi, ít nhất 1 trong 2 sự kiện A,B xảy ra : $C = A + B$
> ![[Pasted image 20230327003558.png]]

> [!warning]
> * Mọi sự kiện ngẫu nhiên dều có thể biểu diễn được dưới dạng tổng của một số sự kiện sơ cấp.
> 
> * Sự kiện chắc chắn ($\ohm$) là **tổng** của mọi sự kiện sơ cấp có thể, hay còn được gọi là **Không gian các sự kiện sơ cấp**

> [!note] Sự kiện TÍCH
> #xstk_fomula 
> C là tích của A và B, C xảy ra khi và chỉ ra cả A và B cùng xảy ra : $C = A*B$
> -> Mở rộng với tích n sự kiện $A_1A_2A_3 ... A_n$ chỉ xảy ra khi cả n sự kiện cùng xảy ra
> ![[Pasted image 20230327004133.png]]

> [!note] Sự kiện ĐỐI LẬP
> #xstk_fomula 
> Sự kiện đối lập của A là $\overline{A}$, là sự kiện xảy ra khi A không xảy ra.
> ![[Pasted image 20230327004248.png]]

> [!note] Sự kiện HIỆU
> #xstk_fomula 
> C là hiệu của A và B, là sự kiện xảy ra khi và chỉ khi A xảy ra nhưng B không xảy ra: $C = A - B$
> -> Tổng quát hoá, ta có công thức:
> $$
> A - B = A * \overline{B}
> $$
> ![[Pasted image 20230327004506.png]]

* Hai sự kiện A và B xung khắc khi chúng không đồng thời xảy ra trong cùng 1 phép thử: $A.B = \emptyset$

### Các phép toán sự kiện
#xstk_fomula 
> [!note]
> * **Giao hoán**:
> $$
> A + B = B + A
> $$
> $$
> A.B = B.A
> $$
> * **Kết hợp**:
> $$
> A + B + C = (A + B) + C = A + (B + C)
> $$
> $$
> A.B.C = (A.B).C = A.(B.C)
> $$
> * **Phân phối**
> $$
> A.(B+C) = A.B + A.C
> $$
> * **Đặc biệt**
> $$
> A + A = A; A + \ohm = \ohm; A + \emptyset = A; A.A = A; A.\ohm = A; A.\emptyset = \emptyset
> $$

## III. Các định nghĩa xác suất
> [!info] Xác suất
> $0 \leq P(A) \leq 1$ đo lường khả năng xuất hiện của sự kiện đó khi phép thử được thực hiện.

* Một số tính chất cơ bản:
	* $P(\ohm)=1$; $P(\emptyset)=0$
	* $P(A) + P(\overline{A})=1$

### Định nghĩa xác suất cổ điển

> [!note] Định nghĩa xác suất cổ điển
> #xstk_fomula 
> Một phép thử có hữu hạn kết cục, các kết cục có đồng khả năng xuất hiện.
> $$
> P(A) = \frac{n_A}{n_{\ohm}} = \frac{\text{Số kết cục thuận lợi}}{\text{Số kết cục có thể xảy ra}}
> $$

### Định nghĩa xác suất theo quan điểm hình học

> [!note] Định nghĩa xác suất theo quan điểm hình học
> #xstk_fomula 
> G\s tập hợp các kết cục đồng khả năng của một phép thử có thể biểu thị bởi một miền hình học $\ohm$ có độ đo (độ dài, diện tích, thể tích .. ) $\neq 0$, còn tập các kết cục thuận lợi cho sự kiện A là một miền A.
> $$
> P(A) = \frac{\text{Độ do của miền A}}{\text{Độ đo của miền } \ohm} = \frac{|A|}{|\ohm|}
> $$

###  Định nghĩa xác suất theo tần suất (thống kê)

> [!note] Định nghĩa xác suất theo tần suất
> #xstk_fomula 
> G\s một phép thử có thể thực hiện lặp lại nhiều lần trong những điều kiện giống nhau. Nếu trong n lần thực hiện, phép thử có m lần xuất hiện sự kiện A. Khi đó tần suất xuất hiện của sự kiện A trong n phép thử $f_n(A) = m/n$.
> Cho số phép thử tăng lên vô hạn:
> $$
> P(A) = lim_{n \rightarrow \infty}(A) = lim_{n \rightarrow \infty}\frac{m}{n}
> $$

> [!hint] Thực tế
> Với n đủ lớn, $P(A) \approx \frac{m}{n}$

> [!warning] 
> Xs theo freq chỉ được dùng cho các phép thử ngẫu nhiên, lặp lại nhiều lần một cách **độc lập** trong các điều kiện giống nhau.
> Việc thực hiện xác định tương đối chính xác giá trị của sx cần số lượng phép thử đủ lớn -> thời gian và chi phí

## IV. Một số công thức tính sx

> [!note] Công thức cộng XS
> #xstk_fomula 
> * Nếu A và B là hai sự kiện bất kì:
> $$
> P(A+B) = P(A) + P(B) - P(AB)
> $$
> * A và B là hai sự kiện xung khắc
> $$
> P(A+B) = P(A) + P(B)
> $$
> **Công thức cộng xác suất tổng quát** : cho n sự kiện ${A_i},i = \overline{1,n}$ 
> $$
> P(\sum^n_{i=1}A_i) = \sum_iP(A_i) - \sum_{i < j}P(A_iA_j) + \sum_{i < j < k}P(A_iA_jA_k) - ... + (-1)^{n-1}P(\prod_iA_i)
> $$
> **TH Đặc biệt:** các sự kiện xung khắc từng đôi
> $$
> P(\sum^n_{i=1}A_i) = \sum_iP(A_i)
> $$

> [!info] Xác suất có điều kiện
> Xác suất xảy ra sk A với điều kiện sk B đã xảy ra được gọi là *xác suất có điều kiện B của sự kiện A*: $P(A|B)$

> [!note] Công thức xs có điều kiện
> #xstk_fomula 
> $$
> P(A|B) = \frac{P(AB)}{P(B)}
> $$

Từ công thức xs có điều kiện, ta có được công thức nhân xs

> [!note] Công thức nhân sx
> #xstk_fomula 
> $$
> P(AB) = P(A|B).P(B) = P(B|A).P(A)
> $$
> A và B được gọi là ***Hai sự kiện độc lập*** nếu việc xảy ra hay không xảy ra sự kiện này không làm ảnh hưởng tới việc xảy ra hay không xảy ra sự kiện kia.
> $$
> P(A) = P(A|B) = P(A|\overline{B})
> $$
> $$
> \text{đồng thời } P(B) = P(B|A) = P(B|\overline{A})
> $$
> **-> Hai sự kiện A và B độc lập khi và chỉ khi: ==$P(AB) =  P(A).P(B)$**==
> <=> $\text{Các cặp sau độc lập: } (A,\overline{B});(\overline{A}, B);(\overline{A},\overline{B})$
> 
> **Công thức nhân tổng quát:** tích n sự kiện ${A_i}, i = \overline{1,n}$
> $$
> P(A_1A_2...A_n) = P(A_1).P(A_2|A_1).P(A_3|A_1A_2)...P(A_n|A_1A_2..A_{n-1})
> $$
> **TH đặc biệt:** với các sự kiện n độc lập tổng thể (sự xảy ra hay không xảy ra của một nhóm sự kiện bất kì không làm ảnh hưởng tới việc xảy ra hay không xảy ra của các sự kiện còn lại.)
> $$
> P(A_1A_2...A_n) = P(A_1).P(A_2).P(A_3)...P(A_n)
> $$

### Công thức Bernoulli

> [!info] Dãy phép thử Bernoulli
> Là việc tiến hành n phép thử độc lập, với mỗi phép thử chỉ xảy ra 1 trong 2 trường hợp:
> * Sự kiện A xảy ra
> * hoặc sự kiện A không xảy ra
> 
> Xác suất xảy ra sự kiện A trong mỗi phép thử luôn bằng p.

> [!note] Công thức Bernoulli
> #xstk_fomula 
> Xác  suất để sự kiện A xuất hiện đúng k lần trong n phép thử của dãy phép thử Bernoulli
