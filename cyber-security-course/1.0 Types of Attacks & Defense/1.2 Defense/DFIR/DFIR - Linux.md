https://tryhackme.com/room/linuxforensics

- OS Version
	- `cat /etc/os-release`
- User Accounts
	- `cat /etc/passwd`
	- `cat /etc/passwd | columen -t -s :`
- Group Information
	- `cat /etc/group`
	- Will also show which users belong to those groups
- Sudoers List
	- `cat /etc/sudoers`
- Login Information
	- `/var/log`
		- Contains log files of all kinds
		- `btmp`
			- Saves information about failed logins
		- `wtmp`
			- keeps historical data of logins
		- These are binary files which have to be read using the `last` utility
		- `last -f /var/log/wtmp`
- Authentication Logs
	- Every user that authenticates on a Linux host is logged in the auth log
	- `/var/log/auth.log`

- System Configuration
	- Hostname
		- `cat /etc/hostname`
	- Timezone
		- `cat /etc/timezone`
	- Network Configuration
		- `cat /etc/network/interfaces`
		- `ip address show` or `ip a s`
	- Active Network Connections
		- `netstat`
		- `netstat -natp`
	- Running Processes
		- `ps`
		- `ps aux`
	- DNS Information
		- `cat /etc/hosts`
		- `/etc/resolv.conf`
			- Information on DNS servers that the machine talks to for DNS resolution

- Persistence Mechanisms
	- Cron Jobs
		- Commands that run periodically after a set amount of time
		- `cat /etc/crontab`
	- Service Startup
		- `ls /etc/init.d`
	- .Bashrc
		- Can be considered a startup list of actions to be performed
		- `cat ~/.bashrc`
		- `cat /etc/bash.bashrc`
		- `cat /etc/profile`

- Evidence of Execution
	- Sudo execution history
		- `cat /var/log/auth.log* | grep -i COMMAND`
	- Bash History
		- Any other commands (apart from sudo) are kept in the bash history
		- Every bash history is kept separately for each user on the machine
			- (same for root)
		- `cat ~/.bash_history`
	- Files Accessed using VIM
		- Also in home directories
		- `cat ~/.viminfo`
Log Files
	Generally found in the `/var/log` directory
- Syslog
	- Contains messages that are recorded by the host about system activity
	- `cat /var/log/syslog`
- Auth log
	- `cat /var/log/auth.log*`
	- note the `*` here includes logs that have been rotated
- Third-party logs
	- `/var/log`
		- There will be sub-directories and log files related to third-party programs/tools

