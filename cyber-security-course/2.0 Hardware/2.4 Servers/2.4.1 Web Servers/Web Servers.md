- A Web Server is software that listens for incoming connections and then utilises the HTTP protocol to deliver web content to its clients. 
- Common software are:
	- Apache
	- Nginx
	- IIS
	- NodeJS
- Web Servers will deliver files from their root directory's (which will be defined in their config)

Virtual Hosts
- Web Servers can host multiple websites with different Domain Names, they do this by using Virtual Hosts
- Web Servers will check the hostname that is requested from HTTP Headers and matches that against their Virtual Hosts
- (these hosts are just text-based config files)
- If the Web Server finds a match, then the correct website will be provided
- If no match is found, then the default website will be provided instead
- Virtual Hosts can have their root directory mapped to different locations on their hard drives. 
	- ie abc.com being routed to /var/www/website_abc
		- def.com being routed to /var/www/website_two
	- There is no limit to the number of different websites you can host on a Web Server

Load Balancers (sometimes one web server might no longer do the job effectively)
- Load balancers provide two main features
	- Ensuring high traffic websites can handle the load
	- Providing a failover if a server becomes unresponsive
- When a request comes in
	- The load balancer will receive your request prior to the Web Server(s) in question
	- Then it will forward the request to one of the multiple servers behind it
	- It will use different algorithms to help it decide which server is best to deal with the request
		- Round-robin
			- Sends requests to each server in turn
		- Weighted
			- Checks how many requests a Web Server is currently dealing with and sends it to the least busy server
	- Health Check
		- Load Balancers also perform periodic checks with each server to ensure they are running correctly 
		- If a server doesn't respond appropriately or even if at all, the Load Balancer will stop sending traffic until it responds appropriately again
	- CDN - Content Delivery Networks
		- A CDN can be an excellent resource for cutting down traffic to a busy website
		- It allows you to host static files from your website
			- JavaScript
			- CSS
			- Images
			- Videos
			And host them across thousands of servers across the world
		- When a request comes for one of the hosted files, then the CDN works out where the nearest server is physically located and sends the request there instead of one 'too far away' as such
	- Databases (DB)
		- Websites will often need a way/method of storing information for their users
		- Web Servers can communicate with databases to store and recall data from them
		- DBs can range from a simple plain text file to complex clusters of multiple servers providing speed and resilience 
		- Common DBs:
			- MySQL
			- MSSQL
			- MongoDB
			- Postgres
			- and much more
	- WAF - Web Application Firewall)
		- WAFs sit between your web request and the Web Server
		- Designed to protect the Web Server from hacking or DOS attacks
		- It will analyse requests for common attack techniques
			- Whether the request is coming from a real browser or a BOT
			- Rate Limiting
				- Checks whether an excessive amount of web requests are being sent by utilising something called Rate Limiting
				- Will only allow a certain amount of requests from an IP per second
		- If a request is deemed as a potential attack, then it will never be sent to the Web Server

Static vs Dynamic Content
- Static Content
	- Content that never changes
		- pictures
		- javascript
		- CSS
		- Can also be HTML that never changes
		- etc
- Dynamic Content
	- Content that does and will change depending on the request that is being received
		- Content that is added by the developer of the website, the site will then show you the updated changes
		- Searching for content on a website and displaying the results
	- These types of changes to content are being done on what is called the Backend of a system with the use of scripting languages such as PHP
	- You can't view a websites source code and see what's happening in the backend (this is kept on the server)
	- Everything you see on the website and on your browser client is what you can consider as the Frontend

Scripting and Backend Languages
- These are what make a website interactive to the user 
- Examples
	- PHP 
	- Python
	- Ruby
	- NodeJS
	- Perl

Step by step: (please take note that there are steps in the relaying of messages back to the web browser client that are not listed here - this is from )
- Request a URL(website name) in the web browser client
- Check local cache for an IP Address
- Check your recursive DNS Server for IP addresses
- Query root server to find the relevant Authoritative DNS Server
- Authoritative DNS Server advises what the IP address is for the website
- Request passes through a Web Application Firewall (WAP)
- Request passes through a Load Balancer
- Connect to the Web Server on either port 80 or 443
- Web Server gets the GET request
- Web application talks to a database
- Your browser renders the HTML into a viewable website

