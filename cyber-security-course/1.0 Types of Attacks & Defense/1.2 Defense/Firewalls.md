Inspects a network's or digital device's incoming and outgoing traffic.

Anything that comes in, or goes out - will be inspected by the firewall first. 

Traffic that is or isn't allowed is based on rules that are set in the firewall.

Most firewalls presently - whether in a corporate environment, and also a private one - offer extra functionalities to protect the device and/or network from the outside world (or outside networks). 

Types of Firewalls:
- Stateless Firewalls
	- Operates on Layer 3 and Layer 4
	- Filters data based on predetermined rules without taking note of the state of the previous connections
		- Meaning that it will match every packet with rules regardless of whether it is part of a legitimate connection or not. 
	- It doesn't maintain any information on the state of previous connections to make decisions for future packets
	- This allows the Stateless Firewall to process packets quickly
	- However, they cannot apply complex policies to the data based on its relationship with previous connections
		- For example, the firewall denies packets from a single source based on the rules it runs by
			- It should block/drop all packets from that source moving forward because the previous packets weren't compliant with policy/rules
			- However, the Firewall keeps forgetting this (lol) and future packets from the same source will be treated as new and matched by its rules again (redundant)
- Stateful Inspection Firewalls
	- Goes beyond filtering packets by predetermined rules
	- Keeps track of previous connections and stores them in a state table
	- Adds another layer of security by inspecting the packets based on their history with connections
	- Operate on layers 3 and 4
	- Will take note of connections that have packets which were allowed, and connections where they weren't allowed - and will make its decision to either allow them in the future (for the ones that were compliant) or automatically drop packets from connections that have been non-compliant in the past
- Proxy Firewalls
	- Application-level firewalls that act as an intermediary between the private network and the Internet (external networks) and operate on Layer 7
	- They inspect the contents of all packets
	- Requests made by users in a network are forwarded by this proxy after inspection and masking them with their own IP address to provide anonymity for the internal IP addresses
	- Content filtering policies can be applied to these firewalls to either allow or deny incoming and outgoing traffic based on their content
- Next Generation Firewalls (NGFW)
	- Most advanced type of firewall
	- Operates on layers 3 through to 7
	- Offers deep packet inspection and other functionalities that can enhance the security of incoming and outgoing network traffic
	- It has an IPS (Intrusion Prevention System) that will block malicious activity in real-time. 
	- Offers heuristic analysis by analysing the patterns of attacks and blocking them instantly before they can reach internal/private networks
	- NGFWs have SSL/TLS decryption capabilities which can inspect packets after decrypting them and correlate the data with threat intelligence feeds to make efficient decisions

Rules in Firewalls
- Customised rules can be defined for systems/networks
- ie - denying all inbound SSH traffic
	- But, allow inbound SSH traffic from specific IP addresses
- Basic components:
	- Source address
	- Destination address
	- Port
	- Protocol
	- Action
		- Allow
		- Deny
		- Forward
		- Applies to firewalls that provide routing functionality and act as gateways between different networks
- Inbound Rules
- Outbound Rules
- Forward Rules

Linux iptables Firewall
- Netfilter
	- The framework inside the Linux OS
	- Includes:
		- Pcaket filtering
		- NAT
		- Connection Tracking
	- This framework serves as the foundation for various firewall utilities available in Linux to control network traffic
	- Some utilities:
		- iptables
			- Most widely used
		- nftables
			- Successor to the 'iptables' utility, enhanced packet filtering and NAT capabilities
		- firewalld
			- Works differently from the previous two above
			- Comes with pre-built network zone configurations
		- All three above are based on the Netfilter framework
- ufw - Uncomplicated Firewall
	- Eliminates complications of making rules in a complex syntax in iptables or its successor
	- 