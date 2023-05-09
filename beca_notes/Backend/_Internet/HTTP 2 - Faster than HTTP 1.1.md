* Introduced in 2015

> [!abstract] Key reasons why HTTP/2 is faster than HTTP/1.1
> 1. **Multiplexing**
> 2. **Server Push**
> 3. **Header Compression**
> 4. **Binary Protocol**
> 5. **Prioritization**

### 1. Multiplexing (Đa kênh)
* HTTP/1.1's biggest limitation is it only allow **single request-response cycle at a time over a single TCP connnection**.
	* If the webpage has many resources (images, scripts, stylesheets ...), each of these resources must **be requested and delivered in a sequence.**

> [!check] HTTP/2 supports multiplexing.
> * Multiple requests and response can be sent over a single TCP connection, at the same time. (parallel loading)
> -> **Reducing tremendously page load times.**

### 2. Server Push
* HTTP/1.1 requires the client to request each resource individually.
-> **Server must wait for each request before sending the corresponding resource.**

> [!check] `Server Push` feature of HTTP/2
> * Allow the server to send resources to the client before they are requested.
> **-> Reducing significantly the latency of subsequent request, since the resources are already in the client cache.**

### 3. Header Compression
* Header are sent with redundant information for every request and response.
**-> A lot of unnecessary data being sent over the network, slowing down page load time.**

> [!check] `Header Compression` feature of HTTP/2
> * Use new compression algorithm called ***HPACK*** to compress headers before they are sent over the network.
> **-> Improving performance and reducing bandwidth usage.**

> [!info]- What is HPACK algorithm
> HPACK is a header compression algorithm used by the HTTP/2 protocol to reduce the size of HTTP headers. The algorithm uses a combination of Huffman encoding and variable-length integer encoding to represent header field names and values in a more compact form. 
> Here's a high-level overview of how HPACK works:
> 1.  The sender creates an indexed table of previously sent header fields, called the "dynamic table". The table is initially empty
> 2.  When sending a new header field, the sender first checks if the field name and value match any entries in the dynamic table. If so, the sender uses an index to refer to the matching entry in the table, which reduces the amount of data that needs to be sent. 
> 3.  If the header field is not in the dynamic table, the sender needs to send both the field name and value. To reduce the size of the data, HPACK uses Huffman encoding to compress the field name and value, which replaces frequently occurring characters with shorter bit patterns. 
> 4.  The sender can also create a new entry in the dynamic table by adding the new header field to the table. The table has a fixed size, so adding a new entry may require removing an older entry.
> 5.  The receiver uses the same indexed table to decode the headers. When receiving an indexed reference, the receiver looks up the corresponding entry in the table and uses the stored field name and value.
> 6.  When receiving a new header field, the receiver needs to decode both the field name and value. The receiver uses the Huffman codebook to decode the compressed data.

### 4. Binary Protocol 
* HTTP/1.1 uses a **text-based protocol** 
	-> **Inefficient for computer to parse, since it need to convert the text into machine-readable code.**

> [!check] HTTP/2 uses Binary Protocol
> * More easy for computer to parse
> **-> Reducing the processing time required for each request, faster page load times.**

### 5. Prioritization
* In HTTP/1.1, all request have the same priority
	* Slower page loading if some resources are more important than others.
> [!check] `Stream priority` feauture of HTTP/2
> - **Stream**: a sequence of frames that belong to a particular request/response exchange.
> -   Streams can be assigned a numerical weight, ranging from 1 to 256, which represents their relative priority compared to other streams.
> -   A dependency relationship can be established between streams, which allows the client to indicate which streams are more important than others.
> -   When a stream has a parent, it inherits the parent's weight and priority.
> -   The server can use this information to determine the order in which requests should be processed.
> -   By prioritizing important requests, HTTP/2 can improve the efficiency of resource allocation and reduce the overall response time for a web page, especially in high-latency environments.
> **-> Allowing critical resources to be delivered more quickly, improving page load times, especially on complex webpages.**