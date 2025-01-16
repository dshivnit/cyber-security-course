https://github.com/mandiant/flare-vm
https://tryhackme.com/r/room/flarevmarsenaloftools

- Packed and obfuscation
	- Obfuscated programs are ones whose execution the malware author has attempted to hide
	- Packed programs are a subset of obfuscated programs in which the malicious program is compressed and cannot be analysed
		- (oreilly.com)

- Flare-VM should ONLY be installed on a VM
- A collection of software installation scripts for Windows systems that allow you to setup (with ease) and maintain a reverse engineering environment on a VM
- Relies on two technologies (mainly):
	- Chocolatey
		- Windows-based Nuget package management system 
			- A package is essentially a ZIP file containing PS installation scripts that download and configure a specific tool
	- Boxstarter
		- Leverages Chocolatey packages to automate the installation of software and create repeatable, scripted Windows environments

Reverse Engineering and Debugging
- Reverse Engineering
	- Pretty much like solving a puzzle backwards (lel)
	- You take a finished program/product/piece-of-software and break it apart to see how it works
- Debugging
	- Identifying errors, understanding why they happen, and correcting the code to prevent them
	- Tools
		- Ghidra
			- NSA developed open-source reverse engineering suite
		- x64dbg
			- Open-source debugger for binaries in x64 and x32 formats
		- OllyDbg
			- Debugger for reverse engineering at the assembly level
		- Radare2
			- A sophisticated open-source platform for reverse engineering
		- Binary Ninja
			- A tool for disassembling and decompiling binaries
		- PEiD
			- Packer, cryptor, and compiler detection tool
		- IDA Pro
			- Interactive Disassembler Professional
			- Translates Machine Code into Assembly Language
			- Creates maps of how software executes, showing the binary instructions used by the processor
			- Can analyse a wide range of executable formats

Disassemblers and Decompilers
- Crucial tools in malware analysis
- Help analysts and teams to understand malicious software behaviour, logic and control flow by breaking it into a more understandable format
- Some tools used:
	- CFF Explorer
		- A PE (Portable Executable) editor designed to analyse and edit Portable Executable (PE) files
	- Hopper Disassembler
		- A debugger, disassembler, and decompiler
	- RetDec
		- Open-source decompiler for machine code
	- IDA Pro
		- Interactive Disassembler Professional
		- Translates Machine Code into Assembly Language
		- Creates maps of how software executes, showing the binary instructions used by the processor
		- Can analyse a wide range of executable formats

Static and Dynamic Analysis
- Two crucial methods in cyber security for examining malware
- Static Analysis
	- involves inspecting the code without executing it
- Dynamic Analysis
	- Involves observing the malware's behaviour as it runs
- Some tools:
	- Process Hacker
		- Sophisticated memory editor and process watcher
	- PEview
		- A portable executable (PE) file viewer for analysis
	- Dependency Walker
		- Tool for displaying an executable's DLL dependencies
	- DIE (Detect It Easy)
		- Packer, compiler, and cryptor detection tool

Forensics and Incident Response
- Involves the collection, analysis and preservation of digital evidence from various sources like computers, networks, and storage devices.
- Incident Response focuses on the detection, containment, eradication, and recovery from cyberattacks. 
- Some tools:
	- Volatility
		- RAM dump analysis framework for memory forensics
	- Rekall
		- Framework for memory forensics in incident response
	- FTK Imager
		- Disk image acquisition and analysis tool for forensic use

Network Analysis
- Includes different methods and techniques for studying and analysing networks to uncover patterns, optimise performance, and understand the underlying structure and behaviour of the network.
- Some tools:
	- Wireshark
		- Network protocol analyser for traffic recording and examination
		- `ip.addr==10.10.10.10` in the filter field will list any packet that has a reference to IP address 10.10.10.10
	- Nmap
		- Vulnerability detection and network mapping tool
	- Netcat
		- Read and write data across network connections with this helpful tool

File Analysis
- A technique used to examine files for potential security threats and ensure proper file permissions
- Some tools:
	- FileInsight
		- A program for looking through and editing binary files
	- Hex Fiend
		- Hex editor that is light and quick
	- HxD
		- Binary file viewing and editing with a hex editor

Scripting and Automation
- Involve using scripts like PowerShell and Python to automate repetitive tasks and processes, making them more efficient and less prone to human error
- Python
	- Mainly automation-focused on Python modules and tools
- PowerShell Empire
	- Framework for PowerShell post-exploitation

