(445 sometimes 139 (netBIOS))
SMB2 protocol in packets

Client-Server communication protocol used for sharing network access to:
	- Files
	- Printers
	- Serial Ports
	- Other resources
Servers will make file systems, printers, named pipes, APIs, and other items available to clients on the network. 
File Servers and the like, etc. 
- SMB is known as a response-request protocol. 
- It transmits multiple messages between the client and itself to establish a connection. 
- Uses:
	- TCP/IP (NetBIOS over TCP/IP - RFC 1001 and 1002)
	- NetBEUI
		- Designed to be used on a single LAN segment
	- IPX/SPX
		- Internetwork Packet Exchange / Sequenced Packet Exchange
		- Used primarily on MS Windows LANs
- Once connected, Clients can send commands (SMBs) to the Server which will allow them access to Shares on the network
	- With permissioned ability to manipulate files depending on levels
	- This is all done over the network
- Who runs it:
	- MS Windows 
	- Samba for Unix-based devices