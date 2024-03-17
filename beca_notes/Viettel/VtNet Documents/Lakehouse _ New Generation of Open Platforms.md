
* Lakehouse Architectural pattern:
	* Based on open direct-access data formats (Apache Parquet, ORC)
	* Support for machine learning and DS
	* Higher performance

> [!note] 1st and 2nd Generations of Data Architecture
> * **First Generation**: 
> 	* Collecting data from operational databases into centralized warehouses.
> 	* Data is written with schema-on-write, which is optimized for downstream decision support and BI.
> 	* Data could be used for decision support and BI.
> * **Second Generation:**
> 	* Raw data is offloaded into *datalakes*, which is low-cost open file format storage systems with file API
> 	* Schema-on-read was used
> 	* Small subset of data in would be ETLed to a downstream data warehouse, which will later be used as in first generation.
> 	* Directly access is possible, support for machine learning systems.

-> Second Gen is complex, easy to delay and fail when ETL from datalake to warehouses.

### 4 majors problems with current architectures
* **Reliability** (tính tin cậy):
	* ETL data between two systems is necessary for continuos engineering.
	* It is risky because data lake and warehouse have different engines.
* **Data staleness**:
	* Data in the warehouse is stale compared to that of the data lake.
* **Limited support for advanced analytics**:
	* None of leading machine learning systems work well on top of warehouses.
		* These systems need to process large datasets using complex non-SQL code 
		-> *Inefficient* 
	* There is no way to directly access the internal warehouse proprietary formats.
* **Total cost of ownership**:
	* Double cost for storage used for copied data in warehouse.

> [!tip]  Targets of Lakehouse Architecture
> * **Reliable data management on data lakes**:
> 	* Store raw data while still supporting ETL/ELT processes curating this data.
> 	* Need to have management features: transactions, rollbacks or cloning.
> 	* Easy and efficiency to query the raw data tables.
> * **Support for machine learning and data science**:
> 	* 
> * **SQL performance**:
> 	* Provide top-notch query performance (like SQL) over massive Parquet/ORC datasets.

> [!check] 
> Lakehouse platform was built based on:
> * _**Delta Lake**_
> * _**Delta Engine**_
> * _**Databricks ML Runtime**_

![[Lakehouse _ New Generation of Open Platforms-20240311233818537.webp]]


