> ***Logic*** là ngôn ngữ hình thức cho phép biểu diễn thông tin dưới dạng các kết luận có thể được đưa ra.

Logic = Syntax + Semantics

> ***Cú pháp (Syntax)*** : xác định các mệnh đề (sentences) trong một ngôn ngữ.
> ***Ngữ nghĩa (Semantics)*** : xác định ý nghĩa của các mệnh đề trong 1 ngôn ngữ (Xác định sự đúng đắn của một mệnh đề)

> [!example] 
> Ví dụ: Trong ngôn ngữ của toán học
> * *(x+2 ≥ y) là một mệnh đề; (x+y > {}) không phải là một mệnh đề
> * (x+2 ≥ y) là đúng nếu và chỉ nếu giá trị (x+2) không nhỏ hơn giá trị y
> * (x+2 ≥ y) là đúng khi x = 7, y = 1
> * (x+2 ≥ y) là sai khi x = 0, y = 6

#### Cú pháp (Syntax)
Cú pháp = Ngôn ngữ + Lý thuyết chứng minh
> **Ngôn ngữ**  - các kí hiệu (symbols), biểu thức (expressions), thuật ngữ (terms), công thức (formulas) hợp lệ.

VD: one plus one equal two

> **Lý thuyết chứng minh (proof theory)** - tập hợp các luật suy diễn cho phép chứng minh các biểu thức

VD: luật suy diễn any plus zero -> any

> **Định lý (Theorem)** - mệnh đề logic cần chứng minh.

> [!warning] Việc chứng minh 1 định lý không cần phải xác định ngữ nghĩa (interpretation) của các ký hiệu.

#### Ngữ nghĩa (semantics)
* Ngữ nghĩa = Ý nghĩa (intepretation) của các ký hiệu

VD:
* I(one) nghĩa là 1 ($\in$ N)
* I(two) nghĩa là 2 ($\in$ N)
* I(plus) nghĩa là phép cộng + : N x N → N
* I(equal) nghĩa là phép so sánh bằng = : N x N → {true, false}
* I(one plus one equal two) nghĩa là true

* Nếu diễn giải của một biểu thức là đúng, ta nói rằng phép diễn giải này là một **mô hình** của biểu thức
	* (x + 2 $\geq$ y) là đúng khi $x = 7, y = 1$

* Một biểu thức đúng đối với bất kỳ phép diễn giải nào thì được gọi là một biểu thức **đúng đắn (valid)**

#### Tính bao hàm
> [!note] Tính bao hàm
> Là một mệnh đề được suy ra từ 1 cơ sở tri thức:
> $$
> KB \models \alpha
> $$
> * Một cơ sở tri thức KB bao hàm mệnh đề $\alpha$ <=> $\alpha$ đúng trong mọi mô hình mà trong đó KB là đúng. (KB đúng -> $\alpha$ đúng) 

VD: Nếu một cơ sở tri thức KB chứa các mệnh đề “Đội bóng A
đã thắng” và “Đội bóng B đã thắng”, thì KB bao hàm mệnh đề “Đội
bóng A hoặc đội bóng B đã thắng”

### Các mô hình (Models)
* Các mô hình là các không gian có cấu trúc, mà trong các không gian đó tính đúng đắn của các mệnh đề có thể đánh giá được.

VD: Mệnh đề (x+y > 5) đúng khi (x,y) = (3,3), (3,7)

> [!info] Mô hình
> m là một mô hình của mệnh đề $\alpha$ nếu $\alpha$ đúng trong m.
> M($\alpha$) là tập hợp tất cả các mô hình của $\alpha$
> * $KB \models \alpha<=> M(KB) \subseteq M(\alpha)$

![[Pasted image 20230607111630.png]]

## 2. Suy diễn Logic
* Mệnh đề $\alpha$ được suy ra từ $KB$ bằng cách áp dụng thủ tục suy diễn $i$ : $KB \vdash_i \alpha$. Nói cách khác, thủ tục $i$ suy ra mệnh đề $\alpha$ từ $KB$

> [!note] Tính đúng đắn (soundness)
> * Một thủ tục suy diễn $i$ được gọi là **đúng đắn (sound)**, nếu thủ tục $i$ suy ra chỉ các mệnh đề được bao hàm (entailed sentences)
> * Thủ tục $i$ là đúng đắn, nếu bất cứ khi nào $KB \vdash_i \alpha$ thì cũng đối xứng với $KB \models \alpha$
> * Nếu thủ tục $i$ suy ra mệnh đề $\alpha$, mà $\alpha$ ko được bao hàm trong $KB$ thì thủ tục $i$ là không đúng đắn (unsound)

> [!note]  Tính hoàn chỉnh (completeness)
> * Thủ tục suy diễn $i$ được gọi là **hoàn chỉnh (completeness)** nếu thủ tục $i$ có thể suy ra **mọi** mệnh đề được bao hàm (entailed sentences)
> * Thủ tục $i$ là hoàn chỉnh, nếu bất cứ khi nào $KB \models \alpha$, thì cũng đúng đối với $KB \vdash_i \alpha$

* **Logic vị từ bậc 1 (First-order logic)**
	* Có khả năng biểu diễn hầu hết các phát biểu logic
	* Với logic vị từ bậc 1, tồn tại 1 thủ tục suy diễn **đúng đắn** và **hoàn chỉnh** 

* Logic là một cách để biểu diễn hình thức và suy diễn tự động
	* ***Suy diễn diễn dịch (deductive reasoning)*** : suy diễn được thực hiện ở mức cú pháp
	* ***Suy diễn dựa trên mô hình (model-based reasoning)***: suy diễn có thể được thực hiện ở mức ngữ nghĩa

