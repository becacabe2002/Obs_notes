
* Scheduling of deliveries + routing of vehicles -> importance in supply chain network

* Mainly focus on **freight transportation**.

> [!tip] Objective of VRP
> * Minimization of the total distribution costs
> * High level distribution services


* Distribution cost (big part of final selling price) consists of:
	* **Fixed costs**:
		* Wage of driver (no considering the specific route or number of customers)
		* Vehicle usage (no considering the specific route or number of customers)

	* **Variable costs**:
		* Fuel costs
		* Length and duration of routes
		* others restrictions/parameters

=> ==Only need to define the VRP variants, formulation of the problems, and the objective function which all contribute to the total cost==

> [!note]
> * **Formulation of the problem**: defining the problem, its params, constraints and objectives in a mathematical or symbolic way to create a mathematical model.
> * **Objective function**: a mathematical expression in problem formulation, which represents the choice of maximize/minimize smthing to achieve goal.

* With the increase in the number of customers, along with their demands, **Optimization Algo** is the key component for effective customer service and efficient operations.

## Variants of VRP
[(5) VEHICLE ROUTING PROBLEM AND ITS VARIANTS | LinkedIn](https://www.linkedin.com/pulse/vehicle-routing-problem-its-variants-sajaykumar-j/)

> [!abstract] 
> VRP variants are classified into 16 categories: CVRP, VRPTW, VRPPD, HFVRP, MDVRP, GVRP, DVRP, 3D-VRP, OVRP, SDVRP, TDVRP, MEVRP, MTVRP, PVRP, ConVRP, TTRP

* Capacitated VRP (CVRP)
* **VRP with time windows (VRPTW)** (cũng có thể là time-dependent)
* **VRP with pickups and deliveries (VRPPD) (continuous pickup and delivers)**
* Heterogenous fleet VRP (HFVRP)
* **VRP with multiple depots (MDVRP) & Collaborative VRP (extension of MDVRP)**
* Green VRP (GVRP)
* **Open VRP** (third party) (OVRP)
* Dynamic (DVRP) and Stochastic VRP (SVRP)
* **Multi-trip VRP** (do access restrictions, traffic congestion ...) (MTVRP)
* Multi-echelon VRP (không thấy có nhắc tới việc có nhiều hơn 2 distribution layers)
* Time-dependent VRP
* Two dimensional and three dimensional VRP
* Consistent VRP
* Split Delivery VRP (SDVRP)
* Periodic VRP (PVRP)
* Truck and trailer VRP

> [!question] Determining the priority of pickup and delivery based on the value of the goods and customer priorities ???

Vẫn liên quan tới Pickups and deliveries

### VRP with time windows - VRPTW
> Packages must be delivered to a set of customers within specificed time windows.

* Constraint:
	* Each customer must be visited within a predifined time window.
		* **Hard**: it cant be too soon or too late (in time)
		* **Soft**: the vehicle can arrive at the end of the time window, but must pay an addition cost.

* Parameters:
	* Number of customers
	* Customer's locations
	* Time windows
	* Vehicle capacities (Ko nhắc tới trong đề bài)
	* The number of available vehicles
	* Transportation costs

### VRP with pickups and deliveries - VRPPD
* Finding a set of optimal routes, for a fleet of vehicles, in order to serve a set of transportation requests.

* Constraints:
	* Visit all pickup and delivery locations
	* **Precedence constraints**: which each pickup location has to be visited prior to visiting the corresponding delivery location.
	* **Pairing constraints**: restrict the set of admissible routes (đường đạt chuẩn?), so that one vehicle has to do both the pickup and the delivery of the load of one transportation request

* Initial parameters:
	* Vehicle: capacity, start location, end location
	* Request: load to be transported, origin, destination

> [!question] Can occur at the same or different locations ??

Có thể pickup/delivery ở nhiều địa điểm

### Open VRP - OVRP
* Each vehicle is not required to return to the central depot after visiting the final customer. (Open path instead of closed circuits).

* Appropriate in a situation where vehicles are hired from a **third-party logistics company**.
	* The cost of the hire is based on the distance traveled while the vehicles are loaded.

### Multi-trip VRP - MTVRP
* External factors (traffic congestion, access restrictions, enviromental regulations) may force companies to use vehicles with **lower capacities**. -> Can only visit a few customers during the trip.

* But they can carry out more than one trip during the working day.


> [!tip] Trending
> The consideration of multiple constraints (from multiple VRP variants) at the same time is defined by researchers as ***RICH VRP***.
> * Use algo on containing variants to simplify the problem.

## Algo Classification

![[Variants of VRP and applied Algos-20231017141506191.webp|807]]
(classification of algo for the VRP)

* The integration of an Algo into system includes testing and evaluation process with benchmarch instance (in literature) or real-life cases.
	* ***Benchmark Instances***: standardized or well-defined problem scenarios

#### High-level Algos

* **Exact**: ensure finding the most optimal solution to an omptimization problem by exploring all possible solutions and exhaustively search for the best one.
	* Suitable for small -> medium size instance.
	* Ex: Branch and bound (B&B), Branch and cut, Integer programming

* **Heuristics** & **Metaheuristics**: balance between solution quality and computational time.
	* **Heuristic**: provide efficient (may be not optimal) solution. They use rules or strategies to quickly generate good solutions.
		* Suitable for larger problem instances, where finding the optimal solution is not feasible within a reasonable time.
		* Ex: Clarke-Wright savings algo, Insertion heuristics (VRP)
	* **Metaheuristics**: guide other heristics or optimization methods to explore and navigate more efficiently in the solution space.
		* Suitable for vast search space, where finding optimal is difficult or too time-consuming
		* They can be applied to a wide range of optimization problems
		* Ex: Genetic algo, simulated annealing, ant colony ...

### In-depth Exploration

> [!note] Exact Algos
* ***Lagrange Relaxation*** - converts a constrained problem into an unconstrained one by using **Lagrange Multipliers**
	* Balance between optimizing the objective function and satisfying the constraints
	-> Find **near-optimal** solutions.

* ***Column Generation*** - generates and considers only a subset of variables (columns) that are relevant to the current problem solution.
	* Iteratively adds new variables to the problem
	* Select those that contribute the most to improving the objective function
	-> Focus on most important vars, useful for problems with a vast number of potential solutions (Ex: network design, resource allocation ...)

> [!note] Heuristic Algos
* CONSTRUCTION: *startes with an empty or partial solution and addes elements step by step*

* TWO-PHASE: *initial phase where the problem is divided or grouped in a way that simplifies the problem. And in the second phase, the grouped elements are optimized or processed to find a solution.*
	* ***Cluster First - Route Second (CFRS)***
		* Clusters/groups elements (Locations or Tasks) into manageable subsets
		* Determines the best routes to handle each subset

	* ***Route First - Cluster Second (RFCS)***
		* Firstly, optimizes individual routes or sequences for elements without considering grouping
		* Then, elements are grouped based on the optimized routes.

* LOCAL IMPROVEMENT: *enhances solutions by making small adjustments within or between routes in a solution.*
	* ***Intra-Route*** - improves the solution within a single route. 
		* Makes localized adjustments to the sequence or order of elements (e.g., in a traveling salesman problem) within a single route to optimize the objective.

	* ***Inter-Route*** - makes changes that involve multiple routes. 
		* Involves swapping or reassigning elements between different routes in a solution, 
		-> Achievies a better overall solution in problems like vehicle routing or job scheduling.

> [!note] Metaheuristic Algos
* POPULATION SEARCH: *generates a new solution from a set of solutions, by combining and pairing existing ones, or making them co-operate through a learning process*
	* ***Genetic Algorithms*** - One of the most popular metaheuristic algorithms
		* At the beginning, a population of solutions (chromosome - nhiễm sắc thể) is selected.
		* Then in each iteration, two parents are selected from the population (according to fitness function) are combined through the crossover procedure to provide the offsprings.
		![[Variants of VRP and applied Algos-20231017171515854.webp|423]]
		* The mutation procedure is applied to ensure the diversity of the population.
		* Et the end of iteration, the best solutions are selected to be used as parents in the next iteration.

	* ***Memetic Algorithms*** - similar to GA's, but a local improvement method is applied for each child.
	* MA's & GA's ⊂ ***Evolutionary Algorithms*** 
	...

* LOCAL SEARCH: *explores the solution space by moving the current solution to another promising one in the neighborhood*
	* ***Tabu Search*** - one of the most frequently applied algorithms.
		* Continues the search even if a **local optimum** has been found.
		* Current solution is moved even if the objective degrades.
		* Previously visited solution was recorded and cannot be revisited.
		![[Variants of VRP and applied Algos-20231017173805285.webp|626]]
		...

> [!tip] Trending
> **Hybrid Algorithms** (combined meta-heuristics) are developed to achieve better result.

## Correlation between VRP Variants and Algorithms

### VRPTW
* TS and GA used to be among the most common applied algos (with Construction)
* A new direction towards Evolutionary Algo (mainly GA's) seems to have formed.

### VRPPD
* Local based metaheuristics prevail (chiếm ưu thế) population-based in the VRPPD.

### OVRP
* ILS
### MTVRP
