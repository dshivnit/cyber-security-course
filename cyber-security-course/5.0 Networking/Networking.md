*Bruh - rationalise/organise this page..*

- WAN (Wide Area Network)
- LAN (Local Area Network)
	- WLAN (Wireless LAN)
- SAN (Storage Area Network)
- Protocols
	- TCP/IP
	  Transmission Control Protocol / Internet Protocol
	  Port 80
	- UDP
	  User Datagram Protocol
	  Ports:
		  - DNS: 53
		  - DHCP: 68
		  - Kerberos: 88
	- BGP
	  Border Gateway Protocol
	  Port 179
	- ARP
	  Address Resolution Protocol
	  Port 219
	- ICMP
	  Internet Control Message Protocol
	  Port 1 (apparently - will need to look into this further, but it doesn't really need a port)
	- PPP
	  Point to Point Protocol
	  Port - none, runs in Layer 2
	- STP
	  Spanning Tree Protocol
	  Port - none, runs in Layer 2
	- HTTP
	  Hyper-Text Transfer Protocol
	  Port 80
	- HTTPS
	  Hypter-text Transfer Protocol Secure
	  Port 443 (I want to double-check this - used to be known as SSL Secure-Sockets Layer, apparently now TLS Transport Layer Security - could be all the same )
	- FTP
	  File Transfer Protocol
	  Ports 20, 21
	- DHCP
	  Dynamic Host Control Protocol
	  Port - none, runs on layer 7 (apparently - I want to look into this further)
	- Telnet
	  Port 23
	- SSH Secure Shell
	  Port 22
	  
- Services
	- DNS
		- Domains (expand on this - TLDs etc)

- Tools
	- Wireshark
	- Sysinternals TCPView
	- nmap (for both Unix and Windows shells)

- CAN (Control Area Network) bus
	- A serial communication protocol that allows devices to exchange data in a reliable and efficient way. Widely used in vehicles, working like a nervous system to connect ECUs in the vehicle.
	- https://www.emqx.com/en/blog/can-bus-how-it-works-pros-and-cons
	- https://en.wikipedia.org/wiki/CAN_bus

- IP Addressing
	- You will know if an IP Address is Classful or Classless by identifying the difference in the subnet length. Classful addressing uses fixed-length subnet masks, classless ones use variable length subnet masks (VLSM)
	- VLSM - Variable Length Subnet Mask
		- Classful *(will need to revise these ranges.. For some reason to me they don't look right and from recollection the actual Classful ones are a bit more specific - I could be entirely wrong)*
			- A: 0.0.0.0 - 126.0.0.0 (Subnet Mask: 255.0.0.0 or /8 )
			- B: 128.0.0.0 - 191.0.0.0 (Subnet Mask: 255.255.0.0 or /16)
			- C: 192.0.0.0 - 223.0.0.0 (Subnet Mask: 255.255.255.0 or /24)
		- Reserved (for private use and are non-routed)
			- 10.0.0.0 - 10.255.255.255
			- 172.16.0.0 - 172.31.255.255
			- 192.16.0.0 - 192.168.255.255
		- Other Reserved:
			- 127.0.0.0 (for loopback and IPC on the localhost)
			- 224.0.0.0 - 239.255.255.255 (for multicast addresses)
		- CIDR (Classless Inter-Domain Routing)
	- Multicasting

Classful Subnets:

Class A

|                  |                 |                       |                     |     |
| ---------------- | --------------- | --------------------- | ------------------- | --- |
| **Network Bits** | **Subnet Mask** | **Number of Subnets** | **Number of Hosts** |     |
| /8               | 255.0.0.0       | 0                     | 16777214            |     |
| /9               | 255.128.0.0     | 2 (0)                 | 8388606             |     |
| /10              | 255.192.0.0     | 4 (2)                 | 4194302             |     |
| /11              | 255.224.0.0     | 8 (6)                 | 2097150             |     |
| /12              | 255.240.0.0     | 16 (14)               | 1048574             |     |
| /13              | 255.248.0.0     | 32 (30)               | 524286              |     |
| /14              | 255.252.0.0     | 64 (62)               | 262142              |     |
| /15              | 255.254.0.0     | 128 (126)             | 131070              |     |
| /16              | 255.255.0.0     | 256 (254)             | 65534               |     |
| /17              | 255.255.128.0   | 512 (510)             | 32766               |     |
| /18              | 255.255.192.0   | 1024 (1022)           | 16382               |     |
| /19              | 255.255.224.0   | 2048 (2046)           | 8190                |     |
| /20              | 255.255.240.0   | 4096 (4094)           | 4094                |     |
| /21              | 255.255.248.0   | 8192 (8190)           | 2046                |     |
| /22              | 255.255.252.0   | 16384 (16382)         | 1022                |     |
| /23              | 255.255.254.0   | 32768 (32766)         | 510                 |     |
| /24              | 255.255.255.0   | 65536 (65534)         | 254                 |     |
| /25              | 255.255.255.128 | 131072 (131070)       | 126                 |     |
| /26              | 255.255.255.192 | 262144 (262142)       | 62                  |     |
| /27              | 255.255.255.224 | 524288 (524286)       | 30                  |     |
| /28              | 255.255.255.240 | 1048576 (1048574)     | 14                  |     |
| /29              | 255.255.255.248 | 2097152 (2097150)     | 6                   |     |
| /30              | 255.255.255.252 | 4194304 (4194302)     | 2                   |     |

Class B

|   |   |   |   |
|---|---|---|---|
|**Network Bits**|**Subnet Mask**|**Number of Subnets**|**Number of Hosts**|
|/16|255.255.0.0|0|65534|
|/17|255.255.128.0|2 (0)|32766|
|/18|255.255.192.0|4 (2)|16382|
|/19|255.255.224.0|8 (6)|8190|
|/20|255.255.240.0|16 (14)|4094|
|/21|255.255.248.0|32 (30)|2046|
|/22|255.255.252.0|64 (62)|1022|
|/23|255.255.254.0|128 (126)|510|
|/24|255.255.255.0|256 (254)|254|
|/25|255.255.255.128|512 (510)|126|
|/26|255.255.255.192|1024 (1022)|62|
|/27|255.255.255.224|2048 (2046)|30|
|/28|255.255.255.240|4096 (4094)|14|
|/29|255.255.255.248|8192 (8190)|6|
|/30|255.255.255.252|16384 (16382)|2|

Class C

|   |   |   |   |
|---|---|---|---|
|**Network Bits**|**Subnet Mask**|**Number of Subnets**|**Number of Hosts**|
|/24|255.255.255.0|0|254|
|/25|255.255.255.128|2 (0)|126|
|/26|255.255.255.192|4 (2)|62|
|/27|255.255.255.224|8 (6)|30|
|/28|255.255.255.240|16 (14)|14|
|/29|255.255.255.248|32 (30)|6|
|/30|255.255.255.252|64 (62)|2|

Class D

|   |   |   |   |
|---|---|---|---|
|**CIDR Block**|**Supernet Mask**|**Number of Class C Addresses**|**Number of Hosts**|
|/14|255.252.0.0|1024|262144|
|/15|255.254.0.0|512|131072|
|/16|255.255.0.0|256|65536|
|/17|255.255.128.0|128|32768|
|/18|255.255.192.0|64|16384|
|/19|255.255.224.0|32|8192|
|/20|255.255.240.0|16|4096|
|/21|255.255.248.0|8|2048|
|/22|255.255.252.0|4|1024|
|/23|255.255.254.0|2|512|
