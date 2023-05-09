 > Sử dụng các tri thức cụ thể của bài toán -> Quá trình tìm kiếm hiệu quả hơn.

## 1. Tìm kiếm best-first
> [!abstract] Idea
> Sử dụng một hàm đánh giá f(n) cho mỗi nút của cây tìm kiếm
> * Đánh giá mức độ phù hợp  của nút đó: ưu tiên xét các nút có mức độ phù hợp cao nhất.

> [!note] Cài đặt
> Sắp thứ tự các nút trong cấu trúc fringe theo trật tự giảm dần về mức độ phù hợp.

![[Pasted image 20230420202616.png]]

### 1.1 Gready best-first
> [!abstract] Nguyên tắc
> Tìm kiếm trạng thái tiếp theo của đồ thị mà có khoảng cách gần nhất đến trạng thái đích. 
> * Việc ước tính khoảng cách bằng cách sử dụng hàm ***heuristic***

> [!note] Xây dựng hàm đánh giá - Heuristic function
> Đáp ứng hai yêu cầu cơ bản:
> * Hàm phải được thiết kế sao cho nó luôn lớn hơn hoặc bằng khoảng cách thực tế từ trạng thái hiện tại đến trạng thái đích. (nếu không, sẽ bõ qua các giải pháp tối ưu)
> * Hàm cần có thời gian tính toán nhanh chóng, vì sẽ được sử dụng nhiều lần trong quá trình tìm kiếm.

![[Pasted image 20230420202859.png]]

```python
# Demo thuat toan
# Gia su do thi duoc bieu dien duoi dang danh sach ke (Adjacency list)

def greedy_best_first_search(graph, start, goal, heuristic):
	visited = set()
	queue = PriorityQueue()
	queue.put(0, start)

	while not queue.empty():
		cost, node = queue.get()
		if node == goal:
			return True
		visited.add(node)
		for neighbor, weight in graph[node].items():
			if neighbor not in visited:
				queue.put((heuristic[neighbor], neighbor))
	return False

# Su dung Greedy best-first search de tim duong di tu A -> D
# trong do thi sau

graph = {
    'A': {'B': 2, 'C': 1},
    'B': {'D': 5},
    'C': {'D': 3},
    'D': {}
}

heuristic = {
    'A': 6,
    'B': 4,
    'C': 3,
    'D': 0
}

start = 'A'
goal = 'D'

result = greedy_best_first_search(graph, start, goal, heuristic)
print(result)
# tra ve True neu tim thay duong di, ko tra ve False
```

**Nhận xét**:
* Tính hoàn chỉnh: 
	* Không - vì có thể vướng trong các  vòng lặp
* Độ phức tạp về thời gian:
	* $O(b^m)$
	-> Một hàm heuristic tốt có thể mang lại cải thiện lớn
* Độ phức tạp về bộ nhớ:
	* $O(b^m)$ - lưu trữ tất cả các nút trong bộ nhớ
* Tính tối ưu:
	* Không

### 1.2 A*
> [!abstract] Nguyên tắc
> Tránh việc xét (phát triển) các nhánh tìm kiếm đã xác định (cho đến thời điểm hiện tại) là có chi phí cao.

* Sử dụng hàm đánh giá 
$$
f(n)=g(n)+h(n)
$$
- $g(n)$ - chi phí từ nút gốc cho đến nút hiện tại n
- $h(n)$ - chi phí ước lượng từ nút hiện tại n tới đích
- $f(n)$ - chi phí tổng thể ước lượng của đường đi qua nút hiện tại n đến đích

![[Pasted image 20230420203000.png]]

