*Giáo viên hướng dẫn*: Cô Vũ Thị Hương Giang
*Người thực hiện*: Ngô Minh Tú - 20205226 - Công nghệ thông tin Việt Pháp
*Đề tài*: Đưa ra hướng giải quyết cho bài toán VRP với nhiều rằng buộc (MAVRP)

**Capacited vehicle routing problems**:
* **Input**: 
	* n customers, 2d locations (x,y) and demand quantity.
	* homogeneous fleet of m vehicles with Q capacity at depot
* **Output**:
	* Delivery routes with optimal cost (at most one route per vehicle)

* NP-hard problems
* with problem consists of 100 customers and single vehicle -> the number of feasible solution is approx 10^158

![[Chuẩn bị báo cáo-20240109144710823.webp]]

**Multi-attribute vehicle routing problems**:

* ***ASSIGNMENT***: assignment of customers and routes to resources
	* Periodic, Multi-depot, Heterogenous Fleet
* ***SEQUENCEING***: choice of sequence of visits

* ***ROUTE EVALUATION***: fixed sequence evaluation, scheduling or load feasibility resolution
	* Time windows, Loading Constraints ...

![[Chuẩn bị báo cáo-20240109083408450.webp|488]]
## Classic heuristic approaches
### Local-improvement procedures
* From an current solution `s`, define a neighborhood `N(s)` of solutions, created by applying changes.
	* Also called **Search space**
* Local Search improvement progress from one sol to another in this search space as long at the cost improves.

![[Chuẩn bị báo cáo-20240109093330997.webp]]

* For optimizing single route (TSP tour):
	* a $\lambda$-opt neighborhood is subset of moves obtained by deleting and reinserting $\lambda$ arc
		![[Chuẩn bị báo cáo-20240109093648873.webp]]

* For optimizing multiple routes together:
	* Insert neighborhood (relocate a delivery)
	* Swap neighborhood (swap two deliveries from different routes)
	* CROSS-exchange (exchange two sequences of visits)
	* I-CROSS (exchange and reverse two sequences)
	* 2-opt* exchange two route tails
		![[Chuẩn bị báo cáo-20240109094023189.webp]]

> [!warning] 
> Apply these neighborhoods with classic heuristics search may lead to **Local optimum**, which can be very different from **global optimum**.
> ![[Chuẩn bị báo cáo-20240109094408476.webp]]

> [!check] Metaheuristics solution
> _**Population-based search**_: manage and improve a population of solutions

---
## Classic Metaheuristics approaches
* Unified Tabu Search (UTS) - Periodic VRP with time windows
* Adpative Large Neighborhood Search Algorithm (ALNS) - pick-up and delivery with time windows

### Hybrid Genetic Algorithm
> is a genetic algorithms, with some twerks

* Giant-tour solution representation:
	* Polynomical Split algorithm to obtain a complete solution
		![[Chuẩn bị báo cáo-20240109104949283.webp]]
* Simple Crossover
* Local search on the offspring
* Population management (spacing constraint)

### Unified Hybrid Genetic Search
* Giant-tour solution representation (same as HGA)
* Efficient local search
* Penalized infeasible solutions
* Promotion of diversity - **Biased fitness**
$$
BF(I) = fit(I) + (1 - \frac{nbElit}{nbIndiv - 1}) * dc(I)
$$
*dc(I) - contribution to the diversity of Individual*
![[Chuẩn bị báo cáo-20240109084205471.webp]]

---
### Survey on classic metaheuristics
**Search Space**:
* Relaxations: 
	* It is more convenient to relax route constraints (Capacity, duration, time windows ...) (Not so convenient with fleetsize)
	* enable more fluent transition in search space between feasible solutions.
	* simple procedure for fleet-size minimization
	* Good solutions tend to be close to the borders of feasibility. -> waving around these borders by adapting the penalty coefficients. (hệ số phạt)
* Indirect representations of solutions:
	* Using **decode algorithm** to obtain the best complete solution from a solution representation
		* 1-to-many relationship
		* narrow down the search space

**Neighborhoods**:
* Polynomially enumerable: 
	* use either local or large neighborhood search.
		* local search neighborhoods is usually used for quadratic size (tập hợp các phần tử có kích thước bằng bình phương số phần tử)
		* Ruin-recreate is frequently used.
* Multiple neighborhoods:
	* the richness, variety of the neighborhoods will reflect the quality of solution (but will be trade-off with searching speed)
	* Addressing all attributes of the problems is key to success.
* Pruning and speed-up techniques:
	* Neighborhood pruning
	* Memory structure: matrices for move evaluations, hashtables for route evaluations.
	* Information preprocessing on subsequences to speed up move evaluations

**Trajectory** (quỹ đạo): 
* Randomization:
	* used as a simple way for avoiding cycling and bringing more diversity

