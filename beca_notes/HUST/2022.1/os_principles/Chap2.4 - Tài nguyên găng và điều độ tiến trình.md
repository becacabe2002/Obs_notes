## 4.1 Khái niệm tài nguyên găng
* Kết quả thực hiện các luồng song song phụ thuộc trật tự truy nhập biến dùng chung giữa chúng.
> [!note] Bài toán người Producer - Consumer
> * hai TT: 
> 	* Producer sản xuất ra các sp
> 	* Consumer tiêu thụ các sp
> * CV của P phải đồng bộ vs S: 
> 	* Ko đưa ra sp khi hết chỗ trống
> 	* Ko lấy được sp khi  chưa có

> [!abstract] Tài nguyên
> Tất cả những gì cần thiết cho thực hiện TT
> > [!info] Tài nguyên găng
> > * Hạn chế về khả năng sử dụng chung
> > * Cần đồng thời cho nhiều TT
> > * Có thể là **thiết bị vật lý** hoặc **dữ liệu dùng chung**

> [!warning] Vấn đề 
> Dùng chung tài nguyên găng có thể dẫn đến không đảm bảo tính toàn vẹn dữ liệu
> => ***Đòi hỏi cơ chế đồng bộ hoá các TT***

### Điều kiện cạnh tranh (Rare condition)
> [!info] Rare condition
> Tình trạng trong đó kết quả của việc nhiều TT cùng truy cập tới dl dùng chung phụ thuộc vào trật tự của các truy nhập
> ***=> Làm cho chương trình ko xác định***

* Ngăn ngừa bằng **đồng bộ hoá** các TT thực hiện đồng thời
> [!note] Synchronize
> * Chỉ một TT truy nhập tới dl dùng chung tại 1 thời điểm
> * Đoạn lệnh truy nhập tới dl dùng chung các TT phải thực hiện theo thứ tự xác định

### Đoạn găng
> [!info] Đoạn găng (Critical section)
> Đoạn chương trình sử dụng tài nguyên găng (thực hiện truy cập và thao tác trên dl dùng chung)

