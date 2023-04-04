In Spring, DI is configured using **XML configuration files**, **Java configuration classes**, or **annotations.**

### XML configuration
> Dependencies are defined in an XML file, then read by Spring IoC Container

```xml
<!-- Define a bean for a customer -->
<bean id="customer" class="com.example.Customer">
   <property name="name" value="John Doe"/>
   <property name="address" ref="address"/>
</bean>

<!-- Define a bean for the address -->
<bean id="address" class="com.example.Address">
   <property name="street" value="123 Main St"/>
   <property name="city" value="Anytown"/>
   <property name="state" value="CA"/>
   <property name="zip" value="12345"/>
</bean>

```

* **`customer`** bean depends on the **`address`** bean, which is defined seperately and then injected back using **`<property>`** element.

### Java Configuration class.
> Configuration is written in Java classes using annotations.
> Define the bean definitions.

```java
@Configuration
public class AppConfig {
   @Bean
   public Customer customer() {
      Customer customer = new Customer();
      customer.setName("John Doe");
      customer.setAddress(address());
      return customer;
   }
   
   @Bean
   public Address address() {
      Address address = new Address();
      address.setStreet("123 Main St");
      address.setCity("Anytown");
      address.setState("CA");
      address.setZip("12345");
      return address;
   }
}

```

* `customer` bean depends on the `address` bean, which is defined in seperate method `address()`. 
* `customer` bean is created and injected with the `address` bean  using the `address()` method.

> [!warning] 
> `customer` and `address` classes must be defined before being used in a configuration class.

### Annotations
> Several annotations can be used to configure DI in a more concise and declarative way.

```java
@Component
public class Customer {
   @Autowired
   private Address address;
   
   // Getter and Setter methods
}

@Component
public class Address {
   private String street;
   private String city;
   private String state;
   private String zip;
   
   // Getter and Setter methods
}
```

* `Customer` class has a dependency on the `Address` class, which is injected using  the `@Autowired` on the `address` field.
* `Adress` class has no dependencies and its defined as a regular Java class.