```python
# Demo thuat toan

import heapq # priority queue
from collection import defaultdict # dictionary of lists

# 3-tuples with (priority, unique_index, item)
# -  priority = f(n)
# - item = obj node
class PriorityQueue: 
	def __init__(self):
		self._queue = []
		self._index = 0
	def insert(self, item, priority):
		heapq.heappush(self._queue, (priority, self._index, item))
		self._index += 1
	def remove(self):
		return heapq.heappop(self._queue)[-1]
	def isEmpty(self):
		return len(self._queue) == 0
	def getSize(self):
		return self._index

class Node:
	# key - indetifier of node
	# forward_cost = h(n)
	def __init__(self, key, forward_cost):
		self.key = key
		self.forward_cost = forward_cost
	def getKey(self):
		return self.key
	def getForwardCost(self):
		return self.forward_cost

class Graph:
	def __init__(self):
		self.nodes = {} # dict of nodes
		self.edges = [] # list of 3d-tuple (source node, dest node, weight)
		self.path = [] # path
		# dict with the lists of SCs of each node, make it faster to get the SCs
		self.successors = defaultdict(list)
		
	def getPath(self):
		return self.path
		
	def addEdge(self, source, dest, weight):
		edge = (source, dest, weight)
		if not self.existEdge(edge): # check whether the edge is exist inside graph
			self.nodes[source], self.nodes[dest] = source, dest # add source node and dest node to dict
			self.edges.append(edge) # add edge to edge list
			self.successors[source.getKey()].append((dest, weight))
			# since defaultdict(list) create a dictionary where the default value of any key is empty list
		else:
			print('Error: edge (%s -> %s with weight %s) already exists!!' \
                % (edge[0].getKey(), edge[1].getKey(), edge[2]))
        
	def existEdge(self, edge):
		for e in self.edges:
			# compare edge start key, compare edge dest key, weight
			if e[0].getKey() == edge[0].getKey()\
			and e[1].getKey() == edge[1].getKey()\
			and e[2] == edge[2]:
			return True
		return False
	# function to run A_star search algo
	def excAStar(self, initial_node, goal_node):
        if not self.edges:
            print('Error: graph not contains edges!!')
        else:
            # checks if both the nodes exists
            if initial_node in self.nodes and goal_node in self.nodes:
                if initial_node == goal_node: # checks if are the same nodes
                    return 0
		
                queue = PriorityQueue() # creates a priority queue (min heap)
				
                # "distance_vector" and "antecessors" are used for reconstruct the path
                distance_vector, antecessors = {}, {}
                for node in self.nodes:
                    distance_vector[node.getKey()] = None # initializes with None
                    antecessors[node.getKey()] = None
                distance_vector[initial_node.getKey()] = 0
		
                # calculates costs
                g_cost, h_cost = 0, initial_node.getForwardCost()
                f_cost = g_cost + h_cost
                queue.insert((initial_node, g_cost, h_cost), f_cost)
                total_cost = None
		
                while True:
		
                    # a item of the queue is a 3-tuple: (current_node, g_cost, h_cost)
                    current_node, g_cost, h_cost = queue.remove()

                    # gets all the successors of "current_node"
                    successors = self.successors[current_node.getKey()]

                    for successor in successors:
                        destination, weight = successor # unpack 2-tuple successor

                        # calculates costs
                        new_g_cost = g_cost + weight
                        h_cost = destination.getForwardCost()
                        f_cost = new_g_cost + h_cost
                        queue.insert((destination, new_g_cost, h_cost), f_cost)

                        # updates "distance_vector"
                        if distance_vector[destination.getKey()]:
                            if distance_vector[destination.getKey()] > new_g_cost:
                                distance_vector[destination.getKey()] = new_g_cost
                                antecessors[destination.getKey()] = current_node.getKey()
                        else:
                            distance_vector[destination.getKey()] = new_g_cost
                            antecessors[destination.getKey()] = current_node.getKey()

                        # verifies that reached the goal
                        if destination.getKey() == goal_node.getKey():
                            # updated "total_cost"
                            if not total_cost:
                                total_cost = f_cost
                            elif f_cost < total_cost:
                                total_cost = f_cost

                    if queue.isEmpty(): # verifies if the queue is empty
                        # reconstruct the path
                        curr_node = goal_node.getKey()
                        while curr_node:
                            self.path.append(curr_node)
                            curr_node = antecessors[curr_node]
                        self.path = self.path[::-1]
                        return total_cost
            else:
                print('Error: the node(s) not exists in the graph!!')
	
```

