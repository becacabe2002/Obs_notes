### Some Clound-Based Relational DBs (DBs-as-a-Service)
![[Pasted image 20230325220231.png]]

### Advantages of Relational DBs
* Create **meaningful information** by joining tables.
* **Flexibility** to make changes while the database is in use
* **Minimize data redundancy** by allowing relationships to be defined between tables
* Offer export and import options that provide **ease of backup and disaster recovery**
* Are **ACID compliant**, ensuring accuracy and reliability in db transactions.

> [!note] ACID
> A set of properties that guarantee **reliability** and **consistency** in db transactions implemented by RDBMS
> 1.  ***Atomicity***: This refers to the property of a transaction where all the steps in a transaction are treated as a single unit of work. If any step in the transaction fails, the entire transaction is rolled back, ensuring that the database remains in a consistent state.
> 2.  ***Consistency***: This refers to the property of a transaction where the database is left in a consistent state after the transaction is complete. This means that any constraints or rules defined by the database schema are enforced during the transaction. 
> 3.  ***Isolation***: This refers to the property of a transaction where it appears to run in isolation from other transactions, even if multiple transactions are executing concurrently. This ensures that each transaction sees a consistent view of the database, even if other transactions are modifying the same data. 
> 4.  ***Durability***: This refers to the property of a transaction where once it is committed, it is guaranteed to be permanently stored in the database, even in the face of system failures or errors.

![[Pasted image 20230325224610.png]]

> [!caution] It is important for ensuring that db transactions are executed reliably and consistently, even in the face of system failures or errors.

### Use cases of RDBMS
* R-DB are well suited for **Online Transaction Processing** application:
	* Support transaction-oriented tasks that can run at high rates
	* Accommodate large number of users
	* Support frequent queries and fast resonse times

* **Data Warehouses** : since it can be optimized for online analytical processing.
* **IoT Solutions**: since it provides the speed and ability to collect and process data from edge devices.

> [!fail] Limitations
>  * Doesn't work well with semi-structured and unstructured data.
>  * Migratio between two RDBMS's is possible only when the source and des tables have the same schemas and data types.
>  * If input value is greater than the defined length of data field, it will cause loss of information.

