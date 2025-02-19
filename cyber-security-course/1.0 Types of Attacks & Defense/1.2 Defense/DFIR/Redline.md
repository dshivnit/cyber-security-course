https://tryhackme.com/room/btredlinejoxr3d
https://fireeye.market/apps/211364

- Collect registry data (Windows machines only)
- Collect running processes
- Collect memory images (before Windows 10)
- Collect browser history
- Look for suspicious things
- And more.

Collecting Data
- Standard Collector
	- Configures the script to gather a minimum amount of data for analysis
	- Fastest method to collect data that is needed
	- Usually takes a few minutes to complete
- Comprehensive Collector
	- Configures the script to gather the most data from the host being analyzed
	- Process can take up to an hour or more
- IOC Search Collector (Windows only)
	- Collects data that matches with IOCs that is created with the help of the IOC Editor (https://fireeye.market/apps/S7cWpi9W)

Looking at an Analysis File
https://fireeye.market/assets/apps/211364/documents/877936_en.pdf
- System Information
	- Information around the machine, BIOS (Win only), OS and user information
- Processes
	- Different attributes like Process Name, PID, Path, Arguments, Parent Process, Username, and so on
	- Four sections when expanded:
		- Handle
			- A connection from a process to an object or resource within the OS
			- OSes use handles for referencing internal objects like files, registry keys, resources etc
		- Memory Sections
			- Unsigned memory sections can be investigated
			- Many processes normally use legitimate DLLs which will be signed
			- Unsigned DLLs will be worth taking a closer look at
		- Strings
			- Information on captured strings
		- Ports
			- Most malware initiate outbound or inbound connections to communicate to their C2 servers to be able to carry out activities like data exfil or transferring a payload
			- Suspicious connections can be reviewed from ports and IP addresses
			- Also ensure that system processes are focused on as well
			- Threat actors like to avoid detection by hiding under system processes
				- explorer.exe
				- notepad.exe
				- These types of processes shouldn't be on the list of processes with outbound connections
		- Other important sections:
			- File System
			- Registry
			- Windows Services
			- Tasks
			- Event Logs
			- ARP and Route Entries
			- Browser URL History
			- File Download History
		- Timeline can assist in better understanding when the compromise happened and what steps the threat actor took to escalate the attack
		- Timeline will also record every action on the file
			- Created, changed, modified, accessed
		- If the time of the event is known then **TimeWrinkles** can be used to filter out the timeline to only the events that took place around that time
		- **TimeCrunches** assists to reduce the excessive amount of data that is not relevant in the table view
		- It will hide the same type of events that occurred within the same minute you specified 

IOC Editor
https://fireeye.market/apps/S7cWpi9W
https://fireeye.market/apps/211404
- Indicator of Compromise
	- Artifacts of the potential compromise and host intrusion on the system or network that you need to look for when conducting threat hunting or performing incident response
		- Can be 
			- MD5, SHA1, SHA256 hashes, IP addresses, C2 domains, file size, filename, file path, a registry key, and so on
	- 