SysInternals Suite
- A collection of advanced system utilities designed to help IT professionals and developers manage, troubleshoot, and diagnose Windows systems
- Some tools within:
	- Autoruns
		- Shows what executables are configured to run during system boot-up
	- Process Explorer
		- Provides information about running processes
	- Process Monitor
		- Monitors and logs real-time process/thread activity

Commonly Used Tools for Investigative Purposes (some):
- ProcMon - Process Monitor (in Windows)
	- You can record issues with your systems applications
	- You can:
		- see
		- record
		- keep track of system and Windows file activity in real-time
	- Useful for tracking system activity, especially regarding malware research, troubleshooting, and forensic investigations
	- Keeps real-time tabs on the file system, registry, and thread/process activity
	- Mimikatz and other tools frequently try to access LSASS memory to try and get credentials if they are held within 
	- Watching processes like LSASS (Local Security Authority Subsystem Service) and identify any odd patterns or processes reading or writing to lsass.exe
- ProcExp - Process Explorer (in Windows)
	- Offers in-depth insights into active processes running on the computer
	- Allows one to delve into the inner workings of the system, providing a comprehensive list of currently running processes and their linked user accounts
	- If you've ever been curious about which program is accessing  a specific file or folder, ProcExp can show that information
- HxD
	- Quick and flexible hex editor for editing files, memory and drives of any capacity
	- Can be applied to forensic investigations, data recovery, debugging, and exact manipulation of binary data
	- Features include, viewing file and memory contents, editing, searching and comparing hex data
- CFF Explorer
	- Thanks to CFF Explorer's comprehensive file information, investigators can generate file hashes for integrity verification, authenticate the source of system files, and validate their validity (by perhaps looking for unusual alterations). 
	- Important to know when analysing malware, as dangerous code may be hidden in altered system files. 
- Wireshark
	- Investigators may use Wireshark to hunt down dubious connections, examine protocols, and spot possible assaults or data exfiltration.
	- Encrypted data - such as those that run in TLS (443) can sometimes be masking harmful activities, or safeguarding normal/legitimate traffic
- PEStudio
	- Static analysis
		- Studying the executable file properties without running the actual code/files
		- This can be done with PEStudio
	- Offers a variety of information about a file without putting users in danger of execution, which aids in identifying executables that seem suspect or harmful
	- Packing and encryption is typical of *dangerous software*
- FLOSS - FLARE Obfuscated String Solver
	- Uses advanced static analysis techniques
	- Automatically extracts and de-obfuscates all strings from malware programs
	- Like strings.exe, it can enhance the basic static analysis of unkown binaries
	- FLOSS includes more Python scripts in the script's directory, which can be used to load the script's output into other programs like IDA Pro, or Binary Ninja

Analysing Malicious Files
- Initial approach
	- Perform a static analysis on a potentially malicious file
		- To get information from the binary of it
	- PEStudio would be a tool to use :) 
		- Take note that when opening files, allow PEStudio to load the various elements - like Functions, Strings etc
	- Check the hashes of the file against tools like Virustotal
	- Also have a look at the comments in PEStudio
	- The absence of a **rich-header** indicate that the file is potentially packed or obfuscated to avoid detection by static analysis tools. 
		- Typical behaviour of sophisticated malware that tries to evade detection by altering critical sections of its PE file
	- The Functions tab list API calls that the file has imported
		- Also known as the IAT (Import Address Table)
		- Sort by all Functions by the **blacklist** tab to see which API calls have been flagged
		- Enables us to understand how malware may behave once it compromises a host
		- Also look at the names of the API calls that have been made - are there any dodgy ones or ones that seem out of the ordinary??
	- FLOSS is another tool
		- Flare Obfuscated String Solver
		- in PS Console
			- `FLOSS .\filename.exe > filename.txt`
			- Examine the contents
			- Any links of the functions that were seen in PEStudio?
	- Analysing with ProcExp and ProcMon
		- ProcExp
			- Checking to see if executables or files are making any network connections (properties > TCP/IP) via ProcExp
		- ProcMon
			- Then use ProcMon to analyse the same file
			- (rerun it)
			- If you were able to identify that the process/file was making an outbound connection or inbound - a network connection to another entity in the previous analysis with ProcExp - then you should be able to see that same operation happening when you run the file and analyse it with ProcMon
				- Thus giving more reliance on the findings you are coming across
				- (note, a program can run thousands of operations within a second)
			- 