**Unified Hybrid Genetic Search heuristic (UHGS)**:
* Problem-independent unified local search
* Genetic operators
* Advanced diversity management methods

> [!info]
> General-purpose solvers for combinational optimization are algos that can be used to address large classes of problem settings, *without requiring extensive adaptations, user involvement or expertise.*

* Component-based heuristic solution framework

* To achieve a high-performance general-purpose solvers, it is necessary to balance between **generality** of scope and **specificity** in particular characteristics, to establish high-quality solutions for the broadest set of problem settings within limited computation time.

* Propose UHGS based on unified problem-independent procedures:
	* Local Search
	* Crossover
	* Split Algorithm
	* Diversity Management

* For a higher efficiency during local-improvement procedures, a **unified route-evaluation methodology** (which is based on infor preprocessing on subsequences, and move evaluations as a concatenation (gach noi) of known subsequences) is used.

> [!note] Main Contributions
> * **A component-based heuristic design** proposed for multi-attribute VRPs -> isolate problem-specific adaptations from the generic framework.
> * **A unified framework** for efficient route evaluations and local search, based on efficient move-evaluation techniques, which exploit information on sub-sequences through concatenation operations to efficiently explore neighborhoods.
> * **Unified versions** of **efficient genetic operators, solution representation,** and **split algo**
> * **A UHGS** which addresses a large set of variants with a single implementation and set of parameters, and yields solutions of exceptional quality on prominent VRP variants and benchmark instance sets

> [!note] CVRP notations
> $G = (V,E)$ is a complete undirected graph with $|V| = n + 1$ vertices.
> * Vertex $v_0 \in V$ represents a depot, which is basement of a fleet of $m$ indentical vehicles with capacity $Q$.
> * Other vertices $v_i \in V$ \ ${v_0}$ represent customers characterized by a demand for $q_i$ unit of product.
> * Edges $(i,j)\in E$ illustrate the cost $d_{ij}$ to travel from customer $v_i$ to customer $v_j$.
> * CVRP requires up to $m$ cycles representing vehicle routes, which start and end at depot $v_0$, in order to service each customer one.
> ![[Unified Solution Framework for multi-attribute vehicle routing problems-20231114173105836.webp]]

## General-purpose solution approaches for MVRPs
> [!abstract] 3 main approaches
> * Rich Solvers
> * Modeling and solution frameworks
> * Component-based frameworks

### Rich Solvers
> Rich Solvers are designed to address a multi-attribute VRP formulation generalizing several variants associated to subsets of its attributes.

* Several well-known VRP heuristics :
	* Unified Tabu Search (UTS)
	* Adpative Large Neighborhood Search Algorithm (ALNS)
	* Iterated Local Searches (ILS)
	* ILS with Set Partitioning (ILS-SP)
	* Integer programming with Set Partitioning (IPSP)

![[Unified Solution Framework for multi-attribute vehicle routing problems-20231115003005024.webp|1321]]
(Comparison in attribute coverage of rich solvers vs Unified Hybrid Genetic Search heuristic)

* Each Rich Solver relies on a "rich" Multi-attribute VRP formulation:
	* UTS - Periodic VRP with time windows
	* ALNS - pick-up and delivery with time windows
	* ILS - General time windows, time-dependent and flexible travel time
	* ILS-SP - Heterogeneous pickup-and-delivery with time windows 

> [!warning] Limitations
> * Intricate (phức tạp) problem, hard to be addressed when the number of considered attributes grows.
> * All the features still present when considering a particular varient with less attributes -> wasted computations, higher complexity.

### Modeling and solution Frameworks
> Seek general properties of the attributes to transform into machine-readable components

* Some typical examples:
	* Desaulniers's Framework (1998): formulated a number of classes of attributes as resources (load, distance, time), extend to following up customer visit through **resource extension functions**.
	* Campbell & Savelsbergh approach (2004): reduced the complexity of route evaluation in difficult EVAL attributes. Meaningful information on sub-sequences of successive visits (partial routes) was exploited to speed up evaluations of new routes.
	* Irnich (2008): considered forward and backward extension of resources, as well as the management of generalized resources extension functions on sub-sequences of visits to perform efficient route evaluations.
	* Puranen (2011): introduced domain model which is capable of transforming VRP variants into routing metamodel based on the concepts of **actors**, **activities**, **resources** and **capabilities**. It implemented both resource extension functions, and mapping-ordering generalization.

> [!caution] Limitations
> Requiring **strong** properties to be efficiently applied.
### Components-based Framework
* Problem attributes are restrain to small **polymorphic method components** which are capable of adapting to the problem specifics.
	* Create a library of basic attribute-dependent operators -> Algo can auto select the neccessary operators in accordance to the problem.
	* Components are designed to be able to integrate attribute-specific strategies

* MAVRPs present a particular structure combining decisions on assignment (and partitioning), sequencing, and fixed-sequence optimization and evaluation

* There are three main classes of attributes concerned in MVRPs:
	* **Assignment of customers and routes to resources (ASSIGN)**:
		* Involve allocating limited resources (vehicle,...) to customer services and routes.
		* Common ASSIGN attributes include handling multiple depots, heterogeneous fleets, split deliveries, site dependencies, inventory, and profit collection.
		- Some MVRP variants focus on *resources to routes* (reassign entire route is feasible) priority on route constraints. Operation cost high.
		- While others deal with *resources to customers* assignments. (infeasible due to independent assignment constraints) priority on customer constraints. Late fee.
	* **Sequence choices (SEQ)**:
		* Impact the customer visit order along a route.
		* Examples include backhaul settings (combining linehaul and backhaul services), multiple trips, and group-based customer visits.
		* Specific graph-related SEQ attributes significantly affect route structures and sequencing methods.
			* routing on a tree or a shoreline
	* **Evaluation of fixed sequences (EVAL)**:
		* come to once routes are determined.
		* Involve evaluating service times, idle time, break placement, speed choices, and product placement in trucks.

> [!note] 3 adaptive components accounting for classes of attributes
> * **Assignment**: Select and check the feasibility of customer and route re-assignments to different ASSIGN attribute resources (day, depot, vehicle type...)
> * **Sequence choice**: Generate neighbor solutions with different sequence alternatives regarding to SEQ attributes
> * **Route evaluations**: evaluate fixed route and optimize side decisions related to EVAL attributes.

==👉 Each class of attributes impacts the resolution methodologies in a different way.==

Với từng components, các chức năng mong muốn cho từng class of attributes.
Algo cho từng components.
Risk của từng components. Ex: gán người gán hàng vào xe nào, nhân viên bị ốm. chỉ xét trong 1 component hay là các components khác cũng liên quan
Constraints cho từng components.