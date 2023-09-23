## 1. Giải quyết vấn đề bằng tìm kiếm
> Tìm chuỗi các hành động cho phép đạt đến (các) trạng thái mong muốn 

> [!note] Process
> **Đầu vào**: Một bài toán (cần giải quyết)
> **Các bước tiến hành**:
> * *Xác định mục tiêu cần đạt đến (goal formulation)*
> 	* Tập hợp các trạng thái đích
> 	* Dựa trên: trạng thái hiện tại (môi trường) và đánh giá hiệu quả hành động (tác tử)
> * *Phát biểu bài toán (problem formulation)*
> 	*  để  xác định các hành động và trạng thái cần xem xét
> * *Quá trình tìm kiếm (search process)*
> 	* Xem xét các chuỗi hành động có thể và chọn chuỗi hành động tốt nhất.
>
> **Đầu ra**: một giải pháp, dưới dạng một chuỗi các hành động thực hiện

```python
# Tác tử giải quyết vấn đề
function SIMPLE_PROBLEM_SOLVING_AGENT(percept)
	static: seq # action sequence, empty
			state # description of current world state
			goal # initially null
			problem # prb formulation
	state <- UPDATE_STATE(state, percept)
	if seq is empty then do
		goal <- FORMULATE_GOAL(state)
		problem <- FORMULATE_PROBLEM(state,goal)
		seq <- SEARCH(problem)
	action <- FIRST(seq)
	seq <- REST(seq)
	return action
```
### Các  kiểu bài toán
* **Bài toán trạng thái đơn** : xác định, có thể quan sát hoàn toàn
	* Tác tử biết chính xác trạng thái tiếp theo mà sẽ chuyển qua
	* Giải pháp cho bài toán: một chuỗi hành động

* **Bài toán thiếu cảm nhận**: không quan sát được
	* Tác tử có thể không biết là nó đang ở trạng thái nào
	* Giải pháp của bài toán: một chuỗi hành động

* **Bài toán có sự kiện ngẫu nhiên**: không xác định và/hoặc có thể quan sát một phần

* **Không biết về không gian trạng thái**
	-> Bài toán thăm dò

### 1.2 Phát biểu bài toán trạng thái đơn

> [!note] Bài toán trạng thái đơn:
> Các thành phần:
> * **Trạng thái đầu**  
> * **Các hành động** - xác định bởi hàm chuyển trạng thái
> $$
> S(current-state) = \{<action,next-state>\}
> $$
> * **Kiểm tra mục tiêu** 
> 	* Trực tiếp: trạng thái hiện thời
> 	* Gián tiếp: qua các func
> * **Chi phí đường đi**
> 	* $c(x,a,y)$ - chi phí bước (bộ phận) : chi phí cho việc áp dụng hành động a để chuyển từ trạng thái x -> y

> [!info] Giải pháp
> Chuỗi các hành động cho phép dẫn từ trạng thái đầu đến trạng thái đích.

#### Xác định không gian trạng thái
* Trong thực tế, các bài toán thường được mô tả phức tạp -> cần khái quát không gian trạng thái để thuận tiện cho việc giải quyết bài toán.

* **Trạng thái (khái quát)** - một tập các trạng thái thực tế

* **Hành động (khái quát)** - một kết hợp phức tạp của các hành động thực tế.

> [!hint] Để đảm bảo việc thực hiện quá trình tìm kiếm, bất kỳ trạng thái thực tế nào cũng cần phải có thể đạt được đến từ trạng thái thực tế khác.

* **Giải pháp (khái quát)** - một tập các đường đi giải pháp trong thực tế.

#### Đồ thị không gian trạng thái
![[Pasted image 20230411003820.png]]
![[Pasted image 20230411003844.png]]

> [!note] Chuyển đổi bài toán tìm kiếm trên đồ thị sang bài toán tìm kiếm trên cây
> * Thay thế mỗi liên kết (cạnh) vô hướng bằng 2 liên kết (cạnh) có hướng
> * Loại bỏ các vòng lặp tồn tại trong đồ thị
> 	*-> tránh không duyệt 2 lần đối với một nút trong bất kỳ đường đi nào*
> 	
> ![[Pasted image 20230411004310.png]]

### 1.3 Tìm kiếm theo cấu trúc cây

#### Các giải thuật tìm kiếm theo cấu trúc cây
> [!abstract] Ý tưởng
> * Khám phá (xét) không gian trạng thái bằng cách sinh ra các trạng thái kế tiếp của các trạng thái đã khám phá. (***Phương pháp khai triển các trạng thái***).

![[Pasted image 20230411004825.png]]

