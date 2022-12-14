## 5.1 Khái niệm bế tắc (Deadlock)
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

> [!warning] Nhận xét
>  Hiệu quả sử dụng tài nguyên thấp
>  * TT chỉ sử dụng TN ở giai đoạn cuối
>  * Tổng số TN đòi hỏi vượt quá khả năng của hệ thống

* **Giải phóng TN**
	* TT giải phóng tất cả TN trước kh xin (xin lại) TN mới

> [!warning] Nhận xét
> * Tốc độ thực hiện TT chậm
> * Phải đảm bảo dữ liệu được giưa trong TN tạm giải phóng ko bị mất

### Điều kiện trưng dụng tài nguyên găng
> [!abstract] Nguyên tắc
> Cho phép trưng dụng tài nguyên khi cần thiết

* TT $P_i$  xin tài nguyên $R_j$
	* $R_j$  sẵn có: cung cấp cho TT
	* $R_j$ không sẵn có: đang bị chiếm dụng bởi tài nguyên $P_k$
		* $P_k$ đang đợi TN khác: 
			* Trưng dụng R_j từ P_k và cung cấp cho P_i theo yêu cầu
			* Thêm R_j vào danh sách các TN đang thếu của P_k
			* P_k được thực hiện trở lại khi có được tiến trình đang thiếu hoặc đòi lại được R_j
		* $P_k$ đang thực hiện:
			* P_i phải đợi (ko được giải phóng tài nguyên)
			* Cho phép trưng dụng TN nhưng **chỉ khi cần thiết**

> [!note] 
> * Chỉ áp dụng cho các TN có thể lưu trữ và khôi phục trạng thái dễ dàng (CPU, Mem)
> * Không áp dụng được cho các TN như máy in

