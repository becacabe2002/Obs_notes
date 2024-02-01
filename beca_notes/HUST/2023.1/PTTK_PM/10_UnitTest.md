## Overview
* Software Quality Assurance (QA):
	* Static analysis (assessing but not executing code)
	* Proofs of correctness
	* Code reviews (let other review code)
	* Software process (placing structure on the development lifecycle)
	...

![[10_UnitTest-20231117143004919.webp]]
*(V Model - different test levels)*

1. Unit Testing: Does each unit (class, method, ..) function correctly?
	* Smallest programming units
	* Strategies: Blackbox and Whitebox
	* Tools: JUnit
	* Techniques

2. Integration Testing: how do components work together?
	* Strategies: Bottom-up, top-down testing

3. System testing: does it work within the overall system?

4. Acceptance testing: user requirements satisified or not?

## Differences between Unit - Integration - Functional Testing

> _**Unit Testing**_ - testing individual modules of an app in **isolation** (without any interaction with dependencies)

> _**Integration Testing**_ - check if different modules are working fine together as a group.

> _**Functional Testing**_ - Testing a slice of functionality in the system (can have interaction with dependencies) to ensure it doing as requirements.

👉 _To optimize the return on investment, the code base should have as many Unit tests as possible, fewer Integration tests and the least number of Functional tests. (since unit tests are easier to write and quicker to execute.)_

---

### Unit Testing

* Unit testing is done **before** Integration testing using `White box testing technique`.
* Unit testing does not only check for positive behavior/correct outputs, it also checks for failure with invalid input.
* Unit testing helps finding issues at the early stage of development, and solves it very easily -> Reduce the project's overal costs ⬇️ 💸.
* Bugs 🪲 found in a unit testcase is independent and do not impact the other testcases.
* Unit testing saves time and cost, and it is reusable ♻️ and easy to maintain.

Ex: JUnit, PHPUnit ...

---

### Intergration Testing
🚩 _Aim of integration testing is to check the functionality, reliability and performance of the system when integrated._

* There are three types of integration testing approaches:
	* _**Big bang Integration Approach**_
	* _**Top - Down Approach**_
	* _**Bottom - Up Approach**_

#### Big bang Integration Approach
* All the modules or units are integrated and tested as a whole at one time. 
_(Usually done when the entire system is ready for integration testing at a single point of time. And it is not system testing.)_


🟢 Everything integrated is tested at one time.

🔴 It is difficult to identify the failures.

#### Top - Down Approach

* First unit is tested individually by writing `test STUBS`. 
* Then the lower levels are integrated one by one until the last level is put together and tested.

🟢 Organic way of integrating as it is consistent with how things happen in the real env.

🔴 The major functionality is tested at the end.

#### Bottom - Up Approach

* Units/Modules are tested from bottom to top level, until all levels of units/modules are integrated and tested as one unit. 
* Stimulator programs called `DRIVERS` are used in this approach.

🟢 Easier to detect issues at the lower levels.

🔴 Higher-level issues can only be indentified at the end (when all units have been integrated.)

---

#### Compare Unit Testing & Integration Testing

|**Unit Testing**|**Integration Testing**|
|:---|:---|
|Tests single component of the whole system (isolated unit)|Tests the system components working together (units collaboration)|
|Faster to excute|Run slower|
|No externel dependency|Requires interation with external dependencies|
|Simple|Complex|
|Cheap maintenance|Expensive maintainance|
|Conducted by dev|Conducted by tester|
|Begins from module specification|Begins from the interface specification|
|Narrow scope|wider scope|
|Uncover the issues within the functionality of individual modules only.|Uncover the bugs arise when different modules interact with each other to form the overall system|

---

### Functional Testing
> **black box testing technique**, where the functionality of the app is tested to generate the desired output on providing certain input.

* The number of test cases depends on the requirements and scenarios.

```shell
<A test case>
- Test summary
- Prerequisites (if needed)
- Input steps
- Test data (if any)
- Expected output
- Notes (if any)
```

* Two forms of functional testing:
	* _**Requirement-based**_: test cases are created as per the requirement and tested accordingly
	* _**Business Scenario-based**_: testing is performed by keeping in mind all the scenarios from a business perspective.
	
🔴 _Redundancy in testing and the possibility of missing some logical errors._