```python
class Node:
	def __init__(self, state, parent_node, action, path_cost, depth):
	self.state = state
	self.parent_node = parent_node
	self.action = action
	self.path_cost = path_cost
	self.depth =  depth

def make_node(state):
	return Node(state, Null, Null, 0, 0)

# chèn tất cả các nodes vào fringe
def insert_all(nodes, fringe):
	return fringe + nodes 

# tạo các trạng thái kế cận cho một nút trước bằng hàm kế thừa
# các khả năng có thể xảy ra tiếp theo
def expand(node, problem):
	successors = set()
	for action, result in problem.successor_fn(node.state):
		s = make_node(result)
		s.parent_node = node
		s.action = action
		s.path_cost = node.path_cost + problem.step_cost(node.state, action, result)
		s.depth = node.depth + 1
		successors.add(s)
	return successors

# take in problem obj and fringe list 
def tree_search(problem, fringe):
	fringe.insert(0, make_node(problem.initial_state))
	while fringe:
		node = fringe.pop(0)
		if problem.goal_test(node.state):
			return solution(node)
		fringe = insert_all(expand(node,problem), fringe)
	return failure # rỗng
```

* **`fringe`** - cấu trúc hàng đợi kiểu FIFO 

> [!note] Xác định chiến lược tìm kiếm
> Các tiêu chí:
> * **Tính hoàn chỉnh** - có đảm bảo tìm ra lời giải (nếu tồn tại)
> * **Độ phức tạp về thời gian** - số lượng các nút được sinh ra
> * **Độ phức tạp về bộ nhớ** - số lượng tối đa các nút được lưu trong bộ nhớ
> * **Tính tối ưu** - có đảm bảo tìm được lời giải có chi phí thấp nhất

> [!note] Đánh giá độ phức tạp về Time and Mem
> * **b** - hệ số phân nhánh tối đa của cây tìm kiếm 
> * **d** - độ sâu của lời giải có chi phí thấp nhất
> * **m** - độ sâu tối đa của không gian trạng thái (có thể là vô hạn)

## 2. Tìm kiếm cơ bản (Uninformed search strategies)
> [!abstract] Chỉ sử dụng các thông tin chứa trong định nghĩa bài toán

### 2.1 Tìm kiếm theo chiều rộng - BFS
> Phát triển các nút theo chiều rộng - các nút được xét theo thứ tự độ sâu tăng dần

* **G=(N,A)** - cây biểu diễn không gian trạng thái của bài toán 
	* **N** - tập các nodes của cây 
	* **A** - tập các cạnh có hướng nối các nodes của cây
* **n_0** - trạng thái đầu của bài toán (root)
* **SC(n)** - tập trạng thái con của trạng thái đang xét n
* **GOAL** - tập các trạng thái đích của bài toán

```python
def bfs_search(G, n_0, GOAL):
	# initialize the fringe with the initial state
	fringe = [n_0]
	# initialize closed with an empty set
	closed = set()

	while fringe:
		# Dequeue the first node from fringe
		n = fringe.pop(0)
		# check if the node is a goal state
		if n in GOAL:
			return n
		# add current node to closed
		closed.add(n)
		# get the set of successive node of the current node
		successors = SC(n)
		for sc in successors:
			# check if the sc is not in the fringe or closed
			if successor not in fringe and successor not in closed:
				# then add successor to fringe
				fringe.append(successor)
	# if goal state not found, return failure
	return "Failure"
	
```

**Nhận xét**: 
* Tính hoàn chỉnh: Có (nếu có hệ số phân tán hữu hạn)
* Độ phức tạp về tgian: 
$$
1 + b + b^2 + b^3 + ... + b^d = O(b^{d+1})
$$
* Độ phức tạp về bộ nhớ: $O(b^{d+1})$ - nếu giữ các node trong bộ nhớ
* Tính tối ưu: Có (nếu chi phí = 1 cho mỗi bước)

### 2.2 Tìm kiếm với chi phí cực tiểu - UCS
> [!abstract] 
> Phát triển các nút chưa xét có chi phí thấp nhất
>* Các nút được xét theo thứ tự chi phí (từ gốc tới nút đang xét) theo chiều tăng dần

* **`fringe`** - cấu trúc hàng đợi, trong đó các phần tử được sắp xếp theo chi phí đường đi

