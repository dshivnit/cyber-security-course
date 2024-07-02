Resources
- https://github.com/krp/python-examples
- https://tryhackme.com/r/room/pythonbasics

- Data Types
	- String
		- Used for combinations of characters, such as letters or symbols
	- Integer - Whole numbers
	- Float - Numbers that contain decimal points or for fractions
	- Boolean - Used for data that is restricted to True or False options
	- List - Series of different data types stored in a collection

- Mathematical Operators
	- Addition ( + )
	- Subtraction ( - )
	- Multiplication ( * ) 
	- Division ( / )
	- Modulus ( % )
		- 10%2=0
	- Exponent ( ** )
	
- Comparison Operators
	- Greater Than ( > )
	- Less Than ( < )
	- Equal To ( == )
	- Not Equal To ( != )
	- Greater Than or Equal To ( >= )
	- Less Than or Equal To ( <= )

- Logical Operators
	- Logical operators allow assignment and comparisons to be made and are used in conditional testing (such as IF statements)
		- Equivalence ( == )
		- Less Than ( < ) 
		- Less Than or Equal To ( <= )
		- Greater Than or Equal To ( >= )
		- Greater Than ( > )
			- Example:
				- if x == 5
				- if x >= 5

- Boolean Operators
	- Boolean operators are used to connect and compare relationships between statements. Like an IF statement, conditions can be TRUE or FALSE.
		- Example:
			- if x >= 5 AND x <= 100:
				- Returns TRUE
			- if x == 5 OR x == 100:
				- Returns TRUE
			- if NOT y:
				- Returns TRUE IF the y if the y value is False
	
- Variables
	- Allow you to store and update data in a computer program. 
	- You have a variable name and you store data to that name
	- Example: 
		- food = " ice cream " 
		  (string data type)
		- money = 20000000 
		  (number data type)
	- You can change the value in a variable throughout your program.
		- Example:
			age = 30
			age = age + 1
			print ( age ) 
		- The above example will output: 31
	
- Loops
	- Loops allow programs to iterate and perform actions a number of times. There are two types of loops:
		- for
			- Example
				websites = ["facebook.com", "google.com", "amazon.com"]
				for site in websites:
					print(site)
			- The above for loop will run three times, outputting each website in the list. 
		- while
			- Example
				i = 1
				while i <= 10:
					print( i )
					i = i + 1
			- This loop will run 10 times, outputting the value of i each time it iterates (or loops). 
			- It will keep running until the value of i is greater than 10
	- Example:
		for i in range(5):
			print ( i )
	- This example will print numbers from 0 to 4
	- Take note that Python like most other programming languages consider 0 to be the 'starting number'
	
- Functions
	- Some of your code may start to get repetitive, this is where Functions come into play
	- A block of code that can be called at different places in your program
	- You could have a function to work out a calculation such as a distance between two points on a map or output formatted text based on certain conditions. 
	- Having functions removes repetitive code. 
	- Functions can be called upon many times. 
	- Example
		def sayHello( name ):
			print("Hello " + name + "! Nice to meet you.")
		sayHello("Shiv") # Output here would be "Hello Shiv! Nice to meet you"
	- def
		- keyword that indicates the beginning of a function
	- name
		- the def function call is then followed by a name that the developer will chose
		- In the example above it is sayHello
		- It can be anything, and this is what will be called in other parts of the program to call the function's code
	- A colon marks the end of a function header
		- Similar to IF statements and ELIF statements
	- There are always indents following a colon from what I've observed
- Functions can return a result
	- Example
		def calcCost(item):
			if ( item == "banana"):
				return 3.99
			elif ( item == "tomato"):
				return. 5.99
		initSpend = 20
		initSpend = initSpend + calcCost("tomato")
		print(" You have spent " + str(initSpend )) # this will print 25.99
- ALWAYS KEEP AN NOTE ON INDENTS!

- Data Structures

- If Statements

- Files
	- You can read and write from files. 
	- In CyberSec it's common to write a script and import or export it from a file
		- Whether that be as a way to store the output of your script or to import a list of 100s of websites from a file to enumerate. 
	- Example:
		f = open( "file_name", "r" )
		print( f.read( ) )
	- The 'r' parameter in the above example is for read
	- 'w' would be for write
		- Used for creating a new file
	- 'a' would be for append
		- Adding to an existing file

- Imports
	- Importing Python libraries (https://docs.python.org/3/library/index.html) 
		- Others: https://docs.pwntools.com/en/stable/
		- https://scapy.readthedocs.io/en/latest/introduction.html
	- You're importing functions that you can use that have already been written (why recreate the wheel unless you make a more efficient one.
		- Examples:
			- datetime
				import datetime
				current_time = datetime.datetime.now()
				print(current_time)
			- 
