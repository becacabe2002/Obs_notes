## APIs basics
> [!info] Application Programming Interface - API
> A way to let software components to talk to each other.
> ![[Pasted image 20221225000248.png]]

* The way APIs implemented are not important.

> [!example] 
> Obj A consists of two methods and two attributes
> * Name
> * Preferred Language
> * *sayHi*
> * *askme*(@question)
> 
> To communicate or use the functionalities of obj a, user have to do that through its API, which are its methods and attributes in this case.

> [!note] 
> API can be anything, in any form as long as it has a way to **communicate with the software components**.

> [!question] How do APIs relate to Web Services ?
> Web Services are just  **APIs**

* REST API =  REST web service

> [!question] What is a REST API/REST Web service?
> A REST API is an API that follows the rules of REST specification.

## REST
> [!question] How does HTTP relate to REST?
> * HTTP is an application layer protocol for sending and receiving messages over a network.
> 	* User can use **GET** method for all sorts of interactions.
> * REST is a specification that dictates how distributed systems on the we should communicate.
> 
> ***=> REST is a way to implement and use the HTTP protocol***

> [!question] How does the WEB relate to REST
> * REST is the underlying architecture of the WEB.

> [!info] Representational State Transfer - REST
> An architectural style that defines a set of constraints to be used for creating web services.
> * ***REST Technology*** - is a more robust Simple Object Access Protocol (SOAP) technology, used to fetch or give some information from a web service.
> 	* Use less bandwith
> 	* Simple
> 	* Flexible.

> [!quote] 
> *Throughout the HTTP standardization process, I was called on to defend the design choices of the Web. That is an extremely difficult thing to do within a process that accepts proposals from anyone on a topic that was rapidly becoming the center of an entire industry. I had comments from well over 500 developers, many of whom were distinguished engineers with decades of experience, and I had to explain everything from the most abstract notions of Web interaction to the finest details of HTTP syntax. That process honed my model down to a core set of principles, properties, and constraints that are now called REST.*
> \- ***Roy Fielding***

* To make an API to be RESTful, it must be able to answer questions:
	1. How can the client tell the service provider which operation it wants to perform? (==Method information==) 
	2. How can the client tell the service provider what data to operate on? (==Scoping information==)

### First rule - Method information
> [!tip] The method information should be expressed in the HTTP verb.

> [!example] 
> ![[Pasted image 20221225103856.png]]

### Second rule - Scoping information
>[!tip] Scoping information should go in the URI

> [!example] 
> ![[Pasted image 20221225104309.png]]

## How REST APIs works ?

> [!note] working mechanism of REST API
> * Use HTTP method **suitably** 
> 	* GET for getting data
> 	* POST for creating
> 
> * **Scoping information** (and other data) goes in the **parameters part of the URI**
> 
> * Use **common data formats** (ex:JSON)
> 
> * Communication is **stateless**

![[Pasted image 20221225104557.png]]