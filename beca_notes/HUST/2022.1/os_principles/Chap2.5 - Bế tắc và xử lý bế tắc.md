## 5.1 Khái niệm bế tắc
> [!info] Bế tắc là tình trạng
> * Hai hay nhiều tiến trình cùng chờ đợi một sự kiện nào đó xảy ra
> * Nếu ko có sự tác động gì từ bên ngoài, sự chờ đợi là vô hạn

![[Hệ Điều Hành-Chuong 2-223-237 (1).pdf]]

## 5.2 Điều kiện xảy ra bế tắc

^811e7f

* **Cần có 4 điều kiện (ko thiếu bất cứ đk nào)**
> [!note] Tồn tại tài nguyên găng
> * TN được sử dụng theo mô hình **không phân chia được**
> 	* Chỉ có 1 TT dùng TN tại 1 thời điểm
> 	* TT khác cũng yêu cầu TN => Yêu cầu phải được hoãn lại tới khi TN  được giải phóng

> [!note] Chờ đợi trước khi vào đoạn găng
> * TT không được vào đoạn găng phải xếp hàng chờ đợi.
> * Trong khi chờ đợi vẫn chiếm giữ các TN được cung cấp

>[!note] Không có hệ thống phân phối tài nguyên găng
>* TN ko thể được trưng dụng
>* TN được giải phóng chỉ bởi TT đang chiếm giữ khi đã hoàn thành nhiệm vụ.

> [!Chờ đợi vòng tròn]
> * Tồn tại tập các TT {P_0,  P_2, ... P_n} đang đợi nhau theo kiểu: 
> ```C
> P_0 -> R_1 -> P_1; P_1 -> R_2 -> P_2; ...; P_n -> R_0 -> P_0
> ```
> * Chờ đợi vòng tròn tạo ra chu trình không kết thúc

### Đồ thị cung cấp tài nguyên (Resource Allocation Graph)
> Mô hình hoá tình trạng bế tắc trong hệ thống.

> [!note] Kết cấu 
> Đồ thị định hướng gồm tập đỉnh V và tập cung E
> * Tập đỉnh V chia thành 2 kiểu:
> 	* P = { P_1, P_2,..., P_n} - chứa tất cả các Tiến trình trong hệ thống
> 	* R = { R_1, R_2, ... , R_m} - chứa tất cả các kiểu Tài nguyên  trong hệ thống
> * Tập cung E gồm hai loại:
> 	* **Cung yêu cầu**: đi từ TT P_i tới TN R_j : $P_i \rightarrow R_j$
> 	* **Cung sử dụng**: đi từ TN R_j tới TT P_i: $R_j \rightarrow P_i$

* Khi 1 TT yêu cầu TN R_j
	* Cung yêu cầu P_i -> R_j được chèn vào đồ thị
	* Nếu yêu cầu được thoả mãn, cung yêu cầu chuyển thành cung sử dụng R_j -> P_i
	* Khi TT P_j giải phóng TN R_j, cung sử dụng R_j -> P_j bi xoá khỏi đồ thị

![[Pasted image 20221130225401.png]]

![[Hệ Điều Hành-Chuong 2-245-248.pdf]]

> [!warning] Lập luận về sự bế tắc
> * Đồ thị không chứa chu trình -> Không có sự bế tắc
> * Nếu đồ thị **chứa chu trình**:
> 	* Nếu TN chỉ có 1 đơn vị => Bế tắc
> 	* Nếu TN có nhiều hơn 1 đơn vị -> có khả năng bế tắc

## 5.3 Các PP xử lý bế tắc
* **Phòng ngừa**:
	* Áp dụng **các biện pháp** để đảm bảo hệ thống **không bao giờ** rơi vào tình trạng **bế tắc**
	* Tốn kém
	* Áp dụng cho hệ thống **hay xảy ra bế tắc** và tổn thất do bế tắc gây ra **lớn**

* **Phòng tránh** : 
	* **Kiểm tra từng yêu cầu TN** của TT và **không chấp nhận** yêu cầu nếu việc cung cấp TN **có khả năng** dẫn đến tình trạng **bế tắc**.
	* Thường yêu cầu các thông tin phụ trợ
	* Áp dụng cho hệ thống **ít xảy ra bế tắc** nhưng **tổn hại lớn**

* **Nhận biết và khắc phục**
	* Cho phép hệ thống hoạt động bình thường (có thể rơi vào tình trạng bế tắc)
	* **Định kì kiểm tra** xem bế tắc có đang xảy ra không
	* Nếu đang bế tắc, **áp dung các biện pháp** loại bỏ bế tắc
	* Áp dụng cho hệ thống **ít xảy ra** bế tắc và thiệt hại **không lớn**

## 5.4 Phòng ngừa bế tắc 
> [!abstract] Nguyên tắc
> Tác động vào 1 trong 4 điều kiện cần của bế tắc để nó ko xảy ra
> [[Chap2.5 - Bế tắc và xử lý bế tắc#5.2 Điều kiện xảy ra bế tắc]]

### Điều kiện tài nguyên găng
* Giảm bớt **mức độ găng** của hệ thống
	* TN phân chia được (VD: file chỉ để đọc) : **sử dụng đồng thời**
	* TN ko phân chia được : **sử dụng không đồng thời**

* SPOOL (simultaneous peripheral operation on-line): 
	* Không phân phối TN khi không thực sự cần thiết
	
	* Chỉ có một số ít TT có khả năng yêu cầu TN

![[Pasted image 20221130234158.png]]

> [!warning] Không phải tài nguyên nào cũng dùng kỹ thuật SPOOL được

### Điều kiện chờ đợi trước khi vào TN găng
> [!abstract] Nguyên tắc
> Đảm bảo 1 TT xin TN chỉ khi không sở hữu bất kỳ TN nào khác

* **Cung cấp trước**
	* TT xin toàn bộ TN ngay từ đầu và chỉ thực hiện khi đã có đầy đủ TN
	* Hiệu quả sử dụng tài nguyên thấp
		* TT chỉ sử dụng TN ở giai đoạn cuối
		* Tổng số TN đòi hỏi vượt quá khả năng của hệ thống
### Điều kiện trưng dụng tài nguyên găng

### Điều kiện chờ đợi vòng tròn


## 5.5 Phòng tránh bế tắc
### Thuật toán người quản lý nhà băng
## 5.6 Nhận biết và khắc phục
> [!abstract] Nguyên tắc
> * Không áp dụng áp dụng các biện pháp phòng ngừa hoặc phòng tránh, để cho bế tắc xảy ra
> * Định kỳ kiểm tra xem bế tắc có đang xảy ra không.
> * Nếu có bế tắc khắc phục
> * Hệ thống cần phải cung cấp: 
> 	* Thuật toán xác định hệ thống đang bế tắc không
> 	* Biện pháp kỹ thuật chữa bế tắc

### Nhận biết - thuật toán dựa trên đồ thị cung cấp tài nguyên

### Nhận biết - thuật toán chỉ ra bế tắc tổng quát

### Khắc phục - Kết thúc tiến trình

### Khắc phục - Trưng dụng tài nguyên
