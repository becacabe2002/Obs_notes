### 1. What are the four major pillars of OOP ?

> [!check]- Answer
> There are four major pillars: **Abstraction**, **Encapsulation**, **Inheritance**, **Polymorphism**
> - ***Abstraction***: provides security by hiding the internal implementation of a class and only exposing the details necessary in the context.
> 
> - ***Encapsulation***: provides security to our application, consists of *private* variable declarations (data hiding) and accessor methods (getter and setter) to access the variables.
> 
> - ***Inheritance***: reduces code redundant by providing code reusability.
> 
> - ***Polymorphism***: provides flexibility by allowing to the declaration of methods with the same name for different purposes.

### 2. Is Java a pure Object - Oriented programming language ?

> [!check]- Answer
> Since several reasons, Java can't be a pure OOP language:
> * It doesn't provide multiple inheritance support for classes.
> * It doesn't provide support for **operator overloading**.
> * We use primitive vars `byte`, `short`, `char`, `int`, `float`, `long` ... which are not objects.

### 3. What are the tightly encapsulated and loosely encapsulated classes ?

> [!check]- Answer
> * A **tightly encapsulated** class doesn't allow public access to any internal data members, the outer can only access them by accessors (getter) and modify them by mutator (setter).
> 
> * A **loosely encapsulated** class doesn't block all direct access to its data members. (Not all modifiers are `private`.)

### 4. What are Coupling and Cohesion ?

> [!check]- Answer
> > ***Coupling*** - the degree of dependency between the components.
> 
> > **Cohesion** - create components with clear, well-defined responsibilities. 
> * If we maintain only one component for all functionalities, then it's known as **low cohesion**. (A class with multiple functions)
> ```java
> public class LowCohesionExample {
>    public void processOrder() {
>        // code for processing the order
>    }
>    
>    public void printInvoice() {
>        // code for printing the invoice
>    }
>    
>    public void sendEmailNotification() {
>        // code for sending email notification
>  }
>}
> ```
> *since the methods inside this class have different responsiblities which are not related, it has low cohesion.*
> * **High cohesion** is creating different components for different functionality.
> ```java
> public class HighCohesionExample{
> 	private List<String\> items;
> 	public void addItem(String item){
> 	// code block for method1
> 	}
> 	public void removeItem(String item){
> 	// code block for method2
> 	}
> 	public boolean containsItem(String item){
> 	// code block for method3
> 	}
> }
> ```
> *since all three methods work together to manage items list, this class has high cohesion*

[More OOP Interview Question](https://howtodoinjava.com/interview-questions/java-oop-interview-questions/)

