> [!info] Ràng buộc
> Quan hệ trên một tập các biến mà mỗi biến gắn với một tập các giá trị có thể nhận (miền giá trị - domain)

* Biểu diễn ràng buộc:
	* Biểu thức (toán học/logic)
	* Bảng liệt kê các phép gán giá trị phù hợp cho các biến.

## Bài toán thỏa mãn ràng buộc
> [!note] Constraint Satisfaction Problem - CSP
> Bao gồm:
> * Tập hữu hạn các biến -  X
> * Miền giá trị hữu hạn cho mỗi biến - D
> * Một tập hữu hạn các ràng buộc - C
> 
> **SOLUTION:** phép gán đầy đủ các giá trị của các biến sao cho thỏa mãn tất cả các ràng buộc.

### Biểu diễn bài toán ràng buộc
![[Pasted image 20230428001653.png]]

* Một bài toán ràng buộc nhị phân (binary CSP): mỗi ràng buộc chỉ liên quan 2 biến.
	* Các nút biểu diễn biến
	* Các cạnh biểu diễn ràng buộc


```start-multi-column
ID: ID_5x4f
Number of Columns: 2
Largest Column: standard
border: off
```


![[Pasted image 20230428002057.png]]

--- column-end ---

![[Pasted image 20230428002108.png]]

=== end-multi-column

### Các kiểu bài toán thỏa mãn ràng buộc
* **Các biến rời rạc**:
	* Các miền giá trị hữu hạn: với n biến và kích thước miền giá trị d
	-> số lượng các phép gán đầy đủ giá trị = $O(d^n)$
	* Các miền giá trị vô hạn: miền giá trị các số nguyên, các chuỗi, ...
		* Cần một ngôn ngữ biểu diễn ràng buộc (constraint language)
* **Các biến liên tục**: 
	* Bài toán với các ràng buộc tuyến tính có thể giải quyết ở mức chi phí thời gian đa thức

> [!note] Các kiểu ràng buộc
> * **Ràng buộc đơn (unary constraint)**: chỉ liên quan đến 1 biến
> * **Ràng buộc nhị phân (binary constraint)**: liên quan tới hai biến
> * **Ràng buộc bậc cao (higher-order constraint)**: liên quan nhiều hơn 2 biến.
> 	* Bậc của một ràng buộc liên quan tới số biến tham gia ràng buộc.

![[Pasted image 20230428080705.png]]

* Vài bài toán CSP thực tế
	* Giao nhiệm vụ
	* Lập thời khóa biểu
	* Lập lịch ...

## Tìm kiếm lời giải bằng kiểm thử
>* Phương pháp giải quyết vấn đề tổng quát nhất.
>* Giải quyết bằng kiểm thử (Gen and test)
>	* Sinh ra một khả năng (candidate) của lời giải.
>	* Kiểm tra xem khả năng có p là lời giải hay không.

> [!note] Áp dụng đối với bài tóan CSP
> B1. Gán các giá trị cho tất cả các biến
> B2. Kiểm tra xem có thỏa mãn các ràng buộc hay ko
> B3. Lặp lại B1 cho tới khi tìm được phép gán thỏa mãn.

> [!failure] Điểm yếu
> Phải xét quá nhiều khả năng gán mà không thỏa mãn ràng buộc.

Ví dụ
• Các biến X,Y,Z lấy các giá trị {1,2}
• Các ràng buộc: X=Y, X $\neq$ Z, Y>Z
• Các phép (khả năng) gán: (1,1,1); (1,1,2); (1,2,1); (1,2,2); (2,1,1); (2,1,2); (2,2,1)

> [!check] Cải thiện phương pháp kiểm thử
> * Sinh ra các khả năng (các phép gán giá trị) một cách thông minh hơn.
> 	* Không theo thứ tự tuần tự.
> 	* Sử dụng các kết quả (thông tin) thu được từ bước kiểm tra (bước 2)
> * Phát hiện sớm các mâu thuẫn
> 	* kiểm tra các ràng buộc sau khi mỗi biến được gán giá trị (ko đợi tới khi gán giá trị cho tất cả các biến)

