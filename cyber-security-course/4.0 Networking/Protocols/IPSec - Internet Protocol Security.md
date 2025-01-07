Internet Protocol Security

- Uses these:
	- AH - Authentication Header
		- Providing Integrity, and Authentication
	- ESP - Encapsulating Security Payload
		- Provides auth, integrity and confidentiality
	- SA - Security Association
		- Negotiates encryption keys and algorithms
			- Such as the IKE (Internet Key Exchange)

Authentication Header (AH)
- Responsible for the authentication and integrity of the data traffic
	- Doesn't consider confidentiality of the data transmitted
- Two modes:
	- Transport Mode
		- Provides authentication for TCP/UDP header and data
	- Tunnel Mode
		- Provides authentication for the IP Header, TCP/UDP Header and data
- Essentially the AH is encapsulated into a packet upon data transmission and retrieval (decapsulated in retrieval, of course)
- Mandatory to implement AH in IPSec-v2, optional in v3

Encapsulating Security Payload (ESP)
- Provides encryption along with authentication and integrity
- Two modes:
	- Transport Mode:
		- Give security (confidentiality and integrity) for the TCP/UDP header and data
	- Tunnel Mode:
		- Gives security as above for the IP Header, TCP/UDP header and data