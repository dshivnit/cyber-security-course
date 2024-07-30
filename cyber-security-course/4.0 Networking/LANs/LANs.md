*This section and other network related sections will be detailed further when I review the Network+ and other related material*

Local Area Networks

- Topologies
	- Star
		- Devices are individually connected via a central networking device (like a Switch, a Hub (lel) or a SOHO Router (that typically has a Switch built into it))
		- More cabling and purchase of dedicated networking equipment is required
		- It's more expensive than other topologies
		- More scalable
			- Straight forward to add more devices/nodes to the network
			- The more it scales/grows, the more maintenance is required to keep the network functional
			- Can make for harder troubleshooting
			- Failures, if the central node fails, connected devices won't be able to send or receive data (stay connected) 
	- Bus
		- Use of a backbone cable
		- Bottlenecks are an issue
			- Especially if all nodes on the network are transmitting/receiving
			- Because one backbone cable, yay
		- Makes for harder troubleshooting
		- Easier and more cost-efficient topologies to set up
		- Little redundancy
			- Single point of failure, cables aren't as resilient as what a centralised node in a Star Topology can be
	- Ring
		- aka Token Topology
		- Each device/node is connected directly to each other to form a loop
		- Little cabling
		- Daisy chain
		- Data is sent across the loop until it reaches its destined device
		- Devices will transmit their own data first before passing on data that has been sent from another device
		- One cable or one device failing will result in a network failure... lel

- Switches
	- Dedicated devices that are designed to aggregate multiple other devices (computers, printers, VOIP phones, IP Cams, connections to other networking equipment and so on)
	- Usually found in larger networks (businesses, schools, similar-sized networks)
	- 4, 8, 16, 24, 32, 64 port Switches
- L3 Switches
	- 
- Routers
	- Connect networks and pass data between them
	- Creating a path between networks


- Subnetting
	- 32 bits in a Subnet Mask (same as with an IP Address)
	- Splitting up a network into smaller, miniature networks within itself
	- Let's you decide how many addresses from the available pool are divided amongst the various needed subnets
	- Identifies:
		- Network Address
			- Identifies the start of the actual network and is used to identify a networks existence
		- Host Address
			- To identify a device on the network
		- Default Gateway
			- Specifies the device that is capable of sending data to another network
	- Provides:
		- Efficiency
		- Security
		- Full Control

- ARP Protocol
	- Address Resolution Protocol
	- Technology that is responsible for allowing devices to identify themselves on a network
	- Allows a device to associate it's MAC Address with its IP Address on the network
	- Each device on a network will keep a log of the MAC Addresses associated with other devices
	- When a device wants to communicate with another, they will broadcast to the entire network searching for that device
		- Devices use the ARP protocol to find the MAC address of a device they are wanting to connect with
	- Addresses are kept in cache
	- ARP Request
		- a broadcast to the network querying what the MAC Address is for the related IP address
	- ARP Reply
		- Devices will respond to the ARP Request with their MAC Address
	- Details are kept in an ARP Cache

- DHCP Protocol
	- Dynamic Host Control Protocol
	- If no manual IP Address assignment
		- Devices will send out a request (DHCP Discover) to see if there are any DHCP Servers on the network that can assign them a Dynamic IP
		- If there is a DHCP Server then they will respond with a DHCP Offer
		- Device then confirms it wants the offer by sending a  DHCP Request
		- DHCP Server then responds with a DHCP ACK confirming this has been completed
		- 