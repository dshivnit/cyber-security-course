Four Areas:
1. Operations
	- Contains all the operations that CyberChef is equipped to perform
	- ie from morse code, URL encode, to/from Base64, to/from hex, to/from decimal, rot13, heaps more
2. Recipe
	- Ability to define whatever operation(s) have been selected and their arguments
	- Ability to save recipe's for later use etc
3. Input
	- The data/input that you want to work with
	- open folder as input
	- open file as input, so on
4. Output
	- Presents the data processing result
	- you can save, copy raw output, replace input with output, etc

General Thought Process:
- Set a clear objective
- Put your data into the input area
- Select the operation(s) you want to use
- Check output to see if it's applicable, correct
- Most likely repeat several times until you get what you're looking for - or seek another solution for your intentions
- Keep practicing

Some Uses
- Extractors
	- IP Addresses
	- URLs
	- Email addresses
- Date and Time
	- From UNIX Timestamp
	- To UNIX Timestamp
- Data Formatting
	- From Base64
	- URL decode
	- From Base85
	- to Base62

Generic approach to converting to Base64
- Take you word or characters and find out the binary equivalent to what they would be
	- refer to a ASCII table 
- Merge the binary together
- Divide and convert to decimal
	- Break the binary into 6 characters each - 6-bit characters
	- Calculate the decimal value of each 
		- ie 010101 = 21
- Identify what those decimals point to in a base64 index table
	- https://en.wikipedia.org/wiki/Base64
- Combine the characters together and there you go - your manually converted Base64 representation of whatever you had typed. GG

URL Encoding
- Default character set in HTML5 is UTF-8
- refer to https://en.wikipedia.org/wiki/Percent-encoding








