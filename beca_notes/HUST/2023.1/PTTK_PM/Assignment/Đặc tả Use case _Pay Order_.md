## 1. Mã Use case
UC0041
## 2. Giới thiệu
Use case mô tả quá trình thực hiện thanh toán của người dùng

## 3. Tác nhân
Khách hàng

## 4. Tiền điều kiện
Đặt hàng thành công

### 5. Luồng sự kiện chính (Thành công)
1. *The AIMS software displays the payment screen*
2. *The customer enters  credit card infor and confirms to pay order.*
3. *The AIMS software asks the Interbank to process the payment transaction*
4. *The Interbank processes the payment transaction*
5. *The AIMS software saves the payment transaction.*
6. *The AIMS software displays transaction information*

## 6. Luồng sự kiện thay thế

| **STT** | **Vị trí** | **Điều kiện**                  |                      **Hành động**                      | **Vị trí tiếp tục** |
|:------- |:---------- | ------------------------------ |:-------------------------------------------------------:| ------------------- |
| 1       | Tại bước 3 | Nếu thông tin thẻ không hợp lệ | Hệ thống AIMS thông báo rằng thông tin thẻ không hợp lệ | Tại bước 1          |
| 2       | Tại bước 5 | Nếu tài khoản không đủ         |     Hệ thống AIMS thông báo rằng tài khoản không đủ     | Tại bước 1          |
| 3       | Tại bước 5 | Nếu thông tin thẻ sai          |    Hệ thống AIMS thông báo rằng thông tin thẻ bị sai    | Tại bước 1          |

## 7. Biểu đồ hoạt động
![[Pay Order (new).png]]
*Biểu đồ hoạt động của usecase "Pay Order"*

## 8. Dữ liệu đầu vào
| No  | Trường dữ liệu | Mô tả | Bắt buộc | Điều kiện hợp lệ                       | Ex                  |
| --- | -------------- | ----- | -------- | -------------------------------------- | ------------------- |
| 1   | Tên chủ thẻ    |       | Có       | Tối đa 50 kí tự                        | NGO MINH TU         |
| 2   | Số thẻ         |       | Có       | 16 chữ số                              | 1234 5678 1234 5678 |
| 3   | Ngày hết hạn   |       | Có       | Bao gồm tháng và 2 chữ số cuối của năm | 10/25               |
| 4   | Mã bảo mật     |       | Có       | 3 chữ số                               | 123                    |
## 9. Dữ liệu đầu ra
| No  | Trường dữ liệu      | Mô tả | Hình thái hiển thị           |                  Ex |
| --- | ------------------- | ----- | ---------------------------- | -------------------:|
| 1   | Mã giao dịch        |       |                              |                     |
| 2   | Tên chủ thẻ         |       |                              |         NGO MINH TU |
| 3   | Số tiền             |       | Căn lề phải. Kí hiệu tiền tệ |       1.200.000 VND |
| 4   | Thông tin giao dịch |       |                              | Thanh toan don hang |
| 5   | Ngày giao dịch      |       | dd/mm/yyyy                   |            3/9/2022 | 

## 10. Hậu điều kiện
Không