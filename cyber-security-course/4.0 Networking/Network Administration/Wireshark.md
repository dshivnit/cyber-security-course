- https://wiki.wireshark.org/CaptureFilters
- https://tryhackme.com/r/room/wireshark
- 

*(I'm most likely not going to describe this tool in this page, well that is the current thought anyway. I suggest to run some modules through THM or do some fiddling on your end :) Very powerful tool)*

- Network packet sniffing tool
- Can be used to find network traffic anomaly's (suspicious traffic)
- Tools like Datto and other RMM solutions can also be used for Enterprise networks - but as far as I am currently aware not to the detail of what Wireshark provides (it literally breaks down a packets details without destroying it :)

Firstly
- Start with a sample capture to ensure that Wireshark is set up correctly and that it is capturing traffic appropriately
- Ensure that the machine/system you are running Wireshark on has enough resources (hardware) to handle the amount of network traffic that it will be handling
	- This will depend on the size of the network that is being analysed
- Ensure you also have ENOUGH DISK SPACE! to store all of the packet captures (.pcaps :) )

Network Taps
- A physical implant in which you physically tap between a cable
- Commonly used by Threat Hunting/DFIR teams, read teams - when in an engagement to sniff and capture packets
	-  Using hardware to tap the wire and intercept traffic as it comes across
		- A vampire tap 
			- ![](https://assets.tryhackme.com/additional/wireshark101/7.gif)
	- Planting a network tap that would be an inline network tap
	- You would plant this between or inline two network devices
	- The tap will replicate packets as they pass the tap
	- Like a throwing star LAN tap
		- ![](https://assets.tryhackme.com/additional/wireshark101/8.jpg)

- MAC Floods
	- Commonly used tactic by Red Teams to actively sniff packets
	- Intended to stress the switch and fill the CAM table
		- When the CAM(Content Addressable Memory) table is filled, the switch will no longer be able to accept new MAC addresses
		- In order to keep the network alive, the switch will send out packets to all ports on the switch
- ARP Poisoning
	- Another technique used to actively sniff packets
	- With ARP poisoning, you can redirect the traffic from the host(s) to the machine you're monitoring from. 
	- This technique will not stress network equipment like MAC flooding

Wireshark Default Packet Colouring Schema:
![](https://assets.tryhackme.com/additional/wireshark101/6.png)


- Filtering Captures in Wireshark
	- Use of boolean and logic operators
		- and
			- `and` / `&&`
		- or
			- `or` / `||`
		- equals
			- `eq` / `==`
		- not equal
			- `ne` / `!=`
		- greater than 
			- `gt` / `>`
		- less than
			- `lt` / `<`
	- contains
	- matches
	- bitwise_and (AND, OR, XOR, NOT)
		- https://www.wireshark.org/docs/wsug_html_chunked/ChWorkBuildDisplayFilterSection.html
	- Basic Filtering
		- `ip.addr == <ip-address>`
		- `ip.src == <src-ip-address> and ip.dst == <dst-ip-address>`
		- `tcp.port eq <port-num> or <protocol-name>`
		- `udp.port eq <port-num> or <protocol-name>`

- Packet Dissection
	- Packets are broken down according to the seven layers in the OSI model
		- Frame
		- MAC Addresses
		- IP Addresses
		- Transport Layer 4 Protocols
		- Protocol Errors
		- Application Protocol
		- Application Data

- ARP Traffic
	- Address Resolution Protocol
	- ARP is a Layer 2 protocol
	- It's used to connect IP Addresses with MAC addresses
	- They will contain REQUEST and RESPONSE messages
	- Ensure that physical addresses are resolved in Wireshark
		- View > Name Resolution > Resolve Physical Addresses (ticked)

- ICMP Traffic
- https://datatracker.ietf.org/doc/html/rfc792
	- Internet Control Message Protocol
	- Runs on Layer 3
	- Used to analyse various nodes on a network
	- Commonly used with utilities like ping and traceroute
	- host-to-host datagram service in a system of interconnected networks
		- Type 8's - request packet
		- Type 0 - reply packet
			- If these codes are altered, then something strange is going on
	- Timestamps
		- Are almost always important to consider
	- Data
		- Typically should just be a random string.

- TCP Traffic
- https://datatracker.ietf.org/doc/html/rfc793
	- Layer 4
	- Don't forget about the default colouring schema that Wireshark incorporates
		- You can change these to your preference too
	- Using tools like **RSA NetWitness** and **NetworkMiner** in conjunction with TCP packet analysis is worthy
		- Otherwise there's just too much to go through by just using Wireshark alone
	- The hand shake (the TCP one ;) ) 
		- syn, synack, ack (**Flags**)
		- If something is out of order in this handshake, or when it includes other packets like an RST packet - then there is something weird going on in the network
		- (like an NMAP scan to a closed port)
	- You can see the original sequence number of a packet
		- edit > pref > protocols > TCP > uncheck relative sequence numbers
	- Typically TCP packets need to be looked at as a whole to get the entire story - as opposed to by one by one... (much fragmentation)

- DNS Traffic
	- Layer 4 (UDP)
- https://www.ietf.org/rfc/rfc1035.txt (1987, hah!)
	- Resolves names with IP addresses
	- Always check out the flags and get familiar with them
	- Look out for what is being queried for signs of weirdness/suspicion 

- HTTP Traffic
	- Layer 7
	- https://www.ietf.org/rfc/rfc2616.txt
	- Straight forward protocol for analysis
		- no handshakes or prerequisites before communication
	- URI's can be informative when a GET request is placed
	- This is HTTP, and not HTTPS - so bear that in mind. Everything's unencrypted 
	- You can organise the protocols present in a capture the **Protocol Hierarchy**
		- Statistics > Protocol Hierarchy
	![](https://assets.tryhackme.com/additional/wireshark101/36.png)
	- Real useful in practical applications like threat hunting to identify discrepancies in packet captures
	- **Exporting an HTTP Object**
		- Allows for the organisation of all requested URIs in the capture
			- File > Export Objects > HTTP
	- **Endpoints**
		- Allows for the organisation of all endpoints and IPs found within a specific capture
			- Statistics > Endpoints
	- **Statistics**
		- There are heaps of options in here!
		- Capture File Properties
		- Resolved Addresses
		- Protocol Hierarchy 
		- Conversations
		- Endpoints
		- Packet Lengths
		- I/O Graphs
		- Service Response Time 
		- Check it out (I was thinking to take a screenshot but Obsidian and uploading to GitHub is a mission - may do later.)

- HTTPS Traffic
	- Before sending encrypted traffic, the client and server need to make an agreement first
		- 1. Both agree on a protocol version
		- 2. A cryptographic algorithm is selected and agreed upon (one that both sides can support)
		- 3. The client and server can authenticate with each other, this is optional?
		- 4. A secure tunnel is created with a public key (which then will lead to the symmetric encryption connection)
	- We can start analysing HTTPS traffic by looking at packets for the handshake between the client and the server
	- Adding an encryption key for debugging..
		- Edit > Preferences > Protocols > TLS (or whatever) > RSA Keys List > Edit > add the relevant bits here. 
			- Port might be '`start_tls'` 
			- Protocol more than likely would be '`http`'
	- Remember, looking out for
		- Request URIs
		- User-Agents
			- Can be useful in practical applications of Wireshark, especially for threat hunting and network administration
		- Also - HTTP Object Feature would now be available too
			- File > Export Objects > HTTP

Having solid knowledge on Threat Intelligence, current, in the past, potential - is vital in knowing what to look out for when doing packet analysis. 

Some Wireshark documenation:
https://www.wireshark.org/docs/