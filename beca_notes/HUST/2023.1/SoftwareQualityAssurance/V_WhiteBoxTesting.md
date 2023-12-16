```shell
<Req Analysis> ---> <Acceptance Test> # == [Validation]
|                     ^
V                     |
# high-level, define API 
<Arch Design> ---> <System Test> (1)
|                     ^
V                     |
# Detail-level
<Prog Design> ---> <Integration Test> (2)
|                     ^
V                     |
<Coding> ---> <Unit Test> (3)
# (1), (2), (3) == [Verification]
# (1) Blackbox Testing
# (2), (3) Whitebox Testing
```

* Blackbox testing - Functional Testing
* Whitebox testing - Integration Testing

---
***Control flow Testing***
## Path Testing

![[V_WhiteBoxTesting-20231023061106506.webp]]

### Các tiêu chí lựa chọn Path
1. **Statement Coverage**: bao phủ tập lệnh
	* Lựa chọn path: $\forall$ đỉnh trên đồ thị G được bao phủ ít nhất 1 lần
	* Là lựa chọn yếu nhất, với số lượng TC ít nhất
1. **Branch Coverage**: lựa chọn các nhánh ít nhất 1 lần
2. **All paths**: tất cả các đường

$V = {1,2,3,4,5,6,7}$
path = (1) ---> (7)

P1: 1 -> 2(F) -> 3(F) -> 6 -> 7
P2: 1 -> 2(T) -> 4(T) -> 5 -> 7
P3: 1 -> 2(F) -> 3(T) -> 5 -> 7
P4: 1 -> 2(T) -> 4(F) -> 6 -> 7

Lựa chọn P1, P2:
P1: 1 -> 2(F) -> 3(F) -> 6 -> 7
P2: 1 -> 2(T) -> 4(T) -> 5 -> 7

* Đã thỏa mãn tiêu chí statement coverage
* Sinh test case:
	* TC1: (Male, 85) | accept = False
	* TC2: (Female, 79) | accept = True

![[V_WhiteBoxTesting-20231023064157934.webp]]

> [!caution] Infeasible path
> 1 -> 2(T) -> 3 -> 5 -> 6(F) -> 8(F) -> 10 (có cả 2 điều kiện y < 0 và y > 0)

![[V_WhiteBoxTesting-20231023073429812.webp|468]]

* Feasible path: 1 -> 2(T) -> 3(F) -> 5 -> 2(F) -> 6

> [!check] 
> Path Testing is applicable to new unit

> [!fail] Limitations of Path Testing
> * Sự chệch khớp của giao diện và các lỗi không được tính tới
> * không phải tất cả các lỗi ban đầu được phát hiện
> * Các lỗi đặc trưng không được phát hiện
## Predicate Coverage
(Tiêu chí bao phủ điều kiện)

> [!info] Predicate
> là một diễn tả có thể được đánh giá bằng giá trị đúng sai.

* Predicate có thể bao gồm:
	* Các giá trị đúng sai
	* Các giá trị không thuộc dạng boolean nhưng được so sánh với nhau bằng các **relational operators** (`>=`, `=<`, `=`, `!=`, `<`, `>`)
	* Các lời gọi boolean function.

* Cấu trúc bên trong có thể được tạo bởi các **logical operators** ($\neg,\rightarrow, \leftrightarrow, \lor,\land, \oplus$)

* Một ***mệnh đề (clause)*** là một predicate không bao hàm các logical operators

Ex: $(a=b) ∨ C ∧ p(x)$ bao gồm 3 mệnh đề

> [!note] 
> Để đảm bảo rằng tất cả các predicate có trong source code được implement đúng, ta xét với mỗi predicate p, ít nhất 1 lần đánh giá p đúng và ít nhất 1 lần đánh giá p sai

![[V_WhiteBoxTesting-20231031093607960.webp]]

==**Sẽ kiểm tra cả Predicate và các clauses riêng lẻ**==

### Predicate Coverage (PC) >< Clause Coverage (CC)
* PC không phải lúc nào cũng kiểm tra tất cả các mệnh đề.
* CC không phải lúc nào cũng đảm bảo PC

