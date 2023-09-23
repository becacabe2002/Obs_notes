Vì logic định đề có giới hạn -> chúng ta cần có loại logic khác để biểu diễn cơ sở tri thức

Biểu diễn bằng biểu thức logic vị từ (first-order predicate logic - FOL)
* `HUST_Student(Tuan)` : "Tuấn là 1 sinh viên HUST"
* $\forall x$: `HUST_Student(x)` -> `Studies_Algebra(x)`: "Mọi sinh viên của HUST đều học môn ĐS"

* Trong logic vị từ, ta có thể chứng minh:
{`HUST_Student(Tuan)`, $\forall x$ : `HUST_Student(x)` -> `Studies_Algebra(x)`} $\vdash$ `Studies_Algebra(Tuan)`

## 1. Ngôn ngữ 
Có 4 kiểu ký hiệu (symbols)
* ***Hằng (Constants)*** - các tên của các đối tượng trong một lĩnh vực bài toán cụ thể (VD: Tuan)

* ***Biến (Variables)*** - các ký hiệu mà giá trị thay đổi đối với các đối tượng khác nhau (VD: x)

* ***Ký hiệu hàm (Function Symbols)*** - các ký hiệu biểu diễn ánh xạ (quan hệ hàm) từ các đối tượng của miền này sang các đối tượng của miền khác (VD: plus(x,y))

* ***Các vị từ (Predicates)*** - các quan hệ mà giá trị logic là đúng/sai (VD: HUST_Student và Studies_Algebra)

> [!note] Mỗi ký hiệu hàm hoặc vị từ đều có 1 tập các tham số.

* ***Phần tử (term)*** - bao gồm các hằng, biến và các ký hiệu hàm đã chứa tham số là một phần tử

> [!warning] Không còn gì khác là một phần tử
> * Các vị từ ko phải là phần tử

* ***Nguyên tử (Atoms)*** - là vị từ có chứa tham số là **các phần tử**
VD: HUST_Student(Tuan)

* ***Các biểu thức (Formulas)***:
	* ***Atomic formula***: Một nguyên tử là một biểu thức
	* ***Compound formula***: Các biểu thức được xây dựng từ tập các atomic formula và các toán tử logic
	* ***Quantified Formula***: $(\forall, \exists)$ được sử dụng để thể hiện trạng thái của tất cả các đối tượng trong lĩnh vực hoặc sự tồn tại của một vài đối tượng nhất định
		* Với $\phi$ là một biểu thức, x là một biến -> $\forall x: \neg\phi(x)$ là một biểu thức

> [!note]
> $\exists x: \phi(x)$ được định nghĩa bằng $\neg \forall x: \neg \phi(x)$ 

> [!warning] Ko còn gì khác là một biểu thức.

## 2. Ngữ nghĩa
* Một **phép diễn giải (interpretation)** của một biểu thức $\phi$ được biểu diễn bằng $<D,I>$
	* **Miền giá trị** $D$ là một tập khác rỗng
	* **Hàm giá trị (Interpretation Function)** $I$ là một phép gán giá trị đối với mỗi hằng, ký hiệu hàm và ký hiệu vị từ:
		* Đối với hằng c: $I(c) \in D$
		* Đối với ký hiệu hàm có n tham số f: $I(f): D^n \rightarrow D$
		* Đối với ký hiệu vị từ có n tham số p: $I(p): D^n \rightarrow \{true,false\}$

* Diễn giải đối với 1 biểu thức logic vị từ: giả sử $\phi, \psi, \lambda$ là các biểu thức vị từ
![[Pasted image 20230613024541.png]]

![[Pasted image 20230613024618.png]]

![[Pasted image 20230613024636.png]]

> [!note] Các đặc điểm của các lượng từ logic
> * **Tính hoán vị**:
> 	* $(\forall x \forall y) \equiv (\forall y \forall x)$
> 	* $(\exists x \exists y) \equiv (\exists y \exists x)$
> * Mỗi lượng tử logic  có thể được biểu diễn bằng lượng từ kia:
> 	* $(\forall x : Thich(x, Kem)) \equiv (\neg \exists x: \neg Thich(x,Kem))$ 
> 	* $(\exists x: Thich(x,Kem)) \equiv (\neg \forall x: \neg Thich(x, Kem))$

![[Pasted image 20230613025243.png]]

