Open Worldwide Application Security Project

1. Broken Access Control
2. Cryptographic Failures
3. Injection
4. Insecure Design
5. Security Misconfiguration
6. Vulnerable and Outdated Components
7. Identification and Authentication Failures
8. Software and Data Integrity Failures
9. Security Logging & Monitoring Failures
10. Server-Side Request Forgery (SSRF)

Broken Access Control
- Protected pages
	- Admin Console
	- Others (system depending)
- Unauth'd access:
	- Visibility over sensitive information
	- Visibility over sensitive/confidential functionality
- Insecure Direct Object Reference (IDOR)
	- Could be files
	- A user
	- A Bank Account in a banking system
	- Anything really that shouldn't be referenced in the first place or have the ability to be referenced in an easy, or straightforward, let alone secure manner

Cryptographic Failure
- Refers to any vulnerability arising from the misuse (or a lack of use) of cryptographic algorithms for securing sensitive information
- WebApps require crypts to provide security and confidentiality for users across all levels
- Encrypting Data in Transit:
	- when traffic between the client and server is encrypted
- Encrypting Data at Rest
	- when data is stored on a Server, it is encrypted
	- Usually held in a Database

Injection
- The application takes user-inputs as commands or parameters from which it will execute for the most part back-end code.
- SQL Injection
	- When User-input is passed into the system as a SQL query. 
	- The User can then toggle the output of queries and sometimes access otherwise sensitive information
		- or delete, modify data
- Command Injection
	- User is able to pass system commands into the WebApp
	- Server-side code execution (like PHP)
	- Make a call to a function that interacts with the Server's console
	- Allows the adversary to take control - as if they were sitting on the Server as root
- Defense:
	- Allow-lists:
		- User-input is referenced to a list of safe inputs or characters
		- If safe, then the input is processed
		- Otherwise, REJECTED
	- Stripping Input
		- If the input contains dodgy characters, said characters are removed before processing

Insecure Design
- For the most part, these vulns become apparent when improper threat modelling is carried out during the planning phases of the application - and drip feed through to the final product. 
- Also tends to happen when Developers make shortcuts around the code to make their testing "easier."
	- ie - disabling MFA, OTP validation to test the app without having to manually enter verification codes at each part of the process ("for the sake of testing") 
- Insecure Password Resets
- More

Security Misconfiguration
- Examples:
	- Inadequate permissions on cloud services, ie S3 Buckets
	- Having unneeded features made available, like services, pages, accounts or privileges
	- Default login account credentials
	- Detailed error messages
	- Not utilising or using HTTP Security Headers
- Exposing Debugging Interfaces
	- Example - When Patreon got hacked in 2015 via its Werkzeug Python debugging console

Vulnerable and Outdated Components
- System/Application version checking
	- Vulnerabilities?
	- UPDATE IF SO or take the system offline until maintenance/patching has been carried out (both)

Identification and Authentication Failures
- Authentication systems are pretty much on all systems that have a back-end (well, every system does when you think about it)
- Most commonly in the form of a uname and pword
	- Session Cookies in this part of a WebApp connection are needed
	- Web Servers use these Cookies to who is sending what data and can then have the ability to keep track of who is doing what on their system(s)
- Types of Weaknesses
	- Barute Force
		- Speaks for itself albeit the name I've mangled
		- How many attempts does the System allow?
	- Weak Auth Creds
		- There should be strong password policies in place by the system being analysed/tested
		- If not, then weak
	- Weak Session Cookies
		- If these pieces of data/information hold predictable variables, then Users/Perps can set their own Cookie variables and access parts of the System that they shouldn't otherwise be able to
- Mitigate as Best You Can
	- Strong password policies
	- Login attempt count and timeout for numerous unsuccessful attempts
	- MFA and additional login processes
	- Sanitise logins

