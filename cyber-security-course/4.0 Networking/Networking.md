*Bruh - rationalise/organise this page..*

[[Protocols]]

[[DNS (Domain Name System)]]

[[Network Administration]]

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


Classful Subnets:

Class A ( 0.0.0.0 - 127.255.255.255)

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
