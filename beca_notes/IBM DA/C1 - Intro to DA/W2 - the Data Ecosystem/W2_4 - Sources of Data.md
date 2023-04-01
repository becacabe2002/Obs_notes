> [!abstract] Common data sources 
> * Relational DB
> * Flat files and XML Datasets
> * APIs and Web Services
> * Web Scraping
> * Data Streams
> * Feeds

* Organizations have **internal** applications for managing their operations:
	* Business activities
	* Customer transactions
	* Human resource activities
	* Workflows
whose data is stored in **relational DB** (SQL Server,  Oracle, MySQL, ...)
![[Pasted image 20230325145549.png]]

* Data stored can be use for analysis
> [!example] 
>* Data from retail transaction system --> analyze --> sales in different regions

**Outside** of the organization, there are datasets that are accessible to the public or private entities.
> [!example] 
>* Public dataset: government orgs releasing demographic and economic datasets
>* Private : Companies sell specific data (Point-of-Sale or Financial Data ...)

* This data can help businesses **define strategy**, **predict demand**, **make decision** related to distribution or marketing promotions...

![[Pasted image 20230325151056.png]]

* Data in flat files **maps to a single table**, unlike relation db.
* Spreadsheet files are similiar to flat file, except they have multiple worksheet, which allows them to maps to different tables.

### APIs and Web Services
* Many data providers and websites provide APIs and Web Services so that multiple users can interact with and obtain data from them.
> [!note]- Review about APIs
> ![[Web7. APIs, REST and REST APIs#APIs basics]]

* APIs and Web Services listen to requests (web request from users, network requests from application).
	* Then data is sent back in form of plain text, XML, HTML or medi files.

### Web Scrapping
* Extract relevant data (text, img, vid, product items ...) from unstructured sources, download them based on defined params.

> [!hint] Use cases of web scrapping
> * Providing price comparisons with collected product details from other retailers.
> * Generating sales leads by analysizing public data sources.
> * Extracting data from posts and authors on a wide range of forums, communities or platforms.
> * Collecting data for training and testing ML models

### Data Streams and Feeds
> Data streams are another widely used source for aggregating constant streams of data flowing from sources such as instruments, IoT devices and applications, GPS data from cars, computer programs, websites, and social media posts

> [!hint] Use cases of Data Streams
> * Stock and market tickers for finanical trading
> * Retail transaction streams for predicting demand and supply chain management
> * Surveillance and video feeds for threat detection.
> * Social media feeds for sentiment analysis ...

> [!note] Technologies used to process data streams
> ![[Pasted image 20230325172405.png]]

> [!info] Really Simple Syndication - RSS feeds
> Data source which used for capturing updated data from online forums and new sites where data is refreshed on an ongoing basis.