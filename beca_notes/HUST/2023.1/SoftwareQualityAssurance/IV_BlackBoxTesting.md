> Kiểm thử được thực hiện dựa trên yêu cầu và đặc tả của chức năng (chỉ quan tâm đầu ra của chức năng mà không quan tâm tới cấu trúc bên trong)
## 1. Equivalance Class partitioning (phân chia lớp tương đương)
> [!info] Lớp tương đương (EC)
> Tập hợp các điểm dữ liệu cho phép chương trình có cùng 1 hành xử. 

* Tất cả các điểm dữ liệu trong lớp là tương đương nhau

* hai lớp cơ bản
	* **Valid class**
	* **Invalid class**

Ex: giá trị x chỉ có thể dao động từ 0 tới 10
* Valid class: 0 <= x <= 10
* Invalid class: x < 0 và x > 10

> [!note] 
> Một testcase tốt khi:
> * Giảm thiểu số lượng các ca kiểm thử khác mà phải được phát triển để hoàn thành mục tiêu đã định của kiểm thử "hợp lý"
> * Bao phủ một tập lớn các ca kiểm thử khác

### 1.1 Xác định các lớp tương đương
* lấy mỗi trạng thái đầu vào và phân chia thành 2 hay nhiều nhóm:
	* Các lớp tương đương hợp lệ: các đầu vào hợp lệ
	* Các lớp tương đương không hợp lệ: mô tả các trạng thái khác của chương trình (sai, thiếu ...)

**NGUYÊN TẮC XÁC ĐỊNH LỚP TƯƠNG ĐƯƠNG**:
* **NT1**: điều kiện đầu vào định rõ giới hạn của một mảng thì chia vùng tương đương thành 3 TH:
	* 1 lớp tương đương hợp lệ
	* 2 lớp tương đương không hợp lệ

Ex: giá trị x nằm trong khoảng 0 -> 10
* valid: 0 <= x <= 10
* invalid:
	* x < 0
	* x > 10

* **NT2**: điều kiện đầu vào là một giá trị xác định thì chia thành 3 TH:
	* 1 lớp tương đương hợp lệ với giá trị = giá trị điều kiện
	* 2 lớp tương đương không hợp lệ với giá trị nằm ở hai đầu của giá trị điều kiện

Ex: x = 10
* valid: x = 10
* invalid:
	* x < 10
	* x > 10

* **NT3**: điều kiện đầu vào chỉ giá định 1 tập giá trị, xác định mỗi giá trị trong đó là một lớp tương đương hợp lệ. Chia thành 2 TH:
	* Các lớp tương đương hợp lệ
	* 1 lớp tương đương không hợp lệ

Ex: Các loại xe được đăng ký là xe bus, xe khách, xe tải, xe taxi và xe máy
* valid: 5 lớp tương đương hợp lệ tương ứng với 5 loại xe: "xe bus", "xe khách", "xe tải", "xe taxi" và "xe máy"
* invalid: "xe đạp"

* **NT4**: nếu đk đầu vào là một kiểu đúng sai, 2 TH:
	* Lớp tương đương hợp lệ: đúng
	* Lớp tương đương không hợp lệ: sai

### 1.2 Xác định testcases
1. Gán 1 số duy nhất cho mỗi lớp tương đương
2. Cho tới khi tất cả các lớp tương dduong hợp lệ được bao phủ bởi testcases, viết 1 ca kiểm thử mới bao phủ càng nhiều các lớp tương đương đó càng tốt.
3. Cho tới khi tất cả các lớp tương đương không hợp lệ được bao phủ, viết 1 ca kiểm thử mà bao phủ một và chỉ một trong các lớp tương đương hợp lệ chưa được bao phủ.
4. Lý do mà mỗi ca kiểm thử riêng bao phủ các trường hợp không hợp lệ là vì các kiểm tra đầu vào không đúng nào đó che giấu hoặc thay thế các kiểm tra đầu vào không đúng khác.

Ex:
Nếu đi xe điện trong khoảng 9h30 -> 16h hoặc sau 19h30, thay vì mua vé thường, ta sẽ được mua vé tiết kiệm. Giả sử tàu hoạt động từ 4h sáng -> 23h
* Liệt kê các vùng hợp lệ và không hợp lệ
* Viết các tcs để test dựa trên các vùng tương đương

Các vùng (0 – 9h30) , (9hh31 – 16h), (16h01 – 19h30), (19h31 – 23h59)
Vé thường:
* Valid: (0 – 9h30), (16h01 – 19h30)
* Invalid: (9hh31 – 16h), (19h31 – 23h59)
Vé tiết kiệm:
* Valid: (9hh31 – 16h), (19h31 – 23h59)
* Invalid: (0 – 9h30), (16h01 – 19h30)
![[IV_BlackBoxTesting-20231211094118981.webp]]
* Các TCs: 
	* TC2 - Xuất phát lúc 3:00 - Không hợp lệ
	* TC5 - Xuất phát lúc 5:30 - Vé bình thường
	* TC8 - Xuất phát lúc 12:00 - Vé tiết kiệm
	* TC11 - Xuất phát lúc 18:00 - Vé bình thường
	* TC14 - Xuất phát lúc 21:00 - Vé tiết kiệm
## 2. Boundary Value Analysis

## 3. Decision Table

## 4. State Transition Testing
