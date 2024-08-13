*Bruh - rationalise/organise this page..*

[[Protocols]]

[[DNS (Domain Name System)]]

[[Network Administration]]

- WAN (Wide Area Network)
- LAN (Local Area Network)
	- WLAN (Wireless LAN)
- PAN (Personal Area Network)
- MAN (Metropolitan Area Network)
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
	- DNSCrypt
		- Network protocol that authenticates and encrypts Domain Name System (DNS) traffic between the User's computer and recursive name servers. DNSCrypt wraps unmodified DNS traffic between a client and a DNS resolver in a cryptographic construction, preventing eavesdropping and forgery by a main-in-the-middle attack.

- Port Forwarding
	- Forwarding data from a device that is internal to a LAN or Private Network to an external network (mainly the WWW)
		- such as in the case of Web Servers
	- Allowing external entities to be able to access internal entities by specifying which external port would be used to cater for that internal connection
		- Internally it could be 172.23.69.69:80 (for the sake of a generic web server) however externally you could configure that port to be accessible via (WAN_IP or External IP Addy:6969)

- Firewall (operates on the third and fourth layers)
	- Permits or denies network traffic from passing to and from a network
	- Can filter on:
		- Where the traffic is coming from
		- What protocols (rulez) are being used
		- What ports are being prompted for
	- Perform packet inspection to identify what kind of elements are being catered for in data traffic
	- Can be standalone service specific devices or software
	- Categories:
		- Stateful
			- Uses the entire information from a connection
			- Rather than analysing an individual packet, will determine the behaviour of a device - based upon the entire connection
		- Stateless
			- Use of a static set of rules to determine whether or not individual packets are acceptable or not
			- Only effective as the rules that define them
			- Good for when receiving large amounts of data from different hosts (such as in a DDOS attack)

- VPNs (Virtual Private Networks)
	- Allows devices on separate networks to communicate securely by creating a dedicated path between each other over the Internet (tunneling) 
	- Essentially forming their own logical private network
	- Offers:
		- Allows networks in different geographical locations to be connected
		- Privacy
			- Use of encryption to protect data
			- Data isn't vulnerable to sniffing
		- Anonymity
			- Depends on how the VPN is set up
				- Logs
				- Data history etc
			- If everything is being noted, then wtf is the point? 
	- Technologies:
		- PPP
			- Point To Point Protocol
			- Used by PPTP
			- To allow authentication and provide encryption of data
			- Use of a private and public key (like SSH)
			- "This technology is not capable of leaving a network by itself (non-routable)" THM
		- PPTP
			- Point To Point Tunneling Protocol
			- Allows data from PPP to travel and leave a network
			- Supported by most devices
			- Weakly encrypted in comparison to alternatives
		- IPSec
			- Difficult to set up compared to alternatives
			- Boasts strong encryption and is also supported by many devices

- Routers
	- Layer 3
	- Routing
		- The process of data travelling across networks
		- Creating a path between networks so that this data can be successfully delivered
	- Normally dedicated devices that do not operate like an L2 switch
		- However, do take into account SOHO (Small Office, Home Office) Routers which are multifunctional devices and not just a standalone Router like you'd normally find in a corporate environment
	- Factors considered:
		- What path is shortest
		- What path is most reliable
		- Which path has the fastest medium (copper, fibre, air)
- Switches
	- L2 devices normally but there are also L3 switches
	- Supporting 3/4 - 63 devices
	- Use of Ethernet Cables
	- Forwarding and receiving of Frames
	- MAC Addresses are what are considered
	- L3 Switches
		- VLANs (Virtual Local Area Networks)
		- Forwarding of packets (obviously based on IP, since packets) to other networks that are identified on the L3 Switch (ie VLANs)
		- These VLANs are physically connected to the Switch, but are logically independent of each other - hence why IP Addresses are considered in such cases

- Services
	- DNS
		- Domains (expand on this - TLDs etc)

- Tools *there is a main Tools page now, slap these over there.*
	- Sysinternals TCPView
	- nmap (for both Unix and Windows shells)
	- dnscrypt

- CAN (Control Area Network) bus
	- A serial communication protocol that allows devices to exchange data in a reliable and efficient way. Widely used in vehicles, working like a nervous system to connect ECUs in the vehicle.
	- https://www.emqx.com/en/blog/can-bus-how-it-works-pros-and-cons
	- https://en.wikipedia.org/wiki/CAN_bus

