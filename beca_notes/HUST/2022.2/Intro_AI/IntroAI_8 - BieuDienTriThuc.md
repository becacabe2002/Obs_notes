> [!info] Dữ liệu (Data)
> Các sự kiện hoặc ký hiệu 

> [!info] Thông tin (Information)
> Dữ liệu đã được xử lý hoặc chuyển đổi thành những dạng hoặc cấu trúc phù hợp

>[!info] Tri thức (Knowledge)
>Sự hiểu biết (nhận thức) về thông tin

![[Pasted image 20230512075857.png]]

* **Biểu diễn tri thức** : bài toán quan trọng của Trí tuệ nhân tạo.

> [!warning] Vấn đề
> * **Tính hoàn chỉnh** (Completeness): có hỗ trợ thu thập và thể hiện mọi khía cạn của tri thức
> * **Tính ngắn gọn** (Conciseness)
> 	* PP biểu diễn có cho phép thu thập tri thức một cách hiệu quả?
> 	* PP biểu diễn có cho phép việc lưu trữ và truy nhập dễ dàng tri thức không?
> * **Tính hiệu quả về tính toán** (Computational efficiency)
> * **Tính rõ ràng, dễ hiểu** (Transparency)
> 	* pp biểu diễn có cho phép diễn giải về các hoạt động và các kết luận của hệ thống?

## I. Biểu diễn bằng Luật sản xuất (Production rules)
> [!abstract] 
> * Là các biểu diễn phổ biến nhất trong các hệ cơ sở tri thức
> * Một luật chứa đựng (biểu diễn) tri thức về việc giải quyết một vấn đề nào đó
> * Các luật được tạo nên khá dễ dàng, dễ hiểu.

Một luật được biểu diễn dưới dạng:
![[Pasted image 20230512090728.png]]

* Mệnh đề điều kiện của một luật
	* Không cần sử dụng toán tử logic `OR`
	* Một luật với toán tử logic `OR` trong mệnh đề điều kiện, thì sẽ được chuyển thành một tập các luật tương ứng không chứa `OR`

VD: IF $A_1 \lor A_2$ THEN $B$ -> (IF $A_1$ THEN B) và (IF $A_2$ THEN B)

* Mệnh đề kết luận của một luật
	* Không cần sử dụng thuật toán logic `AND`
	* Một luật với toán tử logic `AND` trong mệnh đề kết luận, thì sẽ được chuyển thành một tâp các luật tương ứng không chứa `AND`

VD: IF ... THEN $B_1 \land B_2$ -> (IF ... THEN $B_1$) và (IF ... THEN $B_2$)

> [!warning] Không cho phép sử dụng toán tử `OR`

![[Pasted image 20230602082720.png]]

> [!note] Các kiểu luật
> Các kiểu luật khác nhau để biểu diễn các kiểu tri thức khác nhau.
> * **Quan hệ liên kết** : 
> 	* `IF addressAt(x, Hospital) THEN heathIs(x, Bad)`
> * **Quan hệ nguyên nhân (kết quả)** : 
> 	* `IF diseaseType(x, Infection) THEN tempIs(x, High)`
> * **Tình huống và hành động (gợi ý)** : 
> 	* `IF diseaseType(x, Infection) THEN takeMedicine(x,Antibiotic)`
> * **Quan hệ logic** :
> 	* `IF tempGreater(x, 37) THEN isFever(x)`

![[Pasted image 20230602083512.png]]

### Vài vấn đề với biểu diễn luật
* **Các luật có chứa các vòng lặp**:
	* IF A THEN A
	* {IF A THEN B, IF B THEN C, IF C THEN A}
* **Các luật có chứa mâu thuẫn**:
	* {IF A THEN  B, IF B THEN C, IF A AND D THEN $\neg$ C} (phủ C)
* **Các kết luận không thể suy ra được (từ các luật hiện có)**
* **Khó khăn trong việc thay đổi (Cập nhật) cơ sở tri thức**
	![[Pasted image 20230602090507.png]]

### Sử dụng các luật trong suy diễn
> [!note] So khớp mẫu (Pattern matching)
> Kiểm tra một luật có thể được sử dụng hay không?
> > [!example] 
> > Ví dụ: Nếu cơ sở tri thức chứa đựng tập các luật {IF A1 THEN B1, IF A1 AND A2 THEN B2, IF A2 AND A3 THEN B3} và các sự kiện (được lưu trong bộ nhớ làm việc) bao gồm A1 và A2, thì 2 luật đầu tiên có thể được sử dụng

