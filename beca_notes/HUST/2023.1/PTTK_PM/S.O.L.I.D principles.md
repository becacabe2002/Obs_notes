> [!abstract] 
> * Single Responsibility
> * Open-closed
> * Liskov substitution
> * Interface segregation
> * Dependency inversion

-> Make designs easier to understand, maintain and extend

## 1. Single Responsibility
> a class should only solve one problem

```python
class Customer:
	# responsible for holding customer data
    def __init__(self, name, email):
        self.name = name
        self.email = email

class CustomerDB:
	# responsible for manage customer list
    def __init__(self):
        self.customers = []

    def add_customer(self, customer):
        self.customers.append(customer)

    def remove_customer(self, customer):
        self.customers.remove(customer)

    def list_customers(self):
        for customer in self.customers:
            print(f"Name: {customer.name}, Email: {customer.email}")
```

Ex: sample for violating SRP
```python
class Customer:
    def __init__(self, name, email):
        self.name = name
        self.email = email

    def add_customer(self, customer_list):
        customer_list.append(self)

    def remove_customer(self, customer_list):
        customer_list.remove(self)

    def list_customers(self, customer_list):
        for customer in customer_list:
            print(f"Name: {customer.name}, Email: {customer.email}")

    def send_email(self, message):
        print(f"Sending email to {self.email} with message: {message}")
```

### Relation to Coupling and Cohension
* This principle promote **high cohension**, since it ensures a class does not do too much or mix unrelated concerns.
* Ensuring a class is focused on a single task, avoiding unnecessary responsibilities that could lead to **increased coupling**

## 2. Open-closed
> Open to extension, which means the behavior of the class can be extended
> Closed for modification, which means that the source code is fixed and cannot be modified

```java
abstract class Shape {
    abstract void draw();
}

class Circle extends Shape {
    void draw() {
        System.out.println("Drawing a circle");
    }
}

class Rectangle extends Shape {
    void draw() {
        System.out.println("Drawing a rectangle");
    }
}

class ShapeDrawer {
    void drawShape(Shape shape) {
        shape.draw();
    }
}

public class Main {
    public static void main(String[] args) {
        ShapeDrawer drawer = new ShapeDrawer();
        drawer.drawShape(new Circle());  
        // Outputs: Drawing a circle
        drawer.drawShape(new Rectangle());  
        // Outputs: Drawing a rectangle
    }
}
```

* Shape is open for extending classes
* Closed for modifiation

### Relation with Coupling and Cohension
* **Reduce Coupling** by allowing the dependence on abstractions rather than concrete implementations.

Ex: instead of having a class that depends on specific database, you can have a class that depends on an abstract interface that defines the operations u need. Then different subclasses for using different databases are implemented, and passed to the the class as parameters. -> extend the class with new data sources without modifying its code.

```java
interface Database {
    void connect();
    void query(String query);
}

class MySQLDatabase implements Database {
    public void connect() {
        System.out.println("Connecting to MySQL database");
    }

    public void query(String query) {
        System.out.println("Executing query on MySQL database: " + query);
    }
}

class PostgreSQLDatabase implements Database {
    public void connect() {
        System.out.println("Connecting to PostgreSQL database");
    }

    public void query(String query) {
        System.out.println("Executing query on PostgreSQL database: " + query);
    }
}

class Application {
    private Database database;

    public Application(Database database) {
        this.database = database;
    }

    public void start() {
        database.connect();
    }

    public void executeQuery(String query) {
        database.query(query);
    }
}

public class Main {
    public static void main(String[] args) {
        Application app = new Application(new MySQLDatabase());
        app.start();  
        // Outputs: Connecting to MySQL database
        app.executeQuery("SELECT * FROM customers");  
        // Outputs: Executing query on MySQL database: 
        // SELECT * FROM customers

        app = new Application(new PostgreSQLDatabase());
        app.start();  
        // Outputs: Connecting to PostgreSQL database
        app.executeQuery("SELECT * FROM customers");  
        // Outputs: Executing query on PostgreSQL 
        // database: SELECT * FROM customers
    }
}
```

