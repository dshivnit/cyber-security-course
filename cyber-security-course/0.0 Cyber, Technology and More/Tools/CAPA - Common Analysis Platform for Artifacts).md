https://github.com/mandiant/capa
https://tryhackme.com/r/room/capabasics

- Developed by the FireEye Mandiant team. 
- Identifies the capabilities present in executable files like PEs (Portable Executables), ELF binaries, .NET modules, shellcode and also sandbox reports
- It analyses the file and applies a set of rules that 'describe common behaviours,' allowing it to determine what the program is capable of doing - ie network communication, file manipulation, process injection and so on.
- It essentially encapsulates years of reverse engineering knowledge into an automated tool

- ATT&CK's MAEC (Malware Attribute Enumeration and Characterisation) values
	- Launcher
		- Exhibits behaviours that trigger specific actions similar to malware behaviour
		- When CAPA tags a file with a "launcher" value, it indicates that the file demonstrates behaviour that is similar but not limited to:
			- Dropping additional payloads
			- Activating persistence mechanisms
			- Connecting to Command-and-Control (C2) servers
			- Executing specific functions
	- Downloader
		- Indicates that the file demonstrates behaviour similar but not limited to:
			- Fetching additional payloads or resources from the Internet
			- Pulling in updates
			- Executing secondary stages
			- Retrieving configuration files

- MBC - Malware Behaviour Catalogue
- https://github.com/MBCProject/mbc-markdown/blob/main/mbc_summary.md
	- Designed to support various aspects of malware analysis
		- Labelling
		- Similarity analysis
		- Standardised reporting
	- Serves as a catalogue of malware objectives and behaviours

- Micro-Objectives
	- Associated with micro-behaviours
	- Refer to action or actions exhibited by potentially malicious software that isn't necessarily malicious and may service various objectives. 
		- Example are messaging apps - these types of behaviours are typically abused - which is why CAPA may have flagged it.
	- Process
		- Behaviours related to processes such as but not limited to - Creating Process(s), Setting Threat Context, Terminating Process, and Checking Mutex
			- Mutex (Mutual Exclusion)
				- in a multithreaded program, a mutex is a mechanism used to ensure that multiple concurrent threads to not try to execute a critical section of code simultaneously (TechTarget)
	- Memory
		- Behaviours like, but not limited to, Allocating Memory, Changing Memory Protection, and Freeing Memory
	- Communication
		- Behaviours like, but not limited to - DNS, FTP, HTTP, ICMP, SMTP - network traffic
	- Data
		- Behaviours such as but not limited to - checking strings, compressing, decoding and encoding data

- The final output of CAPA, Objective and Micro-Objective are shown under the Objective column

Capability and Namespace
https://github.com/mandiant/capa-rules
- Namespace (Top-Level-Namespace/Namespace/YML Rule)
	- CAPA uses namespaces to group items with the same purpose
		- anti-analysis
		- collection
		- communication
		- compiler
		- data-manipulation
		- executable
		- host-interaction
		- impact
		- internal
			- Rules meant for internal purposes within the CAPA tool - serving as the behind-the-scenes aspect of rule development and execution
		- lib
			- Building blocks to create other rules
		- linking
		- load-code
		- malware-family
		- nursery
		- persistence
		- runtime
		- targeting
- Capability
	- Malware capabilities are referenced to where they fall under a given name-space (above) and a YML rule that is within that namespace
		- The Capabilities will often resemble the YML Rule, word for word (without the dashes)
	- Please see the link up top for further details

Capa Explorer (Web) - also has an offline mode that can be used
https://mandiant.github.io/capa/explorer/#/
- 

- Reading Very Verbose Files (or verbose)
	- These files will often have a lot of cluttered information/text
	- `-j` will emit the content of the file that has been saved (in verbose or very verbose mode) in JSON instead of text
	- However, you'd want to do this first (ie before analysing any given binary file)
		- `capa.bin -j -vv binary-file.bin > binary-file_vv.json`
	- You'll then be able to view the `.json` file via the Capa Explorer (Web) tool, whether online or offline
	- 