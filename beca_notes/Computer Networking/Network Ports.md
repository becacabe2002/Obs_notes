> [!info]  Port
> * Is not a **physical connection**, but more like a **logical connection**, which is used by progs and serv to exchange information.

* Port specifies which prog or serv on computer/server that is going to be used. 

* Port number: **0 - 65535**
Ex: 
*80, 443 - HTTP,HTTPS transfer*
*21 - FTP*
*25 - SMTP*

* A port is always associated with an IP address (ip address helps determine the server location)
	![[Network Ports-20240324093057843.webp]]

### 3 types of Port numbers
* 0 - 1023: **System/Well-known ports** 

* 1024 - 49151: **User/Registered ports**
	* Ports can be registered for a particular serv

* 49152 - 65535: **Dynamic/Private ports**
	* Client-side ports, which are free to use.
	* Computer temporarily assigns these ports to itself during a session.

![[Network Ports-20240324094032525.webp]]

* When a computer establishs a connection with a server, a dynamic port is going to be assigned along with port from the server.
	![[Network Ports-20240324094340691.webp]]