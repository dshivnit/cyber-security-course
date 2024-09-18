*(This will be messy for a while until I go through and edit stuff and make things tidier - bear that in mind please, danke! :) )*
- CHMOD Octals (not sure if octals is the right term but I'm going with it for now)
	- - r
		- 4
	- w
		- 2
	- x
		- 1
	- rwx
		- 7
	- rw
		- 6
	- rx
		- 5
	- wx
		- 3
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
	- wc
	- 

- `man`
	- `/usr/share/man`
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
- Symbolic Links (Symlinks)
	- Soft / Symbolic link - contains the original file name. When you access it, Linux will realise that it is a symbolic link and read the original file name, then automatically access that file
	- `ln -s /path/to/file_or_directory path/to/symlink`
		- Creates a symlink
	- `ln -sf /path/to/new_file path/to/symlink`
		- Overwrites an existing symlink to point to a different file
- Hardlink
	- An alternate address that indexes that data -- accesses to the hard link and accesses to the original file are completely identical, in that they immediately yield the necessary data 
	  `ln /path/to/file path/to/hardlink`
	  
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


- The `dd` command - to wipe a disk
	- `sudo fdisk -l`
		- You will then see a list of the drives that are connected to the system
		- `/dev/sda
			- Now this is the drive itself
			- You may then have other listings associated with sda, ie
				`/dev/sda1`
				`/dev/sda2`
				so on
		- `/dev/sdb`
		- and so on
	- `sudo fdisk /dev/sdb`
		- Some questions will be asked
			- `n` for a new partition
			- default default
			- `w` to commit the write partition
	- Format it
		- `sudo mkfs -t ext4 /dev/sdb1`
			- We're making a filesystem here referenced by sdb1 with a filesystem type of ext4
			- Now there's a usable filesystem
	- Now let's make a directory somewhere in the system that will mount this drive
	- `sudo mount /dev/sdb1 /datavol`
		- (make sure you created that datavol directory first :) )
	- Put some stuff in there
	- Now let's wipe it
	- `sudo dd if=/dev/urandom of=/dev/sdb1`
	- Now let's unmount that filesystem
	- `sudo umount /dev/sdb1`
	- Chur (means cheers, good stuff, have a good one, - in NZ :) )

- If statements in Bash
``` bash
	if [condition];
	then
		statement
	elif [condition]; then
		statement
	else
		do this by default
	fi
```
``` bash
	num=123
	if [ $num -gt 100 ]; then
		echo "$num is higher than 100"
	elif [ $num -lt 100 ]; then
		echo "$num is lower than 100"
	else
		echo "Toodles"
	fi
```
- AND, OR, GREATER THAN, LESS THAN
	- AND `-a`
	- OR `-o`
	- Greater than `-gt`
	- Less than `-lt`

- `sed`
	- `echo $SOMETHINGNEW="A quick brown fox jumps over the lazy dog"
	- `echo $SOMETHINGNEW | sed 's/ //g'`
		Aquickbrownfoxjumpsoverthelazydog
	- /`what to find to replace`/`replace what is found with this`/
	- The forward slashes can be whatever character, just used slashes in this example
	- the s above I think is for separator
	- the g is for global
	- if you don't have the 'g' then only the first character character to replace will be replaced

- `jq`
	- tool for parsing and manipulating JSON data in Linux
	- Allows you to extract, filter, map and transform JSON data, making 

- Shell Expansions
- https://www.gnu.org/software/bash/manual/html_node/Shell-Expansions.html
	- Brace Expansion
		- `echo a{d,c,b}e` - ade ace abe
		- `mkdir {old,new,dist,bugs}
			- Creates all four directories simultaneously
		- `mv {1,3} bugs`
			- Will move files 1 and 3 into the bugs folder
	- Shell Parameter Expansion
		- 