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
- 