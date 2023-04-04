
## Constructor-based Injection
> Dependencies are injected via the constructor of the class.

* This is the preferred method of injection in Spring
	* Enforce the immutability of the injected object
	* Make it easier to reason about the behavior of the class

```java
public class CustomerService {

  private final CustomerRepository customerRepository;

  @Autowired
  public CustomerService(CustomerRepository customerRepository) {
    this.customerRepository = customerRepository;
  }

  // other methods...
}
```

* *without `@Autowired`, Spring will not automatically wire the `CustomerRepository` bean to the `CustomerService` bean. Instead, it relies on the client code to manually create and pass in a `CustomerRepository` instance.*

## Setter-based injection
> Dependencies are injected via setter methods of the class.

```java
public class CustomerService{
	private CustomerRepository customerRepository;

	@Autowired
	public void setCustomerRepository(CustomerRepository customeRepository){
		this.customerRepository = customerRepository;
	}
}
```

* `CustomerService` class has a dependency on a `CustomerRepository`, which is injected via setter method.

 > [!check] Advantage
 > This allows **more flexibility**, as dependencies can be **changed at runtime**.

> [!fail] Disadvantage
> The state of the object can change unexpectedly
> -> Make code harder to reason about.

## Field-based injection
> Dependencies are injected via public or private fields of the class.

* The least preferred method of injection, since it ==violates encapsulation== and make it difficult to reason about the state of the object.
* It is only recommend for use in legacy code.

```java
public class CustomerService {

  @Autowired
  private CustomerRepository customerRepository;

  // other methods...
}
```


## Method-based injection
> Dependencies are injected via any method of the class that is annotated with `@Autowired`.

* Similar to setter-injection, but allows for greater flexibility in naming and number of arguments.

```java
public class CustomerService {

  private CustomerRepository customerRepository;

  @Autowired
  public void setCustomerRepository(CustomerRepository customerRepository) {
    this.customerRepository = customerRepository;
  }

  // other methods...
}
```

> [!warning]
> Have the same issue with setter injection.