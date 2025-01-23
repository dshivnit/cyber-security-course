*Some of these commands will be in relation to tools that are described in the Tools section - rationalisation will be required here*

``` zsh
sudo apt install sl
sl
# Thanks for this Cam =]
```

Covered/covering so far:
- Powershell
- Bash
- zh 

PowerShell
- wsl (Windows Subsystem for Linux)

Bash (pipe to the pipe pipe ;) )
- Reference: https://github.com/RehanSaeed/Bash-Cheat-Sheet
- arch
- whoami
- hostname
- uname -a
- pwd
	- presents the working directory
- cut
	- Example:
		- Log entry:
			`145.76.33.201 - - [31/Jul/2023:12:34:20 +0000] "GET /login.php HTTP/1.1" 200 5678 "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.90 Safari/537.36"`
		- Cut command to select what we want to see from the log above
			```cut -d ' ' -f 1,4,7,9 apache.log | tail -n 4`
		- Will give us this :)
			```
			104.76.29.88 [31/Jul/2023:12:34:23 /index.php 200
			128.45.76.66 [31/Jul/2023:12:34:22 /contact.php 404
			76.89.54.221 [31/Jul/2023:12:34:21 /about.php 200
			145.76.33.201 [31/Jul/2023:12:34:20 /login.php 200
			```
- sort
	- Sorts entries in a file chronologically or alphabetically
	- Either in ascending or descending order (`-r` reverse)
		- Based on criteria given
	- Example:
		- `cut -d ' ' -f 1,4,7,9 apache.log | sort -n | tail -n 4`
		- Gives us
	```		
			203.64.78.90 [31/Jul/2023:12:35:01 /about.php 404
			203.78.122.88 [31/Jul/2023:12:35:10 /contact.php 404
			211.87.186.35 [31/Jul/2023:12:35:01 /contact.php 200
			221.90.64.76 [31/Jul/2023:12:35:08 /login.php 200```
 - 
- uniq
	- Identifies and removes adjacent duplicate lines from sorted input
	- Usually combined with the sort command and piped after running `sort` 
	- Example:
		- `cut -d ' ' -f 1 apache.log | sort -n | uniq -c`
	- Will give us something like
		- ```6 76.89.54.221
	      1 77.188.103.244
	      1 99.76.122.65
	      6 104.76.29.88
	      1 108.76.122.35 ```
	- Here you can see the amount of times that one particular IP address has been picked up in the file `apache.log` 
	- Useful for seeing how many times any specific IP Address is making requests or is referenced in this particular log file