## Tìm kiếm quay lui
> [!info] Backtracking
> Giải thuật tìm kiếm được sử dụng phỏ biến nhất trong CSP
> * Dựa trên giải thuật tìm kiếm theo chiều sâu (DFS)
> * Gán giá trị lần lượt cho các biến (việc gán giá trị của biến này chỉ được làm sau khi đã hoàn thành việc gán giá trị của biến khác.)
> * Sau mỗi phép gán giá trị cho một biến nào đó, kiểm tra xem các ràng buộc có được thỏa mãn bởi tất cả các biến đã được gán giá trị hay chưa. 
> 	* thực hiện **quay lui** nếu không thỏa mãn các ràng buộc.

* Các yếu tố ảnh hưởng đến pp quay lui
	* Thứ tự được xét của các biến?
		* Ưu tiên các biến quan trọng hơn
		* Ưu tiên xét trước các biến có ít giá trị
		* Ưu tiên xét trước các biến tham gia vào nhiều ràng buộc
	* Với mỗi biến, thứ tự được xét của các giá trị?
		* Thứ tự ưu tiên của các giá trị với mỗi biến được định nghĩa tùy thuộc vào bài toán cụ thể.

### Giải thuật tìm kiếm quay lui
![[Pasted image 20230428091221.png]]

![[Pasted image 20230428091816.png]]

### Các vấn đề
* **Lặp đi lặp lại lỗi**: 
	* Lý do: Bỏ qua (ko khai thác) lý do của mâu thuẫn
	* Giải pháp: pp ***Backjumping*** 

> [!note] BackJumping
> Quay lui tới nút cha xa hơn của nút hiện tại (thay vì quay lui trở lại tất cả các nút anh em và con của nút hiện tại)

* **Các kiểm tra không cần thiết**:
	* Lý do: lặp lại các kiểm tra ràng buộc ko cần thiết
	* Giải pháp: pp ***Backchecking***

> [!note] BackChecking
> Quay lui lại các nút đã được xác định và kiểm tra xem chúng có còn đúng hay không.
> * Nếu một giá trị không hợp lệ được phát hiện, thuật toán sẽ thử giá trị khác cho biến tương ứng hoặc quay lui ngay lập tức để tìm kiếm giá trị khác cho các biến đã được gán.

* **Phát hện muộn các vi phạm ràng buộc**:
	* Lý do: các vi phạm ràng buộc chỉ được phát hiện sau khi các giá trị được gán.
	* Giải pháp: pp ***ForwardChecking***

> [!hint] Cải thiện Backtracking CSP
> * Thứ tự xét các biến (ưu tiên biến **bị ràng buộc nhiều nhất**)
> * Thứ tự gán các giá trị đối với mỗi biến
> * Phát hiện sớm các vi phạm ràng buộc sẽ xảy ra

#### Biến bị ràng buộc nhiều nhất (Most Constrained Variable)
> Biến có số lượng các giá trị hợp lệ ít nhất

![[Pasted image 20230428095549.png]]

(Còn gọi là quy tắc ưu tiên các biến có tập giá trị hợp lệ nhỏ nhất ***Minimum Remaining Values***)

> [!question] Khi có nhiều hơn 2 biến có như nhau số lượng giá trị hợp lệ ít nhất ?
> Chọn biến ràng buộc (khống chế) các biến khác (chưa được gán giá trị) nhiều nhất.

![[Pasted image 20230430225010.png]]

> [!question] Đối với một biến, các giá trị được xét (để gán) theo thứ tự nào?
> Chọn giá trị ràng buộc (khống chế) các biến khác (chưa được gán giá trị) ít nhất
> -> giá trị này gây ra hạn chế tối thiểu đối với các khả năng gán giá trị của các biến khác.

![[Pasted image 20230430233139.png]]

### Kiểm tra tiến (Forward Checking)
> Tránh các thất bại, bằng kiểm tra trước các ràng buộc.

* Forward Checking đảm bảo sự phù hợp giữa biến đang được xét gán giá trị và các biến khác có **liên quan (ràng buộc) trực tiếp** đến nó.