```python
# returns the minimum cost in a vector
# if (there are multiple goal states)
def uniform_cost_search(G, n_0, GOAL):
	# Initialize fringe with the initial state and its cost
	fringe = [(0,n_0)]
	# Initialize closed with an empty set
	closed = set()

	while fringe: 
		# Dequeue a node from fringe with the lowest cost
		(cost, n) = heapq.heappop(fringe)
		#check if the node is a goal state
		if n in GOAL
			return n
		# Add the current node to closed
		closed.add(n)
		# Get the set of successive nodes of the current node
		successors = SC(n)
		for sc in successors:
			# Calculate the cost from the initial state to the successor
			new_cost = cost + G[n][sc]
			if sc not in closed:
				# Add the successor and its cost to fringe
				heapq.heappush(fringe, (new_cost, sc))
			elif sc in fringe:
				# else if the successor is already in the fringe, update its cost
				index = fringe.index(sc)
				(old_cost, nodex) = fringe[index]
				if new_cost < old_cost:
					fringe[index] = (new_cost, node)
					heapq.heapify(fringe)# Update the position of an element when its cost is updated
	return "Failure"		
```

> [!caution] 
> UCS trở thành BFS nếu chi phí mỗi bước ở mỗi cạnh của cây tìm kiếm là như nhau

**Nhận xét**:
* Tính hoàn chỉnh: Có (nếu step_cost >= e > 0)
* Độ phức tạp về time: 
	* Phụ thuộc vào tổng số các nút có chi phí =< chi phí của lời giải tối ưu:
$$
O(b^{\lceil{C^*/e}\rceil}) \text{, trong đó C* là chi phí của lời giải tối ưu}
$$
* Độ phức tạp về bộ nhớ:
	* Phục thuộc vào tổng số các nút có chi phí =< chi phí của lời giải tối ưu:
$$
O(b^{\lceil{C^*/e}\rceil})
$$
* Tính tối ưu
	* Có, nếu các nút được xét theo thứ tự tăng dần về chi phí

### 2.3 Tìm kiếm theo chiều sâu, giới hạn độ sâu, sâu dần (DFS, DLS, IDS)

#### DFS -  Depth-First Search
> Phát triển các nút chưa xét theo chiều sâu - Các nút được xét theo thứ tự độ sâu giảm dần

* **fringe** - cấu trúc kiểu ngăn xếp LIFO (các nút mới được bổ sung vào đầu fringe)

```python
def DFS(N, A, n_0, GOAL)
	# initialize fringe with the initial state
	fringe = [n_0]
	# initialize closed with an empty set
	closed = set()
	while fringe:
		#Pop a node from fringe
		n = fringe.pop()
		if n in GOAL:
			return n
		closed.add(n)
		successors = SC(n)
		for sc in successors:
			if sc not in closed and sc not in fringe:
				fringe.append(sc)
	return "Failure"
```
==Implement lại==

**Nhận xét**:
* Tính hoàn chỉnh:
	* Không - thất bại nếu  không gian trạng thái có độ sâu vô hạn
	* Đạt tính hoàn chỉnh đổi với không gian trạng thái hữu hạn
* Độ phức tạp về thời gian:
	* O(b^m): sẽ rất lớn nếu m lớn hơn nhiều so với d
* Độ phức tạp về bộ nhớ:
	* O(bm) (tuyến tính)
* Tính tối ưu: Không

#### DLS - tìm kiếm giới hạn độ sâu 
* pp tìm kiếm theo chiều sau DFS + sử dụng giới hạn về độ sâu D trong quá trình tìm kiếm. 
	-> Các nút ở độ sâu D không có nút con
* Cấu hình:
	* Sửa hàm `SC(n)` trả về rỗng nếu độ sâu nút n là D

> [!warning] Vấn đề
> Nếu tất cả các lời giải (các nút đích) nằm ở độ sâu lớn hơn giới hạn độ sâu D, thì giải thuật DLS thất bại (ko tìm được lời giải)

#### Iterative deepening search (IDS) - tìm kiếm sâu dần
* Áp dụng giải thuật DFS đối với giới hạn độ sâu D = 0
* Nếu thất bại, tiếp tục áp dụng giải thuật DFS với D = 1
* Nếu tiếp tục thất bại, tiếp tục áp dụng giải thuật DFS với D tăng dần cho đến khi:
	* Tìm được lời giải
	* (Hoặc) toàn bộ cây đã đuợc xét mà không tìm được lời giải.

![[Pasted image 20230417000603.png]]

**Nhận xét:**
* Tính hoàn chỉnh: có
* Độ phức tạp về thời gian:
$$
(d+1)b^0 + db^1 + (d-1)b^2 + ... + b^d = O(b^{d+1})
$$
* Độ phức tạp về bộ nhớ: $O(bd)$
* Tính tối ưu: có, nếu chi phí cho mỗi bước (mỗi cạnh của search tree) = 1

#### So sánh DFS và IDS
Với  độ sâu d = 5, hệ số phân nhánh b = 10. Số lượng các nút được sinh ra trong giải thuật tìm kiếm:
* DLS = 111,111
* IDS = 123,456
-> Lãng phí: (123,456 - 111,111)/111,111 = 11%

