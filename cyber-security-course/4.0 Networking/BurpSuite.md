Web Application Security Testing Framework

- Java-based framework
- A solution for conducting WebApp PenTesting
- Industry standard tool for assessing:
	- Web applications
	- Mobile applications
	- APIs
- Captures and enables the manipulation of all the HTTP/S traffic between a browser and a web server
- It's a proxy from where you can do a bunch of stuff to requests :) 
- Abilities to:
	- Intercept
	- View
	- Modify
			web requests before they get to the host server
			Or even responses before they reach
			El fantastico for testing
- Paid-for versions have additions, obviously - some being:
	- Professional:
		- Automated vulnerability scanner
		- Fuzzer/brute-forcer (not rate limited)
		- Ability to save projects for later use and report generation
		- An API to integrate with other tools
		- Unrestricted access to add new extensions for diverse functionality
		- Burp Suite Collaborator access
			- Providing a unique request catcher self-hosted or running on a Portswigger owned box
	- Enterprise:
		- Utilised for continuous scanning
		- Similar to tools like Nessus perform automated infrastructure scanning
		- Lives on a Web Server, scanning target WebApps for vulnerabilities
- Tools
	- Proxy
		- Enables interception and modification of requests and responses between Web Applications
	- Repeater
		- Allows for the capturing, modifying and resending of the same request multiple times
		- Payloads through trial and error
			- ie SQLi (injection) or testing an endpoint for vulns
	- Intruder
		- Rate limited in the Community edition
		- Allows for spraying endpoints with requests
		- Baruta forcing attacks or fuzzing endpoints
	- Decoder
		- Data transformation
		- Decode captured information or encode payloads before sending them to the target
	- Comparer
		- Compares two pieces of data at either the word or byte level
	- Sequencer
		- When assessing the randomness of tokens
			- Session Cookie values
			- Other randomly generated data
			- If the process involved lacks full on randomness or security, it can expose pathways for potential attacks
- Shortcuts :) 
	- Dashboard
		CTRL + SHIFT + D
	- Target
		CTRL + SHIFT + T
	- Proxy
		CTRL + SHIFT + P
	- Intruder
		CTRL + SHIFT + I
	- Repeater
		CTRL + SHIFT + R

- Cookie Jar
	- In Settings > Sessions

- Burp Proxy
	- Interecpt Mode
		- When requests are made they hit the Proxy firs
		- Further actions can be made
			- Forward
			- Drop
			- Edit
			- Send them to other Burp modules
			- This mode can be disabled to allow packets, well the requests to go through freely (Burp will still pick up request and response information)
		- Taking Control
			- Full control by developers/testers of the systems being analysed
		- Capture and Logging
			- Speaks for itself
		- Websocket Support
			- Additional assistance when analysing WebApps
		- Logs and History
			- For further analysis down the line - speaks for itself
	- Interception Rules
		- You can toggle the Proxy to see if a Request was:
			- modified
			- intercepted
			- status codes don't match
			- if the URL is in the target scope for whatever analysis is taking place

- FoxyProxy (have some way of configuring Burp to act as the proxy with config respective of the build you are on)
	- Also ensuring that Intercept is on in BurpSuite
	- Then you can intercept Requests and Responses as you see fit
	- (don't forget to turn that Interceptor off eh ;)  along with whatever Web-Browser Proxy you have running)

- Target
	- Site Map
		- Every page that is visited while the proxy is running will be displayed on the Site Map
	- Issue Definitions
		- List of all the vulns the scanner would look for
			- (comes with the Professional Edition properly)
		- CE (Community Edition) does list all the vulns in detail
			- It's a massive list.
	- Scope
		- Include/exclude specific domains/IPs to define the scope of the testing
		- Scope 'em up (no point looking at redundant nodes when you're wanting to test one, or a series of applications/hosts)

- Browser
	- If you can't toggle a Web Browser-based Proxy
	- Chromium-based Web Browser in BurpSuite
	- 