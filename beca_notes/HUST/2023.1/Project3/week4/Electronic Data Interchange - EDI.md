source:
* [How EDI in Transportation and Logistics Works | Cleo](https://www.cleo.com/blog/knowledge-base-edi-logistics)
* [What is EDI (Electronic Data Interchange)? | EDI Basics](https://www.edibasics.co.uk/what-is-edi/)

## EDI Definitions
> [!info] EDI
> ***Computer-to-computer*** exchange of ***business documents*** in a ***standard electronic format*** between ***business partners***

### Computer-to-computer
* EDI replace postal mail, fax, and email. (while email is an electronic approach, but it still need to be handled by human).
	* human-involving operations 
		-> slow down the processing of the documents
		-> introduce errors.
	* Alternative flow, EDI documents can flow directly into the appropiate software on the receiver's computer. (Order Management System)
		-> Process can start immediately.
	![[Pasted image 20231012215804.png]]
	*with human interception*
	![[Pasted image 20231012215829.png]]
	*without human interception*

### Business documents
* These are any of the documents that are typically exchange between businesses.
	* Ex: purchase orders, invoice (hóa đơn), bill of lading, customs documents ...

### Standard Format
* Since EDI document will be proccessed by computer -> need a standard format.

* It will have to describe what each piece of info is and its format (int, string, date ...)

* There are some EDI standards in use: ANSI, EDIFACT, TRADACOMS, XML.
	* Each standard will have several versions: ANSI 5010 or EDIFACT version D12, Release A

* When two businesses decide exchange EDI documents, they will have to set a agreement on what EDI standard to use and what version of it.
	* They can use **EDI translator**(in-house software or EDI service provider) to translate the EDI format so the data can be used by their internal app -> fluent process.

### Business partners
* It can be two different companies (business partners or trading partners)

> [!example] Example of how EDI can be used
> Imagine you run a small toy store, and you need to restock your shelves. You have a supplier that makes toys. Instead of calling them on the phone or sending faxes to place orders, you both use EDI.
> 1. You create a digital order on your computer, specifying the types and quantities of toys you need.    
> 2. You send this order through the EDI system to your toy supplier.  
> 3. The EDI system at your supplier's end receives the order and processes it, automatically updating their inventory and order management.  
> 4. Your supplier then ships the toys to your store, and they use the EDI system to send you an electronic invoice with the total cost.
> 5. Your EDI system receives the invoice and updates your financial records.
> 
> This whole process happens electronically, without the need for paper, phone calls, or manual data entry. It's efficient, reduces errors, and makes ordering and restocking your store much smoother and quicker.

## Types of EDI
* Many larger companies adopt **hybrid EDI** solutions to connect with their business partner.

### Direct EDI/Point-to-point
* Establish a single connection between two business partners (1-1 connection)

* Offer control for the business partners.
	* Commonly used between larger customers and suppliers with a lot off **daily transactions**.

### EDI via VAN
* Value Added Networks (VANs) are private networks where electronic business documents are exchanged between partners.

* Work **asynchronously**: VAN provider manages the network and provides participants **mailboxes** where they can send and receive EDI documents.

### EDI via AS2
* ***AS2*** - securely internet communications protocol

### Web EDI
* Use standard internet browser
* Different online forms used for information exchange between BPs.
-> Easy, affordable for small/medium-sized orgs that use EDI occasionally.

### Mobile EDI

### EDI Outsourcing
* Enable companies to use external resources to manage their EDI on day-to-day basis.

## Benefits of using EDI
> [!abstract] Major benefits
> * Cost savings
> * Speed and Accuracy
> * Efficiency
> * Strategic

* **Cost Savings**: EDI reduces the need for manual data entry, paper-based communication, and associated labor costs. It streamlines processes, cuts down on errors, and decreases operational expenses.

* **Speed and Accuracy:** EDI enables swift data transmission, often in real-time, reducing delays in information exchange. Automation minimizes human errors, making data more accurate and reliable.

* **Efficiency:** EDI optimizes business processes by automating tasks like order processing, invoicing, and inventory management. This efficiency leads to faster order fulfillment, reduced lead times, and improved supply chain coordination.

* **Strategic:** EDI provides a strategic advantage by fostering better relationships with partners, suppliers, and customers. It enhances collaboration, enabling data-driven decision-making and helping businesses adapt to changing market conditions more effectively.

## EDI in Postal Service
* EDI transmissions can be seen as a **tagged delimited message set**. (tag used to inform how to handle the following data)
* In postal area, **EDI exchanges** is used to refer to the electronic exchange of msgs based on UPU EDI messaging standards.
	* Most postal EDI msgs today are based on ***EDIFACT***

> [!info] EDIFACT
> * UN/EDIFACT - United Nations rules for Electronic Data Interchange for Administration, Commerce and Transport.
> * EDIFACT is a format for EDI exchange, text-based standard.

* An EDIFACT msg = segments
	* segments = data elements
	* data elements = components

![[Pasted image 20231013100015.png]]

> [!example]- Example of a EDIFACT msg
> ```text
> UNB+UNOA:1+FR103:UP+IT102:DL+120301:0900+INTREF886'
> 	UNH+MESREF1159+RESDES:1:912:UP'
> 		BGM++ITMXPAFRCYMADCN20106'
> 		GID++1'
> 		PCI+++CW:ITMXPAFRCYMADCN20106001001455'
> 		FTX+AAQ++CN::139' FTX+INS++N::139'
> 		FTX+RET++N::139'
> 		MEA+WT+AAB+KGM:145.5'
> 		RFF+ACU:20'
> 		DTM+7:1203010838:201'
> 		GID++1'
> 		PCI+++CW:ITMXPAFRCYMADCN20106002101775'
> 		FTX+AAQ++CN::139'
> 		FTX+INS++N::139'
> 		FTX+RET++N::139'
> 		MEA+WT+AAB+KGM:177.5'
> 		RFF+ACU:20'
> 		DTM+7:1203010837:201'
> 	UNT+19+MESREF1159'
> 	UNH+MESREF1160+RESDES:1:912:UP'
> 		BGM++ITMXPAFRCYMACCN20067'
> 		GID++1'
> 		PCI+++CW:ITMXPAFRCYMACCN20067001101273'
> 		FTX+AAQ++CN::139'
> 		FTX+INS++N::139'
> 		FTX+RET++N::139'
> 		MEA+WT+AAB+KGM:127.3'
> 		RFF+ACU:20'
> 		DTM+7:1203010837:201'
> 	UNT+11+MESREF1160'
> 	UNH+MESREF1161+RESDES:1:912:UP'
> 		BGM++ITMXPAFRSLMAACR20060'
> 		GID++1:BG'
> 		PCI+++CW:ITMXPAFRSLMAACR20060001100016'
> 		FTX+AAQ++CR::139'
> 		FTX+INS++N::139'
> 		RFF+ACU:20'
> 		DTM+7:1203010705:201'
> 	UNT+9+MESREF1161'
> UNZ+3+INTREF886'
> ```

* Explain:
	1. **UNB (Interchange Header):**
	    - `UNB+UNOA:1`: This segment specifies the character set (UNOA:1 indicates UN/EDIFACT character set, version 1).
	    - `FR103:UP`: Sender's identification ("FR103") and sender's code ("UP").
	    - `IT102:DL`: Recipient's identification ("IT102") and recipient's code ("DL").
	    - `120301:0900`: Interchange date and time.
	    - `INTREF886`: An internal reference number for the interchange.
	2. **UNH (Message Header):**
	    - `UNH+MESREF1159`: Message reference number ("MESREF1159").
	    - `RESDES:1:912:UP`: The message type and version number, in this case, "RESDES" version 1, release 912, from the sender "UP."
	3. **BGM (Beginning of Message):**
	    - `BGM++ITMXPAFRCYMADCN20106`: Indicates the beginning of the message, with a reference to "ITMXPAFRCYMADCN20106."
	4. **GID (Goods Item Details):**
	    - `GID++1`: Identifies the goods item, in this case, item number "1."
	5. **PCI (Package):**
	    - `PCI+++CW:ITMXPAFRCYMADCN20106001001455`: Provides package information, including the package type ("CW") and a reference to "ITMXPAFRCYMADCN20106001001455."
	6. **FTX (Free Text):**
	    - Various FTX segments provide additional information, such as details about the goods, instructions, and references.
	7. **MEA (Measurements):**
	    - `MEA+WT+AAB+KGM:145.5`: Specifies measurements, in this case, the weight in kilograms (145.5 kg).
	8. **RFF (Reference):**
	    - `RFF+ACU:20`: Provides a reference to "ACU:20."
	9. **DTM (Date/Time):**
	    - `DTM+7:1203010838:201`: Indicates a date and time reference.

> [!question] 
> XML is also capable of represent information in a structural way (tagging elements), so XML and EDIFACT which one should be used?

* EDIFACT: compact, robust and widespread
* XML: flexible, easy to implement, can handle any language.

* XML exchanges is still in early stage -> need more time before switching.

* When configuring EDI Translator to handle postal EDI msg based on EDIFACT, it is necessary to provide the standard of that msg, and its version. (UPU Messaging Standards)

### EDI Message Usages
* **Shipment Tracking**: EDI msg enable real-time tracking and tracing of shipments.
	* Customers and businesses can receive updates on the status and location of their packages
	-> Improve transparency

* **Label Printing**: generate electronic shipping labels
	-> Minimize errors

* **Order Fulfillment**: postal services use EDI to receive orders from businesses and automatically process them for delivery.
	-> Accelerate the fulfillment process

* **Customs Declarations** (International shipments, tạm thời chưa tính)

* **Invoicing and Payment**

* **Change of Address Notifications**: ensures that mail is deliverd to the correct address (even if receivers changes their address)

* **Parcel Data Exchange**: postal services exchange data about parcels, including size, weight, and destination, through EDI. 
	* This information is crucial for planning transportation and logistics.

#### Implementation of EDI Msg in calculating delivery time
> [!note]
> By involving the use of **real-time tracking** and **tracing data**, postal companies are able to monitor the movement and location of packages. From that info, they can estimate delivery times more accurately.

1. **Location Data:** 
	* EDI msg can include package's real-time location data which is collected through tracking and tracing systems (barcodes, RFID, GPS ...)
	* This data is continuously updated and shared via EDI back to postal companies.
	-> They can determine its current location, calculate remaining distance to its destination.
    
2. **Historical Data:** 
	* Over time, postal companies accumulate a wealth of historical data on their delivery operations.
		* Past delivery times for various routes, dest, types of packages.
		-> Analyze them to identify patterns and trends.
Ex: Delivery from city A to city B tends to take more than 3 hours.
    
3. **Route Optimization:** 
	* Along with real-time location data, traffic conditions and weather updates are also sent back to postal companies.
	* Using these data, companies evaluate to choose the most efficient route for current delivery.
	-> Ensure package reach their destinations on time.
Ex: if a truck encouters traffic jam ahead, the system may give driver recommendation for other route to avoid delays.
    
4. **Delivery Time Windows:** 
	* For businesses and customers who need packages delivered within specific time frames, postal companies can use EDI messages to provide more precise delivery time windows to meet these requirements.
	-> Valuable for businesses that plan their operations around incoming shipments.

### Current developments trends in postal EDI standards:
1. **Digital Transformation:** Postal services worldwide were focusing on digital transformation to enhance their services. This included implementing advanced EDI standards to improve efficiency and customer experience.
2. **Adoption of International Standards:** Postal services were increasingly adopting international EDI standards, such as UN/EDIFACT and ANSI X12, to facilitate cross-border exchanges of information and improve interoperability with global partners.
3. **eCommerce Integration:** With the growth of e-commerce, postal services were actively developing and enhancing EDI standards to better integrate with e-commerce platforms. This included improving the electronic exchange of shipment data, tracking information, and customs declarations.
4. **Real-time Tracking and Visibility:** Postal services were investing in EDI standards to provide real-time tracking and visibility to customers. Customers could track the status and location of their shipments through EDI messages and web-based tracking systems.
5. **API Integration:** Many postal services were working on providing Application Programming Interfaces (APIs) to enable businesses and e-commerce platforms to integrate postal services directly into their systems. This allowed for seamless information exchange and label printing.
6. **Secure Data Exchange:** Security remained a top priority, and postal services continued to enhance data encryption and authentication measures in their EDI standards to protect sensitive customer and financial information.
7. **Customs Compliance:** Given the importance of customs declarations in international shipping, postal services were aligning their EDI standards with evolving customs regulations to expedite clearance processes.
8. **Environmental Sustainability:** Postal services were working on EDI initiatives to reduce paper usage and promote electronic invoicing, e-billing, and other eco-friendly practices.

