
- For me the metasploit-framework directory lives here:
	- `/usr/share/metasploit-framework/modules/auxiliary`
- You can find where your msf directory is by:
	- `which msfconsole` 
	- Cat the `msfconsole` file and that will show you were the metasploit-framework directory lives in your system
	
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
- 