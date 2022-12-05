**Consist of two type:**
- **Access Modifiers**
- **Non-Access Modifiers**

## Access Modifiers

>[!info] Access Modifiers
>Are keywords in Object-Oriented languages that **set the accessibility** of classes, methods, and other members.

![[java_modifiers.png]]

### For classes

> [!note] public
>  The class is accessible by **any other class**.

> [!nnote] default
> The class is only accessible by **classes in the same package**.

* This is **used** when you **don't specify a modifier**.

### For attributes, methods and constructors

> [!note] public
> The code is accessible for **all classes**.

> [!note] private

- The code is only accessible **within the declared class**.
- Code **inside subclasses cannot access** the variable or method, nor can code from any external class.

```java
public class Justme{
	private String ny = "Blank";
}
```

#### Accessing private Fields via Accessor Methods

- The private variables can be accessed by using *accessor methods* (getter and setter)

```java
public class Tulanh{
	private String food = "Chocolate";
	public String Antrom(){// this is getter method
		return this.food;
}
	public void Thaydoi(String doan){// this is setter method
		this.food = doan;
}
}
```

#### Private Constructors

- If a constructor is assigned the private Java access modifier → cannot be called from anywhere outside the class.

```java
public class Clock {

    private long time = 0;

    private Clock(long time) {
        this.time = time;
    }

    public Clock(long time, long timeOffset) {
        this(time);
        this.time += timeOffset;
    }

    public static Clock newClock() {
        return new Clock(System.currentTimeMillis());// call the private constructor
    }

}
```

> [!caution]
> - `this.` keyword is used to refer to the current object, i.e.through which the method is called.
> - `this()` is used to call one constructor form the other of the same class.
> - `this` can't be used in static code block

> [!note] default
> The code is only accessible in the same package.

- This is used when u don't specify a modifier.
- Subclasses cannot access methods and member variables in the superclass, unless the subclass and superclass are located in the same package.

> [!note] protected
 The code is accessible in the same **package and subclasses**.

* The protected access modifier let the **subclass access protected methods and variables**, even they **aren't located in the same package**.

### Interface Access Modifiers

- Be meant to specify fields and methods that are publicly available in classes that implement the  interfaces.

⇒ can't use the private, protected and default modifiers  ⇒ always public 

### Access Modifiers and Inheritance

- The subclass 's method methods can't have less accessible access modifiers assigned to them than they had in the superclass.

Ex: if a method in the superclass is protected, in case the subclass **[overrides](https://docs.oracle.com/javase/tutorial/java/IandI/override.html)** the methods, it must be either protected or public in the subclass.

- But it is allowed to expand accessibility of an override method.

## Non-Access Modifiers

### For classes

> [!note] final
> The class **cannot be inherited by other classes**

> [!note] abstract
> The class **can't be used to create objects**

> [!caution] To access an abstract class, it must be inherited from another class.

### For attributes and methods

 > [!note] final
> Attributes and methods **can't be overridden/modified**

- Useful for **storing unchanging values**.

```java
public class Car {
	final int soxe = 10; 
}
public class Main{
	public static void main(String[] args){
		Car xe = new Car();
		xe = 11;// Error: the final field Car.soxe cannot be assigned 
}
}
```

> [!note] static
> Attributes and methods **belong to the class**, rather than an object.

^28f918

```java
public class Main {
  // Static method
  static void myStaticMethod() {
    System.out.println("Static methods can be called without creating objects");
  }
	public static void main(String[] args){
		myStaticMethod();// don't need to create an object
}
```

> [!note] abstract
> Can only be used in an **abstract class**, and can only be used on methods.

- An abstract method **doesn't have a body**.
- The **body is provided by the subclass**.

File: First.java

```java
abstract class First{
	public int so = 10;
	public String kieu = "Type";
	public abstract void Cach();
public class Second extends First{// inherite from superclass
	public int so = 20;
	public void Cach(){
		System.out.println("In chu ra");
}
}
}
```

```java
public class Main{
	Second vat = new Second(){
	System.out.println(vat.so+ "\n"); // print 20
	System.out.println(vat.kieu + "\n");// print Type
	vat.Cach();// print In chu ra
}
}
```

> [!note] transient
> Attributes and methods are skipped when serializing the object containing them

👉 Need to understand what is **Serialization**: is the process of converting an object into a byte stream, and **deserialization** is the opposite of it. 

**Used in some scenarios:**

1. We can use it for derived fields.
2. It is useful for fields that do not represent the sate of the object.
3. We use it for any non-serializable references

[The transient Keyword in Java | Baeldung](https://www.baeldung.com/java-transient-keyword)

> [!note] synchronized
> Methods can only be access by one thread at a time

[Synchronized in Java - GeeksforGeeks](https://www.geeksforgeeks.org/synchronized-in-java/)

> [!note] volatile
> The value of an attributes is not cached thread-locally, and is always read from the "main memory"

[volatile keyword in Java - GeeksforGeeks](https://www.geeksforgeeks.org/volatile-keyword-in-java/)

[[3. Abstraction & Encapsulation]]