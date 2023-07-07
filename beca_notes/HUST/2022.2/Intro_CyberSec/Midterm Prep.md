> [!note] Bài 1
> Xét $g = (E,D)$ là một hệ mã **an toàn ngữ nghĩa** trên $(K,M, C)$ với  $M = \{0, 1\}^L$. Hệ mã nào dưới đây cũng là an toàn ngữ nghĩa? Nếu an toàn hãy đưa ra một chứng minh, nếu ko hãy đưa ra một cách tấn công.
> (a). $E_1(k,m) := 0 || E(k,m)$
> (b). $E_2(k,m) := E(k,m) || parity(m)$
> Ở đây, cho xâu bit $s$,  $parity(s)$ bằng 1 nếu số lượng 1 trong s là lẻ, và bằng 0 ngược lại.

Hệ an toàn về mặt ngữ nghĩa là khi có hai thông điệp có độ dài như nhau, ta không thể suy ra thông điệp gốc từ bản mã. (Có thể có nhiều cặp thông điệp gốc khác nhau nhưng cho ra cùng một bản mã)
* Với định nghĩa như trên, $E_1(k,m)$ là an toàn về mặt ngữ nghĩa.
	* G/s có $m_1$ và $m_2$ là hai thông điệp có độ dài như nhau ($m_1 \neq m_2$), sao cho $E(k, m_1) = E(k,m_2)$ (ko thể phân biệt được bản mã).
		-> Việc thêm bit 0 vào đầu hai bản mã cũng sẽ có kết quả tương tự
* Nhưng $E_2(k,m)$ không an toàn về mặt ngữ nghĩa, vì có thể phân biệt được bản mã của hai thông điệp (trong trường hợp thông điệp $m_1,m_2$ có số lượng 1 khác nhau)


> [!note] Bài 2
> Muốn xây dựng một hệ mã khối $g = (E,D)$ từ hai hệ mã khối $g_1=(E_1, D_1)$ và $g_2 = (E_2, D_2)$ sao cho nếu  ở một thời gian điểm nào đó trong tương lai một trong hai (ko phải cả hai) hệ $g_1$ hoặc $g_2$ bị phá thì hệ $g$ vẫn an toàn. Giả sử cả $g_1$ và $g_2$ được định nghĩa $(K, X)$. Ta định nghĩa $g$ như sau: 
> * $E((k_1,k_2), x) := E_1(k_1, E_2(k_2, x))$
> * $D((k_1, k_2),y) := D_2(k_2, D_1(k_1,  y))$
> Chứng minh rằng $g$ an toàn nếu $g_1$ hoặc $g_2$ an toàn.

Một hệ mã khối an toàn khi không thể suy ra thông tin về thông điệp gốc từ  bản mã.

G/s g1 là an toàn, cần chứng minh rằng với g, không thể suy ra thông điệp gốc từ bản mã.

Gọi $x'= D_1(k_1, y)$. Vì $g_1$ là an toàn -> không thể suy ra thông tin về $x'$ từ $y$ và $k_1$. -> Kẻ tấn công không thể suy ra thông điệp gốc $x$ từ bản mã $y$ và hai khoá $(k_1, k_2)$

Chứng minh tương tự cho trường hợp g2 là an toàn.

=> Hệ g an toàn với điều kiện 1 trong 2 hệ $g_1,g_2$ an toàn

