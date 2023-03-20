## 3.1 Các khái niệm cơ bản
> [!abstract] Nhắc lại bài cũ
> [[Chap2.1 - Tiến trình#1.2 Điều phối tiến trình (Process Scheduling)]]

> [!question] Vậy điều phối CPU (CPU Scheduling) khác gì điều phối tiến trình (Job Scheduling)

> [!note] Answer
>  [CPU Scheduling vs Job Scheduling](https://www.differencebetween.com/difference-between-job-scheduling-and-vs-cpu-scheduling/#:~:text=and%20CPU%20Scheduling%3F-,Job%20Scheduling%20vs%20CPU%20Scheduling,the%20CPU%20to%20that%20process.)

* Hệ đơn c/trình: CPU không được sử dụng -> Lãng phí

* Hệ đa c/trình: cố gắng tận dụng CPU (free) cho các TT khác (waiting)
	* Cần nhiều TT sẵn sàng trong bộ nhớ tại 1 thời điểm
	* Khi 1 TT phải chờ, HĐH lấy lại processor để phân cho TT khác

> [!note] Sự quan trọng của CPU Scheduling đối với HĐH đa nhiệm
> Giúp luân chuyển CPU giữa các TT, khai thác hệ thống hiệu quả hơn
> **-> Điều phối processor là nền tảng trong thiết kế HĐH**

### Chu kỳ thực hiện CPU - I/O
* TT  là chuỗi luân phiên giữa chu kì tính toán và chờ đợi vào ra
![[Pasted image 20221122041328.png]]

> [!note] Phân biệt các kiểu TT
> Dựa trên sự **phân phối thời gian** cho các chu kỳ CPU & I/O
> * ***TT tính toán (CPU-bond process)***: có vài chu kỳ CPU dài
> * ***TT vào ra (I/O-bond process)***: có nhiều chu kỳ CPU ngắn
> -> việc phân biệt giúp chọn giải thuật điều phối thích hợp.

👉 Nhắc lại: [[Chap2.1 - Tiến trình#Job schedular]]

> [!caution] 
> Cần chú ý về [sự khác nhau giữa **job**, **process** and **task**](https://www.geeksforgeeks.org/difference-between-job-task-and-process/#:~:text=Job%20is%20work%20that%20needs,the%20work%20should%20be%20done.)

### Bộ điều phối CPU
* Lựa chọn 1 trong số các TT đang **sẵn sàng** trong bộ nhớ và cung cấp CPU cho nó.
	* Các TT sắp hàng trong hàng đợi (FIFO, ưu tiên, DSLK...)

* Quyết định điều phối CPU xảy ra khi TT chuyển từ t/thai
	* **thực hiện** -> **chờ đợi** (y/c I/O)
	* **thực hiện** -> **sẵn sàng** (hết tgian sử dụng CPU -> ngắt tgian)
	* **chờ đợi** -> sẵn sàng (hoàn thành I/O)
	* Sang **kết thúc**

> [!note] 
> * TH 1 & 4 => ***Điều phối không trưng dụng*** (non-preemptive)
> * TH khác => ***Điều phối trưng dụng*** (preemptive)

> [!info] Điều phối không trưng dụng
> TT chiếm CPU cho tới khi chủ động giải phóng (Kết thúc nhiệm vụ hoặc chuyển sang trạng thái chờ đợi)
> * Không đòi hỏi phần cứng đặc biệt (đồng hồ)
> > [!example] 
> > DOS, Win 3.1, Macintosh

> [!info] Điều phối trưng dụng
> * TT chỉ được phép thực hiện trong 1 khoảng tgian.
> * Hết tgian, ngắt thời gian xuất hiện, bộ điều vận (dispatcher) quyết định phục hồi lại TT hay chọn TT khác.
> * Bảo vệ CPU khỏi các TT "đói-CPU"
> 
> > [!warning]  Vấn đề dữ liệu dùng chung
> > * TT 1 đang cập nhật DL thì bị lấy mất CPU
> > * TT 2, được giao CPU và đọc DL đang cập nhật -> sai
> 
> > [!example] 
> > WinNT, Unix (Các HĐH đa nhiệm)

## 3.2 Tiêu chuẩn điều phối
> [!abstract] Các hệ thống nói chung
> * Công bằng
> 	* Chia sẻ CPU công bằng giữa các TT
> 	* Không phải chờ đợi vô thời hạn
> * Các chiến lược điều phối đề ra phải được tuân thủ
> * **Cân bằng tải** - mọi thành phần  của hệ thống đều bận rộn

^2728c2

### Hệ thống xử lý theo lô
* Sử dụng **CPU lớn nhất**
	* làm CPU hoạt động nhiều nhất có thể (40% - 90%)

* **Thông lượng (output) lớn nhất**
> [!info] Thông lượng
> Số lượng TT hoàn thành trong 1 đơn vị thời gian.
*  1 TT/ giờ (dài) -> 10 TT/giây (ngắn)

* Thời gian **hoàn thành nhỏ nhất**
	* khoảng tgian từ lúc gửi đến hệ thống tới khi TT kết thúc
	* Gồm các khoảng tgain chờ đợi (đưa TT vào bộ nhớ, trong hàng đợi ready, trong hàng đợi thiết bị, thực hiện thực tế)

* Thời gian **chờ đợi nhỏ nhất**
	* Tổng tgian chờ trong hàng đợi sẵn sàng

> [!note]
> Giải thuật điều độ CPU không ảnh hưởng tới các TT **đang thực hiện** hay **đang đợi** thiết bị vào ra.

### Hệ thống tương tác
> [!abstract]  nhanh chóng phản hồi yêu cầu người dùng

* Thời gian **đáp ứng nhỏ nhất**
	* Là khoảng tgian từ lúc gửi câu hỏi cho tới khi câu trả lời đầu tiên được tạo ra
	* TT có thể tạo ra kết quả từng phần
	* TT có thể tiếp tục tính toán kết quả mới trong khi kết quả cũ được gửi tới người dùng

### Hệ thống tgian thực
* Kịp thời hạn mà không mất mát dữ liệu
* Có khả năng dự đoán được việc giảm hiệu năng trong hệ thống đa phương tiện.

## 3.3 Các thuật toán điều phối
*Giả thiết các TT chỉ có **1 chu kỳ tính toán**, yếu tố cần đo đạc: **thời gian chờ đợi trung bình***
### First Come, First Served - FCFS

> [!tip] Nguyên tắc
> * TT sử dụng CPU theo **trình tự xuất hiện**
> * TT sở hữu CPU cho tới khi **kết thúc** hoặc  **chờ đợi vào ra**

![[Pasted image 20221122052214.png]]

> [!note] Đặc điểm
> * Đơn giản, dễ thực hiện 
> * Tiến trình ngắn phải chờ đợi như TT dài

### Shortest Job First

> [!tip] Nguyên tắc
> Mỗi TT lưu trữ thời gian của chu kỳ sử dụng CPU tiếp theo, TT có **thời gian sử dụng ngắn nhất** sẽ sở hữu CPU
> * 2 PP:
> 	* Không trưng dụng CPU
> 	* Có trưng dụng CPU (***Shortest Remaining Time First*** - SRTF)

![[Pasted image 20221122052739.png]]

> [!note] Đặc điểm
> * **Tối ưu** vì có thời gian chờ đợi trung bình nhỏ nhất
> * Không thể biết chính xác tgian của chu kỳ sử dụng CPU (phải dự báo dựa trên những giá trị thước đo)

### Priority Scheduling

> [!tip] Nguyên tắc
> Gắn mỗi TT với **1 số hiệu ưu tiên** (Int)
> * CPU được phân phối cho TT  có **độ ưu tiên cao nhất**
> * SJF: độ ưu tiên gắn liền với tgian thực hiện
> 
> 2 PP:
> * Trưng dụng CPU
> * Không trưng dụng CPU

![[Pasted image 20221122053237.png]]

> [!warning] Vấn đề "nạn đói"
> TT có độ ưu tiên thấp phải chờ đợi lâu (hoặc không được thực hiện)
> > [!check] Giải pháp:
> Tăng dần độ ưu tiên TT theo tgian trong hệ thống

^079cd5

### Roud Robin Scheduling
> [!tip] Nguyên tắc
> * Mỗi TT được cấp 1 **lượng tử thời gian** T để thực hiện
> * Khi hết tgian, TT bị trưng dụng processor đồng thời đưa về cuối hàng đợi
> * Đối với hàng đợi có độ dài n -> thời gian chờ nhiều nhất $(n-1)T$

![[Pasted image 20221122053938.png]]
$T = 4$ (?)

> [!warning] Lựa chọn lượng tử tgian
> * T lớn, chuyển sang [[Chap2.3 - Điều phối CPU#First Come, First Served - FCFS]]
> * T nhỏ: phải luân chuyển CPU nhiều
> 
> > [!check] $10ms \leq T \leq 100ms$

### Multilevel Queue Scheduling
> [!info]
> * Ready queue được **phân chia** thành nhiều hàng đợi nhỏ
> * Có hai kiểu TT có các yêu cầu phản hồi khác nhau: ***foreground*** và ***background***
> * TT được ấn định **cố định cho 1 hàng đợi**
> 	* Dựa tren tính chất: độ ưu tiên, kiểu TT, kích thước bộ nhớ
> * Mỗi hàng đợi sử dụng **thuật toán điều độ riêng**

* Giữa các hàng đợi:
> [!note] Cần điều phối
> Điều phối có trưng dụng, độ ưu tiên cố định
> * TT hàng đợi có **độ ưu tiên thấp** chỉ được thực hiện khi hàng đợi có độ ưu tiên cao **rỗng**.
> * TT độ ưu tiên mức cao, **trưng dụng** CPU của TT độ ưu tiên mức thấp
> * Có thể gặp tình trạng **đói CPU** [[Chap2.3 - Điều phối CPU#^079cd5]]

> [!note] Phân chia thời gian giữa các hàng đợi của
> * **TT foreground** - chiếm **80% tgian CPU cho RR** [[Chap2.3 - Điều phối CPU#Roud Robin Scheduling]]
> * **TT background** - chiếm **20% tgian CPU cho FCFS** [[Chap2.3 - Điều phối CPU#First Come, First Served - FCFS]]

![[Pasted image 20221122213230.png]]

### Multilevel Feedback Queue
* Cho phép các **TT được dịch chuyển giữa các hàng đợi.**

> [!note] Phân chia TT theo đặc điểm sử dụng VXL
> * Nếu **dùng quá nhiều tgian** của VXL 
> -> Chuyển xuống hàng đợi có **ưu tiên thấp**
> * **Vào ra** nhiều 
> -> Chuyển lên hàng đợi có **ưu tiên cao**
>  * Đợi **quá lâu** tại **hàng đợi có độ ưu tiên thấp**
>  -> Chuyển lên hàng đợi có **độ ưu tiên cao**
> > [!check] Ngăn ngừa tình trạng "đói CPU"

* Bộ điều phối được xây dựng dựa trên các tham số:
	* Số hàng đợi
	* Thuật toán điều độ cho mỗi hàng đợi
	* Điều kiện TT được chuyển lên/xuống hàng đợi có độ ưu tiên cao/thấp hơn.
	* Phương pháp xác định một hàng đợi khi TT cần phục vụ

![[Pasted image 20221122214229.png]]

### Thread Scheduling
* 2 cấp độ song song: TT và luồng
* phổ biến là RR

![[Pasted image 20221122214327.png]]

## 3.4 CPU điều phối đa xử lý
> [!warning] Khó khăn
> * Điều phối **phức tạp hơn** so với việc có 1 CPU
> * Gặp vấn đề **chia sẻ tải**

👉 Nhắc lại bài cũ: [[Chap1 - Tổng quan#Hệ thống song song]]

### Đa xử lý không đối xứng
> [!abstract]  
> * Mỗi VXL có **hàng đợi sẵn sàng riêng**
> * Chia các TT vào hàng đợi cố định

![[Pasted image 20221122215605.png]]
> [!check]  Ưu điểm
> Dễ tổ chức thực hiện

> [!failure] Nhược điểm
> Tồn tại VXL  rảnh rỗi với hàng đợi rỗng trong khi VXL khác phải tính toán nhiều

### Đa xử lý đối xứng
> [!abstract] 
> Hàng đợi sẵn sàng dùng chung (Global queue)

![[Pasted image 20221122220044.png]]

> [!check] Ưu điểm
> * Sử dụng hiệu quả CPU
> * Công bằng với các TT

> [!failure] Nhược điểm
> Vấn đề dùng chung cấu trúc dữ liệu (queue)
> * 1 T được lựa chọn bởi 2 processors
> * 1 TT bị thất lạc trên queue

> [!question] Vậy sẽ ra sao nếu chúng ta kết hợp 2 kiểu hàng đợi ??

> [!success] Kết quả nhận được
> ![[Pasted image 20221122220439.png]]
> * Dùng cả local và global queue
> * Chia sẻ tải từ các hàng đợi
> * Mỗi CPU làm việc với local queue của mình



