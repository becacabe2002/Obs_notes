> [!info]
> Rich VRP extends the academic variants of the VRP in the different decision levels by considering at least **four strategic and tatical aspects** in the distribution system and including at least **six different daily restrictions** related to the physical characteristics.

* **Scenario Charateristics (SCs)** and **Problem Physical charateristics (PPCs)** will determine that whether problem is classified as Rich or not.

* Taxonomy is organized with three levels, depend on involved decision types:
	* **strategic (chiến lược) level** and **tatical (chiến thuật) level**: associated with SCs
		* Correspond to the transportation strategy, which decribes the distribution system and designs its main components
		* strategic level: decisions related to the locations and the number of depots used
		* tatical level: order type, visit frequencies and given time horizon would be considered

	* **operational level**: associated with PPCs
		* Describe the distribution plan including vehicle and driver schedules
		* short-term and daily decisions are handled considering each vehicle route.
		* using the designed distribution system from strategic and tatical level
		* Decisions based on the characteristics of vehicles and on specificed constraints (customer, vehicle, driver, road)

![[Rich VRP Taxonomy-20231101024359643.webp|893]]

### Scenario Charateristics
#### Input data
* Deterministic: problem parameters certainly known
* Stochastic: problem parameters are uncertain and are represented as probability parameters
* Dynamic: allows receiving additional information and changes in some problems paramaters.

#### Decision Management Components
Integrating decisions of different functions: purchasing,  inventory control, outsourcing, locating depots, production planning and distribution management

* Related extensions:
	* Inventory-routing:
		* supplier defines the quantities to deliver using inventory levels at consumers to avoid **stock shortages**
	* Location-routing:
		* determine the location of depots serving customers and the routes rooted at those depots simultaneously.
	* Production and distribution planning:
		* determine the quantity produced for each item
		* distribution plans and the quantities of each item delivered to each customer
	* Vehicle,driver scheduling:
		* 

#### Number of depots
* Single:
* Multiple: more realistic (vehicles have different starting and final locations.)
	* The depots may have different charateristics (number, locations, capacities ...)

#### Operation type
* Pickup **or** delivery: goods are either delivered or picked-up
* Pickup **and** delivery: goods are loaded and unload
* Backhauls: goods are loaded on board when the delivery part of route is completed.
	* Transport goods from the depot to linehaul customers
	* Transport goods from backhaul customers back to the depot
* Dial-a-ride

#### Load splitting
* Allow splitting or not:
	* When several products have to be delivered to a customer. 

#### Planning period
* Single period
* Multiple period: all input data is avaiable at the beginning.
	* At each period, one hase to decide which customers are served in this period and which orders are postponed to the next periods.

#### Multiple use of vehicles
* Single trip
* Multi-trip: same vehicle may perform several trip

### Problem Physical Charateristics
#### Vehicles
* Type:
	* Homogeneous (đồng nhất)
	* Heterogeneous (bất đồng nhất)
* Number: fixed - unlimited
* Capacity Constraints
* Driver Regulations
#### Time constraints
* Restriction on customer
* Restriction on road access
* Restriction on depot
* Service time
* Waiting time
#### Time window structure
* Single time window
* Multiple time window

#### Incompatibility constraints
#### Specific constraints
* Outsourcing decisions
* Environmental protection
* **Priorization of customers**
* Cross docking strategy
* Open routes:
* Accessibility constraints
* ...
#### Objective function
* Minimizing:
	* Total traveled distance
	* Total time
	* Total tour cost
	* Fleet size
* Maximizing:
	* Service quality
	* Colleted profit

> [!tip] "Rich Combinations contain more PPCs than SCs"

==***-> Need unified approximate methods to provide good solutions (Generic heuristics)***==