> [!note] Chuỗi suy diễn (Chuỗi áp dụng các luật)
> * Xác định trật tử áp dụng các luật trong quá trình suy diễn (với một tập các luật và một tập các sự kiện (giả thiết), các luật nào nên được sử dụng, và theo trật tự nào, để đạt tới một kết luật cần chứng minh)
> * 2 Chiến lược suy diễn:
> 	* **Tiến (Forward)**
> 	* **Lùi (Backward)**

> [!info] Chiến lược suy diễn tiến (Forward reasoning)
> > Phương pháp xây dựng các kết quả dựa trên các dữ kiện đã biết và các quy tắc suy diễn
> * Bắt đầu với các giả định ban đầu hoặc các sự kiện đã biết, sau đó áp dụng các quy tắc suy diễn để tìm ra các kết luận mới.
> * Kết quả từ mỗi bước suy diễn tiến có thể được sử dụng làm dữ liện cho các bước suy diễn tiếp theo.
> 
> -> *Phương pháp được sử dụng trong hệ thống chuyên gia và hệ thống dựa trên luật để tìm ra các kết quả dựa trên thông tin đã biết và các quy tắc đã được xác định trước*

> [!info] Chiến lược suy diễn lùi (Backward reasoning)
> > Phương pháp xây dựng các dẫn xuất dựa trên mục tiêu hoặc kết quả mong muốn và các quy tắc suy diễn.
> 
> * Bắt đầu với một mục tiêu hoặc kết quả mong muốn, sau đó áp dụng các quy tắc suy diễn để tìm ra các điều kiện hoặc giả định cần thiết để đạt được mục tiêu đó.
> * Kết quả từ mỗi bước suy diễn lùi có thể được sử dụng làm điều kiện cho các bước suy diễn tiếp theo.
> 
> -> *Phương pháp được sử dụng trong hệ thống gợi ý và hệ thống quyết định để tìm ra các điều kiện cần thiết để đạt được mục tiêu mong muốn.*

> [!example]-
> Để minh họa hai chiến lược suy diễn, ta sẽ sử dụng một ví dụ đơn giản liên quan đến việc xác định một loài động vật.
> Giả sử chúng ta có các thông tin sau:
> 1. Động vật A có lông và có vú.
> 2. Động vật A không có cánh.
> 3. Gấu là một động vật A.
> 
> Sử dụng chiến lược suy diễn tiến:
> - Với các thông tin trên, ta có thể áp dụng suy diễn tiến để đưa ra kết luận về đặc điểm của gấu.
> - Bước 1: Động vật A có lông và có vú.
> - Bước 2: Động vật A không có cánh.
> - Bước 3: Gấu là một động vật A.
> - Kết luận: Gấu có lông, có vú và không có cánh.
> 
> Sử dụng chiến lược suy diễn lùi:
> - Giả sử chúng ta muốn xác định xem động vật B có thuộc loài động vật A hay không.
> - Bước 1: Động vật B không có cánh.
> - Bước 2: Động vật B có lông và có vú.
> - Kết luận: Động vật B thuộc loài động vật A.
> 
> Trong cả hai ví dụ trên, chúng ta sử dụng suy diễn tiến để đi từ các giả định ban đầu đến kết quả cuối cùng. Trong ví dụ đầu tiên, ta đi từ thông tin về động vật A đến kết luận về đặc điểm của gấu. Trong ví dụ thứ hai, ta sử dụng suy diễn lùi để xác định xem động vật B có thuộc loài động vật A hay không dựa trên các điều kiện cần thiết.

### Giải quyết xung đột
> Một xung đột có thể xảy ra khi nhiều hơn một luật có thể áp dụng được (phù hợp với các sự kiện trong bộ nhớ làm việc)

> [!warning] Một xung đột ko phải là một mâu thuẫn của tập luật

* Cần có một chiến lược giải quyết xung đột (Conflict Resolution Strategy - CRS) để **quyết định luật nào được ưu tiên áp dụng**.
	* Lựa chọn CRS thích hợp có thể cải thiện quá trình suy diễn của hệ thống.

#### Chiến lược giải quyết xung đột - CRS
* Áp dụng luật **xuất hiện đầu tiên** (theo thứ tự) trong cơ sở tri thức
	* Không áp dụng các luật sinh ra từ kết quả đã có trong bộ nhớ làm việc

* Áp dụng luật **cụ thể nhất** (luật có nhiều điều kiện nhất)