> [!note] Bài 4
> Giả sử H và H' là các **hàm băm kháng xung đột**. Hàm băm H'' trong mỗi câu dưới đây có kháng xung đột hay không? Giải thích.
> (a) $H''(x) = H(x)||0...0$
> (b) $H''(x) = H(H'(x))$
> (c) $H''(x) = H(x)||H'(x)$
> (d) $H''(x) = H(x)\oplus H'(x)$

Xung đột là  khi một cặp $m_0 \neq m_1 \in M: H(m_0) = H(m_1)$

(a) có kháng xung đột, vì $H(x_1) \neq H(x_2) \rightarrow H(x_1)|| 0...0 \neq H(x_2)|0...0$
(b) $x_1 \neq x_2$ && H' là hàm băm kháng xung đột $\rightarrow H'(x_1)\neq H'(x_2)$
* Đặt m = H'(x1), m' = H'(x2) -> $m\neq m'$
* Lại có H cũng là hàm băm kháng xung đột -> $H(m)\neq H(m')$ 
=> H''(x) có kháng xung đột
(c) Chứng minh phản chứng: để H'' không phải là hàm băm kháng xung đột -> tồn tại cặp $m_0 \neq m_1$ sao cho $H''(m_0) = H''(m_1)$
<=> $H(m_0) || H'(m_0) = H(m_1)||H'(m_1)$
Mà lại có H, H' là các hàm băm kháng xung đột -> $H(m_0) \neq H(m_1)$ && $H'(m_1) \neq H'(m_0)$ -> $H(m_0) || H'(m_0) \neq H(m_1)||H'(m_1)$
=> Phản chứng có H'' là hàm băm kháng xung đột.

(d) H''(x) không phải là hàm băm kháng xung đột, lấy ví dụ dẫn chứng:
Lấy H(m_0) = 101000, H'(m_0) = 000101
101000
000101
101101 $= H(m_0) \oplus H'(m_0) = H''(m_0)$
Lấy H(m_1) = 100001, H'(m_1) = 001100
-> $H''(m_1) = 101101 = H''(m_0)$
(Có thể coi $m_0 \neq m_1$)

> [!note] Bài 5 (chương 7)
> Giả sử $(E,D)$ là một hệ mã có xác thực với không gian khoá $K$, không gian bản rõ $\{0,1\}^n$ và không gian bản mã $\{0,1\}^s$. Hệ mã trong mỗi câu dưới đây có xác thực hay không? Hãy giải thích.
> 
> * (a). $E'((k_1,k_2), m) = E(k_2, E(k_1,m))$ và $D'((k_1, k_2), c) = D(k_1, D(k_2,c))$ nếu $D(k_2, c) \neq \perp$ hoặc $=\perp$ nếu ngược lại
> * (b) $E'(k,m) = [c \leftarrow E(k,m), output (c,c)]$ và $D'(k, (c_1,c_2)) = D(k,c_1)$ nếu $c_1 = c_2$ hoặc $=\perp$ nếu ngược lại

*($\perp$ là biểu thị giá trị không xác định, không tồn tại)*
![[Pasted image 20230705154136.png]]

![[Pasted image 20230705155751.png]]

(a). $E'((k_1,k_2), m) = E(k_2, E(k_1,m))$ và $D'((k_1, k_2), c) = D(k_1, D(k_2,c))$ nếu $D(k_2, c) \neq \perp$ hoặc $=\perp$ nếu ngược lại.
* Hệ sử dụng khoá $k_1$ để mã hoá thành 1 bản mã trung gian, sau đó sử dụng $k_2$ để mã hoá bản mã trung gian thành bản mã cuối cùng c
* Thuật toán giải mã kiểm tra xem $D(k_2,c)$ có phải hợp lệ hay không
	* Nếu khác $\perp$, quá trình giải mã bằng khoá $k_2$ thành công, thuật toán tiếp tục giải mã bằng khoá k1
	* Nếu giải mã trả về kết quả không xác thực -> c không hợp lệ -> thuật toán từ chối giải mã và trả về giá trị không hợp lệ.

(b) 
* Giải thích quá trình mã hoá: 
	* Sử dụng khoá k để mã hoá m thành 1 bản mã c
	* Sau đó tạo ra một cặp giá trị (c,c) giống nhau làm đầu ra.
	-> thông điệp xác thực không cung cấp bất cứ thông tin xác thực nào về bản mã.
* Quá trình giải mã sẽ chỉ chấp nhận giải mã với c1 = c2, nếu không sẽ trả về không xác định. (Không có bất cứ bước xác thực nào)
=> Hệ không đáp ứng đủ yêu cầu của một hệ mã có xác thực.

>[!note] Bài 6
> Xét $F: \{0,1\}^n * \{0,1\}^n \rightarrow \{0,1\}^n$ là một PRP an toàn. Ta xây dựng sơ đồ mã hoá $E(k,m)$ từ $F$ như sau:
> * Thông điệp m được chia thành các khối n-bit $m = m_1 || m_2 || ... || m_i$
> * Chọn ngẫu nhiên một số n-bit $r$.
> * Output $r || F(k, r + 1 + m_1) ||  F(k, r + 2 + m_2) || ... || F(k,r + t + m_i)$
> 
> Phương pháp nào sau đây Attacker có thể sử dụng để chỉ ra rằng sơ đồ mã trên **không phải** là CPA (Chosen-Plaintext Attack) an toàn? Hãy giải thích.
> 1. Lấy một n-bit block $m$ bất kỳ; và gửi $M_0 = m || m$ và $M_1 = m || m - 1$ nhận được bản mã $r || c_1 || c_2$. Quyết định output 1 <=> $c_1 = c_2$
> 2. Lấy hai n-bit block $m, m'$ bất kỳ; và gửi $M_0 = m || m$ và $M_1 = m || m'$ nhận được bản mã $r || c_1 || c_2$. Quyết định output 1 <=> $c_1 = c_2$
> 3. Lấy một n-bit block $m$ bất kỳ; và gửi $M_0 = m$ và $M_1 = m || m$ . Quyết định output 0 <=> bản mã nhận được chứa 2 blocks.
> 4. Chọn ngẫu nhiên 4 n-bit blocks $m_1, m_2, m_3, m_4$ và gửi $M_0 = m_1 || m_2$ và $M_1 = m_3 || m_4$. Nhận được bản mã $r||c_1||c_2$. Quyết định output 0 nếu và chỉ nếu $r=0 ... 0$

![[Pasted image 20230705165944.png]]

> [!note] Bài 7
> Giả sử có n + 1 bên, gọi là $B, A_1, ..., A_n$, muốn có một khoá chung cho cả nhóm. Họ muốn có một giao thức sao cho mọi người đều có chung 1 khoá bí mật, nhưng kẻ nghe lén dù thấy được toàn bộ quá trình trao đổi vẫn không xác định được k.
> Các bên thống nhất một nhóm $G$ có cấp nguyên tố $q$ với phần tử sinh $g$ và dùng giao thức sau đây:
> * Mỗi A, chọn một số ngẫu nhiên $a_i$ thuộc $\{1, ..., q\}$ và gửi cho B giá trị $X_i \leftarrow g^{a_i}$
> * Bên B sinh một số ngẫu nhiên $b$ thuộc $\{1, ..., q\}$ và gửi trả lại $A_i$ thông điệp $Y_i \leftarrow X_i^b$
> 
> Khoá cuối cùng của nhóm là $g^b$. Rõ ràng $B$ có thể tính được khoá này. Các $A_i$ tính khoá này ntn? Giải thích.

> [!note] Bài 8
> Nhắc lại rằng hoán vị cửa sập RSA được định nghĩa trong nhóm $Z_N ^*$ với N là tích của hai số nguyên tố lớn. Khoá công khai là $(N,e)$ và khoá bí mật $(N,d)$ với d là nghịch đảo của $e$ trong $Z^*_{\varphi(N)}$.
> Giả sử  trong thuật toán RSA, thay vì lấy $N$ là hợp số bạn lại chọn $N=p$ là số nguyên tố. Hãy chỉ ra rằng trong trường hợp này mọi người đều có thể tính hoặc không tính được khoá bí mật $(N,d)$ từ khoá công khai $(N,e)$ bằng mỗi cách tính dưới đây. Giải thích ngắn gọn
> 1. $d \leftarrow -e \text{(mod p)}$
> 2. $d \leftarrow e^2 \text{(mod p)}$
> 3. $d \leftarrow e^{-1} \text{(mod p)}$
> 4. $d \leftarrow e^{-1} \text{(mod p-1)}$