> [!hint] Ý tưởng
> * Ở mỗi bước gán giá trị, theo dõi các giá trị hợp lệ (có thể được gán) đối với các biến chưa được gán giá trị.
> * Loại bỏ hướng tìm kiếm hiện tại khi có bất kỳ một biến (chưa được gán giá trị) nào đó không còn giá trị hợp lệ.

![[Pasted image 20230430233730.png]]

#### Lan truyền các ràng buộc
* Kiểm tra tiến giúp lan truyền thông tin (ràng buộc) từ các biến đã được gán giá trị đến các biến chưa được gán giá trị.

> [!warning] 
> PP Forward Checking không thể phát hiện trước (ngăn chặn) được tất cả các thất bại.

![[Pasted image 20230430234143.png]]

* Lan truyền các ràng buộc chỉ đảm bảo tính **phù hợp cục bộ (local consistency)** của các ràng buộc.

### Phù hợp cạnh trong đồ thị ràng buộc
* trong đồ thị ràng buộc, một cạnh (X->Y) được gọi là **phù hợp** về ràng buộc 
	<=> **Đối với mỗi giá trị x của biến X, đều có 1 giá trị y của biến Y sao cho ràng buộc giữa 2 biến X và Y được thỏa mãn.**

> [!warning] Định nghĩa về phù hợp cạnh không có tính "đối xứng".

![[Pasted image 20230430234733.png]]

> [!note]
> Để cạnh (X -> Y) là phù hợp ràng buộc, cần loại bỏ bất kỳ giá trị x của biến X mà không có giá trị y nào của biến Y làm cho ràng buộc giữa 2 biến X và Y được thỏa mãn.

![[Pasted image 20230430235247.png]]

> [!note] 
> Sau khi loại bỏ giá trị x khỏi ds các giá trị hợp lệ của biến X 
> -> cần xét lại tất cả các ràng buộc trực tiếp tới biến X (mọi cạnh (... -> X))

![[Pasted image 20230430235502.png]]

> [!check] 
> PP phù hợp cạnh (Arc Consistency) phát hiện được các thất bại **sớm hơn** so với pp Forward Checking.
> -> Kiểm tra phù hợp cạnh có thể được sử dụng trước hoặc sau mỗi phép gán giá trị của mỗi biến

![[Pasted image 20230430235745.png]]

#### Giải thuật phù hợp cạnh AC-3
![[Pasted image 20230430235817.png]]

## Tìm kiếm cục bộ CSP
> Sử dụng các pp tìm kiếm cục bộ cho bài toán CSP
> [[IntroAI_4 - TimkiemVoiTrithucBoSung#2.1 Hill-climbing]]
> [[IntroAI_4 - TimkiemVoiTrithucBoSung#2.2 Simulated annealing]]

* Mỗi trạng thái (của không gian tìm kiếm) ứng với một phép gán đầy đủ giá trị cho tất cả các biến.
	* Không gian tìm kiếm bao gồm **cả các trạng thái trong đó các ràng buộc bị vi phạm**
	* Dịch chuyển trạng thái = Gán giá trị mới cho các biến

* Trạng thái đích = trạng thái trong đó tất cả các ràng buộc được thỏa mãn

> [!note] Quá trình tìm kiếm cục bộ
> * Lựa chọn biến để gán giá trị mới:
> 	* Chọn ngẫu nhiên một biến mà giá trị của nó vi phạm các ràng buộc.
> * Lựa chọn giá trị mới của một biến:
> 	* Dựa theo chiến lược **min-conflicts** (chọn gía trị mà nó vi phạm ít nhất các ràng buộc)

> [!example] 
> Áp dụng pp tìm kiếm cục bộ Hill-climbing với hàm ước lượng h(n) = tổng số các ràng buộc bị vi phạm.
> * Trạng thái tiếp theo được xét là trạng thái ứng với giá trị hàm h(n) tốt hơn (<=> ít ràng buộc bị vi phạm hơn)

![[Pasted image 20230501001718.png]]