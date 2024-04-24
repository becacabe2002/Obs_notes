### 1. Choose the business process
* Describe the business process which the model builds on.

Ex: *sales situation in a retail store.*

### II. Declare the grain
* Exact description of what the dimensional model should be focusing on.

Ex: *an individual line item on a customer slip from a retail store.*

### III. Identify the dimensions
* Dimensions must be align with the defined grains.

* Dimensions are the foundation of the fact table, and is where the data for the fact table is collected.

* Typical dimensions are **nouns**: date, store, inventory

Ex: *date dimension contains year, month and weekday*.

### IV. Identify the facts
* Identify the numeric facts that will populate each fact table row.

Ex: *quantity, cost per unit*

## How to identify facts and dimensions?
> [!check] Using seven W's of Data Warehouse design
> **How?** -> Dimension
> **What?** -> Dimension
> **When?** -> Dimension
> **Where?** -> Dimension
> **Who?** -> Dimension
> **Why?** -> Dimension
> **How many/how much?** -> Fact

Ex: 

## Bridge Tables

* In many cases, a star schema, which has single fact table with direct relationships to dimensions is not the best solution.

* When a fact table should relate to a dimension that is at a **lower level of granularity**.

Ex: *a fact table at the patient grain (one record per patient) may need to relate to the diagnosis dimension (one record per diagnosis).* 
 *-> Need to adjust schema to accommodate when there are more than one diagnosis relate to a single fact record.*

> [!note] Bridge tables
> 

![[Steps of Dimensional Modeling-20240318155235862.webp]]

* 