> [!note] Suy diễn ngữ nghĩa
> Suy diễn ngữ nghĩa ở mức của một phép diễn giải (mô hình):
> * Với một biểu thức, có tồn tại 1 mô hình không ? (**khả năng thỏa mãn?**)
> * Với một biểu thức và một phép diễn giải, kiểm tra xem phép diễn giải có phải là một mô hình của biểu thức không? (**kiểm tra mô hình**)
> Suy diễn ngữ nghĩa ở mức của tất cả các phép diễn giải có thể (**Kiểm tra tính đúng đắn (validity checking)**)

## 3. Logic định đề
> là loại logic đơn giản nhất

### 3.1 Cú pháp
* Một kí hiệu định đề ($S_1, S_2, ...$) là một biểu thức (định đề)
* Các giá trị hằng logic **đúng (true)** và **sai (false)** là các biểu thức

> [!note] 
> Với $S_1, S_2$ là các biểu thức:
> * Phủ định $\neg S_1$ của một biểu thức cũng là biểu thức (**Phép phủ định**)
> * Hợp của hai biểu thức $S_1 \wedge S_2$ cũng là một biểu thức (**Phép kết hợp/và**)
> * Tuyển của hai biểu thức $S_1 \vee S_2$ cũng là một biểu thức (**Phép tuyển/hoặc**)
> * $S_1 \rightarrow S_2$ cũng là một biểu thức (**Phép suy ra/kéo theo**)
> * $S_1 \leftrightarrow S_2$ cũng là một biểu thức (**Phép tương đương**)

> [!warning] Không còn dạng nào ngoài các dạng nêu trên là một biểu thức

VD: ![[Pasted image 20230607220409.png]]

> [!note] Thứ tự ưu tiên của các toán tử logic
> * Từ cao xuống thấp: $\neg$; $\wedge$; $\vee$; $\rightarrow$; $\leftrightarrow$
> * Sử dụng cặp ký tự `()` để xác định mức độ ưu tiên.

![[Pasted image 20230607220743.png]]

### 3.2 Ngữ nghĩa
* Với một mô hình cụ thể, nó sẽ xác định giá trị đúng/sai cho mỗi ký hiệu định đề.
> [!note] Bảng chân lý với các toán tử logic
> #logic_ai 
> ![[Pasted image 20230607221253.png]]

### 3.3 Tương đương logic
* Hai mệnh đề được gọi là **tương đương logic** ($\alpha \equiv \beta$) <=> hai mệnh đề này luôn đúng trong cùng mô hình ($\alpha \models \beta$ và $\beta \models \alpha$)

> [!note] Các tương đương logic cơ bản
> #logic_ai 
> ![[Pasted image 20230607221822.png]]

![[Pasted image 20230607224222.png]]

### 3.4 Mâu thuẫn và Tautology
* Một biểu thức logic định đề luôn có giá trị sai (false) trong mọi phép diễn giải (mọi mô hình) thì được gọi là **mâu thuẫn (contradiction)**
VD: $(p \wedge \neg p)$

* Một biểu thức logic định đề luôn có giá trị đúng (true) trong mọi phép diễn giải (mọi mô hình) thì được gọi là ***tautology***
VD: $(p \vee \neg p)$

### 3.5 Tính thỏa mãn và Tính đúng 
* Một biểu thức logic định đề là **thỏa mãn được (satisfiable)** nếu biểu thức đó đúng trong *một mô hình nào đó*
VD: $A \vee B$

* Một biểu thức là **không thể thỏa mãn được (unsatisfiable)** nếu không tồn tại bất cứ mô hình nào mà trong đó biểu thức là đúng.

* Một biểu thức là **đúng đắn (valid)** nếu biểu thức đó đúng trong *mọi mô hình*.
VD: $(A \vee \neg A)$

## 4. Bài toán chứng minh logic 
* Với một cơ sở tri thức là tập các mệnh đề KB, và một mệnh đề $\alpha$ cần chứng minh (một định lý).
* Ta cần biết liệu cơ sở tri thức KB có bao hàm về mặt ngữ nghĩa $\alpha$ hay không ?  ($KB \models \alpha$ ?)
	* Hiểu một cách đơn giản: $\alpha$ có thể được suy ra từ cơ sở tri thức KB được ko?

> [!question] Có tồn tại 1 thủ tục (suy diễn) có thể giải quyết bài toán chứng minh logic trong 1 số hữu hạn các bước?

> [!abstract] Có 3 pp chứng minh phổ biến
> * Sử dụng bảng chân lý (Truth-table)
> * Áp dụng các luật suy diễn (Inference rules)
> * Chuyển về bài toán chứng minh thỏa mãn (áp dụng chứng minh phản chứng)

### 4.1 Chứng minh dựa trên bảng chân lý
* Kiểm tra tất cả các phép diễn giải có thể mà trong đó KB đúng, xem $\alpha$ có đúng hay sai
	* Nếu $\alpha$ đúng trong mọi TH KB đúng -> điều cần chứng minh
	* Ngược lại

![[Pasted image 20230608001141.png]]

* Đối với logic định đề, pp này có tính **đúng đắn** và **hoàn chỉnh**

* Độ phức tạp tính toán của pp chứng minh dựa trên bảng chân lý
	* $O(2^n)$ - n là số lượng các ký hiệu định đề 

### 4.2 Chứng minh bằng các luật suy diễn
![[Pasted image 20230608004707.png]]
![[Pasted image 20230608004942.png]]

* Tất cả các luật suy diễn trên đều có tính đúng đắn

VD:
![[Pasted image 20230608005346.png]]