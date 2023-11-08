![[4_Architectural Design-20231022033830294.webp]]
* Từ đầu ra SRS, thông qua bước phân tích và thiết kế, ta thu được Design Model, Architecture Document và Data Model.

> [!caution] Quá trình "Analysis and Design" không tuân theo Bottom-Up hay Top-down.

> [!note] Mục tiêu của phân tích Use-case
> * Giải thích mục tiêu của Use-case và vị trí bắt đầu của lifecycle của nó.
> * Xác định các class có thể thể hiện luồng sự kiện của usecase
> * Phân bổ các hành vi của use-case tới các class đó, xác định vai trò của các class.
> * Phát triển use-case realizations mô hình hóa sự tương tác giữa các đối tượng của lớp xác định.

![[4_Architectural Design-20231022034712267.webp]]
*(Use-Case Analysis trong ngữ cảnh thực)*

![[4_Architectural Design-20231022034945621.webp]]

![[4_Architectural Design-20231022035545403.webp]]

* **Boundary Classes**:
	* đứng giữa giao diện và thế giới bên ngoài (phụ thuộc vào các tương tác ngoài)
		* User interface class: tập trung vào các thông tin được trình bày tới user
		* System interface class: tập trung vào các protocols phải được định nghĩa
			* Ko cần tập trung vào cách thức implement của protocols
		* Device interface class
	* Một boudary class cho mỗi cặp actor/usecase
	![[4_Architectural Design-20231022040953763.webp]]

* **Entity Classes**: 
	* Độc lập với môi trường (chứa và quản lý thông tin trong hệ thống)

* **Control Classes**:
	* Cung cấp các hành vi phối hợp với hệ thống 
	* cụ thể hóa cho từng usecase (phụ thuộc vào use-case, độc lập với môi trường)
	* thường sẽ có 1 control class cho mỗi usecase (có thể có nhiều hơn)

### Phân bổ các hành vi tới các lớp
* Với mỗi luồng sự kiện của use-case:
	* Xác định các lớp phân tích
	* phân bổ các trách nhiệm của ca sử dụng tới các lớp phân tích
	* Mô hình hóa các lớp phân tích bằng các interaction diagrams
	![[4_Architectural Design-20231022042429820.webp]]

### Các Architectural Patterns
* MVC
* Front-end Back-end
* MVVM, MVP (android)