Ví dụ $p=a\vee b$
Chọn {a,b} = {T,F}||{F,T} -> CC nhưng ko PC

**Combinatorial Coverage (CoC)**: với mỗi predicate p, các test case cần đảm bảo rằng các clauses trong p cần xem xét tất cả các tổ hợp của truth values.

Ex: Write all the clauses and the Combination of Clauses (CoC) of the given predicate 
$P = ((a >b) \lor C) \land p(x)$

| a > b |  C  | p(x) |  P  |
|:-----:|:---:|:----:|:---:|
|   T   |  T  |  T   |  T  |
|   T   |  T  |  F   |  F  |
|   T   |  F  |  T   |  T  |
|   T   |  F  |  F   |  F  |
|   F   |  T  |  T   |  T  |
|   F   |  T  |  F   |  F  |
|   F   |  F  |  T   |  F  |
|   F   |  F  |  F   |  F  |

> [!caution] Vấn đề với Coc
> * Tốn kém nếu có nhiều clauses trong predicate.
> * Với mỗi điểm quyết định có N điều kiện, cần $2^N$ test cases

> [!note] Motivation
> * Các predicate nên được xét T/F trong các test case.
> * Mỗi clause được kiểm tra độc lập với nhau.
> * Mỗi clause ảnh hưởng tới cả predicate (thay đổi giá trị của clause -> thay đổi giá trị của predicate)

### Active Clause Coverage

* Một clause được gọi là **Major Clause**, định nghĩa một predicate <=> thay đổi clause đó làm thay đổi giá trị của predicate.

* **Minor clause**: các clause còn lại ngoài major clause

* Với mỗi p $\in$ P và mỗi major clause $c_i\in C_p$, chọn minor clauses $c_j$ (i $\neq$ j) sao cho c_i xác định p.
* Test Requirement có 2 yêu cầu cho $c_i$. c_i = T và c_i = F.

Ex0:
với $p = a \vee b$, có 4 yêu cầu trong TR, 2 cho a và 2 cho b.
* b cần False để a xác định p và ngược lại

Có bảng
| Mj      | a   | b   |
| ------- | --- | --- |
| c_i = a | T   | F   |
|         | F   | F   |
| c_i = b | F   | T   |
|         | F   | F   |

-> có 3 tổ hợp (a,b) = (T,F), (F,T),(F,F)

Ex1:
![[V_WhiteBoxTesting-20231031143326042.webp]]

Ex2: cho $P= a \land (b \lor c)$, nếu coi a là AC -> cần gán giá trị nào cho b và c?
* Giá trị của b và c sao cho khi thay đổi giá trị của a, giá trị của P cũng thay đổi
-> $(b \lor c) = T$, khi đó giá trị của P được xác định bởi a
Có thể gán b = 1, c = 1

Ex3:
P = f (c_1, c_2, ..., c_k)
Mệnh đề c_i là mệnh đề chính: P = P(c_i)
	-> Phải xác định các gtrị cụ thể của các mệnh đề phụ, $\forall c_j$ (j != i).
Với ACC, $\forall c_i$ là mệnh đề chính, cần xét hai TH:
* TC1: c_i = T
* TC2: c_j = F
Với $P = a \vee b$
	Để a là mệnh đề chính: b = F -> có hai TC: (T,F);(F,F)
	Tương tự, với b là mệnh đề chính -> có hai TC: (F,F);(F,T)
	-> Có 3 TC thỏa mãn ACC: (T,F);(F,T);(F,F)

Ex4:
$P = c_1 \wedge c_2 \wedge c_3 \wedge c_4$ 
c_1 - credit completed > 30
c_2 - cummulative GPA > 2.0
c_3 - fulltime status
c_4 - termed GPA > 2.0
Đưa ra tập TC thỏa mãn ACC(P)


> [!note] Phát biểu ACC
> với mỗi predicate **p** và mỗi major clause **c** của p, chọn minor clauses sao cho c xác định p. 
> 2 yêu cầu để đảm bảo ACC: c nhận giá trị True, và c nhận giá trị False.