**Memories and control**:
* Populations:
	* Several types of memories: 
		* Short term (tabu list) - avoid local optima
		* Medium/Long term - direct overall exploration
	* Standard memory form is using **populations**, which can store full sol, sol representations, routes and other kind of fragments of sol.
* **Population management**:
	* with population-based methods, it is necessary to have a *diverse, high-quality solutions*
	* Avoid premature convergence (when population information is poor, redundant)
	* using promotion of diversity and based on distance measures, in objective/solution space

![[Chuẩn bị báo cáo-20240109175512443.webp|485]]

**Guidance**:
* Explicitly collect, analyze and exploit on the past search to direct the future trajectories.
	* Historical statistics on solution features, arcs, sets of arcs, routes, or problem specic attributes.
	* Actions could be taken based on guidance:
		* *intensify* the search around promising solution features.
		* *diversify* the search around promising unexplored areas.
		* Apply penalties or encourage on solution features
		* Head to elite solutions or restarts...

**Hybridizations**:
* On general level, metaheuristics are naturally hybrids (combination of different variants)

---
## New general-purpose approach

> [!tip] Goal
> Define a unified method, which can achieve generality and efficiency

* Challenges:
	* Dealing with Rich VRP attributes, both activated and not-activated 
	* Addressing the problem but relegating problem-specificities
	* Each separate need to be acquired with modern solution evaluation and search procedures.

### Attribute-based modular design
* Let assignment/sequencing/route-evaluation operators be responsible for attribute-dependent tasks.
* Attribute-dependent modules are selected and combined base on the problem structure to implement the assignment, sequencing and route evaluations.

![[Chuẩn bị báo cáo-20240109084920365.webp]]

### Efficient unified local search for MAVRPs

> [!note] Route evaluation Operators based on re-optimization
> * Any local-search move involving a bounded number of *node relocations* or *arc exchanges* that can be presented as a **concatenation of a bounded number of sub-sequences**.
> * The same subsequences appear many times during different moves

![[Final Report - Project 3 - 20205226-20240109191536040.webp|699]]
<small>
<ul>
	<li><b>Intra-Route Relocation</b> - A stop may change its position inside its route.</li>
	<li><b>Intra-Route Exchange</b> - a stop switch its position with another stop (in the same route).</li>
	<li><b>Inter-Route Relocation</b> - A stop may be moved to another route.</li>
	<li><b>Inter-Route Cross-Exchange</b> - Two sets of consecutive stops of two different routes may be switched.</li>
</ul>
</small>
* Preprocessing on subsequences builds the information which can help speedup the search.

---
**SCHEMA FOR ROUTE EVALUATION COMPONENTS**
_Phase 1: Data Construction (pre-processing)_
* `INT(σ)` - initialize the data $𝒟(v_0)$ for a sub-sequence containing a single visit

* `FORW(σ)` - compute the data of $𝒟(σ ⊕ v_i)$ from the data of sub-sequence σ and vertex $v_i$ (moving forward node)

* `BACK(σ)` - compute the data of $𝒟(v_i \oplus σ)$ from the data of vertex $v_i$ and sub-sequence σ (moving backward node)

_Phase 2: Route evaluation_

* `EVAL2(σ1, σ2)` - evaluate cost and feasibility of the concatenated sequence $σ_1 ⊕ σ_2$

* `EVALN(σ1,..., σn)` - evaluate cost and feasibility of the concatenated sequence $σ_1 ⊕ ... \oplus σ_n$
---

> [!example] Route evaluation for distance and capacity constraints
> 
> * **manage**: Partial loads $Q(\sigma)$ and distance $D(\sigma)$
> </br>
> * **Init**: For a sequence $\sigma_0$ with a single visit $v_i$, $Q(\sigma_0) = q_i$ and $D(\sigma_0) = 0$
> </br>
> * **Forw, Back**: increase $L(\sigma)$ and $D(\sigma)$
> </br>
> * **Eval**: compute the data by induction on the concatenation operator
> 	* $Q(\sigma_1 \oplus \sigma_2) = Q(\sigma_1) + Q(\sigma_2)$
> 	* $D(\sigma_1 \oplus \sigma_2) = D(\sigma_1) + d_{\sigma_1(|\sigma_1|)\sigma_2}+ D(\sigma_2)$
<small>
<ul>
	<li>d_{\sigma_1(|\sigma_1|)\sigma_2} - distance between subsequence \sigma_1 and subsequence \sigma_2 (start from the last node of subseq1 to the first node of subseq2)</li>
</ul>
</small>

---
**GENERIC LOCAL-SEARCH BASED ON RE-OPTIMIZATION ROUTE EVALUATION OPERATORS**

