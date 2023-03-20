## What is DNS
> [!info] Domain Name System - DNS
> * Phonebook of the Internet (distributed database of mapped addresses to domain names)

## How does DNS work?

* Converting a hostname (xxx.com) into a computer-friendly IP address (also called ***DNS Resolution***)

![[Pasted image 20221225144334.png]]

> [!info] DNS Query (DNS request)
> A demand for information sent from a client to a DNS server.

* In most case, a DNS request is sent to ask for the IP address associated with a domain name.
* An attempt to reach a domain is a DNS client querying the DNS server to get the IP address, which related to that domain.
> [!note] There is two ways of resolving a domain name
> * ***Recursice query*** - DNS client directly gets the IP address of a domain, by asking the name server system to perform the complete translation.
> 
> * ***non-Recursive query*** - DNS client contacts the name servers, onen by one, until it finds the server, containing the needed information.

## DNS Resolvers
> [!info] DNS Resolver
> A server that takes care of the DNS Resolution for the browser.
> * It sends and receives queries to and from a ***DNS Server***, which has the contact list of the Internet.
> 
> ![[Pasted image 20221225145153.png]]

> [!question] Why do we need DNS Resolvers?
> It increase the **speed** and **efficiency** of the DNS Resolution process.
> * Whitout DNS Resolvers, clients will have to keep track of the different DNS Servers: their addresses, their working status ...
> * Clients also need a security measure against [DNS attack](https://cybernews.com/resources/what-is-a-dns-attack/#:~:text=Some%20of%20the%20most%20common%20types%20of%20DNS,TCP%20SYN%20Floods%2C%20and%20Domain%20lock-up%20attack.%20)
> 

## DNS Servers & Different Stages of a DNS Query
![[Pasted image 20221225152934.png]]

* The mapping of domain names to IP  addresses works in a hierarchical order using DNS zones.

> [!info] Root Servers
> * First step in the name resolution of any domain name, tops of the hierarchy.
> * They publish the root zone file. 
> 	* top-level domains: .com, .net, .org
> 	* country code top-level domains: .vn, .uk

* Root servers help narrow down the scope of searching, which bring up a faster process to get the result.

> [!info] Top-level Domain (TLD) Server
> Nameserver that keeps all the information for all domain names that share a common domain extension.
> Ex: .com, ...

* TLD servers help in forwarding to the right DNS Server that has the IP Address that we are searching.

***More about [What Is TLD Server?](https://threat.media/definition/what-is-a-tld-server/)***

> [!info] Authoritative Server
> Provide original and definitive answers to DNS queries.
> * It is final node on the hierarchy.
> * It only returns answers to queries about domain names that are installed in its configuration system.

> [!question] Why do we need both Root Server and TLD Server?
> While the Root Server serve the "." domain, the TLD servers serve the top level domain, which directly below the ".". 
> 
> > [!example] 
> > Ex: with the ".de" is the german country domain. DNS servers managed by DE-NIC. The "." root name servers know the DNS Servers for the .DE domain and tie it all together. But they are not the top level domain servers themselves.

## The Process of DNS Resolution (DNS Lookup)
### Recursive Query
1. User opens browser and enters `https://www.\<domain_name\>.com` to search.
	* The computer doesn't know the IP address for that domain, so it sends a request to the user's  DNS Resolver.

2. The Resolver does not know the IP address for `www.\<domain_name\>.com`, so it will querry one of the root DNS Server (in this case: `.com`)

3. The Root Servers know the locations of the `.com` TLD server but they don't know the IP for `www.\<domain_name\>.com`, so they return the location of the `.com` servers.

4. Once the query reaches the `.com` TLD servers, it will find the Authoritative DNS server of `www.\<domain_name\>.com` and will reply to the resolver with that server.

5. The Resolver will send a query to the Authoritative DNS Server of the domain and will resolve it.

6. The Authoritative DNS Server of the  domain will check within its database and will find an entry for `www.\<domain_name\>.com`, which has an IP address.

7. Finally, the resolver will know the IP address for `www.\<domain_name\>.com` and will send the result to the user's computer.

### Non-Recursive Query
Similar to Recursive Query, except from the DNS clients has to do it all by themselves.