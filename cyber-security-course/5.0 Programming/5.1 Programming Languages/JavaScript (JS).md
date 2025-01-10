*Add more when you can and touch up on your JavaScript*
- Used to control the functionality of web pages
- A page would not have interactive elements without JS
- Updates the page in real-time
- the "script" tag can be included with the src attribute, ie:
	- script src=" /location/of/javascript_file.js" then /script
		- Don't forget the less than and greater than symbols (both at the end of the src tag, as well as in the ending script tag)

---

Example: 
(always check for what functions do if you're unsure)
document.write(unescape(atob(b64)));
- atob() 
	- A built-in JavaScript function to decode a base64-encoded string. 
	- This function passes in the b64 variable that was previously declared as its input
- unescape()
	- Function converts any escaped characters in the decoded string into their original form. 
	- This is necessary because base64-encoded strings may contain special characters that must be appropriately formatted before being displayed on a webpage
- document.write()
	- Function displays the decoded and unescaped string on the webpage where the code is executed
  Good fun. 

Variables
- Containers that allow you to store data values in them
- Three ways to declare variables
	- `var`
		- Function-scoped
	- `let`
		- Block-scoped
	- `const`
		- Block-scoped
- Block-scoped variables offer better control over variable visibility within specific code blocks

Data Types
- Data types define the type of value a variable can hold
- Examples:
	- `string`
	- `number`
	- `boolean`
	- `null`
	- `undefined`
	- `object`
	- `arrays`

Functions
- Represents a block of code designed to perform a specific task. 
- Code is grouped to perform a similar task
	- ie, printing results for an exam that students have taken. You can have a function to print the results so that you don't have to repeatedly write similar code for every single student in the class

Loops
- Allow code to be run multiple times as long a particular condition is true
- Common loops:
	- `for`
	- `while`
	- `do..while`

Request-Response Cycle
- When a browser sends a request to a web-server, and the server responds with the requested information.

- JS is an interpreted language, so it runs directly on the client's web-browser without any prior compilation on the server-side (mainly)
-  You can run JS on the fly to test things in a web-browser
	- Just go to the console and run some code in there

- Usually JS works with HTML and CSS to create dynamic and interactive content as opposed to rendering it

- Internal JS
	- Refers to the embedding of JS code directly within an HTML document. 
	- Preferable for beginners because it allows them to see how the script interacts with the HTML code
	- Script is inserted between the `<script></script>` tags 
		- Which can be within the `<head>` and/or `<body>` tags
		- In `<head>` if the script needs to be loaded before the page is rendered
		- In the `<body>` tag where it can be used to interact with elements as they load on the web-page
- External JS
	- Creating and storing JS Code in a separate file which ends with a `.js` file extension. 
	- Keeps the HTML document clean and organised. 
	- The external JS file can be stored or hosted on the same web server as the HTML document or stored on another web server

Abusing Dialogue Functions
- One main function of JS is to present dialogue boxes for users to interact with, and to also dynamically update content on the web- pages themselves. 
- JS has built-in functions, such as:
	- `alert`
		- `alert("hello there human");`
		- This dialogue function will have only an OK option for the user to choose
	- `prompt`
		- `name = prompt("What is your real name?")`
			- `alert("Hello " + name)`
		- This dialogue function will have an OK and a Cancel option for the user to choose from
	- `confirm`
		- `confirm("Ready to go?")`
		- This dialogue function will have an OK option which will return a true value if clicked, and a Cancel option which will return a false value if clicked by the user
	- That are able to facilitate the above functionalities
	- They allow developers to be able to display messages, gather input, and obtain user confirmations.
- If not implemented securely, however, attackers may be able to exploit these features to carry out XSS (cross-site scripting) attacks and the like.
- Exploiting

Control Flow Statements
	- `if` `else`
	- `while`
	- `do` `while`
	- `for`

- Minification
	- The process of compressing JS files by removing all unnecessary characters, such as spaces, line breaks, comments, and shorting variable names at times too
	- Helps to reduce the file size and improves loading times of web-pages
		- Especially for prod environments
- Obfuscation
	- Can make code harder to read
	- Sometimes by adding undesired code, renaming variables and functions to meaningless names
	- There could also be some dummy code in there
	- This kind of thing - whatever it takes to the make the code obfuscated

Best Practices
- Avoid Relying on Client-Side Validation only
	- Users can manipulate the client-side code
	- You can do data validation on the server-side, where the User is highly unlikely to have administrative privileges or access to
- Refrain from Adding Untrusted Libraries
	- Do your due diligence before trusting outside/third-party scripts - they could be bogus and/or malicious
	- Also bear in mind that those scripts, since they are external to your web-system, could end up getting compromised somewhere later down the line of time
		- How will you know if they have? Since they've been compromised, you're more than likely to have your system get pwnd too.
- Avoid hard-coded secrets
		- API Keys
		- Access Tokens
		- Credentials
	- The above should never be hard-coded into your code for the public to see visibly blatantly 
- Minify and obfuscate your code
