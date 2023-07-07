> [!note] Go >> Java ?
> * Go is compiled language, whereas Java requires JVM distribution. (more enviroment dependency)
> * Go produces smaller build artifacts -> faster startup time
> * Go developer doesn't need to worry about style  or configuring intergrated development env (which is time-consuming)
> * Go is used for tooling (Docker, Kubernetes ...)
> * Go is more effective to build concurrencies (luồng)

![[Pasted image 20230703205623.png]]

* Go is strongly-typed (like Java) -> eliminate data types errors

* Go has a built-in garbage collection. -> avoid memory leaks

* Go is built to last (is a advantage, since replacing old code always generate monetary and velocity cost)

* Go limitations make team members to write things as simply as possible.

* Go facilitates concurrency through ***Goroutines*** (simplified version of threading)

* Go have a special type of variable called ***a channel*** that helps share data between Goroutines.

* Go dependencies management is being improved. (***Go modules***)

## More Comparisons with Java
### The differences
* **Interface:** 
	* Interfaces in Go is kept to be as small as possible.
	* If a type implements all methods of an interface, it automatically implements that interface (no `implements` declaration is needed)
		* A third-party library's type can be imposed an interface by user (ex: for testing)

* **Pointer:**
	* Unlike C, Go disallow any pointer arithmetic and backed by the garbage collector -> safe
	* When a var is passed to a func, a copy is maded (the original val of that var remains the same)
	* User must tell the compiler when to pass a var by reference.

* **Public & Private:**
	* The visibility of funcs,  types or fields is defined at **package level**.
	* There are no keyword such as `public` or `private`
		* An identifier is public if its name **starts with an uppercase letter** (can be called by other packages)
		* An identifier is private if its name **starts with an lowercase letter** (can only be called by within the package)

### New features
* **Native Concurrency**

* **Self-contained binaries** :
	* They dont need any dynamic libs pre-installed on the system.
		* Ex: the code can be compiled on machine A and run on machine B without worrying about missing runtime or libs.

* **Native cross-compilation without a target toolchain** 

* **Functions are first-class citizens**
	* Funcs in Go can be used as vars and passed to or returned from funcs.

### Missing features
* Inheritance
* Method overloading
* Exceptions