## 3. Liskov substitution
> Derived classes extend the base class without chaging behavior.

* Subclass should respect the expectation of its superclass, both in terms of inputs and outputs.

Ex: Violate LSP
```java
class Rectangle {
    protected int width, height;

    public void setWidth(int width) {
        this.width = width;
    }

    public void setHeight(int height) {
        this.height = height;
    }

    public int getArea() {
        return width * height;
    }
}

class Square extends Rectangle {
    @Override
    public void setWidth(int width) {
        super.setWidth(width);
        super.setHeight(width);
    }

    @Override
    public void setHeight(int height) {
        super.setWidth(height);
        super.setHeight(height);
    }
}

public class Main {
    public static void main(String[] args) {
        Rectangle rect = new Square();
        rect.setWidth(4);
        rect.setHeight(5);
        System.out.println(rect.getArea());  
        // Outputs: 25, but we expect 20
    }
}
```
* In here, the behaviors of Square have been changed from Rectangle, so if we use a Square obj in place of a Rectangle obj, hthe getArea() will not return the expected result.
-> Use composition, not inheritance

## 4. Interface segregation
> It's better to have many small interfaces than a few large ones

* Many customer-specific interfaces >> one large general-purpose interface
* Classes can implement multiple specific interface

Ex:
```java
interface Printer {
    void print();
}

interface Fax {
    void fax();
}

interface Scanner {
    void scan();
}

class MultiFunctionPrinter implements Printer, Fax, Scanner {
    public void print() {
        System.out.println("Printing document");
    }

    public void fax() {
        System.out.println("Sending fax");
    }

    public void scan() {
        System.out.println("Scanning document");
    }
}

class SimplePrinter implements Printer {
    public void print() {
        System.out.println("Printing document");
    }
}

public class Main {
    public static void main(String[] args) {
        MultiFunctionPrinter mfp = new MultiFunctionPrinter();
        mfp.print();
        mfp.fax();
        mfp.scan();

        SimplePrinter sp = new SimplePrinter();
        sp.print();
    }
}
```

### Relation with coupling and cohension
* Reduces coupling and increases cohesion, since it allows user to design smaller and more focused interfaces that only expose the relevant functionality for each client.
-> Avoid bloated and rigid interfaces that create **unwanted coupling**.

## 5. Dependency inversion
> High-level modules should not depend on low-level modules, but depend on abstractions.
> Details should depend on abstractions.

Ex:
```java
interface Database {
    void connect();
}

class MySQLDatabase implements Database {
    public void connect() {
        System.out.println("Connecting to MySQL database");
    }
}

class PostgreSQLDatabase implements Database {
    public void connect() {
        System.out.println("Connecting to PostgreSQL database");
    }
}

class Application {
    private Database database;

    public Application(Database database) {
        this.database = database;
    }

    public void start() {
        database.connect();
    }
}

public class Main {
    public static void main(String[] args) {
        Application app = new Application(new MySQLDatabase());
        app.start();  
        // Outputs: Connecting to MySQL database

        app = new Application(new PostgreSQLDatabase());
        app.start();  
        // Outputs: Connecting to PostgreSQL database
    }
}
```
* Application is a high-level module, and MySQLDatabase and PostgreSQLDatabase are low-level modules.
* high and low modules depend on abstract class Database

### Relation to Coupling and Cohension
* Reduce coupling and increase reusability because it allows dev to **decouple** classes from the details of their dependencies
-> make them more flexible and adaptable.

Ex: 
If user have a class that depends on a specific implementation of a service or a component -> **tight coupling**. 
Better approach is to have that class depend on abstract interface that defines the contract or the behavior of the service or component, and use dependency injection to provide the concrete implementation at runtime.
