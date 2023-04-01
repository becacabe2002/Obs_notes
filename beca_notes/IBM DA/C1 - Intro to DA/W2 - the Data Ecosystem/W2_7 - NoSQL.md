==NoSQL allows data to be stored in a schema-less or free-form fashion.==

> [!abstract] Types of NoSQL DB
> * Key-value store
> * Document Based
> * Column Based
> * Graph Based

### Key-value Store DB
#nosql

> [!note] Data is stored as a collection of key - value pairs.
>*  **Key** - an attribute of the data that is unique.

* Both keys and values can be anything (even JSON doc)

> [!check] Use cases
> * Storing user session data and user preferences
> * Making real-time recommendations/targeted advertising
> * In-memory data caching

> [!fail] Not fit for
> * Querying the data on specific data value
> * Need relationship between data values
> * Need to have multiple unique keys

* Some examples:
![[Pasted image 20230326090154.png]]

### Document Based DB
#nosql 

> [!note] Store each record and its associated data within a single document.

* It is fexible for indexing, powerful for ad hoc querying and analytics over collections of documents.

> [!check] Use cases
> * eCommerce platforms
> * Medical record storage
> * CRM (Customer Relationship Management) platforms
> * Analytics platforms.

> [!fail] Not fit for
> * Running complex search queries
> * Multi-operation transactions

* Some examples:
![[Pasted image 20230326090915.png]]

### Column-based DB
#nosql 

> [!note] Store data in cells grouped as columns of data instead of rows.
> * A logical grouping of columns (columns are usually accessed together) called ***column family*** 

Ex: customer name + customer profile infor usually accessed together

* Since they store all cells corresponding to a column as a continuous disk entry
	**-> Accessing and searching the data are pretty fast.**

> [!check] Use cases
> * Systems that require heavy write requests
> * Storing time-series data
> * Weather data
> * IoT data

> [!failure] Not fit for
>  * Need to use complex queries
>  * Change querying patterns frequently

* Some examples:
![[Pasted image 20230326091800.png]]

### Graph-based DB
#nosql 

> [!note]
> * Use a graphical model to represent and store data
> * Circles are nodes, which contain data.
> * Arrows represent relationship between data.

> [!check] Use cases
> Useful for visualizing, analyzing and finding connection between different pieces of data.
> * Social networks
> * Real-time product recommendations
> * Network diagrams
> * Fraud detection
> * Access Management

> [!fail] Not fit for
> * Process high volumes of transactions (since it isn't optimized for large-volume analytics queries.)

* Examples:
![[Pasted image 20230326095233.png]]

### Advantages of NoSQL
✅ Ability to handle large volumes of structured, semi-structured and unstructured data.

✅ Ability to run as a distributed system scaled across multiple data centers

✅ An efficient and cost-effective scale-out architecture that provides additional **capacity** and **performance** when adding new nodes

✅ Simpler design, better control over availability, improved scalability 
-> Agile, flexible and support quick iterations.
