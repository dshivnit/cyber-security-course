*(Please Do Not Throw Sausage Pizza Away ;) -- as a term of reference to the various layers, I don't give a toss what you do with your pizza just don't waste food.)*

*(I'll fill in more on these sections as I review the Network+ and other course material)*

Specific processes take place to each bit of data that passes through these layers, from bottom down to bottom up respectively.

Pieces of data added and also removed as they move between layers. 
Encapsulation and decapsulation are terms to define the adding and removing of such data in this context. 

It is also useful to note that you can identify technical issues and which layer they reside in - some Teams in the professional/corporate environment tend to live and focus in specific areas, and will relay with other Teams to further troubleshoot identified issues. (ie Network Engineers to Software Developers and so on)

- Application
	- Email Clients
	- Web Browsers
	- GUI-based Applications
	- DNS
	- SFTP
	- SSH
	- HTTP
	- SMTP
- Presentation
	- Acts as a translator for data to and from the 7th layer. 
	- The receiving computer will also understand data sent to a computer in one format destined for another format
	- You may send an email with Outlook, however, the person receiving it may be using Thunderbird. 
		- Either way the content will still need to be presented in the same way
- Session
	- The Fifth Layer
	- Will begin to create a connection to the computer that the data from the previous, Sixth Layer, is meant for.
	- When a connection is established, a session is created
	- Whilst the connection is up, so is the session
	- Will synchronise the two computers to ensure that they are on the same page of progress before data is transmitted and received. 
	- Once these checks are in place, it will begin to divide up data into smaller chunks of data (packets) and begin to transmit these one at a time (well process these, as it may be receiving as well)
		- This is helpful as if the connection between the two nodes happens to go down, then it will only be the remaining packets that will need to be sent. 
	- Sessions are unique
		- Data doesn't travel over different sessions but stay within the one
- Transport
	- TCP (Transmission Control Protocol)
		- Three-way handshake
		- Connection-based
		- Provides a constant connection between the two devices for the amount of time that it would take for the data transfer to complete
		- Incorporates error checking to ensure that all the packets are sent and also received
		- Reliable
		- Accurate
		- Synchronising the connection between devices so as to not cause flooding on either side (well the receiving side) 
		- Requires a reliable connection
		- A slow connection can bottleneck one device
		- Slower than UDP because there is more processing that is involved
		- Used for:
			- File sharing
			- Web browsing
			- Emails
			- FTP
		- Packet Details:
			- Source Port
			- Destination Port
			- Source IP
			- Destination IP
			- Sequence Number (SEQ)
			- Acknowledgement Number (ACK)
			- Checksum
			- Data
			- Flag
		- Three-way Handshake
			- SYN
			- SYN/ACK
			- ACK
			- DATA
			- FIN
			- RST
				- Ends all communication
				- Indicates that there was some problem during the connection
					- low resources
					- application error
					- etc
			- TCP will close a connection once it has been determined that all data has been sent AND received
			- It is best to close TCP connections as soonest as possible, as they do soak up resources
			- a FIN packet is sent to initiate the closing of a connection
	- UDP (User Datagram Protocol)
		- Stateless (not a government state but a connectionless state - lel)
		- No error checking or reliability
		- Sending device will transmit regardless if the receiver receives the packets or not
		- No synchronisation between either device
		- Full send
		- Much faster than TCP
		- Lets the Seventh Layer decide how quickly packets are sent
		- Sometimes can result in a terrible end-user experience for the receiving side
		- Useful for when small pieces of data are being sent
			- ARP 
			- DHCP
		- Also useful for larger files
			- Video streaming
				- Consider pixelation when streaming, nyaar not all packets are being received properly
		- Packet Contents:
			- Time To Live (TTL)
			- Source Address
			- Destination Address
			- Source Port
			- Destination Port
			- Data
		
- Network
	- Routing
	- Re-assembly of data
	- Determines the optimal path that packets should travel
	- OSPF
		- Open Shortest Path First
	- RIP
		- Routing Information Protocol
	- Everything IP Address
- Data Link
	- Frames
		- No IP addresses
	- MAC Addresses associated with NICs (Network Interface Cards)
	- MAC Addy's can't be changed, BUT they can be spoofed
	- When data is transmitted, it is the MAC (physical) Address that is used to identify where it came from
	- Also responsible for presenting data suitable for transmission
- Physical
	- 1s 
	- 0s
	- Electrical signals being transmitted