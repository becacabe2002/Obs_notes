## Băng thông

## Thông lượng
> Tốc độ (bits/sec) truyền tin tại một điểm nào đó trong mạng
> - **Tức thời**: thông lượng tại 1 thời điểm
> - **Trung bình**: thông lượng tính trung bình trong 1 khoảng thời gian.

***Nút thắt cổ chai*** (bottleneck): điểm mà tại đó thông lượng bị giới hạn trên đường truyền.
* R_s >R_c -> xuất hiện thắt cổ chai

## MTU
> Maximum Transmission Unit - kích thước tối đa của gói tin có thể truyền trên đường truyền

### ❔Vì sao cần MTU
👉 **Giảm tỉ lệ gói tin bị lỗi bit**
- BER (tỉ lệ bit lỗi) thường là const, nếu MTU < xác suất gói tin có lỗi -> giảm nguy cơ có lỗi

👉**Giảm xác suất (kích thước dữ liệu) phải truyền lại do mất gói tin**

=> <mark> MTU làm giảm kích thước dữ liệu phải truyền lại</mark>

### Vì sao MTU ko nên quá nhỏ
* Có thể làm giảm hiệu suất truyền
	* Gói tin = header + payload
	* Header = const
	* Hiệu suất truyền: $$H = \frac{paypload}{header + payload}$$

## Độ trễ

![[Pasted image 20221102075237.png]]

$$d_{nodal} = d_{proc} + d_{queue} + d_{trans} + d_{prop}$$
* *$d_{trans}$ - trễ truyền tin
	$$d_{trans} = L/R$$
	- L : kích thước dữ liệu (bits)
	- R: băng thông (bps)

* $d_{prop}$ - trễ lan truyền (truyền dẫn)
	$$d_{prop} = d/s$$
	* d: độ dài đường truyền
	* s: tốc độ lan truyền tín hiệu (prox $2x10^8$ m/sec)

* $d_{proc}$ - trễ xử lý
	* Kiểm tra lỗi bit
	* Xác định liên kết ra
	* < microsec

### Trễ hàng đợi - $d_{queue}$

![[Pasted image 20221102080030.png]]
* Độ lớn của trễ hàng đợi phụ thuộc vào $L*a/R$
	* $L*a/R \approx 0$ : trễ hàng đợi **nhỏ**
	* $L*a/R = 1$ : trễ hàng đợi **lớn**
	* $L*a/R > 1$ : trễ **vô cùng**
-> Bài toán điều phối tốc độ a trên kênh end-to-end

![[Pasted image 20221103131516.png]]

### Trễ khứ hồi - Round Trip Time
* Trễ hai chiều giữa nút nguồn và nút đích.
![[Pasted image 20221102081209.png]]
* $RTT =t_3 - t_0$
* Trễ 1 chiều: $t_1 - t_0$

## Độ mất gói tin
