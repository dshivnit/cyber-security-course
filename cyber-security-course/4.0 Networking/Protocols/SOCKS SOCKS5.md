Socket Secure
- A proxy protocol for data exchange through a delegate server (SOCKS5 proxy)
- Used to secure Layer 7 (Application Layer) protocols

The Process (consider a firewall between two recipients who want to speak with each other)
- Client Initiation
	- Anne connects with a SOCKS5 proxy server and sends a first byte (0x05) to the server where 5 is the SOCKS version
	- Anne then sends a second byte (0x01) identifying that authentication is supported
	- Anne then sends a third byte (either 0x00, 0x01, 0x02, 0x03)
		- These will identify the supported authentication methods and the length can vary
- SOCKS5 Proxy Reply
	- The proxy server then sends back a second byte, which identifies the chosen authentication method (which is decided by the server)
	- After the initiation packet, Anne will send a request packet - this includes the BHOST and BPORT numbers
	- A successful connection can then be established between Anne and the SOCK5 Proxy Server
	- The same things happen with Ben on the other side
- Data Transfer
	- Now, both Anne and Benzo can share and exchange data and these will be routed through the SOCKS5 proxy server