https://tryhackme.com/r/room/wifihacking101
https://en.wikipedia.org/wiki/Wi-Fi_Protected_Access
https://github.com/morrownr/USB-WiFi
https://www.aircrack-ng.org/

Terminologies:
- SSID - Service Set Identifier
	- The network "name" that one normally connects to
	- The name of a wireless network
	- Can be up to 32 characters long, case-sensitive
- ESSID - Extended Service Set Identifier
	- "May" apply to multiple access points
	- Such as what may be seen in a company office, forming a bigger network
- BSSID - Basic Service Set Identifier
	- 48-bit
	- The MAC address of an AP
	- Ad-hoc networks, the BSSID is generated randomly
- WPA2-PSK - Wi-Fi Protected Access 2 Pre-Shared Key
	- 4-way handshake
		- A process which is crucial, ensuring both the client and the AP have the correct PSK without actually transmitting it. 
		- A transient Pairwise Transient Key (PTK) is generated for secure data exchange
			- AP sends a random number (ANonce) to the client
			- Client responds with its random number (SNonce)
			- AP calculates the PTK from these numbers and sends an encrypted message to the client
			- Client decrypts this message with the PTK confirming successful authentication
	- WLAN Networks you connect to by providing a password that is the same for everyone
	- Incorporates AES 
- WPA2-EAP - Wi-Fi Protected Access 2 Extensible Authentication Protocol
	- Authentication is granted by a RADIUS server via the use of a supplied username and password
- WPA3 - Wi-Fi Protected Access 3
	- Replaces PSK with Simultaneous Authentication of Equals (SAE) exchange
		- A more secure initial key exchange in personal mode and forward secrecy
	- Supports Opportunistic Wireless Encryption (OWE) for open Wi-Fi networks that do not have passwords
- RADIUS
	- A server for authenticating clients

- Tools (hard/soft)
	- `aircrack-ng` package - which includes
		- `aircrack-ng`
		- `airdecap-ng`
		- `airmon-ng`
		- `aireplay-ng`
		- `airodump-ng`
		- `airtun-ng`
		- `packetforge-ng`
		- `airbase-ng`
		- `airdecloak-ng`
		- `airolib-ng`
		- `airserv-ng`
		- `buddy-ng`
		- `ivstools`
		- `easside-ng`
		- `tkiptun-ng`
		- `wesside-ng`
	- 