https://tryhackme.com/room/analysingvolatilememory

- Volatile memory stores data currently accessed or manipulated by the OS or the user
- This memory type is characterized by the temporary retention of data, which is removed upon system shutdown or restart.

- Some key data that can be found when investigating volatile memory can be:
	- Running processes on a system
	- Active network connections, including open ports
	- Threat information, execution states, and stack traces
	- System configurations including settings, environment variables, etc

A Page
- In Windows memory management, a **page** is a piece of memory
	- Memory management system splits the physical memory into fixed-sized blocks - known as pages
- When a program needs to store data in memory, the system assigns it a certain number of pages
- The system allows for efficient use of memory
	- Each program only uses the amount of memory it needs
- The size of a page can vary - but it is 4KB on most OSes
- Pages are crucial for virtual memory - they allow the OS to page out less frequently used memory sections on the disk, freeing up physical memory for other tasks

RAM - Random Access Memory
- This is the volatile memory that stores the data and information about the current programs, opening files etc - that are being used or loaded on to the CPU
- It is volatile, meaning that all contents in RAM will be lost when the rig is powered off
	- How Memory is Allocated
		- When a program is launched, the OS allocates a portion of RAM to store the data and code so that the program can function as it needs to 
		- This means any file or DLL that the program needs to function will also be loaded or at least have a pointer to it
	- Page File
		- Windows also uses the `pagefile.sys` as an extension to the RAM
		- When a program needs more RAM, but RAM is full
			- Microsoft sorts this issue by transferring less frequently used programs or data into the page file on a hard disk
			- This provides RAM the capacity that is needed for the data being used actively
	- What happens to Memory when the System hibernates?
		- RAM content can be turned into a hibernation file `hiberfil.sys` which is placed on the Disk (usually on the C: drive)
		- The purpose of the hibernation file is to resume the computer while preserving the state of the running programs
		- Access the hibernation file can provide valuable information about the Machine's state when it entered hibernation mode
	- Crash Dumps
		- Crash dumps are needed for debugging purposes
		- Windows provides options for dumping crash files when a crash happens
		- Some configs store the volatile data about the running processes, system configuration, etc when the crash happens
		- Which can be super useful from a forensics point of view

Pagefile - Continued
- Pagefiles extend the system's RAM
- When RAM gets full and cannot hold any more data, such as processes, network connections and so on - Windows turns to the pagefile
- How does it work?
	- It transfers less frequently used memory pages from RAM to a designated storage place on a Hard Drive
- Where is it located? 
	- By default - `C:\pagefile.sys`
- Configuration related to the page file can be found in registry:
	- `Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SessionManager\Memory Management`
	- Also within the `SYSTEM Hive`

Extracting using FTK Imager
- FTK Imager can be used to extract the `pagefile.sys`
	- Load up the volume that you want to analyze as evidence > browse to the pagefile.sys file > right-click and export it
- Analyzing the Pagefile.sys file
	- The `strings.exe` utility can be used to extract strings from the file to see if there is anything that stands out in human-readable format
	- `strings.exe .\pagefile.sys > pagefile-strings.txt` for example
- Keep in mind that the `pagefile.sys` file is 4GB'ish in size

Bulk Extractor (better than taking the `strings.exe` route imo)
- Bulk Extractor is a forensics tool for scanning and extracting files and critical data from the provided disk images, storage devices etc
- It can extracts data from a page file
- `bulk_extractor.exe -o output .\pagefile.sys`
- You can get outputs that define URLs for example (like `url.txt` ), or domains (`domain.txt`), heaps more

Hibernation File
- `hiberfil.sys`
- This is a compression version of RAM, pretty much like a snapshot of RAM
- Some key bits of information that can be extracted:
	- Information around user activities
	- Running processes
	- Network Connections
	- Recently opened files
- Keep note that this were what was happening when the device had been put into hibernation mode
- Extracting the Hibernation File (`hiberfil.sys`)
- Same way with `FTK Imager` - export the file after you've loaded a volume into the tool
- Decompressing the `hiberfil.sys` compressed file
	- Remember that the hibernation file is compressed (or know that it is)
	- The tool "**Hibernation Recon**" can be used 
	- Make sure you have a `hiberfil.sys` file already exported from FTK Imager
	- Process the `hiberfil.sys` file when you have it exported
	- Hibernation Recon will parse the file and place a raw image in the destination you choose
	- Volatility can then be used to extract information from the decompressed hibernation file

Volatility
- `vol.exe -f <path-to-ActiveMemory.bin> windows.info.Info`
	- Will get us information around the image we just extracted and decompressed
	- The metadata about the image
- `vol.exe -f <path-to-ActiveMemory.bin> windows.pslist.PsList`
	- Information around the running processes when the system went into hibernation
- `vol.exe -f <path-to-ActiveMemory.bin> windows.pstree.PsTree`
	- More details about the processes that were running
	- The path from where the process was executed
	- The parent process
	- and so on
-  `vol.exe -f <path-to-ActiveMemory.bin> windows.cmdline.CmdLine`
	- Information around what commands were executed on the host 
- There are more Volatile plugins that can be used as well [[1.0 Types of Attacks & Defense/1.2 Defense/DFIR/Volatility|Volatility]]