- sed
	- Text processing tool 
	- For example - to replace `31/Jul/2023` with `July 31, 2023` we can:
		- `sed 's/31\/Jul\/2023/July 31, 2023/g' apache.log`
	- Which will give us:
		- `176.145.201.99 - - [July 31, 2023:12:34:24 +0000] "GET /login.php HTTP/1.1" 200 1234 "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.90 Safari/537.36"`
	- Original would have read like this:
		- `76.145.201.99 - - [31/Jul/2023:12:34:24 +0000] "GET /login.php HTTP/1.1" 200 1234 "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.90 Safari/537.36"`
	- The backslash character `\` is needed to escape the forward slash in our pattern and tell `sed` to treat the forward slash `/` as a literal character
	- the `-i` parameter can be used to overwrite the file that is being analysed (be careful with this and make sure you have a backup!)
- awk
	- Conditional actions based on specific fields in the file being analysed
	- ie from the example that we've been working with above, printing out HTTP Responses which are 400 (remember that these signify an error has been thrown by the Web Server) or higher
		- `awk '$9 >= 400' apache.log` | tail -n 1
		  Remember that it's the space `' '` between characters that signify the field (in the example above) - hence why this is $9 - ie, the ninth field
	- Will give us:
		- ```
		  128.45.76.66 - - [31/Jul/2023:12:34:29 +0000] "GET /about.php HTTP/1.1" 404 4321 "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.210 Safari/537.36"
			203.64.78.90 - - [31/Jul/2023:12:34:25 +0000] "GET /about.php HTTP/1.1" 404 4321 "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.81 Safari/537.36"
			128.45.76.66 - - [31/Jul/2023:12:34:22 +0000] "GET /contact.php HTTP/1.1" 404 5678 "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.54 Safari/537.36" ```
- grep
	- `grep "admin" apache.log`
		- Will return any references to the word "admin" in the apache.log file
	- `grep -c "admin" apache.log'`
		- Will return how many times the word 'admin' was referenced in the apache.log file
	- `grep -n "admin" apache.log`
		- Will return what line numbers the word "admin" is in the file apache.log
	- `grep -v "/index.php" apache.log | grep "203.64.78.90"`
		- Will list entries that have 203.64.78.90 but doesn't have any references to index.php in the apache.log file
	- `grep -C 5 "something"` 
		- Will return 5 lines before and after any line that has the word "something" in it 
	- `grep -A 5 "something"`
		- Will return 5 lines after any lines containing the word "something"
	- `grep -B 5 "something"`
		- Will return 5 lines before any lines containing the word "something"`

	- Different log - this one has the below entries in a file called `apache-ex2.log`
		-```
			203.0.113.1 - - [02/Aug/2023:10:15:23 +0000] "GET /blog.php?post=12 HTTP/1.1" 200 - "Mozilla/5.0"
			87.45.189.243 - - [02/Aug/2023:12:45:32 +0000] "GET /blog.php?post=7 HTTP/1.1" 200 - "Mozilla/5.0"
			132.56.98.71 - - [02/Aug/2023:15:30:18 +0000] "GET /index.php HTTP/1.1" 200 - "Mozilla/5.0"
			59.234.76.18 - - [02/Aug/2023:17:58:45 +0000] "GET /blog.php?post=5 HTTP/1.1" 200 - "Mozilla/5.0"
			115.68.210.87 - - [02/Aug/2023:19:27:10 +0000] "GET /admin/settings.php HTTP/1.1" 200 - "Mozilla/5.0"
			78.22.183.98 - - [02/Aug/2023:21:15:01 +0000] "GET /products.php HTTP/1.1" 200 - "Mozilla/5.0"
			210.77.55.132 - - [02/Aug/2023:23:40:12 +0000] "GET /login.php HTTP/1.1" 200 - "Mozilla/5.0"
			45.78.231.101 - - [03/Aug/2023:02:10:05 +0000] "GET /contact.php HTTP/1.1" 200 - "Mozilla/5.0"
			66.78.92.112 - - [03/Aug/2023:05:21:55 +0000] "GET /blog.php?post=26 HTTP/1.1" 200 - "Mozilla/5.0"
			87.67.101.77 - - [03/Aug/2023:08:55:30 +0000] "GET /login.php HTTP/1.1" 200 - "Mozilla/5.0"
			
		- Say we wanted to only show a pattern where the post has an ID between 22 and 26
			- `grep -E 'post=2[2-6]' apache-ex2.log`
			
		- Will list only those ID's, between 22 and 26 (notice how the first 2 is outside of the square brackets - identify the pattern there ;) )
	
- redis-cli
	- Connecting to a Redis server in bash
	- keys *
		- Will show all keys stored (databases it seems as well)
	- select *index_number*
		- Will connect to a database with the given index number
		- Refer to the keys command before
	- 
- chmod (User, Group, Other)
- su
	- login as root or SUPERUSER in the shell (password if configured will be needed, password should have been configured initially anywho :) ) 
- sudo 
	- SUPERUSER DO!
	- Run a command as a superuser whilst in the environment/shell as another regular (non admin) user
- awk
	- Tool and programming language that allows users to process and manipulate data and produce formatted reports. 
		- To list all usernames on the system:
			- awk -F: '{ print $1 }' /etc/passwd   OR
			- cat /etc/passwd   (this will get you a more detailed list of users, with UIDs etc)
- id
	- Print real and effective user and group IDs
	- Example:
		- id
			- Will get you the current User's UID, GID, and the GROUPS the User belongs to
		- id *username*
			- Will get you the given usernames UID, GID and the GROUPS the given username belongs to
			- In the context of UIDs, don't forget that anything that isn't 0, is NOT root.
