*Note, I'm putting this here based upon the fact that a SQL Server is normally housed on a machine on a given network - this section will not delve into the intricacies of the language itself and what its purpose is- you should already know. I will fill in details in their relevant sections (Programming Languages, Databases) at a later date. :) 

- MySQL is made up of the Server and Utility Programs that help in the admin of its databases
- The Server handles all DB instructions like:
	- creating
	- editing
	- and accessing data
- IT takes those instructions and communicates them using the MySQL protocol. 
- Basic process:
	- MySQL creates a DB for storing and manipulating data
	- Defines relationships between tables
	- Clients make requests by making specific SQL queries
	- The Server will respond to the Client with whatever information (well data...) has been requested
- Normally housed in what is called the LAMP package:
	- Linux
	- Apache
	- MySQL
	- PHP
- It can however run on various platforms, Win, Linux, etc
- MySQL Schema
	- synonymous with database
	- You can replace DATABASE with SCHEMA
		- CREATE SCHEMA
				- as opposed to CREATE DATABASE
	- Other DB's differentiate between the two pretty distinctively
- Hashes
	- MySQL hashes can be used in a number of ways
		- Index data to a hash table
		- Each has a UID (Unique ID in this case) that points to the original data
		- An index is created that is significantly smaller than the original data
			- Allowing for search queries to be more efficient when looking up and wanting to access values

Tools:
- default-mysql-client
	- mysql -h (db_host an ip will do) -u (username) -p (password)
		- You'd probably be prompted for a password but I put that in there anywho
- metasploit (msfconsole)
	- This is a pretty structured and well documented program
		- Read up on it if you haven't already and refer to notes as per whatever your process is
	- mysql_sql
		- use mysql_sql
		- info
		- info -d
	- mysql_schemadump
	- mysql_hashdump
- nmap mysql-enum script (if you don't want to take the metasploit route)
