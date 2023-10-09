
> [!abstract] 
> Phát biểu rằng bất cứ hệ thống **dữ liệu phân tán** nào chỉ có thể đảm bảo hai trong ba yếu tố sau:
> * Tính nhất quán (Consistency)
> * Tính khả dụng (Availability)
> * Tính chịu thương tổn phân vùng (Partition Fault Tolerance)

|**Consistency**|**Availability**|**Partition Fault Tolerance**|
|---|---|---|
|Mỗi lần đọc sẽ nhận được dữ liệu mới nhất hoặc lỗi (error)|Mỗi truy vấn luôn nhận được một trả lời không lỗi (non-error response), nhưng không đảm bảo dữ liệu trả về chứa thông tin mới nhất.|Hệ thống liên tục hoạt động bình thường mặc dù một số lượng bất kỳ các thông điệp (msg) bị mất (hoặc trễ) vì lỗi mạng giữa các node.|

![[Pasted image 20230924131839.png]]

* Khi lỗi phân vùng mạng (network partition failure) xảy ra, hệ thống phải lựa chọn một trong hai phương án sau đây:
	* Hủy tác vụ, điều làm giảm tính khả dụng (availability) nhưng đảm bảo tính nhất quán (consistency) của hệ thống.
	* Tiếp tục thực hiện tác vụ để đảm bảo tính khả dụng nhưng có thể dẫn đến không nhất quán trong dữ liệu trả về.
-> Phải chọn giữa **tính nhất quán** >< **tính khả dụng**.

> [!caution] Phân biệt giữa consistency của CAP và consistency của ACID

### Giải thích CAP Theory
* Không có HPT nào có thể đảm bảo an toàn trước các sự cố mạng.
	-> Cần phải phân vùng mạng.

* Khi mạng đã được phân vùng, ta chỉ có thể thỏa mãn 1 trong 2 yếu tố: nhất quán và khả dụng.
	* Khi chọn tính nhất quán thay vì tính khả dụng, hệ thống sẽ trả lại lỗi (error) hoặc lỗi hết thời gian chờ nếu thông tin được truy vấn không thể đảm bảo được là mới nhất.
	* Khi chọn tính khả dụng thay vì tính nhất quán, hệ thống sẽ luôn xử lý truy vấn và cố gắng trả lại phiên bản hiện có của thông tin, ngay cả khi nó không thể đảm bảo đó là phiên bản mới nhất.

* Cả trong trường hợp không phân vùng, cả tính nhất quán lẫn tính khả dụng của thông tin đều được đảm bảo.

> [!question] Khi nào nên chọn tính nhất quán, khi nào nên chọn tính khả dụng?
> * Các hệ thống csdl truyền thống (RDBMS) được thiết kế dựa trên tính chất **ACID** ưu tiên tính **nhất quán** thay vì tính khả dụng.
> * Các hệ thống được thiết kế dựa trên lý thuyết **BASE** (NoSQL), ưu tiên tính **khả dụng** thay vì tính nhất quán.

