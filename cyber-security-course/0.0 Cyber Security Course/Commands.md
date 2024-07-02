*Some of these commands will be in relation to tools that are described in the Tools section - rationalisation will be required here*

Windows
- wsl (Windows Subsystem for Linux)

Bash
- Reference: https://github.com/RehanSaeed/Bash-Cheat-Sheet
- pwd
	- presents the working directory
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
	