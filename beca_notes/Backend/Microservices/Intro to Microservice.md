> [!info] Microservice
> Architectural approach that involves dividing large application into smaller, functional units capable of functioning and communicating independently.


```start-multi-column
ID: ID_19o6
Number of Columns: 2
Largest Column: standard
Border: off
```


> [!failure] Limitations of Monolithic Architecture
> * Large container holding all software components of an application.
> 	* Inflexible
> 	* Unreliable
> 	* Develop slowly


--- column-end ---

> [!check] Advantages of Microservices
> * Each unit is independently deployable, but can communicate with each other when necessary.
> 	* Scalability
> 	* Simplicity
> 	* Flexibility
>
>-> For building much more sophisticated applications.

=== end-multi-column
## How does Microservices architecture work?

```start-multi-column
ID: ID_z8ko
Number of Columns: 2
Largest Column: standard
Border: off
```


![[Pasted image 20230418142540.png]]

--- column-end ---

* Each microservices addresses an application's particular aspect and function.
* Requests from clients come to API gateway.
* One or more microservices are commissioned through the API gateway to perform the requested task.

=== end-multi-column

