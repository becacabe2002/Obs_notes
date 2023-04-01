### Data Warehouse
![[Pasted image 20230326102955.png]]

> [!info] Data Warehouse
> A multi-purpose storage for different use cases.
> * When data comes into warehouse, it has already been modeled and structured for a specific purpose (ready for analysis)

* Data Warehouse is **necessary for an organization** since there is a massive amount of data coming from the operational systems which needs to be ready for reporting and analysis.

* Data warehouse serves as a **single source of truth** 
	* Storing current and historical data that has been cleaned, conformed (làm cho đúng) and categorized.

* A data warehouse enables both operational and performance analytics.

### Data Marts
![[Pasted image 20230326153834.png]]

> [!info] Data Marts
> A sub-section of the data warehouse, built specifically for a particular business function, purpose or a community of users.

==Provide stakeholders the data that most relevant to them, when they need it.==

Ex: The sales or finance teams accessing data for their quarterly reporting and projections.

* Data mart offers analytical capabilities for a restricted area of data warehouse
**➡️ Isolated security and isolated performance.**

### Data Lake

![[Pasted image 20230326154101.png]]

> [!info] Data Lake 
> A storage repo for storing large amounts of structured, semi-structured and unstructured data, which stay in their native format, tagged and classified with metadata.

* Data warehouse store processed data for a specific need >< Data Lake store raw data, only named with a unique identifier and tagged with metatags for further use.

> [!check] Use cases for Data Lake
> * Generating, or having access to, large volumes of data on an ongoing basis but dont want to be restricted to **specific or pre-defined use cases**.
> 	* Data from data lake is selected and organized based on the use case you need it for.

* Data lake could retain all source data, without any exclusions.
	* Data could include all types of data sources and types.

> [!hint] Data Lake could be used as a Staging area of a data warehouse
> The most important role of a data lake is in **predictive** and **advanced analytics**.

### Extract, Tranform and Load Process
![[Pasted image 20230326154556.png]]

#### 1. Extraction

> [!note] Batch processing
> Large chunks of data moved from source to dest at scheduled intervals
> ![[Pasted image 20230326161714.png]]

> [!note] Stream processing
> Data pulled in real-time from source, transformed in transit and loaded into data repository
> ![[Pasted image 20230326161824.png]]

#### 2. Transform
> execution of rules and functions that converts raw data into data that can be used for analysis.

* Standardizing date formats and units of measurement
* Removing duplicate data
* Filtering out data that is not required
* Enriching data
* Establishing key relationships across tables
* Applying business rules and data validations

#### 3. Load
> Transportation of processed data into a data repo

> [!note] Loading methods
> * ***Initial Loading*** - populating all of the data in the repo
> * ***Incremental Loading*** - applying updates and modifications periodically
> * ***Full Refresh*** - erasing a data table and reloading fresh data

> [!note] Load verification
> * Data checks for mising or null values
> * Server performance
> * Monitoring load failures.
> 	* Ensure the right recovery mechanisms are in place.

*With the emergence of streaming ETL tools, they are increasingly being used for real-time streaming data as well.*

### Data Pipeline

> [!info] Data Pipeline
> The journey of moving data from sys to another, including the ETL process.

* Can be used for both batch and streaming data.

* Support both long-running batch queries and smaller interactive queries

* Normally load data into data lake, but can also load data into a variety of tagert dests (including other apps or visualization tools)