### Suy diễn logic và  Tìm kiếm
* Để chứng minh $\alpha$ là đúng đối với tập giả thiết $KB$, cần áp dụng một **chuỗi các luật suy diễn đúng đắn**

> [!question] Chọn luật nào để áp dụng cho mỗi bước suy diễn?
> -> Bài toán tìm kiếm 

* Trong logic định đề, có thể bao gồm nhiều liên kết ($\neg$; $\wedge$; $\vee$; $\rightarrow$; $\leftrightarrow$) và có thể bao gồm nhiều biểu thức con (lồng khác)

> [!check] Giải pháp
> Chuyển đổi biểu thức logic định đề thành 1 biểu thức tương đương chỉ chứa các liên kết $\neg$; $\wedge$; $\vee$ dễ biểu diễn hơn.

## 1. Các dạng chuẩn
* Biểu thức logic định đề có thể được chuyển đổi về một trong các ***dạng chuẩn (Normal forms)*** để đơn giản hóa quá trình suy diễn. 

> [!info] Dạng chuẩn kết hợp (Conjunctive normal form - CNF)
> Là kết hợp (liên kết `VÀ` - $\wedge$) của các mệnh đề (clauses) mà trong đó mỗi mệnh đề là 1 liên kết `HOẶC` - $\vee$ của các ký hiệu định đề đơn

VD: $(p \vee q) \wedge (\neg q \vee \neg r \vee s)$

> [!info] Dạng chuẩn tuyển (Disjunctive normal form - DNF)
> Là liên kết `HOẶC` - $\vee$ của các mệnh đề mà trong đó mỗi mệnh đề là một liên kết `VÀ` - $\wedge$ của các ký hiệu định đề đơn
> 

### 1.1 Chuyển đổi về dạng chuẩn CNF
VD: Chuyển đổi biểu thức sau về dạng chuẩn CNF : $\neg (p \rightarrow q) \vee (r \rightarrow p)$ 

1. Loại bỏ các liên kết $\rightarrow, \leftrightarrow$ bằng các tương đương logic
	$$
	\neg (\neg p \vee q) \vee (\neg r \vee p)
	$$
2. Sử dụng các phép biến đổi tương đương (ở đây sử dụng luật De Morgan và phép phủ định 2 lần)
	$$
	(p \wedge \neg q) \vee (\neg r \vee p)
	$$
3. Sử dụng các luật kết hợp và phân bố
	$$
	(p \vee \neg r \vee p ) \wedge (\neg q \vee \neg r \vee p)
	$$
	$$
	(p \vee \neg r ) \wedge (\neg q \vee \neg r \vee p)
	$$
#### Bài toán chứng minh SAT 
> Chứng minh khả năng thỏa mãn (Satisfiability - SAT) của một biểu thức ở dạng chuẩn kết hợp. (Có đúng hay không)

> [!Note] 
> Đây là một trường hợp của bài toán thỏa mãn ràng buộc CSP

* Với mỗi mệnh đề, ít nhất 1 trong các đinh đề đơn phải đúng
* Tất cả các mệnh đề được liên kết bởi phép `VÀ` trong biểu thức phải đúng

> [!question] Cách giải quyết bài toán SAT
> * PP Backtracking
> * PP Tối ưu hóa lặp (Iterative Optimization Methods)

> [!note] Phương pháp Backtracking
> * Áp dụng chiến lược tìm kiếm theo chiều sâu (Depth-first search)
> * Xét một biến (một định đề đơn), xét các khả năng gán giá trị (Đúng, sai) cho biến đó.
> * Lặp lại, cho đến khi tất cả các biến được gán giá trị, hoặc việc gán giá trị cho tập con của tập tất cả các biến, làm cho **biểu thức là sai.**