* Detect the good combination of eval ops relative to the problem atrributes
* Build re-optimization data on subsequences with `INIT`, `FORW` and `BACK` ops
**while** some improving moves exist in neighborhood(N):
	**for** move($\mu_i$) in N:
		**for** route ($r^{\mu}_j$) produced by the move:
			Determine the *k* sub-sequences $[\sigma_1, ...,\sigma_k]$ that are concatenated to produce $r^{\mu}_j$
			**if** *k* == 2, then NEWCOST(r) = `EVAL2(`$\sigma_1, \sigma_2$`)`
			**elseif** *k* > 2, then NEWCOST(r) = `EVALN(`$\sigma_1, .... \sigma_k$`)`
		**end for**
		if ACCEPTCRITERIA($\mu_i$) the perform the move $\mu$ and update the re-optimization data on for each route $r^{\mu}_j$ using the `INIT`, `FORW` and `BACK` ops.
	**endfor**
**end while**

* <small>The neighbor solutions issued from moves are explored in random order, with acceptance criterion: It_{NI} = 2500 iterations without improvement, and a time limit of 5 hours.</small>
* <small>2-OPT*, and 2-OPT neighborhoods are used, as well as the inter-route and intra-route CROSS and I-CROSS neighborhoods, restricted to sub-sequences of length smaller than Lmax = 2 </small>

---

## Unified Hybrid Genetic Search (UHGS) for MAVRPs

> [!note] 
> UHGS = Classic GA framework + 4 main ingredients
> * Hybridization of GA with efficient LS (replace mutation with **Education**)
> 	* Crossovers allows us to explore a wide diversity of structurally different sols
> 	* LS drives the search towards high-quality local optimums.
> </br>
> * Solution representation without trip delimiters with optimal `Split()` procedure for delimiter computation
> </br>
> * Penalized infeasible solutions
> 	* Used and managed through two distinct sub-populations during the search.
> 	* Allow to transition towards higher-quality search space
> </br>
> * Diversity and cost objective for solution evaluation
> 	* Reduce the risk of premature population converage
> 	* Promote the discovery of new solutions

<small><b>Trip delimiter</b> is a point in the route where a vehicle returns to the depot or starts a new trip. It is used to divide the route into multiple trips, each of which starts and ends at the depot. The trip delimiter can be a physical location, such as a warehouse or a parking lot, or a virtual location, such as a time window or a maximum travel distance.</small>

![[Final Report - Project 3 - 20205226-20240109210428224.webp]]

1. UHGS iteratively selects two individuals in the merged sub-populations to serve as the input for **crossover** operator, output one offspring (1 subpopulation for feasible, and one for infeasible)
2. The outputed offspring then goes through **Split** procedure to compute trip delimiters
3. Next, it will be **educated** with Local Search and **repaired** with Probability $P_{rep}$ if it is infeasible.
4. Then it will be **merged** with suitable sub-population
5. Each sub-population is managed separately to trigger a **survivor selection** when reaching a maximum size.
6. **Diversification and decomposition** phases are regularly used to enhance the diversity and intensify the search around elite solution characteristics.
7. The loop is breaked when successiving It_max without imporving the best solutions, or when reaching time limit T_max.

![[Final Report - Project 3 - 20205226-20240128142624587.webp]]

### 1. Search Space
* Allow controlled exploration of infeasible solutions may **ehance** the performance of the search.
* So search space is defined as the combination of feasible and infeasible (obtained by relax the constraint)



### Solution representation and Unified Split
* MAVRPs involve two level of decisions relative to the assignment of customer services to some ASSIGN Attribute Resources (AARs), and the optimization of routes for each AAR.
![[Final Report - Project 3 - 20205226-20240110004140260.webp]]
* Accord to problem structure, solutions are presented as a set of **giant tours without explicit mention of visits to the depot** 
	* Each giant tour corresponds to a different combination of AAR.
	* Problem without ASSIGN attributes will only be represented as a **single grant tour** (Nếu chỉ tính riêng CVRP)

* To extract a full solution out of an individual and its giant tours, we need a *generic split procedure* based on route-evaluation components. 
	* For any giant tour $\tau = (\tau_1, ..., \tau_v)$ contains v customers, the splitting problem is similar to Shortest path problem on a directed acyclic auxiliary graph $G' = (V,A)$.
	* V includes v + 1 nodes notated from 0 to v.
	* Any arc a_ij $\in$ A with i < j represents the route originating from the depot, visiting customer $\sigma_{i+1}$ to $\sigma_j$ and returning. 
	* Cost of each arc is set to the cost of the associated route.

---
**GENERIC SPLIT**

![[Final Report - Project 3 - 20205226-20240110013810160.webp|579]]

---
* All arc costs can be computed by calling $O(v^2)$ times FORW and EVAL2
	* Setting a maximum value r on the number of customers in a route enable to reduce to $O(vr)$
* After this preprocessing, the shortest path is solved by m interations of Bellman-Ford algorithm

### 

### Unified crossover operator

![[Final Report - Project 3 - 20205226-20240110013952477.webp|1058]]