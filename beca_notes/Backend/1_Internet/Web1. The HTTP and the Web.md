## What is HTTP?
> [!info] HTTP - Hypertext Transfer Protocol
> An **Application layer protocol** that allows web-based applications to communicate and exchange data.
> It is a **TCP/IP based** protocol.

![[Pasted image 20221220213700.png]]

* The HTTP is the **messenger of the web**.

* It is used to deliver contents(img, vid, audio, doc...)

* Computers that communicate via the HTTP must speak the HTTP protocol

## Three important features
> [!abstract] Three important things ab the HTTP
> 1. At the **Application layer**, HTTP is **connectionless**.
> 2. HTTP can deliver **any sort of data** (as long as two com are able to read it)
> 3. The  HTTP is a stateless.

> [!info] Connectionless
> After making the request, the client **disconnect** from the server. Then when the response is **ready** the server **re-establish the connection** again and deliver the response.

> [!info] Stateless
> The client and server know about each other just **during the current request**. If it closes, and the two computers want to connect again, they need to **provide info** to each other anew (một lần nữa), and  the connection is handled **as the very first one**.

## Why HTTP
* When http was designed, it was used mainly to fetch html docs and sends it to the client.

* As it kept elvoving, many features were added to it.

> [!check] HTTP became the most convenient way to quickly and reliably move data on the web.

## Request - Respone Cycle
> [!warning] Prerequisite
> The computer has to be connected to the Internet.

1. Client sends a **Request**, which is an HTTP message.

2. Since it is connectionless, client disconnects from the server, waiting for the response.

3. Server process the request and prepare the response.

4. Server establishes the connection again and send back the **Response**, which is an HTTP message.

5. The two coms completely disconnect.

## Request HTTP Message
> [!note] Components of an HTTP Message
> * ***Start line*** 
> * ***Headers*** 
> * ***Body*** (Maybe not require for a request)
> All of them contain plain text based information. Sometimes the Body contains binary data.

* The **information** in these three sections vary **depending on the HTTP message**, whether it is a request or a response
> [!example]
> ![[Pasted image 20221220221108.png]]

> [!note] The start line =  **HTTP Method** + **URI** + **HTTP version**
> \<Method\> \<path/to/file.ext\> \<http/version\>

![[Pasted image 20221220231544.png]]

## HTTP Methods
> [!info] HTTP method
> Command that tells the server what to do

> [!note] 
> * ***GET*** - used to retrieve information from the given server using a given URI. Requests using GET should only retrieve data and **should have no other effect on the data**.
> 
> * ***POST*** - used to send data to the server using HTML forms.
> 
> * ***HEAD*** - same as GET, but transfers the status line and header section only.
> 
> * ***PUT*** - replaces all current representations of the target resource with the uploaded content.
> 
> * ***DELETE*** - removes all current representations of the target resource given by a URI
> 
> * ***CONNECT*** - establishes a tunnel to the server identified by a given URI.
> 
> * ***OPTIONS*** - describes the communication options for the target resource.
> 
> * ***TRACE*** - performs a message loop-back test along the path to the target resource.

> [!info] URI
> a set of readable characters and a way to locate the resource.

> [!example] 
> ![[Pasted image 20221220235757.png]]
> Host : address of the server which client send request to
> Accept-language : specify the language
> Accept : what kind of file request to

## Response HTTP Message
> [!note] 
> * ***Start line*** =  \<http/version\> \<status code\>
> * ***Header***
> * ***Body*** - contain requested file

> [!info] Status code
> Tell the client if the request succeeded or failed.
> Ex: 
> * 200 - ok
> * 404 - file not found
> 
> > [!tip]
> > More about [status code](https://www.tutorialspoint.com/http/http_status_codes.htm)

