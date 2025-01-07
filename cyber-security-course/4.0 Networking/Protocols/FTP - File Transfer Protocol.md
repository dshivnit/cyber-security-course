- Listens on Port 21 by default (and 20)
- Sessions operate using two channels:
	- command (control) channel
	- data channel
- Client-server protocol
- Active Connection
	- Client establishes the control connection to send commands and request parameters to the server
	- Once authenticated and when the client requests it, the server will establish a data connection to the client and start transferring data
	- Client connects to the server on server port 21 to create a command connection
	- Server connects to the client on server port 20 to create a data connection
	- Bear in mind the client sitting behind a firewall in scenarios where one is considering an Active Connection
- Passive Connection
	- Client creates both the control and data connections
	- Server sends a random server port to the client, once the client gets it, it will establish a connection to the given server port and the data transfer can begin
- unencrypted (note, this is not FTPS but just FTP, same thing really just that TLS isn't incorporated, or could be. The protocol is otherwise pretty much the same)
- FTPS differences
	- Implicit Connection
		- Both control and data are encrypted over TLS
	- Explicit Connection
		- The client requests the server to invoke a SSL/TLS session on port 21
		- Three communication modes for control and data
			- Encrypt only control
			- Encrypt only data
			- Encrypt both control and data

Some FTP Data Types
- ASCII/Type A
	- Default for text file transfers
	- If needed, data can be converted into 8-bit ASCII before transmission and converted back upon receiving
- Image/Type I
	- Referred to as binary mode
	- Uses byte-to-byte transmission
- EBCDIC/Type E
	- For the EBCDIC character set
- Local Type L n
	- Used for when devices do not support 8-bit byte transfer (parameter `n` represents the byte size)

Some FTP Commands:
- USER - used to enter the username..
- PASS - used to enter related username's password..
- RETR - (retrieve) used to download a file from the FTP server to the client
- STOR - (store) used to upload a file from the client to the FTP server
....
- help will get you a list of possible commands as well
- 