* Khi có nhiều TT sử dụng tài nguyên găng thì phải điều độ [[Chap2.4 - Tài nguyên găng và điều độ tiến trình#Yêu cầu của chương trình điều độ]]

***=> Đảm bảo ko có quá 1 TT nằm trong đoạn găng***

### Yêu cầu của chương trình điều độ
>[!note] Loại trừ lẫn nhau (Mutual Exclusion)
>Mỗi thời điểm, tài nguyên găng ko p phục vụ một số lượng TT vượt quá khả năng của nó.
* 1 TT đang thực hiện trong đoạn găng -> ko TT nào được quyền vào đoạn găng đó.
> [!note] Tiến triển (Progress)
> Tài nguyên găng còn khả năng phục vụ và tồn tại TT muốn vào găng, thì TT đó phải được sử dụng tài nguyên găng.

> [!note] Chờ đợi hữu hạn (Bounded Waiting)
> Nếu tài nguyên găng hết khả năng phục vụ và vẫn tồn tại TT muốn vào đoạn găng, thì TT đó phải được xếp hàng chờ (sự chờ đợi hữu hạn)

>[!tip] Quy ước
>Có 2 TT P1&P2 thực hiện đồng thời, dùng chung 1 tài nguyên găng
>![[Pasted image 20221123090023.png]]
>* TT phải xin phép trc khi vào đoạn găng *{phần vào}*
>* TT khi thoát ra khỏi đoạn găng thực hiện *{phần ra}*

## 4.2 Phương pháp khoá trong
* Công cụ cấp thấp

> [!abstract] Nguyên tắc
> * Mỗi TT dùng **1 byte** trong vùng nhớ chung **làm khoá**
> 	* TT vào đoạn găng, đóng khoá (byte khoá = true)
> 	* TT ra khỏi đoạn găng, mở khoá (byte khoá = false)
> * TT muốn vào đoạn găng, phải **kiểm tra khoá** của TT còn lại
> 	* Đang khoá -> Đợi
> 	* Mở -> được quyền vào đoạn găng

### Thuật toán điều độ
![[Pasted image 20221123094915.png]]
![[Pasted image 20221123094920.png]]

> [!caution] Điều độ chưa hợp lí
> * 2 TT yêu cầu tài nguyên tại cùng 1 thời điểm
> 	* Vấn đề loại trừ lẫn nhau (TH1)
> 	* Vấn đề tiến triển (TH2)
> 
> > [!note] Nguyên nhân
> > [!note] Nguyên nhân
> > Do tách rời giữa
> > * Kiểm tra quyền vào đoạn găng
> > * Xác lập quyền sử dụng tài nguyên găng

### Thuật toán Dekker
* Sử dụng biến `turn` để chỉ ra TT được quyền ưu tiên
![[Pasted image 20221123095449.png]]

> [!note] Nhận xét
> * Điều độ hợp lý cho **mọi trường hợp**
> * **Không đòi hỏi** sự hỗ trợ đặc biệt của **phần cứng** nên có thể thực hiện bằng ngôn ngữ bất kỳ
> * Quá **phức tạp** khi số **TT và số tài nguyên tăng lên**
> * Phải chờ đợi tích cực (busy waiting) trước khi vào đoạn găng
> 	* Khi chờ đợi vẫn phải thực hiện kiểm tra quyền vào đoạn găng
> 	-> Lãng phí thời gian processor

^ec2879

> [!warning] Thuật toán có thể thực hiện sai trong một số TH
> * CPU cho phép thực hiện các lệnh không đúng trật tự
> * Chương trình dịch thực hiện tối ưu hoá khi sinh mã
> 	* Các mã bất biến bên trong vòng lặp được đưa ra ngoài

## 4.3 Phương pháp kiểm tra và xác lập (Test and Set)
* Công cụ cấp thấp
> [!abstract] Nguyên tắc
> * Sử dụng sự **hỗ trợ từ phần cứng**
> * Phần cứng cung cấp các câu lệnh **xử lý không tách rời**
> 	* Kiểm tra và thay đổi nội dung của 1 word
> 	* Hoán đổi nội dung của 2 word khác nhau
> * **xử lý không tách rời** (auto)
> 	* Khối lệnh không thể bị ngắt khi đang thực hiện
> 	* Được gọi đồng thời, sẽ được thực hiện theo thứ tự bất  kì
> 
> ![[Pasted image 20221123215546.png]]

### Thuật toán với lệnh `TestAndSet`
* Biến dùng chung **Boolean: Lock** (trạng thái của tài nguyên)
	* Bị khoá (Lock = true)
	* Tự do (Lock = false)
* Khởi tạo: `Lock = false` (TN tự do)
> [!note] Thuật toán cho TT Pi
> ![[Pasted image 20221123221657.png]]

### Thuật toán với lệnh `Swap`
* Biến dùng chung **Lock** cho biết trạng thái tài nguyên
* Biến địa phương cho mỗi TT: **Key** (boolean)
* Khởi tạo: `Lock = false` -> tài nguyên tự do
> [!note] Thuật toán cho TT Pi
> ![[Pasted image 20221123222048.png]]

> [!note] Nhận xét
> * Đơn giản, **không phức tạp** khi số **TT và số đoạn găng tăng lên** (Khác với [[Chap2.4 - Tài nguyên găng và điều độ tiến trình#Thuật toán Dekker]])
> * Các TT phải chờ đợi tích cực trước khi vào đoạn găng
> 	* Luôn kiểm tra xem tài nguyên găng đã được giải phóng chưa
> 	-> Sử dụng processor ko hiệu quả
> * Không đảm bảo **yêu cầu chờ đợi hữu hạn**
> 	* TT được vào đoạn găng tiếp theo, sẽ phụ thuộc thời điểm giải phóng tài nguyên của TT đang chiếm giữ
> 
> 	=> Cần khác phục.

## 4.4 Kỹ thuật đèn báo
* Công cụ cấp thấp
### Đèn báo (Semaphore)
>[!info] Đèn báo (Semaphore)
>Một biến nguyên S, khởi tạo bằng **khả năng phục vụ** của tài nguyên nó điều độ
>* Số tài nguyên có thể phục vụ tại một thời điểm (VD: 3 máy in)
>* Số đơn vị tài nguyên có sẵn (VD: 10 chỗ trống trong buffer)

* Chỉ có thể thay đổi giá trị bởi 2 thao tác cơ bản P và V:
>[!note] P(S) (wait(S))
>```C
>wait(S){
>	while(S <= 0) no-op;
>	S --;
>}
>```

> [!note] V(S) (signal(S))
> ```C
> signal(S){
> 	S++;
> }
> ```

> [!caution] Các thao tác P(S) và V(S) xử lý không rời

* Đèn báo là công cụ điều độ tổng quát.

![[Pasted image 20221117130332.png]]

### Sử dụng đèn báo
* Điều độ nhiều tiến trình qua đoạn găng.
	* Sử dụng nhiều biến phân chia mutex kiểu Semaphore
	* Khởi tạo mutex bằng 1
	* Thuật toán cho tiến trình P_i

```C
do{
wait(mutex);
	{Đoạn găng của tiến trình}
signal(mutex)
	{Phần còn lại của tiến trình}
}while(1);
```

* Điều độ thứ tự thực hiện bên trong các tiến trình
	* Hai tiến trình $P_1$ và $P_2$ thực hiện đồng thời
		* $P_1$ chứa lệnh $S_1$, $P_2$ chứa lệnh $S_2$
		* Yêu cầu $S_2$ được thực hiện chỉ khi $S_1$ thực hiện xong.
	* Sử dụng đền báo `synch` được khởi tạo giá trị 0
	* Đoạn mã cho P_1 và P_2
![[Pasted image 20221117131101.png]]

### Huỷ bỏ chờ đợi tích cực
* Sử dụng 2 thao tác đơn giản:
> [!note] `block()`
> Ngừng tạm thời tiến trình đang thực hiện

> [!note] `wakeup(P)`
> Thực hiện tiếp t/trình P dừng bởi lệnh `block()`

* Khi tiến trình gọi **P(S)** và đèn báo S không dương
	* Tiến trình phải dừng bởi gọi tới câu lệnh `block()`
	* Lệnh `block()` đặt tiến trình vào hàng đợi gắn với đèn báo S
	* Hệ thống lấy lại CPU giao cho tiến trình khác (điều phối CPU)
	* Tiến trình chuyển sang trạng thái chờ đợi (waiting)
	* Tiến trình nằm trong hàng đợi đến khi tiến trình khác thực hiện thao tác **V(S)** trên cùng đèn báo S

* Tiến trình đưa ra lời gọi **V(S)**
	* Lấy một TT trong hàng đợi ra (nếu có)
	* Chuyển TT lấy ra từ trạng thái chờ đợi sang trạng thái ready và đặt lên hàng đợi sẵn sàng bởi gọi tới `wakeup(P)`
	* TT ms sẵn sàng có thể trưng dụng CPU từ tiến trình đang thực hiện nếu thuật toán điều phối CPU cho phép.

### Cài đặt đèn báo
> [!note] Semaphore S
> ```C
> typedef struct{
> 	int value;
> 	struct process * Ptr;
> }Semaphore;
> ```

> [!note] wait(S)/P(S)
> ```c
> void wait(Semaphore S){
> 	S.value --;
> 	if(S.value < 0){
> 		// them TT vao S.Ptr
> 		block();
> 	}
> }
> ```

> [!note] signal(S)/V(S)
> ```c
> void signal(Semaphore S){
> 	S.value++;
> 	if(S.value <= 0){
> 		//Lay r  TT P tu S.Ptr
> 		wakeup(P);
> 	}
> }
> ```

![[Hệ Điều Hành-Chuong 2-172-179.pdf]]

***Nhận xét***
* Dễ dàng áp dụng cho các hệ thống phức tạp
* Không tồn tại hiện tượng chờ đợi tích cực
* Hiệu quả sử dụng phụ thuộc vào người dùng

![[Pasted image 20221117133847.png]]

* Các phép xử lý P(S) và V(S) là không phân chia được
=> Bản thân P(S) và V(S) cũng là 2 tài nguyên găng => Cần điều độ
* Hệ thống một VXL: cấm ngắt khi thực hiện wait(), signal()
* Hệ thống nhiều VXL: 
	* Không thể cấm ngắt trên VXL khác
	* Có thể dùng phương pháp khoá trong -> Hiện tượng chờ đợi tích cực, nhưng thời gian chờ đợi ngắn (10 lệnh)

> [!example]- Ví dụ:
> ![[Pasted image 20221123222951.png]]
> ![[Pasted image 20221123223006.png]]

## 4.5 Ví dụ về đồng bộ tiến trình

![[Hệ Điều Hành-Chuong 2-186-208.pdf]]

## 4.6 Công cụ điều độ cấp cao (Monitor)
> [!info] Monitor
> * Là 1 kiểu dữ liệu đặc biệt
> * Bao gồm các thủ tục, dữ liệu cục bộ, đoạn mã khởi tạo
> * Các TT chỉ có thể truy cập tới các biến bằng cách gọi tới các thủ tục trong Monitor
> * Tại 1 thời điểm chỉ có 1 TT được quyền sử dụng Monitor -> TT khác muốn sử dụng, phải chờ đợi
> * Cho phép các TT đợi trong Monitor -> Sử dụng các biến điều kiện (condition var)
> > [!example]  Cú pháp của Monitor
> > ```C
> > monitor monitorName{
> > 	// Khai bao cac bien chung
> > 	procedure P1(...){
> > 	...
> > 	}
> > 	...
> > 	procedure Pn(...){
> > 	...
> > 	}
> > 	{
> > 	// Ma khoi tao
> > 	}
> > };
> > ```
> > ![[Pasted image 20221123224050.png]]

### Biến điều kiện
> [!info]
> Tên của 1 hàng đợi

* Khai báo: `condition x,y;`
*  Chỉ sử dụng được với hai thao tác là `wait()` và `signal()`

> [!note] `wait()`
> * Được gọi bởi các thủ tục của Monitor
> * Cú pháp: 
> ```java
> x.wait()
> // or
> wait(x)
> ```
> * Cho phép TT đưa ra lời gọi tạm dừng (block), cho tới khi được 1 TT khác kích hoạt bằng cách gọi tới `signal()`

> [!note] `signal()`
> * Được gọi bởi các thủ tục của Monitor
> * Cú pháp: 
> ```java
> x.signal()
> // or
> signal(x)
> ```
> * Kích hoạt chính xác 1 TT đang đợi tạ biến điều kiện x (nằm trong hàng đợi x) ra tiếp tục hoạt động, nếu ko có, thao tác bị bỏ qua.

![[Pasted image 20221123224808.png]]

### Sử dụng Monitor: một tài nguyên chung
![[Pasted image 20221123225054.png]]

![[Pasted image 20221123225115.png]]

### Bài toán Producer - Consumer
![[Pasted image 20221123225133.png]]

![[Pasted image 20221123225140.png]]