**Nhận xét**:
* Tính hòan chỉnh:
	* Với không gian trạng thái là hữu hạn và có giải pháp để tránh việc xét lặp lại các trạng thái -> A* hoàn chỉnh
	* Với không gian trạng thái là hữu hạn và không có giải pháp để tránh việc xét lặp lại các trạng thái -> A* không hoàn chỉnh
	* Với không gian trạng thái là vô hạn -> A* không hoàn chỉnh
* Độ phức tạp về thời gian:
	* Bậc của hàm mũ (số lượng nút được xét là hàm mũ của độ dài đường đi của lời giải)
* Độ phức tạp về bộ nhớ:
	* Lưu giữ tất cả các nút trong bộ nhớ
* Tính tối ưu:
	* Có (với đk đặc biệt)

> [!note] Các ước lượng chấp nhận được
> $0\leq$**h(n)**$\leq$ h*(n) với h*(n) là chi phí thật đi từ nút n đến nút đích.
> * Ước lượng chấp nhận được không đánh giá quá cao (overestimate) đối với chi phí để đi tới đích (lạc quan)
> 
> **-> Nếu h(n) là đánh giá chấp nhận được, thì A* tối ưu cho `TREE-SEARCH`**

VD: chò trơi ô chữ 8 số:
- h1(n) = số các ô chữ nằm sai vị trí (so với  vị trí của ô chữ đấy ở trạng thái  đích)
* h2(n) = khoảng cách dịch chuyển ngắn nhất (bước) để dịch chuyển các ô chữ sai vị trí về vị trí đúng
![[Pasted image 20230420231730.png]]
-> h1(S) = 8; h2(S) = 3 + 1 + 2 + 2 + 2 + 3 + 3 + 2 = 18

> [!note] Ước lượng ưu thế
> Ước lượng h2 được gọi là **ưu thế (trội hơn)** ước lượng h1 nếu : 
> $$
> h*(n)\geq h_2(n) \geq h_1(n) \forall{n}
> $$
> * Nếu ước lượng h2 chiếm ưu thế hơn h1 -> **Nên sử dụng h2 thay cho h1 trong quá trình tìm kiếm.**

