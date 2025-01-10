
- MySQL
- MongoDB
- Oracle Database
- Maria DB

Benefits
- Fast
	- Massive batches of data can be returned almost instantaneously (lol) due to how little storage space is used and high processing speeds
- Easy to Learn
	- Plain English
- Reliable
	- Can guarantee a level of accuracy when it comes to data by defining a strict structure where data will be stored/inserted
- Flexible
	- Data analysis
	- Tailored queries
	- Vast data analysis is possible

Basics
- `CREATE DATABASE database_name;
- `SHOW DATABASES;`
- `USE database_name;`
- `DROP database_name;`
	- This will remove the DB
- `CREATE TABLE table_name ( 
	`column_1_name data_type,
	`column_2_name data_type,
	`column_3_name data_type
	`);`
	- SQL can support over 1000 columns
	- Example:
		```SQL
		CREATE TABLE cologne_stock (
		cologne_id INT AUTO_INCREMENT PRIMARY KEY,
		cologne_maker VARCHAR(255) NOT NULL,
		cologne_name VARCHAR(255) NOT NULL,
		cologne_purchase_date DATE
		);
		```
- `SHOW TABLES;`
- `DESCRIBE table_name;` OR `DESC table_name;`
	- Will show what columns and their specifications and datasets are in a table
- `ALTER TABLE table_name;`
	- When you need to modify the table structure, renaming a column, adding/removing columns, changing data types for a column..
- `DROP TABLE table_name;`

- CRUD Operations (Create, Read, Update, Delete)
	- Create Operation
		`INSERT INTO table_name (column1_descriptor, column2_descriptor, column3_descriptor)`
		`VALUES (column1_data, column2_data, column3_data`);
		- Bear in mind that CHARs data-types will need to be inserted with double-quotes around them, as with date
	- Read Operation
		- `SELECT * FROM table_name;`
		- `SELECT column_name, column_name FROM table_name`
	- Update Operation
		`UPDATE table_name`
		`SET column_name = new-data-for-the-row`
		`WHERE column_name = row-identifier-in-column;`
	- Delete Operation
		- `DELETE FROM table_name WHERE id = 1`

Clauses
- A part of a statement that specifies the criteria of data that will be manipulated
	- Helps to define the type of data and how it should be retrieved/stored
	- `FROM`
	- `WHERE`
	- `DISTINCT`
		- Used to avoid displaying duplicate records when running a query
		- `sql SELECT DISTINCT column_name FROM table_name;`
	- `GROUP BY`
		- Aggregates data from multiple records and will group the query results in columns
		- Good for aggregating functions
			```sql
			SELECT column_name1, COUNT(*)
			FROM table_name
			GROUP BY column_name1;
			```
	- `ORDER BY`
		- Used to sort the records returned by a query in either ascending (`ASC`) or descending (`DESC`) order
			```sql
			SELECT *
			FROM table_name
			ORDER BY column_name_date ASC;
			```
	- `HAVING`
		- This clause is used with other clauses to filter groups/results based on a particular condition
		- HAVING filters results after data aggregation has taken place
			```sql
			SELECT column1, COUNT(*)
			FROM table_name
			GROUP BY column1
			HAVING column1 LIKE '%something%';
			```
		- the `'%something%'` has two wildcards around it, so whatever has "something" in it will be displayed and the count of how many times in the table will be shown as per the query above

Operators
- Ways of filtering and manipulating data
- LOGICAL Operators
	- Return a boolean value
	- LIKE
		- Used in conjuction with WHERE
		- Filter for specific patterns within a column
			```sql
			SELECT *
			FROM table_name
			WHERE column_name LIKE "%something%";
			```
		- Just like the previous example but describing it further, lel. (please remember, I'm notetaking here for this particular part of this repo - at some stage the major clean up will happen -- maybe.. I'll probably just end up loading code I've created and forget about this book, but - let's see :) )
	- AND
		- Uses multiple conditions in a query and will return TRUE if all of them are as such, true
		- More specific when compared to LIKE
			```sql
			SELECT *
			FROM table_name
			WHERE column_name = "something specific" AND column_name2 = "something specific as well";
			```
	- OR
		- Combines multiple conditions within queries and returns TRUE if at least *one* is true.
			```sql
			SELECT *
			FROM table_name
			WHERE column1 LIKE "%something%" OR column1 LIKE "%something_else%";
			```
	- NOT
		- Where we don't want a result being pulled from the query
			```sql
			SELECT *
			FROM table_name
			WHERE NOT column1 LIKE "%something%";
			```
	- BETWEEN
		- Pulls results for values that exist within a defined range
			```sql
			SELECT *
			FROM table_name
			WHERE column1_like_id BETWEEN 2 AND 4;
			```
- COMPARISON Operators
	- Equal To (=)
		```sql
			SELECT *
			FROM table_name
			WHERE column_name = "something specific" AND column_name2 = "something specific as well";
			```
	- Not Equal To (!=)
		- Same as above but change the ='s to !='s 
	- Less Than (<)
		- Put them in where the other comparison operators would go - refer to the examples above
	- Greater Than (>)
		- As above
	- Less Than or Equal To || Greater Than or Equal To (<= || >=)
		- As above

Functions
- Can assist in streamlining queries and operations as well as with manipulating data
- String Functions
	- `CONCAT()`
		- Used to add two or more strings together
			```sql
			SELECT CONCAT(column1, "is a type of ", column2, " something.") AS query_name FROM table_name;
			```
	- `GROUP_CONCAT()`
		- Used to concatenate data from multiple rows into one field
			```sql
			SELECT column1, GROUP_CONCAT(column2 SEPARATOR ", ") AS query_name FROM table_name GROUP BY column1;
			```
	- `SUBSTRING()`
		- Retrieves a substring from a string within a query, starting at a determined position. 
		- Length can be specified as well
			```sql
			SELECT SUBSTRING(column1, 1, 4) AS column1_sub_identifer FROM table_name;
			```
			- Example:
				```sql
				SELECT SUBSTRING(published_date, 1, 4) as published_year FROM books;
				```
				Returning the first four characters of each row from the published_date column. (the example would have returned the year substring from rows in the published_date column, and then put it in to a query named published_year)
	- `LENGTH()`
		- Returns the number of characters in a string
		- `SELECT LENGTH(column_name) AS query_name FROM table_name`

Aggregate Functions
- Aggregate the value of multiple rows within one specified criteria in the query
- Can combine multiple values into one result
- `COUNT()`
	- `SELECT COUNT(*) AS column_name_like_total_records FROM table_name_like_total_number_of_records;`
- `SUM()`
	- Sums all values (not NULL) of a defined column
	- `SELECT SUM(column_name) AS total_column_name FROM table_name;`
- `MAX()`
	- Defines the maximum value in a given column
	- `SELECT MAX(ie_date_column) AS latest_date FROM table_name;`
- `MIN()`
	- As above

- Example:
	```sql
	SELECT GROUP_CONCAT(name SEPARATOR " & ") FROM hacking_tools WHERE NOT amount LIKE "%0";
	```
	- This will list (in one row) all tools that have an amount that doesn't end with 0 







{"email":"' or 1=1--", "password":"a"}
	' 
		will close the brackets in the query
	or
		will return true if either side of it is true
	1=1
		is always true
	-- 
		will comment out anything that follows it
