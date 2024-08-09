Examples:
- The below is from a sql log file:
- ...`[GET /products.php?q=books' UNION SELECT null, null, username, password, null FROM users--` ...
	- The calling of the `'` before the `UNION SELECT` - the query can sometimes escape the legitimate SQL query with that single quote
	- Thus leading to an injected SQL query (selecting data related to Users from the "users" Table.)
- 