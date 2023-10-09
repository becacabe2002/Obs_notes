## 1. Mã Use case
UC0040
## 2. Giới thiệu
Use case mô tả quá trình đặt hàng của người dùng

## 3. Tác nhân
Khách hàng

## 4. Tiền điều kiện
không có

### 5. Luồng sự kiện chính (Thành công)
1. *The customer requests to place order in the cart.*
2. *The AIMS software checks the availability of products in the cart.*
3. *The AIMS software displays the form of delivery information.*
4. *The customer enters and submits delivery information.*
5. *The AIMS software calculates shipping fees*
6. *The AIMS software  displays the invoice*
7. *The customer confirms to place order.*
8. ***The AIMS software calls UC "Pay order"***
9. *The AIMS software creates a new order.*
10. *The AIMS software makes the cart empty.*
11. *The AIMS software sends notification email and the order information.*
12. *The AIMS software displays the successful order notification and the order information.*



## 6. Luồng sự kiện thay thế

|**STT**|**Vị trí**|**Điều kiện**|**Hành động**|**Vị trí tiếp tục**|
|:---|:---|---|:---:|---|
|1|Tại bước 3|Nếu sản phẩm không còn hàng|Hệ thống AIMS thông báo rằng có sản phẩm trong giỏ hàng không còn hàng và yêu cầu người dùng cập nhật giỏ hàng|Kết thúc usecase|
|2|Tại bước 5|Nếu thông tin giao hàng không hợp lệ|Hệ thống AIMS thông báo rằng thông tin giao hàng không hợp lệ|Tại bước 3|
|3|Tại bước 5|Nếu người dùng chọn hình thức giao hàng nhanh|Hệ thống AIMS chèn usecase **"Đặt hàng nhanh"**|Tại bước 5|
|4|Tại bước 9|Nếu thanh toán đơn hàng không thành công|Hệ thống AIMS thông báo rằng thanh toán không thành công|Tại bước 8|

## 7. Biểu đồ hoạt động
![[Place Order (new).png]]
*Biểu đồ hoạt động của usecase "Đặt hàng"*

## 8. Dữ liệu đầu vào
| No  | Trường dữ liệu    | Mô tả             | Bắt buộc | Điều kiện hợp lệ | Ex                         |
| --- | ----------------- | ----------------- | -------- | ---------------- | -------------------------- |
| 1   | Tên người nhận    |                   | Có       |                  | Ngo Minh Tu                |
| 2   | SĐT               |                   | Có       | 10 số            | 0987654321                 |
| 3   | Quận              | Chọn từ danh sách | Có       |                  | Hanoi                      |
| 4   | Địa chỉ           |                   | Có       |                  | số 9, ngõ X, Phố Y, Quận Z |
| 5   | Chỉ dẫn giao hàng |                   | Không    |                  |                            | 

## 9. Dữ liệu đầu ra
| No  | Trường dữ liệu     | Mô tả                                                                           | Hình thái hiển thị                                           | Ex                              |
| --- | ------------------ | ------------------------------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------- |
| 1   | Tên                | Tên của sản phẩm media                                                          |                                                              | DVD Phim Cuộc chiến vương quyền |
| 2   | Giá                | Giá tương ứng với sản phẩm                                                      | Dấu `,` ngăn cách đơn vị nghìn. Số nguyên dương. Căn lề phải | 100,000                         |
| 3   | Số lượng           | Số lượng của loại sản phẩm                                                      | Số nguyên dương. Căn lề phải                                 | 3                               |
| 4   | Số tiền            | Số tiền tương ứng của loại sản phẩm                                             | Dấu `,` ngăn cách đơn vị nghìn. Số nguyên dương. Căn lề phải | 300,000                         |
| 5   | Tạm tính trước VAT | Tổng số tiền của các sản phẩm trong giỏ trước thuế VAT                          | Dấu `,` ngăn cách đơn vị nghìn. Số nguyên dương. Căn lề phải | 2,000,000                       |
| 6   | Tạm tính           | Tổng số tiền các sản phẩm sau VAT                                               | (tương tự cái trên)                                          | 2,160,000                       |
| 7   | Phí vận chuyển     |                                                                                 | (tương tự cái trên)                                          | 40,000                          |
| 8   | Tổng tiền          | Số tiền sau cùng khách hàng phải thanh toán (bao gồm sản phẩm và phí giao hàng) | (tương tự cái trên)                                          | 2,200,000                       |
| 9   | Loại tiền          |                                                                                 |                                                              | VND                             |
| 10  | Tên                |                                                                                 |                                                              | Ngo Minh Tu                     |
| 11  | SĐT                |                                                                                 |                                                              | 0987654321                      |
| 12  | Tỉnh               | Chọn từ một danh sách                                                           |                                                              | Hanoi                           |
| 13  | Địa chỉ            |                                                                                 |                                                              | số 9, ngõ X, Phố Y, Quận Z      |
| 14  | Chỉ dẫn giao hàng  |                                                                                 |                                                              |                                 |

## 10. Hậu điều kiện
Không