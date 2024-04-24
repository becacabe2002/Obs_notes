> [!info] Proxy
> * Proxy is a server, which acts like a middlman, which sits between a private network and the public internet.

### Forward Proxy
![[Proxy _ Reverse Proxy-20240324185119201.webp]]

* Regulate traffic by blocking harmful websites (go out of a network)

* Hide the identity of the clients by masking their IP address

* Logs user activity

* Bypass restricted content

 * Increases loading speed by caching copies of website in its db.

### Reversed Proxy
![[Proxy _ Reverse Proxy-20240324214100740.webp]]

* Regulate traffic going to the network

* Increase the security by hiding the IP address of the servers (only address of rev proxy server is visible)

* Block malicious traffic such as DDOS attacks.

* Load balancing

![[Proxy _ Reverse Proxy-20240324214806113.webp]]

> [!check]  Conclusion
> **Forward Proxy** protects users, meanwhile **Reverse Proxy** protects servers.