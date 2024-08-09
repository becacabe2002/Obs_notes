* **Point-In-Time (PIT) Table**:  special type of table that gather data from historical satellites around hub (from Data Vault). 
	* present a easy way to get data look like at a point in time.
	* design to improve performance of data vault with historical queries.

* **Bridge Table**: gathers associated hubs into one place.
	* Use to improve the performance of "long chain" by reducing the number of joins needed.
	* Link by usage

> [!example] 
> Raw vault with 3 hubs, 1 satellite per hub.
> -> Need 8 joins to get the information of satellite in one query.