> [!note] Ước lượng kiên định
> Một ước lượng h được xem là **kiên định** nếu với mọi nút n, n' (sinh ra từ n bởi hành động a):
> $$
> h(n) \leq c(n,a,n') + h(n')
> $$
> * Với ước lượng h là kiên định -> f(n') = g(n') + h(n') = g(n) + c(n,a,n') + h(n') >= g(n) + h(n) = f(n)
> -> **f(n) không giảm trong bất kì đường đi tìm kiếm nào đi qua n**
> 
> => **Nếu h(n) là kiên định, thì phương pháp tìm kiếm A* sử dụng giải thuật `GRAPH-SEARCH` là tối ưu** 

### A* vs UCS
* UCS - phát triển theo mọi hướng
* A* - phát triển chủ yếu theo hướng đích, nhưng vẫn đảm bảo tính tối ưu.

![[Pasted image 20230420233504.png]]

## 2. Tìm kiếm cục bộ
* Khi bài toán có nhiều điểm cực trị địa phương 

> [!abstract] Các giải thuật tìm kiếm cục bộ
> * Sử dụng cho các bài toán muốn tìm kiếm trạng thái đích (không tìm bước, hành động để tới đích)
> * Chỉ lưu một trạng thái, với mục tiêu cải thiện trạng thái hiện thời theo một tiêu chí nào đó.

VD: bài toán 8 quân hậu: tìm vị trí các quân mà ko quan tâm tới đuờng đi dẫn tới trạng thái đó. 

### 2.1 Hill-climbing
> [!abstract] Nguyên lí
> Tạo ra hàng xóm cho trạng thái hiện thời và di chuyển sang hàng xóm có hàm mục tiêu tốt hơn.

> [!fail] Nhược điểm 
> * Có thể tắc ở các điểm cực đại cục bộ
> * Không tìm được lời giải tối ưu toàn cục

![[Pasted image 20230421002141.png]]

![[Pasted image 20230421002235.png]]

![[Pasted image 20230421002452.png]]

* Bài toán 8 quân hậu có pp tối ưu cục bộ, trong đó số cặp quân hậu ăn nhau (h) = 1 (f(n) = -h)

### 2.2 Simulated annealing

> [!abstract] Nguyên lí
> Sử dụng chiến luợc tìm kiếm ngẫu nhiên, trong đó chấp nhận các thay đổi làm tăng giá trị hàm mục tiêu (cần tối ưu) và cũng chấp nhận (*nhưng có hạn chế*) các thay đổi làm giảm hàm mục tiêu.
> (Thoát khỏi cá điểm tối ưu cục bộ bằng cách **cho phép dịch chuyển "tồi"** từ trạng thái hiện thời, nhưng **giảm dần tần xuất** của các di chuyển này)
> * Sử dụng một tham số điều khiển T: bắt đầu cao, giảm dần về 0 (kiểm soát tần xuất các di chuyển tồi)

![[Pasted image 20230421003020.png]]

* Nếu T giảm chậm, thì pp tìm kiếm Simulated  Annealing sẽ tìm được lời giải tối ưu toàn cục với xs xấp xỉ 1.

> [!check] Ưu điểm 
> Có thể tránh được các điểm tối ưu cục bộ

### 2.3 Local beam
* Ở mỗi thời điểm (trong quá trình tìm kiếm), luôn lưu giữ k trạng thái tốt nhất (thay vì 1)
Bắt đầu: 
* ***Bước 1:** k chọn ngẫu nhiên.
* ***Bước 2**: Ở mỗi bước tìm kiếm, sinh ra tất cả các trạng thái kế tiếp của k trạng thái này.
* ***Bước 3**:
	* Nếu một trong số các trạng thái là trạng thái đích -> giải thuật kết thúc
	* Nếu ko, chọn k trạng thái tiếp theo tốt nhất (từ tập các trạng thái tiếp theo) và lặp lại bước 1

### 2.4 Genetic Algorithms
> [!abstract] Nguyên lí
> * Áp dụng pp tìm kiếm ngẫu nhiên (stochastic search) để tìm được lời giải tối ưu.

* Giải thuật di truyền có khả năng tìm đực các lời giải tốt nhất thậm chí ngay cả với các không gian tìm kiếm không liên tục và phức tạp.

![[Pasted image 20230421004138.png]]

![[Pasted image 20230421004258.png]]

> [!note] Mô tả
> * **Xây dựng quần thể ban đầu**:
> 	* Tạo nên một số các giả thiết (khả năng của lời giải) ban đầu
> 	* Mỗi giả thiết khác các giả thiết khác
> * **Đánh giá quần thể**:
> 	* Đánh giá mỗi giả thiết (bằng cách kiểm tra độ chính xác của hệ thống trên một tập dữ liệu kiểm thử...)
> 		* (quan điểm sinh học) Đánh giá dựa trên **độ phù hợp (fitness)** của giả thiết đó.
> 	* Xếp hạng các giải thiết theo mức độ phù hợp, chỉ giữ lại các giả thiết **phù hợp nhất**
> * **Sản sinh ra thế hệ tiếp theo**:
> 	* Thay đổi ngẫu nhiên các giả thiết được giữ lại để sản sinh ra thế hệ tiếp theo (con cháu)
> * Lặp lại quá trình trên đến khi ở một thế hệ có giải thiết tốt nhất có độ phù hợp cao hơn giá trị phù hợp mong muốn được định trước.

![[Pasted image 20230421004732.png]]
