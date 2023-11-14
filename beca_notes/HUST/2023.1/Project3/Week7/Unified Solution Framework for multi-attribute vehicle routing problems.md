Unified Hybrid Genetic Search heuristic (UHGS):
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
> $G$ 

