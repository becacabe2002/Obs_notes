## 1. Khái niệm
> [!info] Tác tử - Agent
> Là bất cứ cái gì có khả năng **cảm nhận** môi trường xung quanh nó thông qua các bộ phận cảm biến (sensors) và **hành động** phù hợp theo môi trường đó thông qua các bộ phận hoạt động (actuators)

![[Screenshot from 2023-04-09 17-47-54.png]]

> [!info] Hàm tác tử
> Hàm ánh xạ từ lịch sử nhận thức tới các hành động
> $$
> f: P^* \rightarrow A
> $$

> [!info] Chương trình tác tử
> Hoạt động dựa trên kiến trúc thực tế của hàm $f$

![[Pasted image 20230409175539.png]]

### 1.1 Tác tử hợp lí
* Tác tử cần phấn đấu để "làm đúng việc cần làm", dựa trên:
	* Những gì nhận thức được (nhận biết)
	* Các hành động mà nó có thể thực hiện

> [!note] Sự hợp lý
> Một hành động được coi là **hợp lý** nếu hành động đó giúp cho tác tử đạt được **thành công cao nhất** đối với mục tiêu đặt ra.
> 

* ***Đánh giá hiệu quả hoạt động***: tiêu chuẩn để đánh giá mức độ thành công trong hoạt động của một tác tử

> [!note] Tác tử hợp lý
> là tác tử mà với mỗi **chuỗi nhận thức** có được, cần phải lựa chọn hành động giúp cực đại hóa tiêu chí đánh giá hiệu quả hoạt động của tác tử đó, dựa trên các thông tin được cung cấp bởi chuỗi nhận thức và các tri thức được sở hữu bởi tác tử đó.

> [!warning] Sự hợp lý $\neq$ Sự thông suốt mọi thứ
> * Sự thông suốt là việc biết tất cả mọi thứ, với tri thức vô hạn
> * Các nhận thức có thể không cung cấp tất cả các thông tin liên quan.

* Các tác tử có thể thực hiện các hành động nhằm thay đổi các nhận thức trong tương lai (thu nhập thông tin, khám phá tri thức mới)

> [!info] Tác tử tự trị (Autonomous agent)
> Một tác tử mà các hành động của nó được quyết định bởi chính kinh nghiệm của tác tử đó (đi kèm với khả năng **học** và **thích nghi**)

## 2. Môi trường công việc

> [!note] PEAS 
> * **Performance measure** - tiêu chí đánh giá hiệu quả hoạt động
> * **Environment** - môi trường xung quanh 
> * **Actuators** - các bộ phận hành động
> * **Sensors** - các bộ phận cảm biến

> [!hint] Để thiết kế một tác tử thông minh (hợp lý), trước tiên cần phải xác định các giá trị của các thành phần của PEAS

> [!example]
> Thiết kế một tác tử lái xe taxi tự động
> * Đánh giá hiệu quả hoạt động (P): an toàn, nhanh, đúng luật giao thông, mức độ hài lòng của khách hàng, tối ưu lợi nhuận ...
> * Môi trường xung quanh (E): các con đường, các phương tiện khác cùng tham gia giao thông, những người đi bộ, các khách hàng ...
> * Các bộ phận hành động (A): bánh lái, chân ga, phanh, đèn tín hiệu, còi xe, ...
> * Các bộ phận cảm biến (S): máy quay, đồng hồ tốc độ, GPS, đồng hồ đo khoảng cách quãng đường, các cảm biến động cơ...

## 3. Các kiểu môi trường
> [!note] Môi trường có thể quan sát được hoàn toàn - 1 phần
> Các bộ cảm biến của một tác tử cho phép nó truy cập tới trạng thái **đầy đủ** của môi trường tại mỗi thời điểm.

> [!note] Môi trường xác định - ngẫu nhiên
> * Trạng thái tiếp theo của môi trường được xác định hoàn toàn dựa trên trạng thái hiện tại và hành động của tác tử tại trạng thái hiện tại này.
> * Nếu môi trường là xác định, ngoại trừ đối với các hành động của các tác tử khác - ***Môi trường chiến lược***

> [!note] Môi trường phân đoạn - liên tiếp
> * Lịch sử kinh nghiệm của tác tử được chia thành **các giai đoạn (chương/hồi)**
> 	* Mỗi giai đoạn bao gồm việc nhận thức của tác tử và hành động mà nó thực hiện
> 	* Ở mỗi giai đoạn, việc lựa chọn hành động để thực hiện chỉ phụ thuộc vào giai đoạn đó (ko phụ thuộc vào các giai đoạn khác)

> [!note] Môi trường rời rạc - liên tục
> Tập các nhận thức và các hành động là hữu hạn, được định nghĩa phân biệt rõ ràng.

> [!note] Môi trường tác tử đơn lẻ - đa tác tử
> Một tác tử hoạt động độc lập/ liên hệ với các tác tử khác trong một môi trường

## 4. Các kiểu tác tử
> [!abstract] 4 kiểu tác tử cơ bản
> * Tác tử phản xạ đơn giản (simple reflex agent)
> * Tác tử phản xạ dựa trên mô hình (model-based reflex agent)
> * Tác tử dựa trên mục tiêu (goal-based agent)
> * Tác tử dựa trên lợi ích (utility-based agent)

