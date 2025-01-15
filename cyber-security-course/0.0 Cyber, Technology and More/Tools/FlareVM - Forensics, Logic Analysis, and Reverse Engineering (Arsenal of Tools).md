https://github.com/mandiant/flare-vm
https://tryhackme.com/r/room/flarevmarsenaloftools

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
- 
