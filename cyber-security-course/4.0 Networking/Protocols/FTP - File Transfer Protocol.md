- Listens on Port 21 by default (and 20)
- Sessions operate using two channels:
	- command (control) channel
	- data channel
- Client-server protocol
- Active Connection
	- Client opens a port and listens
	- Server actively connects to it
- Passive Connection
	- Server opens a port and listens
	- Client connects to it
- Separation of channels allows for commands to be sent whilst waiting for current data transfers to complete
	- More efficient
- unencrypted (note, this is not sFTP but just FTP)

Some FTP Commands:
- USER - used to enter the username..
- PASS - used to enter related username's password..
- RETR - (retrieve) used to download a file from the FTP server to the client
- STOR - (store) used to upload a file from the client to the FTP server
....
- help will get you a list of possible commands as well
- 