Software and Data Integrity Failures
- Data Integrity
	- The need to ensure that data remains credible and is unjustifiably modified. 
		- ie, whatever you may be accessing on the Internet, is it how it should be? You aren't seeing that data/information live on the server, it is being transferred to you - has anything happened in transit? Has it been manipulated, corrupted? 
		- Checksums have been put in place for scenarios like the above - so that both ends know that the integrity of the file is how it should be with ACKs and confirmations. Usually in the form of a hash
- Mitigation
	- Do integrity checks on both sides! (well, mainly on the receiving side)
- Software Integrity Failures
	- Linking to external/third-party resources
		- Such as linking a script in src to an external reference)
		- It's not in your zone/scope to maintain the integrity of that external source, if it becomes compromised that inadvertently will impact the security of your system as well
		- Subresource Integrity (SRI) - Mordern Web-Browsers have an integrity check comparing hash's between entities (sources and receivers/pullers) to ensure .. Integrity (farms)
			- srihash.org

Data Integrity Failures
- Session Tokens
	- Cookies
		- Key-value pairs that a WebApp will store on the Users end that will be automatically repeated with each Request made to the Website, by that User
		- Each User would have their own Cookie that would contain their Username
		- The Server would know which User/Session to respond to by with what is sent by the Client's Browser (what Cookie is sent) 
		- Nothing is stopping the User from tampering with said Cookie
			- Could potentially lead to a failure in data integrity 
			- Mitigation:
				- Integrity mechanism(s)
				- ie JSON Web Tokens
					- use of either a private secret or a public/private key between Server and Client
					- JWT Tokens are formed with three parts:
						- Header
							- Indicating that *this* is a JWT
							- Signing algorithm (ie HS256)
						- Payload
							- If this is changed, the Websystem will know by verifying that the signature won't match the payload
						- Signature
					- Unlike simple hashing, this matching signature needs and uses the Secret Key method. 
					- The three-parted token is simply plaintext encoded with base64
				- Vulnerability
					- JWT and the None Algorithm
						- Changing the alg: part of the header to "none" from whatever algorithm was in there prior
						- Payload "username" to admin
						- This vuln was from a while ago

Security Logging and Monitoring Failures
- Every action should be logged
- More than useful, a necessity, because if something happens, an incident say, logs should be able to outline every action that had taken place through (and before) the event/incident had taken place. 
	- ie who logged in and where, when, etc
		- What did they do? 
- Attackers may want to dispose of such logs prior to their exit, so do the logs live in one place? Or are they actively copied to a redundant location? (this may not be the right term to use - but you know what I mean, hopefully.)
- Regulatory damage
	- if sensitive, personal information is compromised and if there is no record outlining this - the application owners could be subject to fines or further prosecution depending on local and sometimes other regulations
- Risk of further attacks
	- An attackers exploits may be undetected without logging which could allow for further attacks/breaches/exploits further down the line of time. 
		- Defensive Teams will need to be able to reflect on what actions, methods (etc)  took place by the attacking side to be able to determine where previous, current, and what are possible flaws could be
- Usual information stored in logs:
	- HTTP Status Codes
	- Time Stamps
	- Usernames
	- API Endpoints/Page Locations
	- IP Addresses
	(bear in mind that these are items from OWASP - Application Security, so I haven't included other items that could also be considered in logs - such as Server Names (these could be multiple devices depending on what has happened) etc)
- Ideally you want to be monitoring for any suspect movements/activity in real-time with the idea to stop the perpetrator actively or to reduce their efforts. 
- Some examples of suspect activity :) :
	- Multiple unauth'd attempts for a particular action
	- Requests coming from anomalous IP addresses or geographical locations, these can be false positives but should be looked into. Or there should be a common task/job that runs looking out for such activity in defense systems
	- Automated Tools - patterns of how frequently some requests or tasks are being made
	- Common Payloads - some attackers will use well-known or identified payloads in the industry.

Server-Side Request Forgery
- When an Adversary/Attacker manipulates a Server to send Requests on their behalf
- They keep control of the contents of the Request
- These vulns usually happen when the Web Application relies upon a third party services
localhost:Port/admin%23&id=12345
	%23 here is a URL-encoded "#"  (which is a comment character in URLs, anything after it isn't processed..)