(*không cần c = p, cũng như không cần giá trị truth của p = giá trị truth của c*)

==-> Số lượng test cases của điểm quyết định với N điều kiện giảm còn **N+1**==

> [!question] Vậy làm sao để có thể chọn giá trị cho các giá trị đúng sai trong minor clause?

> [!abstract] 
> Chia ra làm 3 tiêu chí của Active Clause định nghĩa các giá trị mà Minor Clause sẽ nhận:
> * General active clause coverage (GACC)
> * Correlated active clause coverage (CACC)
> * Restricted active clause coverage (RACC)

### 👉 **GENERAL ACTIVE CLAUSE COVERAGE** (GACC)
Với ví dụ: $P= a \land (b \lor c)$
* Với mỗi clause c_i, chọn giá trị cho minor clauses c_j sao cho c_i xác định P
* clause c_i được xét ở hai giá trị đúng, sai
* Các minor clause c_j không cần phải giống nhau trong TH c_i đúng lẫn trong TH c_i sai.

![[V_WhiteBoxTesting-20231031150929857.webp|562]]

> [!tip] Kết luận
> $$
> c_j(c_i = true) = c_j(c_i = false) \forall c_j
> $$
> OR 
> $$
> c_j(c_i = true) != c_j(c_i = false) \forall c_j
> $$
> Với c_i là major clause, c_j là minor clause.

* Giá trị của c_j có thể giống hoặc khác với c_i nhận giá trị đúng hoặc sai
(các operands trong c_j có truth value khác nhau)

> [!note] 
> Định nghĩa: GACC **bao hàm CC, nhưng không bao hàm PC**.

Ex: P = a <-> b
* Test case T = {(a=T, b=T), (a=F,b=F)} satisfy GACC, but not PC, all both cases, P = T
* Test case T = {(a=T, b=F), (a=F,b=T)} satisfy GACC too, but not PC either, all both cases, P = F

### **CORRELATED ACTIVE CLAUSE COVERAGE (CACC)** (tương quan)
* Bổ sung thêm: các giá trị chọn cho Minor clause c_j phải khiến cho P đúng với một giá trị của major clause c_i và sai cho giá trị còn lại.
$$
P(c_i = true) != P(c_i=false)
$$

* c_j không cần phải giống nhau (tương tự GACC)
Ex:
![[V_WhiteBoxTesting-20231031154057084.webp]]

-> Chọn 1 trong các cặp 1,2,3 + 5,6,7

> [!note]
> CACC bao hàm GACC, từ đó bao hàm CC và cũng như PC

Ex: tìm các test case thỏa mãn GACC, CACC
![[V_WhiteBoxTesting-20231108164414735.webp]]
* Coi a là c_i, có b <-> c cần phải = true để a là major clause -> chọn row 1, 4, 5, 8
	* Chọn cặp lấy mỗi bên 1 thành phần để tạo thành các cặp thỏa mãn GACC (1,5), (1,8), (4,5), (4,8)
	* Chọn cặp (4,8), (1,5) để thỏa mãn CACC

### 👉 **RESTRICTED ACTIVE CLAUSE COVERAGE (RACC)**
* Thỏa mãn CACC
$$
\forall c_j, c_j(c_i=true) = c_j(c_i=false)
$$
* Mệnh đề phụ phải giữ nguyên giá trị khi mệnh đề chính thay đổi giá trị
* Là một phiên bản nghiêm ngặt hơn của CACC

> [!note] 
> RACC bao hàm cả CACC, GACC, CC và PC

> [!warning] RACC thường dẫn tới các test requirements bất khả thi

Ex:
Với $b\vee c = P$ (ko áp dụng tiêu chí phụ)
Với $P = a \wedge (b \vee c)$ -> áp dụng tiêu chí phụ

Minor Clause được lựa chọn thỏa mãn *(1)* hoặc *(2)*
*(1)*: $\forall c_j: c_j(c_i = T) = c_j (c_i = F)$