### 4.1 Tác tử phản xạ đơn giản 
> Hành động theo một quy tắc (luật) có điều kiện phù hợp với trạng thái hiện thời (của môi trường)

```python
function SIMPLE-REFLEX-AGENT(percept) # 
static: rules # tập các luật có dạng: điều kiện - hành động

# agent uses the percept to determine its current state
state  <- INTERPRET-INPUT(percept)

# find the first rule in the set of rules 
# that matches the current state
rule <- RULE-MATCH(state, rules)

# retrieve the corresponding action
action <- RULE-ACTION[rule]
return action
```

![[Pasted image 20230410182230.png]]

### 4.2 Tác tử phản xạ dựa trên mô hình

> [!note] 
> Tác tử phản xạ dựa trên mô hình :
> * Sử dụng một mô hình nội bộ để giám sát trạng thái hiện tại của môi trường.
> * Lựa chọn hành động: giống như đối với các tác tử phản xạ đơn giản.

```python
function REFLEX-AGENT-WITHS-STATE(percept)
static: state # mô tả trạng thái hiện tại của hành động
		rules # tập các luật có dạng: điều kiện - hành động 
		action # hành động gần nhất

# Update the internal state of the agent based on the current state, previous action and current percept as params
# 1. Update the state <- previous action (effects of *previous action*)
# 2. Update the state <- current percept (agent's current sensory input)
# 3. Updated state is returned -> determine agent's current understanding of the env.
state <- UPDATE-STATE(state, action, percept)

rule <- RULE-MATCH(state, rules)

action <- RULE-ACTION[rule]

return action
```

![[Pasted image 20230410221208.png]]

###  4.3 Tác tử dựa trên mục tiêu
* Cần biết thêm thông tin về mục tiêu (bên cạnh việc biết về trạng thái hiện tại của môi trường)
	* VD: trạng thái hiện tại của môi trường: taxi có thể rẽ trái, rẽ  phải hoặc đi thẳng ở một ngã tư
		* Thông tin về mục tiêu: xe taxi cần đi tới đích đến của khác hàng

> [!note] Tác tử dựa trên mục tiêu
> * Theo dõi trạng thái hiện tại của môi trường
> * Lưu trữ một tập các mục tiêu (cần đạt được)
> * Chọn hành động cho phép sẽ đạt đến các mục tiêu

![[Pasted image 20230410212737.png]]
### 4.4 Tác tử dựa trên lợi ích
* Các thông tin về mục tiêu ko đủ để đánh giá hiệu quả của các hành động, mà cần **đánh giá lợi ích đối với tác tử**
	* VD: có nhiều chuỗi các hành động cho phép taxi đi đến đích (đạt mục tiêu) nhưng chuỗi hành động nào nhanh hơn, an toàn và đáng tin cậy hơn ... (tốt hơn)

> [!note] Hàm lợi ích (Utility Function)
> Ánh xạ từ chuỗi các trạng thái của môi trường tới một số giá trị số thực, qua đó thể hiện mức lợi ích đối với tác tử

![[Pasted image 20230410221720.png]]

## 5. Tác tử có khả năng học 
* Cho phép tác tử cải thiện hiệu quả hoạt động của nó

> [!note] 4 thành phần tạo của 1 tác tử có khả năng học
> * **Hành động** - lựa chọn các hành động
> * **Đánh giá** - đánh giá hiệu quả hoạt động
> * **Học** - cải thiện hiệu quả hoạt động bằng cách thay đổi thành phần hành động dựa trên các đánh giá.
> * **Sản sinh kinh nghiệm** - đề xuất các hành động giúp sản sinh ra các kinh nghiệm mới.

![[Pasted image 20230410225210.png]]

> [!info] Cơ sở tri thức (knowledge base)
> Tập các mệnh đề (phát biểu) được biểu diễn trong một ngôn ngữ hình thức, cung cấp tri thức (hiểu biết) cho một tác tử.

* Tác tử khai thác cơ sở tri thức mà nó sở hữu trong quá trình đưa ra các hành động.
	* Thu thập, cập nhật các tri thức mới
	* Cập nhật việc biểu diễn đối với môi trường xung quanh
	* Suy diễn các thuộc tính **ẩn** của môi trường xung quanh
	* Suy luận để đưa ra các hành động hợp lý

## 6. Đa tác tử
* Trong các bài toán thực tế, môi trường hoạt động luôn thay đổi -> tác tử cần có sự cập nhật.
	* Cần một mô hình biểu diễn kế hoạch của các tác tử khác.

* ***Các tác tử cộng tác***:
	* Chia sẻ các mục tiêu hoặc các kế hoạch
	* Phân tách và phân phối  các nhiệm vụ cho  mỗi tác tử.
* ***Các tác tử cạnh tranh***:
	* Các tác tử nhận biết sự tồn tại và họat động của các tác tử khác
	* Dự đoán được ác kế hoạch của một số toán tử khác.
	* Tính toán ảnh hưởng của các kế hoạch của các tác tử khác đối với kế hoạch của nội tại.
	* Quyết định hành động tối ưu với dự đoán ảnh hưởng này.