 Hyper-Text Transfer Protocol
	  Port 80
	  The protocol that is used whenever you visit/view a website
	  Developed by Tim Berners-Lee and his team between 1989-1991

Elements (or HTML Tags)
	- Building blocks of HTML pages and tell the browser how to display content that is requested
	- Identified by a less-than and greater-than symbol
	- !DOCTYPE html
		- Defines the page is an HTML document
		- Helps with standardisation across different browsers
	- html
		- the root element of the HTML page
		- All other tags/elements come after this
	- head
		- Contains information about the page (ie, its title)
	- body
		- defines the body of the page, only the content that is within the body are displayed on the client-side browser
	- h1
		- defines a large heading
	- p
		- Paragraph
	- There MANY more elements, these are just the basic ones
- HTML Entity Encoding
	- HTML Entities are special sequences of characters used to represent reserved characters and other special characters in HTML
		- example: &#80;&#97;&#114;&#114;&#111;&#116;&#80;&#111;&#115;&#116;&#32;&#83;&#101;&#99;&#117;&#114;&#101;&#32;&#87;&#101;&#98;&#109;&#97;&#105;&#108;&#32;&#76;&#111;&#103;&#105;&#110
		- These can be decoded with tools like CyberChef
	- 

Sensitive Data Exposure
- When a website doesn't properly protect (or remove) sensitive clear-text information to the end-user, usually found in the sites frontend source code
	- There could be HTML comments with temporary login credentials
	- If you viewed the pages source code and found this, you could then use these creds to log in else where on the application (or worse, access other backend components on a website)
- Whenever you're assessing a web application for security issues, one of the first things you should do is review the page source code to see if you can find fany exposed login credentials or hidden links

HTML Injection (also put this into Types of Attacks)
- A vulnerability that occurs when unfiltered user input is displayed on the page
- if a website fails to sanitise user input (filter any "mailicious" text that a user inputs into a website) and that input is used on the page, an attacker can inject HTML code into a vulnerable website
- Input Sanitisation
	- important in keeping a website secure
	- Removing any unsafe characters from user inputs
	- Validating will check to see if the data is in the expected format and type
	- Sanitizing modifies the input to ensure it's in a valid format for display, or before insertion in a database

- 