> [!note] Các phương pháp tối ưu hóa lặp
> * Bắt đầu với một phép gán ngẫu nhiên các giá trị đúng/sai cho các ký hiệu định đề.
> * Đổi giá trị (Đúng -> Sai, Sai -> Đúng) đối với **một biến**
> * Có Heuristic : ưu tiên các phép gán giá trị làm cho nhiều mệnh đề hơn đúng
> * Sử dụng các pp tìm kiếm cục bộ: 
> 	* [[IntroAI_4 - TimkiemVoiTrithucBoSung#2.2 Simulated annealing]]
> 	* ***Walk-SAT***

#### Bài toán suy diễn vs Bài toán thỏa mãn được SAT

|Bài toán suy diễn logic|Bài toán SAT|
|---|---|
| Cần chứng minh: biểu thức logic (định lý) $\alpha$ được bao hàm bởi tập các mệnh đề $KB$ <br> (với mọi phép diễn giải mà trong đó $KB$ đúng, thì $\alpha$ đúng) |Cần chứng minh: $\exists$ phép gán giá trị đúng/sai cho các ký hiệu định đề sao cho biểu thức $\alpha$ đúng|

> [!note] Mối quan hệ của bài toán suy diễn logic - SAT
> $$
> KB \models \alpha \Leftrightarrow (KB \wedge \neg \alpha) \text{ là không thể thỏa mãn được} 
> $$

#### Luật suy diễn hợp giải (Resolution)
$$
\frac{p \vee q, \neg q \vee r}{p \vee r}
$$

* Luật suy diễn hợp giải áp dụng được đối với các biểu thức logic ở dang chuẩn CNF.

* Luật suy diễn hợp giải có **tính đúng đắn (sound)** nhưng **ko có tính hoàn chỉnh (incomplete)**

> [!note] Giải thuật hợp giải
> * Chuyển đổi tất cả các biểu thức trong KB về dạng chuẩn CNF
> * Áp dụng liên tiếp luật suy diễn hợp giải (Resolution rule) bắt đầu từ: $(KB \wedge \neg \alpha)$ 
> 	* KB là kết hợp của các biểu thức ở dạng chuẩn CNF
> 	* Do đó, $(KB \wedge \neg \alpha)$ cũng là một biểu thức ở dạng chuẩn CNF.
> * Quá trình áp dụng luật suy diễn hợp giải dừng lại khi:
> 	* Có mâu thuẫn xảy ra
> 		* Sau khi hợp giải, thu được (suy ra) biểu thức rỗng (mâu thuẫn): $\frac{p, \neg p}{\{\}}$
> 	* Không có biểu thức mới nào được sinh ra nữa.

VD:
![[Pasted image 20230612222630.png]]
![[Pasted image 20230612222702.png]]
![[Pasted image 20230612222732.png]]

### 1.2 Dạng chuẩn Horn 
> [!info] Biểu thức logic dạng chuẩn Horn
> * Biểu thức đó là liên kết `VÀ` của các mệnh đề
> * Mỗi mệnh đề là một liên kết `HOẶC` các ký hiệu, có tối đa 1 kí hiệu khẳng định (positive literal)

VD: $(p \vee \neg q) \wedge (\neg p \vee \neg r \vee s)$ 

> [!warning] Không phải mọi biểu thức logic định đề đều có thể được chuyển về dạng Horn.

#### Biểu diễn tập giả thiết $KB$ ở dạng chuẩn Horn
* **Các luật (Rules)**: 
	$$
	(\neg p_1 \vee \neg p_2 \vee ... \vee \neg p_n \vee q) \text{ tương đương với luật } (p_1 \wedge p_2 \wedge ... \wedge p_n \rightarrow q)
	$$
* **Các sự kiện (Facts)**: $p, q$

* **Các rằng buộc toàn vẹn (Integrity constraints)**: 
	$$
	(\neg p_1 \vee \neg p_2 \vee ... \vee \neg p_n) \text{ tương đương với luật } (p_1 \wedge p_2 \wedge ... \wedge p_n \rightarrow sai)
	$$

> [!note] Luật suy diễn Modus Ponens tổng quát
> #logic_ai 
> $$
> \frac{(p_1 \wedge p_2 .. \wedge p_n \rightarrow q), p_1, p_2, .., p_n}{q}
> $$

* Luật suy diễn Modus Ponens có tính đúng đắn và hoàn chỉnh đối với các ký hiệu định đề và đối với tập các biểu thức KB **ở dạng chuẩn Horn**

> [!note] 
> Luật suy diễn Modus Ponens có thể được sử dụng với cả hai chiến lược suy diễn:
> * **Suy diễn tiến**
> * **Suy diễn lùi**

**SUY DIỄN TIẾN (FORWARD CHAINING)**: *Với một tập các mệnh đề giả thiết KB, cần suy ra mệnh đề kết luận Q*

> [!abstract] Ý tưởng
> Lặp lại hai bước dưới cho tới khi suy ra được kết luận
> 1. Áp dụng các luật có mệnh đề giả thiết được thỏa mãn trong KB
> 2. Bổ sung kết luận của luật đó vào KB

![[Pasted image 20230613000054.png]]

**SUY DIỄN LÙI (BACKWARD CHAINING)** 

> [!abstract] Ý tưởng
> Quá trình suy diễn bắt đầu từ mệnh đề kết luận Q
> * Để cmr Q = tập mệnh đề KB:
> 	* Kiểm tra xem Q đã được chứng minh trong KB chưa
> 	* Nếu chưa, tiếp tục chứng minh tất cả **các mệnh đề giả thiết của một luật nào đó trong KB có mệnh đề kết luận là Q**
> * Tránh các vòng lặp
> 	* Kiểm tra xem các mệnh đề mới đã có trong ds các mệnh đề cần chứng minh chưa? Nếu có -> ko bổ sung nữa
> * Tránh việc chứng minh lặp lại đối với 1 mệnh đề
> 	* Đã được chứng minh trước đó là đúng
> 	* Đã được chứng minh trước đó là không thể thỏa mãn được (sai) trong KB

![[Pasted image 20230613001143.png]]

> [!question] Nên chọn Suy diễn tiến hay Suy diễn lùi
> * Suy diễn tiến là quá trình **dựa trên dữ liệu** (data-driven)
> * Suy diễn tiến có thể thực hiện nhiều bước suy diễn **dư thừa** (ko liên quan tới mục tiêu cần chứng minh)
> * Suy diễn lùi là quá trình **hướng tới mục tiêu** (goal-driven)
> 	-> Phù hợp cho việc giải quyết vấn đề

## 2. Ưu/nhược điểm của Logic định đề
> [!check] Ưu điểm của logic định đề
> * Cho phép dễ dàng biểu diễn cơ sở tri thức bằng tập các mệnh đề
> 
> * Cho phép làm việc với các thông tin ở dạng phủ định, dạng tuyển
> 
> * Có tính cấu tạo (ngữ nghĩa của mệnh đề được suy ra từ ngữ nghĩa của các định đề cấu thành)
> 
> * Ngữ nghĩa trong logic định đề ko phụ thuộc ngữ cảnh
> 	* VD: ngôn ngữ tự nhiên bị phụ thuộc vào ngữ cảnh của câu nói

> [!failure] Nhược điểm của logic định đề
> Khả năng diễn đạt hạn chế
> * Ko thể diễn đạt được như ngôn ngữ tự nhiên
> * Phải liệt kê (xét) mọi khả năng gán giá trị chân lý cho các định đề

## 3. Giới hạn của Logic định đề 
![[Pasted image 20230613001922.png]]