Crash Dump
- The OS copies data into the paging file and moves it to the crash dump after the system is turned on 
- There are different configuration options to handle system failure
	- Control Panel -> System and Security -> System -> Advanced System Properties -> Settings (check the options under System Failure)
	- Small Memory Dump
		- Creates a small memory dump file (minidump) containing minimal information about the system state during the crash
	- Kernel Memory Dump
		- Contains all the kernel memory contents at the time of the crash
		- Kernel memory dumps can be significantly larger than small memory dump
	- Complete Memory Dump
		- Creates a dump file that contains all the contents of RAM at the time of the crash 
		- Complete memory dumps are the largest type of dump files
	- Automatic Memory Dump
		- Similar to the Kernel Memory Dump but is automatically triggered when Windows detects a system crash
		- Size is dynamically adjusted based on the amount of RAM installed on the system ensuring enough space is available to capture the necessary information
	- Active Memory Dump
		- Contains the memory dump of the active users and kernel modes
- Settings for the crash dump can be viewed in Registry Hives
	- `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl`
	- `CrashDumpEnabled` 
		- 0 - none
		- 1 - Complete
		- 2 - Kernel
		- 3 - Small
		- 7 Automatic

Reliability Monitor
- When investigating - it can be useful to check how many times the system had previously crashed and then look for crash dump files to extract information that could assist in the investigation
- Control Panel > System and Security > Security and Maintenance > Reliability Monitor

- Creating a Crash Dump
	- If a suspicious process is found, a crash dump of the active process can also be created by
		- Task Manager > right-clicking on the process > making a manual dump 
	- Go to the path where Crash Dumps are stored and save it to the desktop for further investigation
		- Usually around here: `%SystemRoot%\MEMORY.DMP` but check Startup and Recovery to be sure
- Analysing a Crash Dump
	- Remember that the amount of volatile data contained within a crash dump will depend on the type of crash configured in the settings prior to the crash
	- WinDbg
		- This is a common debugger provided by Microsoft
		- Commonly used for analyzing and debugging Windows applications, crash dumps and drivers
		- Load up the crash dump file
		- `!analyze -v`
			- To get the debugger to analyze the file
		- `!time`
			- To get the time of the crash
		- `!sysinfo`
			- To get System Information 
			- `!sysinfo cpuinfo`
			- There are others parameters/options you can switch as well under `!sysinfo`
				- `!sysinfo [ cpuinfo | cpumicrocode | cpuspeed | gbl | machineid | registers | smbios ] [-csv | -noheaders]`
		- `!vm`
			- To get information around the physical and virtual memory usage on the system
			- Also brings out a list of processes that were running as well 
		- `.tlist`
			- Displays all running processes on the system 
		- Extracting Process Details
			- `!process 0 0`
				- Extracts information about running processes, parent process, session, ID's etc
		- PEB (Process Environment Block)
			- !peb
			- The PEB is a data structure that is maintained by the OS that contains information about the Win Environment and the state of the process, including the configuration settings, environment variables and so on

Memory Forensics
- A subset of computer forensics that analyzes volatile memory - normally on a compromised computer
- Memory analysis can help us with an immediate snapshot of an application's or a timestamp of an attackers actions
- Crucial since evidence collected through memory forensics can become invaluable in creating a chronology of events
- Memory Forensics can be broken down into two main phases
	- Memory Acquisition
		- Live memory is dumped - ie copied to a file
		- This allows for memory analysis to be performed without risking the loss of data from an inadvertent reboot on the compromised system
	- Memory Analysis
		- The obtained memory dump is analyzed

Memory Acquisition
- Several ways to acquire memory from the target machine - some tools can assist
- Imaging Tools
	- Windows
		- FTK Imager
			- https://www.exterro.com/digital-forensics-software/ftk-imager
		- WinPmem
			- https://github.com/Velocidex/WinPmem
	- Linux
		- LIME
			- https://github.com/504ensicsLabs/LiME
	- MacOS
		- OSXPmem
			- https://code.google.com/archive/p/pmem/wikis/OSXPmem.wiki
Memory Analysis
- Tools
	- Volatility3
		- Can analyse memory dumps from the three different OSes
- General syntax:
	- `vol -f <memorydump.file> windows.info.Info`
		- Just an example
- Searching for Suspicious Activity
	- Network Activity
		- `vol -f <memdump.file> windows.netstat.NetStat` 
		- Look out for suspicious connections, access to sites
	- Processes that are running
		- `vol -f <memdump.file> windows.pstree.PsTree`
		- Check the names of the process running
			- Mal-actors commonly use names to try to disguise the process
		- Common Windows Processes would be:
			- System
				- smss.exe
			- csrss.exe
			- wininit.exe
			- services.exe
				- svchost.exe
					- RuntimeBroker.exe
					- taskhostw.exe
				- lsaiso.exe
				- lsass.exe
			- winlogon.exe
			- explorer.exe
		- Examine files accessed that are stored in the Memory Dump - to see if you can form a connection between the executable that was run and where it was run from
			- `vol -f <memdump.file> windows.filescan.FileScan`
		- More detailed information like when the file was accessed or modified
			- `vol -f <memdump.file> windows.mftscan.MFTScan`
		- `windows.memmap`
			- `vol -f <memdump.file> -o . windows.memmap --dump --pid <pid-number>`
			- this will create a new .dmp file 
			- `strings` the file
			- Will show more information around what human-readable information is contained with the given subject/artifact
			- 