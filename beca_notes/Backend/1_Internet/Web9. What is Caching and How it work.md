## What is Caching?
* Caching is one way to solve performance degradation issues.

>[!info] Caching Layer
>* Any location that could be used to quickly retrieve results.
>![[Pasted image 20221226211213.png]]

* Getting results from Caching Layer can be **much fastter** than getting them from the main source.

> [!note] 
> The most popular way to implement caching is using In-memory Data Store 
> > [!example] RAM, which is really fast in Input/Output

> [!info] Caching
> Using the computer's main memory to **efficiently** manage **frequently used data**. 

> [!check] Caching benefits
> Since caching helps increasing the speed of **data retrieval** and **data manipulation**, it improves apps in:
> * Performance 
> * Scalability
> * Availability

## Caching Usecases
* In **Databases** - to speed up read/write  operation & for scaling purposes

* In **Web Apps** 
	* In Server side: 
		* Resource Intensive computations
		* Frequent Queries
	* In Client side:
		* Static Resource
		* Credentials

* In **OS** (CPU) - slove the imbalance between processing and I/O

* In **Networking** - for DNS, CDNs (Content Delivery Network)

## How Caching works
> [!note] Implementation of Caching in Web Apps
> * It could be implement throughout layer, from end to end.
> ![[Pasted image 20221226213847.png]]
> 
> * **Client**:
> 	* CacheAPI
> 	* IndexedAPI
> 	* WebStorage API
> 	* HTTP cache headers - cache requests and responses
> * **DNS** :
> 	* DNS Resolvers
> 	* Different DNS Servers
> * **Proxies** :
> 	* Centralized Data Stores
> 	* CNDs
> 	* Reverse Proxies
> * **App Server** :
> 	* Key-value Stores
> 	* Local Caches
> * **Database** :
> 	* Adjacent Data-Access Layers

> [!warning] Over time, the demanding for a larger cache becomes inevitable.
> -> Need a method to replace or make room for other items in cache.

## Cache size & Populating the Cache

> [!tip] The Cache size will be foundation for:
> * Determines the **type of caching** to be used: local, external ...
> * Determines the **right technology** to be used.

### Populating Cache Techniques
> [!info] Upfront Population
> ![[Pasted image 20221226215724.png]]
> Populate the cache with all needed values when the system keeping the cache is starting up.
> * Require to know what data to populate the cache with (which not always know)

> [!info] Lazy Population
> ![[Pasted image 20221226215737.png]]
>Populate the cache the first time a certain piece of data is needed.
>* First, check the cache to see if the data is there or not.
>* If the data already exists in the cache, return to the client.
>* Else, it is read from the remote system and inserted into the cache.

|Technique|<b>Upfront</b>|<b>Lazy</b>|
|---|---|---|
|<i>Advantage</i>|No one-off cache read delays|Only caches data that is actually read.</br> Has no upfront cache build delay.|
|<i>Disadvantage</i>|The initial build of the cache may take long time </br>Risky caching data that is never read|Not have any speedup from the first cache read </br><b><i> -> Inconsistent user experience.</i></b>|

***👉More about Caching Techniques: [Caching Techniques (jenkov.com)](https://jenkov.com/tutorials/software-architecture/caching-techniques.html#:~:text=Caching%201%20Populating%20the%20Cache%20The%20first%20challenge,in%20Server%20Clusters%20...%205%20Cache%20Products%20)***

## Cache Management 
#### Eviction (Truc xuat) Policy
> [!info] Cache eviction policies
> Specific algorithms for managing data in a cache, consider what data to keep or what to remove over time.

 * Most common policies:
	* ***Least Recently Used*** - LRU
		* Replace the item that is not requested for the longest time with the new one.
	
	* ***Most Recently Used*** - MRU
		* Replace the item used most recently.
	
	* ***Least Frequently Used*** - LFU
		* Remove the item in the cache used the least since its entry.

👉 ***[Cache Eviction Policies | Codecademy](https://www.codecademy.com/article/cache-eviction-policies)***

#### Synchronization
> [!note] Synchronization
> Keep data in Cache and data in Remote System the same.

* Some techniques:
	* ***Write-through Caching*** - cache allows both reading and writing. What written to cache is also written to the remote system.
	
	* ***Time Based Expiry*** - let the data in the cache expire and be removed after a certain time. When it is needed again, a fresh version of data is read from the remote system and inserted into the cache.
	
	* **Active Expiry** - client can send a message to the computer keeping the cache whenever the remote system is updated, instructing it to expire the data that was updated.


## Caching Technologies and Security

* Caching could be implemented in different ways, different levels and according to different rules.

> [!note] Caching Technologies
> - ***Key-value***
> - ***Fully-Indexed***

> [!warning] Threat to System using Caching.
> - ***Stale Data***
> - ***Weak Encryption***

