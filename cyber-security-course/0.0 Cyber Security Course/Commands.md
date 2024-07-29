*Some of these commands will be in relation to tools that are described in the Tools section - rationalisation will be required here*

Covered/covering so far:
- Powershell
- Bash
- zh 

PowerShell
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
	- -x : can enumerate hidden files, or remote directories (ie: php, txt, html   and so on. This actually specifies specific file types you want the scan/search to pick up :) )
	- -e : can be used for completing printing URL when extracting a hidden file or directory
	- -o : save the output to a filename (you'll have to describe it)

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
	- 