### Điều kiện chờ đợi vòng tròn
[[Chap2.5 - Bế tắc và xử lý bế tắc#^7922c4]]
* Đặt ra một thứ tự toàn cục của tất cả các kiểu TN
	* R = {R_1, R_2, ... , R_n} tập tất cả các kiểu TN 
	* Xây dựng hàm trật tự f: R -> N
		* Hàm f được xây dựng dựa trên trật tự sử dụng các TN
		$f(BangTu) = 1$ 
		$f(DiaTu) = 5$
		$f(MayIn) = 12$
* TT chỉ được yêu cầu TN theo trật tự tăng
	* TT chiếm giữ TN kiểu R_k chỉ được xin TN kiểu R_j thoả mãn **$f(R_j) > f(R_k)$**
	* TT yêu cầu tới TN R_k sẽ phải giải phóng tất cả TN R_i thoả mãn điều kiện **$f(R_i)$ > = $f(R_k)$**

## 5.5 Phòng tránh bế tắc

![[Hệ Điều Hành-Chuong 2-264-269.pdf]]

> [!abstract] Nguyên tắc
> * Phải biết trước các thông tin về TT và TN
> 	* TT phải khai báo lượng TN lớn nhất mỗi loại sẽ yêu cầu khi thực hiện
> * Quyết định dựa trên kết quả kiểm tra t/thái cung cấp TN (Resource - Allocation State) - T/thái hệ thống 
> 	* T/thái cung cấp TN xác định bởi các thông số:
> 		* Số đơn vị TN
> 			* Có sẵn trong hệ thống 
> 			* Đã được cấp cho mỗi TT
> 			* Lớn nhất mỗi TT có thể yêu cầu
> 	*  Nếu hệ thống an toàn, sẽ đáp ứng cho yêu cầu
> * Thực hiện kiểm tra mỗ khi nhận được yêu cầu TN
> 	**-> Đảm bảo trạng thái hệ thống luôn an toàn, chỉ chuyển từ trạng thái an toàn này sang trạng thái an toàn khác**

### Trạng thái an toàn
* Có thể cung cấp TN cho từng TT (đến yêu cầu lớn nhất) theo 1 trật tự nào đấy mà ko xảy ra bế tắc
* Tồn tại ***chuỗi an toàn*** của tất cả các TT

> [!nfo] Chuỗi an toàn
> * Với mỗi TT P_i, mọi yêu cầu TN trong tương lai đều có thể đáp ứng nhờ vào:
> 	* Lượng TN hện có trong hệ thống
> 	* TN đang chiếm giữ bởi tất cả các TT $P_j$ (j < i)
$
* Trong chuỗi an toàn, khi $P_i$ yêu cầu TN
	* Nếu ko thể đáp ứng ngay lập tức, $P_i$ đợi cho tới khi $P_j$ kết thúc (j < i)
	* Khi $P_j$ kết thúc và giải phóng TN, $P_j$ sẽ nhận được TN cần thết, thực hiện, giải phóng các TN đã được cung cấp và kết thúc. 
	* Khi $P_i$ kết thúc và giải phóng TN = $P_{i + 1 }$ sẽ được nhận TN cần thiết và kế thúc được.
	* Tất cả các TT trong chuỗi an toàn đều kết thúc được.

> [!example]- Ví dụ:
>  ![[Pasted image 20221201212015.png]]
>  ![[Pasted image 20221201212032.png]]


> [!attention] Nhận xét
>  * Hệ thống an toàn -> các TT đều có thể kết thúc được -> Không xảy ra bế tắc
>  * Hệ thống không an toàn -> Có khả năng xảy ra bế tắc

> [!note] Phương pháp:
> * Không để hệ thống rơi vào tình trạng không an toàn
> * Kiểm tra mọi yêu cầu TN
> 	* Nếu hệ thống vẫn an toàn khi cung cấp -> Cung cấp
> 	* Nếu hệ thống không an toàn khi cung cấp -> Phải đợi

> [!tip] Thuật toán
> * Thuật toán dựa vào độ thị cung cấp tài nguyên [[Chap2.5 - Bế tắc và xử lý bế tắc#Thuật toán dựa vào đồ thị cung cấp tài nguyên]]
> * Thuật toán người quản lý nhà băng [[Chap2.5 - Bế tắc và xử lý bế tắc#Thuật toán người quản lý nhà băng]]

### Thuật toán dựa vào đồ thị cung cấp tài nguyên
> [!note] 
> Sử dụng khi mỗi kiểu TN chỉ có 1 đơn vị
>* Có chu trình, sẽ có bế tắc.

* Thêm vào đồ thị loại cung mới: cung đòi hỏi $P_i \rightarrow P_j$ 
	* Cùng hướng với cung yêu cầu, thể hiện trong đồ thị -> Cho biết $P_i$ có thể yêu cầu $R_j$ trong tương lai.

* TT khi tham gia hệ thống, phải thêm tất cả các cung đòi hỏi tương ứng vào đồ thị 
	* Khi Pi yêu cầu $R_j$, cung đòi hỏi $P_i \rightarrow R_j$ chuyển thành cung yêu cầu $P_i \rightarrow R_j$ 
	* Khi P_i giải phóng $R_j$, cung sử dụng $R_j \rightarrow P_i$ chuyển thành cung đòi hỏi $P_i \rightarrow R_j$

> [!tip] Thuật toán dựa vào đồ thị cung cấp tài nguyên 
> Yêu cầu tài nguyên R_j của TT được thoả mãn chỉ khi việc chuyển cung yêu cầu $P_i \rightarrow R_j$ thành cung sử dụng $R_j \rightarrow P_i$ không tạo chu trình trên đồ thị.
> * Ko chu trình: hệ thống an toàn
> * Có chu trình: việc cung cấp tài nguyên đẩy hệ thống vào tình trạng ko an toàn

![[Hệ Điều Hành-Chuong 2-278-281.pdf]]

### Thuật toán người quản lý nhà băng
* Thích hợp cho các hệ thống gồm các kiểu TN có nhiều đơn vị 

* 1 TT mới xuất hiện trong hệ thống cần khai báo **số đơn vị lớn nhất** của mỗi kiểu TN sẽ sử dụng  
	* *Không được vượt quá tổng số TN của hệ thống*

* Khi 1 TT yêu cầu TN, hệ thống kiểm tra liệu đáp ứng cho yêu cầu hệ thống có còn an toàn?
	* Nếu hệ thống vẫn an toàn => **cung cấp TN**
	* Nếu hệ thống không an toàn => **TT phải đợi**

> [!tip] Thuật toán người quản lý nhà băng
> Cần có:
> * Các cấu trúc dữ liệu biểu diễn trạng thái phân phối TN
> * Thuật toán kiểm tra tình trạng an toàn của hệ thống
> * Thuật toán yêu cầu TN

#### Các cấu trúc dữ liệu
> [!info] Hệ thống
> * n số TT trong hệ thống 
> * m số kiểu TN trong hệ thống

> [!note] Các kiểu cấu trúc dữ liệu
> - ***Available*** : Vector chiều dài m cho biết số đơn vị TN sẵn có trong hệ thống  (Ex: Có 8 đơn vị của TN 3 sẵn có trong hệ thống -> `Available[3] = 8`)
> 
> - ***Max*** : Ma trận n * m cho biết số lượng mỗi kiểu TN đã cấp cho TT (Ex: Số yêu cầu tối đa TN 3 của TT 2 là 5 đơn vị tài nguyên -> `Max[2, 3]  = 5`)
> 
> - ***Allocation*** - Ma trận n * m cho biết số lượng mỗi kiểu TN đã cấp cho TT (`Allocation[2,3] = 2 `)
> - ***Need*** - Ma trận n * m chỉ ra số lượng mỗi kiểu TN còn cần đến của từng TT (`Need[2,3] = 3`)
> $$
> Need[i][j] = Max[i][j] - Allocation[i][j]
> $$

> [!abstract] Quy ước
> * X, Y là các vector độ dài n (bằng số lượng TT)
> 	* $X \leq Y <=> X [i] \leq Y[i]$  -   $\forall i  = 1,2, ..., n$
> 
> * Các dòng của ma trận ***Max***, ***Need***, ***Allocation*** được xử lý như các vector
> 
> * Thuật toán tính toán trên các vector

* Các cấu trúc cục bộ:
	* **Work** - vector độ dài m cho biết mỗi TN còn bao nhiêu
	* **Finish** - vector độ dài n, cho biết TT có chắc chắn kết thúc hay ko

#### Thuật toán kiểm tra an toàn
```shell
BOOL Safe(Current Resource-Allocation State){
	Work←Available // số đơn vị tài nguyên có sẵn trong hệ thống
	for (i : 1 → n) Finish[i]←false // nạp các trạng thái vào vector finish
	flag← true
	While(flag){
		flag←false
		for (i : 1 → n)
			if(Finish[i]=false AND Need[i] ≤Work){ // cập nhật khả năng hoàn thành cho TT 
													//nếu yêu cầu về TN của tiến trình i 
													// có thể được đáp ứng
				Finish[i]← true
				Work ← Work + Allocation[i] // TT trả lại TN sau khi hoàn thành
				flag← true
			}//endif
	}//endwhile
	for (i : 1 → n) if (Finish[i]=false)return false
	return true; // chỉ cần có 1 TT ko được đáp ứng TN, kết quả trả về sẽ là ko an toàn
}//End function
```

![[Pasted image 20221201230458.png]]
![[Pasted image 20221201230512.png]]
![[Pasted image 20221201230531.png]]
![[Pasted image 20221201230607.png]]

#### Thuật toán yêu cầu tài nguyên 
-  **Request[i, j]** - vector yêu cầu tài nguyên $R_j$ của TT $P_i$ (Request[3,2] = 2 - TT 3 yêu cầu 2 đơn vị của TN 2)

 > [!note] Khi $P_i$ yêu cầu TN
 > ```python
 > if(Request[i] > Need[i])
 > 	Error() # Yêu cầu vượt quá khai báo TN
 > if(Request[i] > Available)
 > 	Block() # Không đủ TN, TT phải đợi
 > # Thiết lập trạng thái phân phối TN mới cho hệ thống
 > Available  = Available  - Request[i]
 > Allocation[i] +=  Request[i]
 > Need[i] = Need[i] - Request[i]
 > # Phân phối TN dựa trên kết quả kiểm tra tính an toàn của trạng thái phân phối TN mới
 > if(Safe(New Resource Allocaton State))
 > 	# phân phối cho P_i theo yêu cầu
 > else
 > 	# TT P_i phải đơji
 > 	# Khôi phục lại trạng thái cũ (Available, Allocation, Need)
 > ``` 

![[Hệ Điều Hành-Chuong 2-291-301.pdf]]

## 5.6 Nhận biết và khắc phục
> [!abstract] Nguyên tắc
> * Không áp dụng áp dụng các biện pháp phòng ngừa hoặc phòng tránh, để cho bế tắc xảy ra
> * Định kỳ kiểm tra xem bế tắc có đang xảy ra không.
> * Nếu có bế tắc khắc phục
> * Hệ thống cần phải cung cấp: 
> 	* Thuật toán xác định hệ thống đang bế tắc không
> 	* Biện pháp kỹ thuật chữa bế tắc

### Nhận biết - thuật toán dựa trên đồ thị cung cấp tài nguyên
* Áp dụng mỗi khi TN trong hệ thống có 1 đơn vị
* Ktr hệ thống có bế tắc không bằng cách kiểm tra chu trình trên đồ thị
	* Nếu trên đồ thị có chu trình, hệ thống đang bế tắc.

* Định kỳ gọi tới các thuật toán kiểm tra chu trình trên đồ thị
	* Đòi hỏi $n^2$ với n là số đỉnh của đồ thị

* Sử dụng đồ thị chờ đợi - phiên bản thu gọn của đồ thị cung cấp tài nguyên
	* Chỉ có các đỉnh dạng TT
	* Cung chờ đợi $P_i \rightarrow P_j$ - chương trình P_i đợi TT P_j giải phóng tài nguyên P_i cần
	* Cung chờ đợi $P_i \rightarrow P_j$ tồn tại trên đồ thị đợi khi và chỉ khi trên đồ thị phân phối tài nguyên tương ứng tồn tại đồng thời cung yêu cầu $P_i \rightarrow R$ và cung sử dụng $R \rightarrow P_j$

### Nhận biết - thuật toán chỉ ra bế tắc tổng quát

### Khắc phục - Kết thúc tiến trình

### Khắc phục - Trưng dụng tài nguyên
