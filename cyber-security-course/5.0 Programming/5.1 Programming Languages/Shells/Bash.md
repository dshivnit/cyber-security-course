- Some Commands:
	- date
	- pwd
	- ls
	- echo
	- man
	- which
	- read
	- line
	- while
		- do
		- done
	- 

- Variables
	- There are no Data Types in Bash
	- Variables can store numeric values, individual characters, or strings of characters
	- Some example Variable assignments:
		- word=Whatever
		- whatever=$word
	- You can access Variables by appending a `$` to the Variable name
		- in example `echo $whatever`
	- Variables should either start with a underscore (`_`) or a letter
	- Variable names can contain:
		- letters
		- numbers
		- underscores
		- no spaces
	- They are case-sensitive

- Command-line Arguments
	- `$1` denotes the initial argument passed
	- `$2` denotes the second argument passed, and so on
	- `./script_name arg1 arg2 arg3`
	- `echo "$1 $2 $3"` 
		- Will print arg1 arg2 arg3 on to the command-line

- Displaying Output
	- Printing to the terminal
		- `echo "Hello World!"`
			- Will print Hello World to the terminal
- Writing to a File:
	- `echo "Hello World!" > sample.txt`
		- Overwrites whatever is in sample.txt
	- `echo "Hello World!" >> sample.txt`
		- Appends to the end of sample.txt
- Redirecting Output:
	- `ls > files.txt`
		- Will pass whatever the result of the `ls` command is into a file called files.txt
		- Take note of the `>` and the `>>`'s 
	- 

- `read`
	- Can read from a file
		```
		while read line
		do
			echo $line
		done < input.txt```
- 
	- The above will read through each line in the file `input.txt` and echo it
	- 
- Scripts
	- Normally the `.sh` extension is used, however, not required
	- Will start with a `!#/bin/bash`
	- 