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