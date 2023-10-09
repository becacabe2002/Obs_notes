## 1. Mã Use case
UC0040
## 2. Giới thiệu
Use case mô tả quá trình đặt hàng chuyển phát nhanh của người dùng

## 3. Tác nhân
Khách hàng

## 4. Tiền điều kiện
không có

### 5. Luồng sự kiện chính (Thành công)
1. *Customer chooses Place rush order option.*
2. *The AIMS software checks products and delivery addresses whether support rush delivery or not.*
3. *The AIMS software requires customers to update rush delivery information.*
4. *The AIMS software updates shipping fee calculation, recalculate shipping fee.*

## 6. Luồng sự kiện thay thế

|**STT**|**Vị trí**|**Điều kiện**|**Hành động**|**Vị trí tiếp tục**|
|:---|:---|---|:---:|---|
|1|Tại bước 2|Nếu không có sản phẩm nào hỗ trợ giao hàng nhanh|Hệ thống AIMS thông báo rằng không có sản phẩm hỗ trợ giao hàng nhanh và yêu cầu người dùng cập nhật thông tin giao hàng|Kết thúc usecase|
|2|Tại bước 2|Nếu địa chỉ giao hàng không hỗ trợ giao hàng nhanh|Hệ thống AIMS thông báo rằng địa chỉ giao hàng không hỗ trợ giao hành nhanh và yêu cầu người dùng cập nhật thông tin giao hàng|Kết thúc usecase|

## 7. Biểu đồ hoạt động
![[Call Place Rush Order.png]]
*Biểu đồ hoạt động của usecase "Đặt hàng"*

## 8. Dữ liệu đầu vào
| No  | Trường dữ liệu           | Mô tả                                            | Bắt buộc | Điều kiện hợp lệ                                                        | Ex                                                                                                                                                                 |
| --- | ------------------------ | ------------------------------------------------ | -------- | ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | Thông tin giao hàng      | Các thông tin giao hàng đã được khách hàng nhập  | Có       | Tất cả các trường phải hợp lệ theo điều kiện trong đặc tả "Place Order" | {"ReceiverName": "Ngo Minh Tu",</br>"PhoneNumber":"0987654321",</br>"Province":"Hanoi",</br>"Address":"số 9, ngõ X, Phố Y, Quận Z",</br>"ShippingInstructions":""} | 
| 2   | Danh sách hàng trong giỏ | Danh sách mã sản phẩm có trong giỏ của khác hàng | Có       | Dãy có kích thước tương đương số loại hàng                              | [SP102, SP103, SP104]                                                                                                                                              |
| 3   | Thời gian nhận giao hàng | Thời gian nhận giao hàng cho giao hàng nhanh     | Có       | Có dạng dd/mm/yyyy. Thời gian không quá thời gian đặt hàng 3 tháng      | 10/09/2022                                                                                                                                                         |
## 9. Dữ liệu đầu ra
Không

## 10. Hậu điều kiện
Không