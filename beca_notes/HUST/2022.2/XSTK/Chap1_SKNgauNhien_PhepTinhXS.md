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

> [!note] Quy tắc cộng
> Một cv có thể chia là **k TH**: $k_1$ có $n_1$ cách giải quyết, $k_2$ - $n_2$ , ...
> -> Có $n_1 + n_2 + ... n_k$ cách giải quyết công việc trên

> [!note] Quy tắc nhân
> Một cv có thể chia là **k giai đoạn**: $p_1$ có $n_1$ cách giải quyết, $p_2$ - $n_2$ ...
> ->  Có $n_1*n_2* ... *n_k$ cách giải quyết cv

* BT: cần lấy ra k phần tử từ n phần tử
	* Có thứ tự:
		* Có lặp -> Chỉnh hợp lặp
		* Không lặp: -> chỉnh hợp lặp ( $n\neq k$ ) || Hoán vị ($n=k$)
	* Không có thứ tự:
		* Không lặp -> tổ hợp 

> [!note] Chỉnh hợp lặp
> $$
>\shadowbox{\makebox[1in][r]{\em a 1in}}
> $$

\begin{alignat}

\end{alignat}

> [!example] 
> *Có một tập hợp có n phần tử, có bao nhiêu cách để chia thành k nhóm với n1, n2, ... nk phần tử*
> -> có $\frac{n!}{(n+1-k)!}$ (Sai)
> Đáp án thầy: $\frac{n!}{n_1!*n_2!...*n_k!}$ (Đúng)

