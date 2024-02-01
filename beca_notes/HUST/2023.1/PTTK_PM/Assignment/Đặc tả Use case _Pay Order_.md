## 1. Mã Use case
UC0041
## 2. Giới thiệu
Use case mô tả quá trình thực hiện thanh toán của người dùng

## 3. Tác nhân
Khách hàng

## 4. Tiền điều kiện
Người dùng bấm nút xác nhận thanh toán ở màn hình hiển thị invoice

### 5. Luồng sự kiện chính (Thành công)
1. *The AIMS software displays the payment screen*
2. *The customer choose payment method: VNPay or Paypal*
3. *The AIMS software displays payment web portal*
4. *The customer perform payments in that webview .*
5. *Subsystem processes the payment transaction and return response.*
6. *The AIMS software saves the payment transaction.*
7. *The AIMS software displays transaction information*

## 6. Luồng sự kiện thay thế

| **STT** | **Vị trí** | **Điều kiện** | **Hành động** | **Vị trí tiếp tục** |
| :--- | :--- | ---- | :--: | ---- |
| 1 | Tại bước 5 | Nếu người dùng gián đoạn  quá trình thanh toán giữa chừng | Hệ thống AIMS thông báo thanh toán không thành công | Tại bước 1 |
| 2 | Tại bước 5 | Nếu response trả về thanh toán không thành công | Hệ thống AIMS thông báo giao dịch không thành công. <br> Hệ thống không lưu thông tin giao dịch. | Tại bước 1 |

## 7. Biểu đồ hoạt động
![[Pay Order (new).png]]
*Biểu đồ hoạt động của usecase "Pay Order"*

## 8. Dữ liệu đầu vào
| No  | Trường dữ liệu   | Mô tả                  | Bắt buộc | Điều kiện hợp lệ | Ex       |
| --- | ---------------- | ---------------------- | -------- | ---------------- | -------- |
| 1   | Khoản thanh toán | Số tiền cần thanh toán | Có       | dạng long        | 10000000 |
| 2    | Phương thức thanh toán                 |                        | Có         | 1 trong hai trường định sẵn (VNPay/Paypal)                 |          |

## 9. Dữ liệu đầu ra
| No | Trường dữ liệu | Mô tả | Hình thái hiển thị | Ex |
| ---- | ---- | ---- | ---- | ---: |
| 1 | Mã hóa đơn |  | Int | 30 |
| 2 | Người đặt hàng |  | String | user1 |
| 3 | Hình thức thanh toán |  | String | VNPay |
| 4 | Trạng thái thanh toán |  | String | success |
| 5 | Tổng tiền |  | Int | 100 |

## 10. Hậu điều kiện
Không