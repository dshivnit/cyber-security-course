https://tryhackme.com/r/room/sqlmapthebasics
https://portswigger.net/web-security/sql-injection/cheat-sheet

- A login page for a web-system that doesn't incorporate 'proper' sanitisation and validation of data entered into username and password fields for example - can lead to the system becoming compromised. 
- Let's say we have such a system. An attacker attempts to login as "bob" (which is a legitimate username in the web-system)
- And the attacker enters `blahblah' OR 1=1;-- -` as the password
- The web-system will send a query similar to this to the related database:
	- `SELECT * FROM users WHERE username = 'bob' AND password = 'blahblah' OR 1=1;-- -';`
	- The database will see that bob is listed in the users table, however `blahblah` isn't the respective password for bob, BUT, there is another condition now, the `OR` condition which states `1=1` .. Which is obviously true so it will grant access for the said attacker to login
	- The `-- -` at the end of the query would comment anything after the `1=1`, meaning that the query would be executed successfully
	- The attacker has now logged in as user `bob` ... The THM link above explains this much better, although I hope you get the drift and these are notes more for me. :) 
		- *If you are reading, then kudos to you! (I at some stage will be revising all these notes into something a bit more, organised.)*

SQLMap
- An automated tool that is used for detecting and exploiting SQL Injection vulnerabilities in web-applications
- Simplifies the process of identifying these vulnerabilities
	- A sense of automation if you will
- `sqlmap --wizard`
- `--dbs`
	- Will enumerate/extract all DB names
- `-D database_name --tables`
	- Will then allow you to enumerate the tables in those DBs
- `-D database_name -T table_name --dump`
	- Will now allow the contents/records of that table to be enumerated

- First step is to look for a vulnerable URL or request
- Some URLs use GET requests/parameters to retrieve data
	- `http://sqlmaptesting.thm/search?cat=1`
	- uses a parameter `cat` that would take the value `1`
	- After searching for a cat, the URL responds with something like `cat=1` in the URL.. (The result of the GET Request )
- If you see any web-application using GET parameters in the URL to retrieve data, you can test that URL with the -u flag in the SQLMap tool (with permission from the systems owner!)
	- This is considered to be what is called `HTTP GET-based` testing
- Example:
	- `sqlmap -u http://sqlmaptesting.thm/search/cat=1`
		- (not going to include the results of the test, but just an example of a GET-based test command)
	- `sqlmap - u http://sqlmaptesting.thm/search/cat=1 --dbs --level=5`
		- Will get you additional DB names that the web-system connects/queries with
	- `sqlmap -u http://sqlmaptesting.thm/search/cat=1 -D users --tables` --level=5
		- Now we can get some tables from one of those DBs, in this case `users`
		- `--level=5` can be used to extract all the available tables of a database
	- `sqlmap -u http://sqlmaptesting.thml/search/cat=1 -D users -T table-name --dump`
		- We can now `dump` the contents of the stated table, perhaps get some username and passwords (or password hashes) 
- POST-based testing can also be done
	- login forms, registration forms, that kind of thing
	- A POST Request needs to be intercepted on the login or registration page and saved as a txt/text file. 
	- Then:
		- `sqlmap -r intercepted-post-request.txt`
		- *more to cover on this*
- Getting the GET Request
	- IF the GET request doesn't show up in the URL after filling out some fields in a form on a web-page
		- One can try to inspect the page > network tab > enter in some random input into the text-fields > and see if the GET request shows up in the Network tab (general flow - browser dependant re the process here)
	- Make sure to put the URL between single-quotes to avoid errors with characters like `?`
	- 

Examples:
- The below is from a sql log file:
- ...`[GET /products.php?q=books' UNION SELECT null, null, username, password, null FROM users--` ...
	- The calling of the `'` before the `UNION SELECT` - the query can sometimes escape the legitimate SQL query with that single quote
	- Thus leading to an injected SQL query (selecting data related to Users from the "users" Table.)
- 