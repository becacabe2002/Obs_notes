* Trong bất cứ các quy trình phát triển phần mềm nào, cũng cần áp dụng mô hình phát triển thác nước

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

* **Failure** - sk khi hệ thống có hành vi không tương ứng với các hành vi đặc tả của hệ thống.

* **Error** <-(gây ra)- **Fault**

* **Fault localizing** - xác định lỗi

> [!note] Chất lượng phần mềm
> * Mức độ một hệ thống hay một thành phần hay một tiến trình đạt được các yêu cầu đặt ra.
> * Mức độ một hệ thống hay một thành phần hay một tiến trình đạt được những mong đợi của kh hay người dùng hệ thống đó.

* **2 cách** tiếp cận chính khi xây dựng các mô hình chất lượng.
	* Mô hình chuẩn
	* Các mô hình mang tính thực dụng hơn.

* Mỗi mô hình chất lượng được xây dựng xựa trên: 
	* **Nhân tố** (factors) - trong các mô hình chất lượng được sử dụng để mô tả góc nhìn từ phía bên ngoài đối với sản phẩm phần mềm hay góc nhìn từ quan điểm người dùng sp.
	* **Tiêu chí** (criteria) - trong các mô hình chất lượng được sử dụng để mô tả góc nhìn từ bên trong của sản phẩm phần mềm, hay góc nhìn về quan điểm chất lượng phần mềm từ developer.
	* **Độ đo** (Metrics) - định nghĩa và sử dụng để cung cấp một thước đo và phương pháp cụ thể để đo lường một cách định tính hoặc định lượng các tiêu chí chất lượng phần mềm.

