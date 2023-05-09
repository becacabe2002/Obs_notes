### Cơ chế hoạt động của  Trivium

![[Pasted image 20230502123336.png]]

> Là stream cipher sử dụng khóa có độ dài  80-bit

* Bao gồm 288 bit internal state ($S_1 -> S_{288}$): 
	* Thanh ghi (register) A: 93 bit
	* Thanh ghi (register) B: 84 bit
	* Thanh ghi (register) C: 111 bit

* Với mỗi vòng, cipher thực hiện:
	* $t_1 = S_{066}\oplus S_{093}$
	* $t_2 = S_{162}\oplus S_{177}$
	* $t_3 = S_{243}\oplus S_{288}$
> [!hint] -> Output bit = $t_1 \oplus t_2 \oplus t_3$
* Then feedback bits:
	* $fb_1 = t_1 \oplus (S_{091}.S_{092}) \oplus S_{171}$
	* $fb_2 = t_2 \oplus (S_{175}.S_{176}) \oplus S_{264}$
	* $fb_3 = t_3 \oplus (S_{286}.S_{287}) \oplus S_{069}$
* Các thanh ghi dịch phải 1 bit với các bit đầu vào:
	* $S_{001} = fb_3$
	* $S_{094} = fb_1$
	* $S_{178} = fb_2$

### Khởi tạo Trivium
* Khóa (key) được viết vào **$S_1 -> S_{80}$**
* Giá trị khởi tạo (IV) được viết vào **$S_{94} -> S_{173}$**
* Các bit còn lại được set = 0, ngọai trừ 3 bit cuối $S_{286} = S_{287} =S_{288} = 1$

### Generate Key
* 1152 output bit đầu tiên được sinh ra từ Trivium ko được lấy làm keystream (để đảm bảo keystream phụ thuộc vào khóa k và IV).
* Keystream được lấy bắt đầu từ output bit 1153.

### Encrypt and Decrypt File
* File được đọc và chuyển sang dạng bytes stream -> bits stream
* Cho trivium chạy clock 1152 lần 
* Gen key stream có độ dài tương ứng độ dài bits stream của file.
* bits stream file XOR với key stream, kết quả thu được ghi vào trong file cũ.
	* Trường hợp flag = 0 -> Encrypt file
	* Trường hợp flag = 1 -> Decrypt file