- ftp
	- ftp *hostname/ip-address* 
		- This will connect you to the host that you are trying to get into (via ftp of course)
		- You would then normally be asked for a username and sometimes (bloody well better be always) a password
	- help 
		- When connected to an ftp server running on a host, you can type "help" to see a list of available commands
		- You may notice that a lot of the listed commands are similar to the bash shell
	- get
		- Used to retrieve files from the ftp server
- gobuster
	- gobuster --help
		- Always helpful
	- man gobuster
		- Also, helpful. 
		- Take note that this will open in a CLI text editor
	- Wordlists and Domains will be helpful if trying to brute into a box/machine/server (take note that these are also required by the gobuster)
		- Example: 
			gobuster -m dir -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt -u http://10.129.1.15/
	- -x : can enumerate hidden files, or remote directories (ie: php, txt, html   and so on. This actually specifies specific file types you want the scan/search to pick up :) )
	- -e : can be used for completing printing URL when extracting a hidden file or directory
	- -o : save the output to a filename (you'll have to describe it)
- nc (netcap)
	- nc -lvnp 6969 (will start listening on port 6969 and will show you traffic)
- curl
	- Transfers data to or from a server
- which <function/package name> 
	- will show you if the package is installed on the machine or not (ie, which python3 > if it returns /usr/bin/python3 then python3 is installed)

zsh (z Shell) (/bin/zsh (providing it's there) will change $SHELL on the fly, zsh is cool)
*remember that some commands will require you to do a sudo*
- id
	- Lists the current user's:
		- uid
		- gid
		- groups
- id *username*
	- Lists the above for the given user
- groupadd *groupName*
	- Will create a new group named with the given name
	- To verify that the group was added, you can do a:
		- tail /etc/group
- usermod *options* 
	- Modify a user account
	- -a --append
	- -G --groups GROUP
		- new list of supplementary GROUPS
		- example: sudo usermod -a -G *groupName userName*
		- You can verify by:
			- tail /etc/group | grep *groupName*
- tcpdump
	- Data-network packet analyser program that runs in terminal (CLI). Displays TCP/IP and other packets transmitted or received over a NIC
	- tcpdump -i (interface#refence) port 389 (this would be for LDAP services per say)
- scp
	- Secure Copy
	- Check out help/man details for further information, functionality
	- scp SOURCE DESTINATION
		- Sending:
			- scp text.file username@ipaddress,computername,domain/filedirectory
		- Receiving/pulling:
			- scp username@ipaddress,computername,domain/filedirectory filename you want to save the file to
- ps
	- Shows processes running
	- ps aux
		- will show processes running from other users not in the session (mainly the system)
- top
	- Another variant as to what processes are running
	- More real-time updates
	- Shows additional system information as well

- kill
	- kill (pid) killing specific processes
	- SIGTERM - kill the pid, but allow it do some cleanup tasks first
	- SIGKILL - kill the pid, don't do any cleanup
	- SIGSTOP - stop/suspect a pid

- NAMESPACES
	- Only PIDs in the same namespace will be able to see each other
	- Good for security as it divvies up various processes running on any given system

- systemctl
	- Control the systemd system and service manager
	- freedesktop.org/software/systemd/man/systemctl.html
	- systemctl stop (service name)
		- start
		- enable
		- disable
- history
	- lel
- Shelling
	- - python -c 'import pty;pty.spawn("/bin/bash")'
		- Uses Python in the Reverse Shell / Bind Shell to spawn a more featured bash shell (you might need to specify python2 or python3 depending on the Linux box you are shelling to/from)
		- export TERM=xterm
			- additional access to commands such as 'clear'
		- Background the shell with CTRL+Z (backgrounds the Remote Shell) THEN stty raw -echo; fg (turns off our own terminal echo (which gives us access to commands like tab autocompletions, arrows, CTRL+C then bring the Remote Shell back into the Foreground)
				- reset
					- Re-enable terminal echo (from when the 'stty raw -echo' command was issued -- otherwise the Terminal will be pretty shiddy)
- Linux
	- CTRL+U
		- delete text to the left
	- CTRL+K
		- delete text to the right
- 