* Áp dụng các luật phù hợp với các sự kiện được đưa vào trong bộ nhớ làm việc **gần thời điểm hiện tại nhất**

* Không áp dụng lại 1 luật, nếu nó vẫn sinh ra cùng 1 tập các sự kiện như lần trước.

* Áp dụng luật **có độ tin cậy cao nhất**

* Có thể kết hợp các chiến lược trên.

### Hệ thống suy diễn dựa trên luật
Kiến trúc điển hình của một hệ thống suy diễn dựa trên luật (RBS)
![[Pasted image 20230604164201.png]]

> [!info] Bộ nhớ làm việc (Working memory)
> * Lưu trữ các sự kiện (các giả thiết đúng, đã được chứng minh)
> * Các sự kiện này sẽ quyết định những luật nào được áp dụng (bởi interpreter)

> [!info] Bộ nhớ các luật (Rule memory)
> * Chính là cơ sở tri thức của hệ thống
> * Lưu giữ các luật có thể áp dụng

> [!info] Bộ diễn dịch (Interpreter)
> * Hệ thống bắt đầu bằng việc đưa một sự kiện (dữ liệu) phù hợp vào bộ nhớ làm việc
> * Khi sự kiện (dữ liệu) trong bộ nhớ làm việc phù hợp với các điều kiện của một luật trong bộ nhớ các luật, thì luật đó sẽ được áp dụng.

> [!check] Ưu điểm của RBS
> * Cách biểu diễn (diễn đạt) phù hợp
> 	* Rất gần với cách diễn đạt trong ngôn ngữ tự nhiên
> 	* Rất dễ dàng để diễn đạt nhiều tri thức bởi các luật
> * Dễ hiểu
> 	* Các luật dạng IF-THEN rất dễ hiểu đối với người sử dụng
> 	* Trong một lĩnh vực (bài toán) cụ thể, cách biểu diễn bằng luật giúp các chuyên gia có thể đánh giá và cải tiến các luật
> * Một cách biểu diễn tri thức theo kiểu khai báo (declarative)
> 	* Thu thập tri thức (ở dạng các luật IF-THEN) về một lĩnh vực cụ thể, và đưa chúng vào trong một cơ sở các luật (rule base)
> 	* (Có thể) không cần phải quan tâm đến khi nào, làm thế nào, và theo trật tự nào mà các luật được sử dụng (Hệ thống sẽ tự động đảm nhận các nhiệm vụ này)

> [!failure] Nhược điểm của RBS
> * Khả năng biểu diễn (diễn đạt) bị giới hạn
> 	* Nhiều lĩnh vực bài toán thực tế ko phù hợp với cách biểu diễn dạng IF-THEN
> * Sự tương tác giữa các luật và trật tự của các luật trong cơ sở luật có thể gây ra các hiệu ứng không mong muốn.
> 	* Trong quá trình thiết kế (design) và bảo trì (maintenance) một cơ sở luật: mỗi luật mới được đưa vào cần phải được cân nhắc với các luật đã có từ trước đó.
> 	* Rất khó khăn và tốn kém chi phí để xem xét tất cả các tương tác có thể giữa các luật

## II. Biểu diễn bằng Khung (Frames)
> Biểu diễn một đối tượng bằng : **(OBJECT, PROPERTY, VALUE)**

* Nếu gộp nhiều thuộc tính của cùng một kiểu đối tượng thành 1 cấu trúc -> Biểu diễn hướng đối tượng (object-centered representation)

* Bằng cách sử dụng obj - prop - val, ta có thể biêu diễn các đối tượng
	* **Đối tượng cụ thể (Physical objects)**: Một cái bàn có các thuộc tính chất liệu bề mặt, số ngăn kéo, độ rộng, độ dài, độ cao, màu sắc, ...
	* **Các tình huống (Situations)**: Một lớp học có các thuộc tính mã số phòng học, danh sách sinh viên tham dự, giáo viên, ngày học, thời gian học, ...

> [!note] Các loại khung
> * **Individual Frames**: biểu diễn một đối tượng cụ thể
> * **Generic Frames:** biểu diễn một lớp (loại) các đối tượng

* Biểu diễn một khung:
![[Pasted image 20230604183307.png]]

## III. Biểu diễn bằng Mạng ngữ nghĩa (Semantic networks)

## IV. Biểu diễn bằng Ontology

## V. Biểu diễn bằng các Mô hình xác suất (probabilistic models)

    