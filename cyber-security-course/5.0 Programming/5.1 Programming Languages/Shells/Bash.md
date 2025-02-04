*(This will be messy for a while until I go through and edit stuff and make things tidier - bear that in mind please, danke! :) )*
- 
- Permissions
	- CHMOD Octals (not sure if octals is the right term but I'm going with it for now)
		- r
			- 4
			- user/group/other - ability to read the file (or list files in the directory)
		- w
			- 2
			- user/group/other - ability to modify the file (or create/delete files that are in the directory)
		- x
			- 1
			- user/group/other - ability to execute the file, ie run it (or be able to enter the directory, change to it `cd`)
		- rwx
			- 7
			- user/group/other
		- rw
			- 6
			- user/group/other
		- rx
			- 5
			- user/group/other
		- wx
			- 3
			- user/group/other
		- CHMOD Characters (not sure if characters is the right term, but I'm going with it for now)
			- Examples:
				- `chmod u+rwx 'file-name'`
				- `chmod g+rx 'file-name'`
				- `chmod o-rwx 'file-name'`
				- `chmod go-rwx 'file-name`
					- toggling for both Group and Other to not have any permissions to said file-name
				- `chmod u=rw 'file-name'`
					- Note the `=` as opposed to `+` or `-` 
					- This overwrites any current permissions of the file for the user owner of it
				- `chmod a=rwx 'file-name'``
					- `a` denoting all, user, group and other :) 
				- `chmod u=rwx,g=r,o=- 'file-name'` 
					- You can statically set permissions for all three user types, note the `o=-`, this meaning that other users will have no permissions
					- Note the commas `,`'s that are used
				- `chmod a=r,u=rw 'file-name'`
					- Set permissions for all user types to have read, then state the user owner to have read and write permissions
		- *So you can see that you can use both letter characters as well as with the octal solution. Depends on your style and what you're doing and what would be more efficient :)* 
			- `u` - denotes the user owners permissions of the file
			- `g` - denotes the group owners permissions of the file
			- `o` - denotes any other users permissions of the file
			- the `rwx` denotes the permission settings as above
			- See if you can find some tutorials online that cover this. **pwn.college** (https://pwn.college) is a great place to run through various tutorials and challenges :) 
	- If you're lazy (but please don't be - it's good to know these numbers in moving forward):
		- https://chmod-calculator.com/
	- Permissions are denoted into three characters representing the following:
		- Owner
			- The owner that owns the file
		- Group
			- The group that owns the file
		- Other
			- (other users, other groups)
	- Example:
		- `drwxrwxr-x  2 dshivnit dshivnit`
		- Take note of the first d
			- This denotes that the respective file is in fact, a directory
			- The next three characters depict what kind of access the Owner has
			- The next three after depict what kind of access the Group to the directory has (in this case, yours respectfully, also dshivnit)
			- The next depict all other users and/or groups
			- In this Case both owner and group owners of the directory have all access to it (being read, write and execute permissions)
			- The last others only has read and execute
	- The `chmod` command will allow you to toggle these permissions, providing that you have the permission to be able to do so!
		- Example:
			- `chmod 777 'file-name'`
				- Will grant the Owner, Group, and Other all access to the file-name file (read, write and execute)
				- Don't do this.. lol
				- You can figure out the rest
	- SUID
		- if an `s` is in place where an `x` or a `-` would normally be under the Owners permissions for a file (or command/directory) - then any user will be able to run that file/command/directory with the same permissions as the Owner of it
		- Example:
			- `-rwsr-xr-x 1 root root 118168 Dec  7 01:51 /usr/bin/passwd`
			- See how there's an `s` there? That identifies that the passwd command can be run by any user (however, the way the passwd command is written only allows any given user to change only their own password, no one elses)
		- Handy article to read:
			- https://linuxhandbook.com/suid-sgid-sticky-bit/
		- `chmod u+s 'file-name'`
			- Will set SUID to the given file-name
		- `chmod u-s 'file-name'`
			- Will remove SUID from the given file-name
			OR
		- `chmod 4766 'file-name'` 
			- the number 4 as the prepended digit to the usual 3-digits will always represent SUID
			- The octal 4 always represent SUID
		- `chmod 0766 'file-name'`
			- Will remove SUID from the given file-name
	- In the case of a capital S as opposed to a small one for SUID
		- This means that there wasn't an executable permission to said file in the first place
		- a capital S would mean that there is an error that would normally need to be looked into
	- In essence, the owner of the file would need to have had executable permissions to the related file to begin with prior to SUID access being configured - otherwise, it's just pointless. 
	- Finding all files with SUID
		- `find / -perm /4000 2> /dev/null`
- SGID
	- Pretty much the same as SUID - but for Group permissions to be allowed by any user
	- Same rules apply as SUID just syntax is slightly different
	- Benefit here is normally when an SGID is applied to a directory, all the sub-directories of said directory, and the files contained within them, get the same group ownership as the main directory
	- A practical example would be Samba Server being used to share files on a local network
		- It would be guaranteed that any new file created will not lost permissions desired, regardless of 'who' created it
	- `chmod g+s 'directory-name'`
		OR
	- `chmod 2775 'directory-name'`
		- TAKE NOTE:
			- Executable permissions - ie the number 7 (or a permission with executable permissions) MUST be used otherwise it's pointless
			- The octal number is alwayd 2 for SGID
	- Removing SGID
		- `chmod g-s 'folder-name'`
		- `chmod 0775 'folder-name'`
	- Finding SGIDs:
		- `find / -perm /2000 2> /dev/null`
- STICKY BIT
	- Works on directories
	- All files in the directory can only be deleted or renamed by the file owners only, or root.
	- Normally used in the `/tmp` directory 
	- `chmod +t 'directory-name'`
	- `chmod 1775 'directory-name'`
		- The octal 1 will always be used for Sticky Bits
	- `chmod -t 'directory-name'`
	- `chmod 0755 'directory-name'`
	- Finding Sticky Bits
		- `find / -perm /1000 2> /dev/null`
	- 
- File Types
	- `d`
		- Directory
	- `-`
		- Normal file
	- `c`
		- Character device
		- Interacting with these types often result in changes to the display output

- Chaining with Semicolons
	- `$ echo TESTING WHAT UP > prac.txt; cat prac.txt`
		`TESTING WHAT UP`
	- 

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
	- id
	- chown
	- chgrp

- `man`
	- `/usr/share/man`
	- `/` search forward
	- `?` to search backwards
	- `n` go to the next result
	- `N` go to the previous result
- File Descriptors
	- A number that describes communication channel in Linux
		- `FD 0` - Standard Input
		- `FD 1` - Standard Output
		- `FD 2` - Standard Error
		- ie - `/path/script-to-run 2> error.log`
			- will return any errors reported by `script-to-run` to a file called `error.log` that is in the current working directory
		- another ie - `find -name file_a -type f > some_test_file.txt 2> some_test_file_errors.txt`
			- Will print non-error results to the `some_test_file.txt` file and all errors into the `some_test_file_errors.txt` file
- Redirecting input
	- using the lesser-than symbol
	- `<`
	- `rev < text.file` will output whatever is in the text_file file in reverse
	- `/path-to/executable-file < /path-to/list-of-stdin-stuff`
		- Will put in to the executable-file whatever is in the list-of-stdin-stuff file
	- 
- Redirecting File Descriptors to each other
	- `2>& 1`
		- Redirects stderr (standard error) to stdout (standard output)
	- You can pipe a grep command to this combined stderr stdout if needed 
		- `2>& 1 | grep 'something'`
- `tee` command
	- Read from standard input and write to standard output and files
	- `cat text3.txt > text4.txt | tee`
		- Will show what is being written from text3.txt to text4.txt
	- `find / -name file_a -type f > some_test_file.txt 2> some_test_file_errors.txt | tee`
		- Will show you the output of findings to some_test_file.txt via stdout, stderr will still be put into the `*errors.txt` file
	- `command_1 | tee >(command_2) >(command_3)`
	- `echo HELLO | tee >(rev)`
		- `HELLO`
		- `OLLEH`
- `read`
	- Reads input from the command line
	- Reads input from a file into a variable as well
		- `read VARNAME < file-name.txt`
		- `echo $VARNAME`
- REDIRECTION SUMMARY
	- `>` - for stdout
	- `2>` - for stderr
	- `<` - for stdin
	- `>>` and `2>>` for append-mode redirection
	- `>&` for redirecting to other file descriptors (0,1,2)
	- `|` - piping to another command

- Variables
	- Storing a command into a variable
		- `VARIABLENAME=$(cat ~/filename.txt)`
		- `echo $VARIABLENAME`
			- backticks work to replace the `$()` as well
			- But this isn't so functional if wanting to do nest command substitutions and so on
				- Like `$(cat $(find / -name file.txt))`
		- Make sure to have the path where the file resides preceding the command
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
	- Variables are local to each shell that they are created/live in
		- Meaning that variables that are defined in the BASH shell will live in there, ones created in the zsh shell will live in there, sh, and so on
	- Exporting Variables
		- Variables are passed into the environment variables of child processes when exporting them
		- ie `TEST=test`
			- `export TEST`
			- `sh`
			- `echo $TEST` 
			- test
	- Printing exported variables
		- `env`
	- Command Substitution
		- 
- Processes
	- `init` - Initializer process
		- which launches a series of other processes which lead to the launching of even more processes (lol)
		- All the way through to the CLI (which too, is a process)
		- The shell, in turn, launches processes in response to the commands that are entered into it
	- `ps`
		- List running processes
		- Process Snapshot, Process Status
		- PID - Process ID
		- TTY
			- The terminal that the process is running on 
		- `e` every process
		- `f` full format
		- `a` list processes for ALL users
		- `x` list processes that aren't running in a terminal
		- `u` list for a user-readable output
- Killing Processes
	- `kill`
		- do a `ps -aux` first to see what the pids are, or `ps` whatever argument to get more information
- Interrupting Processes
	- `ctrl+c` 
- Suspending Processes
	- `ctrl+z`
	- Processes will come up with a `T` status when listing processes in `ps` commands
- Resuming Processes
	- `fg`
- Background Processes
	- `bg`
	- Processes will come up with a `S` status when listing processes in `ps` commands
- 

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

- Error Codes
	- Running `echo $?` after a command has been run can determine whether the previous command that was run was completed successfully or not
	- a `0` will return if the command or process had completed successfully
	- If an error occurs, there will normally be a return of the value of `1` 
	- Sometimes there may be other numbers that can signify particular error codes (which represent an actual error that occurred, ie something specific)


---
Help Commands (from pwn.college)
```
GNU bash, version 5.2.32(1)-release (x86_64-pc-linux-gnu)
These shell commands are defined internally.  Type `help' to see this list.
Type `help name' to find out more about the function `name'.
Use `info bash' to find out more about the shell in general.
Use `man -k' or `info' to find out more about commands not in this list.

A star (*) next to a name means that the command is disabled.

 job_spec [&]                                              history [-c] [-d offset] [n] or history -anrw [filenam>
 (( expression ))                                          if COMMANDS; then COMMANDS; [ elif COMMANDS; then COMM>
 . filename [arguments]                                    jobs [-lnprs] [jobspec ...] or jobs -x command [args]
 :                                                         kill [-s sigspec | -n signum | -sigspec] pid | jobspec>
 [ arg... ]                                                let arg [arg ...]
 [[ expression ]]                                          local [option] name[=value] ...
 alias [-p] [name[=value] ... ]                            logout [n]
 bg [job_spec ...]                                         mapfile [-d delim] [-n count] [-O origin] [-s count] [>
 bind [-lpsvPSVX] [-m keymap] [-f filename] [-q name] [->  popd [-n] [+N | -N]
 break [n]                                                 printf [-v var] format [arguments]
 builtin [shell-builtin [arg ...]]                         pushd [-n] [+N | -N | dir]
 caller [expr]                                             pwd [-LP]
 case WORD in [PATTERN [| PATTERN]...) COMMANDS ;;]... e>  read [-ers] [-a array] [-d delim] [-i text] [-n nchars>
 cd [-L|[-P [-e]] [-@]] [dir]                              readarray [-d delim] [-n count] [-O origin] [-s count]>
 challenge [--fortune] [--version] [--secret SECRET]       readonly [-aAf] [name[=value] ...] or readonly -p
 command [-pVv] command [arg ...]                          return [n]
 compgen [-abcdefgjksuv] [-o option] [-A action] [-G glo>  select NAME [in WORDS ... ;] do COMMANDS; done
 complete [-abcdefgjksuv] [-pr] [-DEI] [-o option] [-A a>  set [-abefhkmnptuvxBCEHPT] [-o option-name] [--] [-] [>
 compopt [-o|+o option] [-DEI] [name ...]                  shift [n]
 continue [n]                                              shopt [-pqsu] [-o] [optname ...]
 coproc [NAME] command [redirections]                      source filename [arguments]
 declare [-aAfFgiIlnrtux] [name[=value] ...] or declare >  suspend [-f]
 dirs [-clpv] [+N] [-N]                                    test [expr]
 disown [-h] [-ar] [jobspec ... | pid ...]                 time [-p] pipeline
 echo [-neE] [arg ...]                                     times
 enable [-a] [-dnps] [-f filename] [name ...]              trap [-lp] [[arg] signal_spec ...]
 eval [arg ...]                                            true
 exec [-cl] [-a name] [command [argument ...]] [redirect>  type [-afptP] name [name ...]
 exit [n]                                                  typeset [-aAfFgiIlnrtux] name[=value] ... or typeset ->
 export [-fn] [name[=value] ...] or export -p              ulimit [-SHabcdefiklmnpqrstuvxPRT] [limit]
 false                                                     umask [-p] [-S] [mode]
 fc [-e ename] [-lnr] [first] [last] or fc -s [pat=rep] >  unalias [-a] name [name ...]
 fg [job_spec]                                             unset [-f] [-v] [-n] [name ...]
 for NAME [in WORDS ... ] ; do COMMANDS; done              until COMMANDS; do COMMANDS-2; done
 for (( exp1; exp2; exp3 )); do COMMANDS; done             variables - Names and meanings of some shell variables
 function name { COMMANDS ; } or name () { COMMANDS ; }    wait [-fn] [-p var] [id ...]
 getopts optstring name [arg ...]                          while COMMANDS; do COMMANDS-2; done
 hash [-lr] [-p pathname] [-dt] [name ...]                 { COMMANDS ; }
 help [-dms] [pattern ...]
```

- 