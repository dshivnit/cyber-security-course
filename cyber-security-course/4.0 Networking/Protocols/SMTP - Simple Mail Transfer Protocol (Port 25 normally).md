- Used to handle the sending of emails. 
- In order to support email transfers, a pairing with either POP or IMAP is required
- Outgoing Mail Servers (SMTP)
- and Incoming Mail Servers (either IMAP or POP)
- SMTP performs:
	- verification on who is sending email through the Server
	- Sends relevant emails (outbound)
	- If undeliverable, the Server will send it back to the Sender
- Each of these Mail Servers will have their own configuration

- Basic Commands:
	- HELO or EHLO - creates/initiates an SMTP session
	- MAIL FROM - identifies the sender's email address
	- RCPT TO - identifies the recipients email address
	- DATA - indicates that the client will begin sending the content of the email 
	- . - is sent on a line by itself to indicate the end of the connection/transmission

- Simple break-down of the process:
	- Mail Client connects to the SMTP Server of a Domain
	- Handshake initiates
	- SMTP Session starts
	- Client will:
		- Send to the Server:
			- Sender and Receiver Email Addresses
			- Body of the Email
			- Attachments
	- Server will:
		- Check whether the Domain of the Receiver and the Sender are the same
		- If not:
			- Will make a connection to the Receivers SMTP Server
			- If the responding Server is unavailable then the Email gets put into a SMTP queue
	- Receiving SMTP Server will:
		- Verify the inbound Email
			- Checks the Domain and Username have been recognised
		- Forward the Email to respective POP or IMAP Servers for processing
	- Email shows up on the Receiver's side

- SMTP is generally available on all OS platforms

Tools
- MetaSploit (msfconsole command to launch it) MetaSploit Framework
	- search (module name)
	- use (module name)
	- info 
		- when inside a module to find out htf to use it xD
	- info -d 
		- for module setup instructions if required
		- smtp_version 
			- Scan a range of IP addresses and determine the version of any mail servers it comes across
			- Grabs the banner from the SMTP Server
		- smtp_enum
			- Scans wordlists to attain Usernames
	- There is extensive documentation on how to use this tool
		- docs.metasploit.com 
	- You can also view the Help Menu when in the program itself and it will list you a series of base commands
		- I will not list them here, you can do that and reference them on your own accord and system/processing should you wish :) 
	- Postfix
		- A free and open-source MTA (Mail Transfer Agent) that routes and delivers Emails.
		- MTA (Mail Transfer Agent)
			- Responsible for receiving Email messages
	- Hydra
		- For all purposes relating to testing
- SMTP Service
	- Has two internal commands to outline Users
		- VRFY
			- Confirming the names of valid Users
		- EXPN
			- Reveals actual address of User Aliases and lists DLs (Distribution Lists, Mailing Lists -- preferably call them Mailing Lists as DLs could be more an MS thing..)
- smtp-user-enum
	- Even better for clarifying OS-level Users on Solaris via the SMTP service
	- Inspects responses to VRFY, EXPN, and RCPT TO commands
	- This tool is something to keep in mind if you're preparing for the OSCP
	- *Could* be adapted in future work against SMTP daemons
	- 