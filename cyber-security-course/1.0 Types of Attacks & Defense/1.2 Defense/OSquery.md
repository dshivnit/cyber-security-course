https://tryhackme.com/room/osqueryf8
https://www.osquery.io/

- Open source agent created by Facebook back in 2014
- Coverts the operating system into a relational database
- Allows questions to be asked using SQL queries
	- Like returning the list of running processes,
	- A user account created on the host
	- The processes of communicating with certain suspicious domains
- Installable on Win, Linux, MacOS and FreeBSD

- Interactive mode
	- Terminal > `osqueryi`
	- `.help` is your friend
	- `.tables` to list all the tables that can be queried
	- To see what tables are associated with another table, format:
		- `.tables process`
		- `.tables user`
	- List a tables schema with 
		- `.schema <table-name>`
	- `select column1, column2, from table-name`
	- `.help`
		- `mode MODE (csv, column, line, list, pretty)`
			- Line can be a neat way to lay out findings/results of queries in a lined format as opposed to in the usual SQL table structure 
				- depends on what you want
		- 

- Schema Documentation
- https://osquery.io/schema/5.5.1/
	- Interactive way to see the schema of the various tables that can be displayed in osquery (check it out)
	- Note that you can select multiple OS variants (not just one) so you can see common tables between the various platforms that are available

- Creating SQL Queries
	- Keep in mind that the SQL language in osquery is not the full SQL language but a superset of the SQLite variant
	- `SELECT` is the main statement that one will be using
		- However, `UPDATE` and `DELETE` can be possible as well
		- Only if one is creating run-time tables (VIEWS) or using an extension if it supports these
	- `FROM` and of course the semi-colon `;`
- Exploring Installed Programs
		- `.schema programs` so you know the layout of the table that you will be working with
		- Or of course also look at the documentation for schema above
	- `SELECT * FROM programs LIMIT 1;`
	- `SELECT COUNT(*) FROM programs;`
	- `SELECT * FROM users WHERE username = 'Bobba';`
- WHERE Filters
		- `=`
		- `<>` (not equal)
		- `>`, `>=`
		- `<`, `<=`
		- `BETWEEN` (a range)
		- `LIKE` (pattern wildcard searches)
		- `%` (wildcard, multiple characters)
		- `_` (wildcard, one character)
- Matching Wildcard Rules
	- `%` - Match all files and folders for one level
	- `%%` - Match all files and folders recursively
	- `%abc` - Match all within-level ending in "abc"
	- `abc%` - Match all within-level starting with "abc"
- Matching Examples
	- `/Users/%/Library`
		- Monitor for changes to every user's Library folder, but not the contents within
	- `/Users/%/Library/`
		- Monitor for changes to files within each Library folder, but not the contents of their subdirectories
	- `/Users/%/Library/%`
		- Same, changes to files within each Library folder
	- `/Users/%/Library/%%`
		- Monitor changes recursively within each Library folder
	- `/bin/%sh`
		- Monitor the `bin` directory for changes ending in `sh`
- Some tables need a `WHERE` clause - like the `file` table
	- Otherwise you'll get errors
- Joining Tables using a JOIN Function
- https://osquery.readthedocs.io/en/stable/introduction/sql/
	- Two tables can be joined based on a column that is shared between the two tables
	- For example the `uid` between the Users and the Processes table can be joined
	- `SELECT p.pid, p.name, p.path, u.username FROM processes p JOIN users u on u.uid=p.uid LIMIT 10;`