*(2)*: $\forall c_j: c_j(c_i = T) != c_j(c_i = F)$

* Chọn a là major clause <-> $b\vee c = True$
-> ACC(a): (b,c) $\in$ {(T,F);(F,T);(T,T)}
-> {1,2,3} x{5,6,7} -> có 9 cặp thỏa mãn
Để GACC(a) ->:
	b(a = T) = b(a = F) hoặc b(a = T) != b(a = F)
	c(a = T) = c(a = F) hoặc c(a = T) != c(a = F)
-> chọn các cặp {1,5};{2,6};{3,7} và {2,7};{3,6} (5 trường hợp)


* Chọn b làm major clause, a = true để b xác định
	GACC(b) <-> ACC(b), có c là minor clause: $\forall c$ (cả c = T và c = F)
	GACC(c) <-> ACC(c), có b là minor clause: $\forall b$ (cả b = T và b = F)
-> cần các tiêu chí phụ để giảm số trường hợp TC
CACC: chọn minor clause sao cho P đúng với 1 giá trị main clause và sai với giá trị còn lại -> {2, 4} và {3,4}

### Logical Operators in Source Code
![[V_WhiteBoxTesting-20231108170131234.webp]]

---
***Data Flow Testing***
> [!tip] Goal
> Ensure values are computed and used correctly by considering how data accessed and modified.

> [!abstract] Date Flow Test Coverage Criteria
> * All-defs coverage
> * All-uses coverage
> * All-DU-Paths coverage
> * All-p-uses/some-c-uses coverage
> * All-c-uses/some-p-uses coverage
> * All-p-uses coverage
> * All-c-uses coverage

$P = G(V,E)$
V: nodes -> definition/use
E: edges -> variables

* Variable is **defined** whenever its value is modified.
	```python
	y = 20 # assign
	read(y) # input statement
	update(x, &y) # call-by-reference parameter
	```

* Variable is **used** whenever its value is read.
	```python
	y = x + 17 # y is defined, x is used
	y = sqrt(x) 
	```

* Variable use: ***p-use*** and ***c-use***
	* p-use (predicate-use): use in the predicate of a branch statement
	* c-use (computation-use): any other usage

```java
if (x > 0) { // p-use of x
	print(y); // c-use of y
}
```

* a variable can be also used and then re-defined in a single statement when it appears. 
	Ex: y = y + x
	increment(&y)

> [!info] Definition-Clear-Path
> * A path is definition-clear to a variable v *if it has no variable re-definition of v on this path*.

> [!info] Complete-Path
> * A path is complete if the initial node of this path is a *entry node* and its final node is an exit node

> [!info] Definition-Use Pair (DU-pair)
> Is a pair (d,u) such that:
> * **d** is a node defining v
> * u is a node or edge using v
> 	* When it is a p-use of v, u is an out-going edge of the predicate statement
> * There is a def-clear path of v from d to u
> ![[V_WhiteBoxTesting-20231202174652558.webp|480]]
> 


> [!note] All-Defs Coverage
> For every var *v*, at least **one def-clear path** from every definition of v to at least one c-use/p-use of v must be covered.


> [!note] All-Uses Coverage
> For every var *v*, at least **one def-clear path** from every def of v  to every c-use/p-use (all outgoing edges of the predicate statement) of v must be covered.

* All du-pairs covered.

* A path is **simple** if all edges within the path are **distinct**
* A path is **loop-free** if all nodes within the path are **distinct**

> [!info] DU-Path
> A Path $<n_1, n_2, ...,n_j, n_k>$ is a **DU-Path** to var *v*, if *v* is defined at node **n1** and either:
> * have **c-use** of v at node $n_k$ and the rest is a **def-clear simple** path.
> * have **p-use** of v at edge $<n_j, n_k>$ and the rest is a **def-clear loop-free** path

* ***All DU-Paths Coverage***: for every var v, every du-path from every def of v to every c-use and every p-use of v must be covered.
Ex:
![[V_WhiteBoxTesting-20231202180753301.webp]]
## Summary
![[V_WhiteBoxTesting-20231202180648150.webp|785]]