- Subnets
	- Numbers to remember
		- 128
		- 192
		- 224
		- 240
		- 248
		- 252
		- 254
		- 255
	- You will know if an IP Address is Classful or Classless by identifying the difference in the subnet length. Classful addressing uses fixed-length subnet masks, classless ones use variable length subnet masks (VLSM)
	- VLSM - Variable Length Subnet Mask
		- Classful *(will need to revise these ranges.. For some reason to me they don't look right and from recollection the actual Classful ones are a bit more specific - I could be entirely wrong)*
			- A: 0.0.0.0 - 126.0.0.0 (Subnet Mask: 255.0.0.0 or /8 )
			- B: 128.0.0.0 - 191.0.0.0 (Subnet Mask: 255.255.0.0 or /16)
			- C: 192.0.0.0 - 223.0.0.0 (Subnet Mask: 255.255.255.0 or /24)
		- Reserved (for private use and are non-routed)
			- 10.0.0.0 - 10.255.255.255
			- 172.16.0.0 - 172.31.255.255
			- 192.168.0.0 - 192.168.255.255
		- Other Reserved:
			- 127.0.0.0 (for loopback and IPC on the localhost)
			- 224.0.0.0 - 239.255.255.255 (for multicast addresses)
		- CIDR (Classless Inter-Domain Routing)
	- Multicasting
		- Multicast is a type of group communication where data transmission is addressed to a group of destination computers simultaneously. Multicast can be one-to-many or many-to-many distribution. Multicast differs from physical layer point-to-multipoint communication. (Wikipedia)
		- A single source of communication with simultaneous multiple receivers
		- Only certain, designated receivers will receive the transmission. (orhanergun.net)
	- Broadcast
		- All devices connected to the network will receive the transmission. (orhanergun.net)
	- Subnetting:
		- Logical Operations:
			- AND
			- OR
			- NOT
			- These are used to calculate and manipulate IP addresses and Subnet Masks
		- AND:
			- Used to determine the Network Address from an IP Address and a Subnet Mask
			- You do this by performing what is called a bitwise AND between the IP Addy and the Subnet Mask (convert them to binary first)
			- Both bits **have** to be 1
			- Example:
				- IP Address:        11000000.10101000.00000001.00001010
								192.168.1.10
				- Subnet Mask:    11111111.11111111.11111111.00000000
								255.255.255.0
				- Network Add:    11000000.10101000.00000001.00000000
								192.168.1.0
		- OR:
			- Used to calculate the Broadcast Address of a Subnet
			- Involves performing a bitwise OR between the Network Address and the Inverted Subnet Mask (where all the Host Bits are converted to 1)
			- **At least one** of the bits in the comparison have to be a 1
			- Example:
				- Network Add:    11000000.10101000.00000001.00000000
							   192.168.1.0
				- Inv Sub Mask:    00000000.00000000.00000000.11111111
							   0.0.0.255
				- Broadcast Add:  11000000.10101000.00000001.11111111
							   192.168.1.255
		- NOT:
			- Used to invert the bits of the Subnet Mask to find the Host portion
			- You find the Host portion (how many possible hosts) by inverting the Subnet Mask (like in the above example)
	
- Finding the Integer representation of an IP Address:
	- Each IP Address is made up four octets
	- Convert the IP Address into its binary form first
	- And then into a 32-bit integer
	- Formula:
		- Example IP: 192.168.123.152
		- (192 x 256^3) + (168 x 256^2) + (123 x 256^1) + (152 x 256^0)

Private Networks
- Private Class A Network
	- 10.0.0.0 - 10.255.255.255
- Private Class B Network
	- 172.16.0.0 - 172.31.255.255
- Private Class C Network
	- 192.168.0.0 - 192.168.255.255


---

IPv4 CIDR blocks

| Address  <br>format | Difference  <br>to last address | Mask              | Addresses     |     | Relative  <br>to class  <br>A, B, C | Restrictions  <br>on _a_, _b_, _c_ and _d_  <br>(0..255 unless noted) | Typical use                                                                                                                                           |
| ------------------- | ------------------------------- | ----------------- | ------------- | --- | ----------------------------------- | --------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| Decimal             | 2_n_                            |                   |               |     |                                     |                                                                       |                                                                                                                                                       |
| _a.b.c.d/32_        | +_0.0.0.0_                      | _255.255.255.255_ | 1             | 20  | 1⁄256 C                             |                                                                       | Host route                                                                                                                                            |
| _a.b.c.d/31_        | +_0.0.0.1_                      | _255.255.255.254_ | 2             | 21  | 1⁄128 C                             | _d_ = 0 ... (2_n_) ... 254                                            | Point-to-point links ([RFC](https://en.wikipedia.org/wiki/RFC_(identifier) "RFC (identifier)") [3021](https://datatracker.ietf.org/doc/html/rfc3021)) |
| _a.b.c.d/30_        | +_0.0.0.3_                      | _255.255.255.252_ | 4             | 22  | 1⁄64 C                              | _d_ = 0 ... (4_n_) ... 252                                            | Point-to-point links (glue network)                                                                                                                   |
| _a.b.c.d/29_        | +_0.0.0.7_                      | _255.255.255.248_ | 8             | 23  | 1⁄32 C                              | _d_ = 0 ... (8_n_) ... 248                                            | Smallest multi-host network                                                                                                                           |
| _a.b.c.d/28_        | +_0.0.0.15_                     | _255.255.255.240_ | 16            | 24  | 1⁄16 C                              | _d_ = 0 ... (16_n_) ... 240                                           | Small [LAN](https://en.wikipedia.org/wiki/LAN "LAN")                                                                                                  |
| _a.b.c.d/27_        | +_0.0.0.31_                     | _255.255.255.224_ | 32            | 25  | 1⁄8 C                               | _d_ = 0 ... (32_n_) ... 224                                           |                                                                                                                                                       |
| _a.b.c.d/26_        | +_0.0.0.63_                     | _255.255.255.192_ | 64            | 26  | 1⁄4 C                               | _d_ = 0, 64, 128, 192                                                 |                                                                                                                                                       |
| _a.b.c.d/25_        | +_0.0.0.127_                    | _255.255.255.128_ | 128           | 27  | 1⁄2 C                               | _d_ = 0, 128                                                          | Large [LAN](https://en.wikipedia.org/wiki/LAN "LAN")                                                                                                  |
| _a.b.c.0/24_        | +_0.0.0.255_                    | _255.255.255.0_   | 256           | 28  | 1 C                                 |                                                                       |                                                                                                                                                       |
| _a.b.c.0/23_        | +_0.0.1.255_                    | _255.255.254.0_   | 512           | 29  | 2 C                                 | _c_ = 0 ... (2_n_) ... 254                                            |                                                                                                                                                       |
| _a.b.c.0/22_        | +_0.0.3.255_                    | _255.255.252.0_   | 1,024         | 210 | 4 C                                 | _c_ = 0 ... (4_n_) ... 252                                            | Small business                                                                                                                                        |
| _a.b.c.0/21_        | +_0.0.7.255_                    | _255.255.248.0_   | 2,048         | 211 | 8 C                                 | _c_ = 0 ... (8_n_) ... 248                                            | Small [ISP](https://en.wikipedia.org/wiki/ISP "ISP")/ large business                                                                                  |
| _a.b.c.0/20_        | +_0.0.15.255_                   | _255.255.240.0_   | 4,096         | 212 | 16 C                                | _c_ = 0 ... (16_n_) ... 240                                           |                                                                                                                                                       |
| _a.b.c.0/19_        | +_0.0.31.255_                   | _255.255.224.0_   | 8,192         | 213 | 32 C                                | _c_ = 0 ... (32_n_) ... 224                                           | [ISP](https://en.wikipedia.org/wiki/ISP "ISP")/ large business                                                                                        |
| _a.b.c.0/18_        | +_0.0.63.255_                   | _255.255.192.0_   | 16,384        | 214 | 64 C                                | _c_ = 0, 64, 128, 192                                                 |                                                                                                                                                       |
| _a.b.c.0/17_        | +_0.0.127.255_                  | _255.255.128.0_   | 32,768        | 215 | 128 C                               | _c_ = 0, 128                                                          |                                                                                                                                                       |
| _a.b.0.0/16_        | +_0.0.255.255_                  | _255.255.0.0_     | 65,536        | 216 | 256 C = B                           |                                                                       |                                                                                                                                                       |
| _a.b.0.0/15_        | +_0.1.255.255_                  | _255.254.0.0_     | 131,072       | 217 | 2 B                                 | _b_ = 0 ... (2_n_) ... 254                                            |                                                                                                                                                       |
| _a.b.0.0/14_        | +_0.3.255.255_                  | _255.252.0.0_     | 262,144       | 218 | 4 B                                 | _b_ = 0 ... (4_n_) ... 252                                            |                                                                                                                                                       |
| _a.b.0.0/13_        | +_0.7.255.255_                  | _255.248.0.0_     | 524,288       | 219 | 8 B                                 | _b_ = 0 ... (8_n_) ... 248                                            |                                                                                                                                                       |
| _a.b.0.0/12_        | +_0.15.255.255_                 | _255.240.0.0_     | 1,048,576     | 220 | 16 B                                | _b_ = 0 ... (16_n_) ... 240                                           |                                                                                                                                                       |
| _a.b.0.0/11_        | +_0.31.255.255_                 | _255.224.0.0_     | 2,097,152     | 221 | 32 B                                | _b_ = 0 ... (32_n_) ... 224                                           |                                                                                                                                                       |
| _a.b.0.0/10_        | +_0.63.255.255_                 | _255.192.0.0_     | 4,194,304     | 222 | 64 B                                | _b_ = 0, 64, 128, 192                                                 |                                                                                                                                                       |
| _a.b.0.0/9_         | +_0.127.255.255_                | _255.128.0.0_     | 8,388,608     | 223 | 128 B                               | _b_ = 0, 128                                                          |                                                                                                                                                       |
| _a.0.0.0/8_         | +_0.255.255.255_                | _255.0.0.0_       | 16,777,216    | 224 | 256 B = A                           |                                                                       | Largest [IANA](https://en.wikipedia.org/wiki/IANA "IANA") block allocation                                                                            |
| _a.0.0.0/7_         | +_1.255.255.255_                | _254.0.0.0_       | 33,554,432    | 225 | 2 A                                 | _a_ = 0 ... (2_n_) ... 254                                            |                                                                                                                                                       |
| _a.0.0.0/6_         | +_3.255.255.255_                | _252.0.0.0_       | 67,108,864    | 226 | 4 A                                 | _a_ = 0 ... (4_n_) ... 252                                            |                                                                                                                                                       |
| _a.0.0.0/5_         | +_7.255.255.255_                | _248.0.0.0_       | 134,217,728   | 227 | 8 A                                 | _a_ = 0 ... (8_n_) ... 248                                            |                                                                                                                                                       |
| _a.0.0.0/4_         | +_15.255.255.255_               | _240.0.0.0_       | 268,435,456   | 228 | 16 A                                | _a_ = 0 ... (16_n_) ... 240                                           |                                                                                                                                                       |
| _a.0.0.0/3_         | +_31.255.255.255_               | _224.0.0.0_       | 536,870,912   | 229 | 32 A                                | _a_ = 0 ... (32_n_) ... 224                                           |                                                                                                                                                       |
| _a.0.0.0/2_         | +_63.255.255.255_               | _192.0.0.0_       | 1,073,741,824 | 230 | 64 A                                | _a_ = 0, 64, 128, 192                                                 |                                                                                                                                                       |
| _a.0.0.0/1_         | +_127.255.255.255_              | _128.0.0.0_       | 2,147,483,648 | 231 | 128 A                               | _a_ = 0, 128                                                          |                                                                                                                                                       |
| _0.0.0.0/0_         | +_255.255.255.255_              | _0.0.0.0_         | 4,294,967,296 | 232 | 256 A                               |                                                                       | Entire IPv4 Internet, [default route](https://en.wikipedia.org/wiki/Default_route "Default route").                                                   |

Classful Subnets:

Class A ( 0.0.0.0 - 126.255.255.255)

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

Class B (128.0.0.0 - 191.255.255.255)

|                  |                 |                       |                     |
| ---------------- | --------------- | --------------------- | ------------------- |
| **Network Bits** | **Subnet Mask** | **Number of Subnets** | **Number of Hosts** |
| /16              | 255.255.0.0     | 0                     | 65534               |
| /17              | 255.255.128.0   | 2 (0)                 | 32766               |
| /18              | 255.255.192.0   | 4 (2)                 | 16382               |
| /19              | 255.255.224.0   | 8 (6)                 | 8190                |
| /20              | 255.255.240.0   | 16 (14)               | 4094                |
| /21              | 255.255.248.0   | 32 (30)               | 2046                |
| /22              | 255.255.252.0   | 64 (62)               | 1022                |
| /23              | 255.255.254.0   | 128 (126)             | 510                 |
| /24              | 255.255.255.0   | 256 (254)             | 254                 |
| /25              | 255.255.255.128 | 512 (510)             | 126                 |
| /26              | 255.255.255.192 | 1024 (1022)           | 62                  |
| /27              | 255.255.255.224 | 2048 (2046)           | 30                  |
| /28              | 255.255.255.240 | 4096 (4094)           | 14                  |
| /29              | 255.255.255.248 | 8192 (8190)           | 6                   |
| /30              | 255.255.255.252 | 16384 (16382)         | 2                   |

Class C (192.0.0.0 - 223.255.255.255)

|                  |                 |                       |                     |
| ---------------- | --------------- | --------------------- | ------------------- |
| **Network Bits** | **Subnet Mask** | **Number of Subnets** | **Number of Hosts** |
| /24              | 255.255.255.0   | 0                     | 254                 |
| /25              | 255.255.255.128 | 2 (0)                 | 126                 |
| /26              | 255.255.255.192 | 4 (2)                 | 62                  |
| /27              | 255.255.255.224 | 8 (6)                 | 30                  |
| /28              | 255.255.255.240 | 16 (14)               | 14                  |
| /29              | 255.255.255.248 | 32 (30)               | 6                   |
| /30              | 255.255.255.252 | 64 (62)               | 2                   |

Class D 224.0.0.0 - 239.255.255.255
(Multicast Addressing)

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

Class E (reserved for research and/or Government use)