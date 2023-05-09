> [!info] Uniform Resource Identifier - URI
> It is a string of chars used to identify a resource on the internet either by **location** or by **name**, or both.

> [!info] Uniform Resource Locator - URL
> It is a string of chars but it refers to just the **address**. It is the most used way to locate resources on the web

> [!info] Uniform Resource Name - URN
> It is a string of chars but it refers to just the **name**.

* URIs can be URN or URL.

> [!warning]
> Since two or more resource can have the same name, it is ineffective to use URNs
> ***--> Most of the time, we use URLs to identify resources.***

## URLs
* An URL consists of two required components:
	* ***The protocol***
	
	* ***The Domain***
	
	* Other optional components:
		* **The Path** - specifies the exact location of the web page, file or any resource that the user wants access to.
		
		* **The Port Number** - specifies the type of service that is requested by the client since servers often deliver multiple services.
		
		* Others

> [!example]  
> http ://www.mywebsite.com:80/resgister.php
> * The protocol : http
> * The domain name: www.mywebsite.com
> * Port number: 80
> * Path: register.php

> [!info] Domain name
> Identity of one or more IP address, provided by Domain registras.
> More about [domain name](https://www.javatpoint.com/what-is-domain)

### Query Strings and Fragments
> [!info] Query String
> Specify the @params of the data that is being queried from a website's database.
> * Each query str is made up of a @param and a val (<param_name>=val)
> 	* In case of multiple @param, they are seperated using the `&` sign.
> * It was preceded by a `?`, which tell the browser that a specific query is being performed.
> ```
> https://www.example.co.uk:443/blog/article/search?docid=720&hl=en
> ```

* The @param can be a num, str, encrypted val or any other form of data on the db.

> [!info] Fragment
> * Usually appers at the end, end begin with a `#`
> * Indicates a specific location within a page
> 	* ex: name or id attribute for an HTML element.
> ```
> https://www.example.co.uk:443/blog/article/search?docid=720&hl=en#dayone
> ```
