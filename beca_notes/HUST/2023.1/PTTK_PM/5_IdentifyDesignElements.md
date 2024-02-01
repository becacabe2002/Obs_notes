- 
![[5_IdentifyDesignElements-20231022042714690.webp]]

![[5_IdentifyDesignElements-20231022042740393.webp|528]]

![[5_IdentifyDesignElements-20231022043731669.webp]]
*(map từ lớp phân tích tới đối tượng thiết kế)*
* Một lớp phân tích có thể được map trực tiếp tới 1 lớp thiết kế nếu nó là một lớp đơn giản, thể hiện một logic đơn
	* Lớp phân tích phức tạp hơn có thể được chia thành nhiều lớp || trở thành 1 subsystem

### Nhóm các lớp phân tích vào Packages
* Các yếu tố có thể dựa vào để phân Package:
	* Đơn vị cấu hình
	* Phân bổ nguồn lực giữa các nhóm phát triển
	* Phản ánh loại người dùng
	* Đại diện cho các sản phẩm và dịch vụ hiện có trên hệ thống.

* **Boundary Classes**:
	![[5_IdentifyDesignElements-20231022044633835.webp]]
	* TH1: giao diện hệ thống sẽ có những thay đổi đáng kể
	* TH2: giao diện hệ thống sẽ không có những thay đổi đáng kể

* **Functionally Related Classes**:
	* Các yếu tố xác định:
		* Hai đối tượng trao đổi nhiều message
		* Một lớp biên sẽ liên hệ về mặt chức năng với lớp đối tượng nếu các function của lớp biên là để thể hiện lớp đố tượng
		* Hai lớp tương tác với, hoặc chịu ảnh hưởng bởi sự thay đổi của cùng tác nhân

> [!caution] Hai lớp không nên đặt cùng package
> * Hai lớp liên hệ tới các tác nhân khác nhau
> * Lớp bắt buộc và lớp tùy chọn ko nên để chung package

![[5_IdentifyDesignElements-20231022045300807.webp]]
* Theo quan điểm của nguyên tắc đóng gói, chỉ có các lớp public mới có thể truy nhập từ bên ngoài.

> [!note] Package Coupling
> * Các package ko nên phụ thuộc chéo
> * Packages ở tầng thấp hơn không nên phụ thuộc vào package ở tầng cao hơn.
> * Ko nên nhảy cóc tầng
![[5_IdentifyDesignElements-20231022080715967.webp]]

## Subsystems and interfaces
> Subsystems:
> * Một behavior được đóng gói riêng biệt
> * Thể hiện khả năng độc lập với các interfaces rõ ràng (tái sử dụng)
> * Để phân chia hệ thống thành các thành phần phát triển độc lập, có thể thay đổi mà không gây nứt gẫy tới các phần khác của hệ thống.

![[5_IdentifyDesignElements-20231022081615171.webp|486]]

| Subsystems                  | Packages                          |
| --------------------------- | --------------------------------- |
| Cung cấp behavior           | Không cung cấp behavior           |
| Hoàn toàn đóng gói nội dung | Không hoàn toàn đóng gói nội dung |
| Được thay thế dễ dàng       | Không thể thay thế dễ dàng        |

* Một subsystem có thể triển khai 1 hoặc nhiều giao diện giúp định nghĩa hành vi của nó.

![[5_IdentifyDesignElements-20231022083059610.webp]]

### Candidate Subsystems
Các thành phần có thể trở thành **subsystems**:
* Lớp phân tích:
	* Cung cấp các dịch vụ (tiện ích) phức tạp
	* Các lớp biên (User interfaces và interfaces hệ thống ngoài)
* Các sản phẩm hiện có hoặc hệ thống ngoài trong thiết kế:
	* Phần mềm giao tiếp
	* Hỗ trợ truy nhập Database
	* Các dạng cấu trúc dữ liệu?
	* các tiện ích thông dụng
	* Sản phẩm riêng biệt của ứng dụng
![[5_IdentifyDesignElements-20231022084146505.webp]]

