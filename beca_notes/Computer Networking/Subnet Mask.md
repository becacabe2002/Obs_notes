* IPv$ address consists of two parts (each octet range from 0 - 255)
	![[Subnet Mask-20240325001838144.webp]]

![[Subnet Mask-20240325002001308.webp]]

* A subnet mask reveals **how many bits in the IP address are used for the network** by masking the network portion of the IP address 

![[Subnet Mask-20240325003352830.webp]]

![[Subnet Mask-20240325004251697.webp]]

* Default subnet mask
	![[Subnet Mask-20240325004548067.webp|362]]

> [!question] Why does an IP address have a network and a host part?
> * For management, to breakdown a huge network into small sub network.

* **Subnetting** is done by changing the default subnet mask by borrowing some of the bits from the host portion.
	![[Subnet Mask-20240325012126628.webp]]
	

![[Subnet Mask-20240325011116547.webp]]

Ex: *192.168.1.0 /24* -> 24 bit network -> 1 network with 254 hosts

