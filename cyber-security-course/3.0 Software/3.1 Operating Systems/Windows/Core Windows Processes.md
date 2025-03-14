**Core Windows Processes (from a Defense perspective)**
- https://0xcybery.github.io/blog/Core-Processes-In-Windows-System
- https://tryhackme.com/r/room/btwindowsinternals
	- https://learn.microsoft.com/en-us/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode
	- User Mode
		- Each application is provided with a private virtual address space where other user applications that are running can not manipulate or access one another's virtual-memory/address space
	- Kernel Mode
		- Also assigned a virtual private address but the difference is that kernel-mode drivers aren't isolated from other drivers or the OS. 
		- If a kernel-mode driver accidentally writes to the wrong virtual address, it could compromise the data belonging to the operating system or another driver
		- If a kernel-mode driver crashes, it causes the entire OS to crash

	***Make sure to have the binary path column visible and sorted when looking for random/potentially-rogue binary paths!***
	- Process Explorer
		- https://learn.microsoft.com/en-us/sysinternals/downloads/process-explorer
	- Process Hacker (pretty good)
		- https://processhacker.sourceforge.io/downloads.php

	- System Processes
		- **ntoskrnl.exe** (PID 4 - always)
		- https://malwaretips.com/blogs/ntoskrnl-exe-what-is-ntoskrnl-exe-should-i-remove-it/
			- Central component of the Win OS 
			- Handles:
				- Memory management and paging
				- Processor scheduling and thread management
				- Object and security management
				- I/O management
				- Interrupt handling
				- Networking and inter-process communication
			- Lives in:
				- C:\Windows\System32
			- Parent Process
				- System Idle Process (PID 0)
		- **smss.exe**
		- https://en.wikipedia.org/wiki/Session_Manager_Subsystem
				- Lives in:
					- C:\Windows\System32
				- Parent Process
					- System (4)
				- Instances:
					- One parent/master instance and child instance per session
						- Child instance exits after creating the session
				- Local Account:
					- Local System
					- NT AUTHORITY\SYSTEM
			- Session Manager Sub-System
			- Monitors different system processes and makes sure that they run correctly 
			- Also responsible for creating new sessions
			- User-mode application that is started by the kernel
			- Starts 
				- Session 0 (an isolated Windows session for the OS):
					- csrss.exe
					- wininit.exe 
				- Session 1 (user-session)
					- csrss.exe
					- winlogon.exe
			- The first child instance creates new child instances in new sessions, via smss.exe copying itself into the new session and self-terminating
			- Any other subsystem listed in the `Required` value of `HKLM\System\CurrentControlSet\Control\Session Manager\Subsystems` is also launched
			- Also responsible for creating environment variables, virtual memory paging files and starts winlogon.exe
		- **csrss.exe**
			- https://en.wikipedia.org/wiki/Client/Server_Runtime_Subsystem
				- Lives in:
					- %SystemRoot%\System32\csrss.exe
				- Parent Process: 
					- Created by an instance of smss.exe (which is self-terminated shortly after, so there should be a non-existent process as the parent)
				- Number of instances:
					- Two or more
				- User Account
					- Local System
					- NT AUTHORITY\SYSTEM
			- Client Server Runtime Process
			- The user-mode side of the Windows Sub-System
			- Always running, a critical process
			- Responsible for the WIn32 console window and process threat creation and deletion
				- For each instance a:
					- csrsrv.dll
					- basesrv.dll
					- winsrv.dll 
					are loaded, along with others.
			- Also responsible for making the Windows API available to other processes, mapping drive letters, and handling the Windows shutdown process. 
		- **wininit.exe**
				- Lives in 
					- %SystemRoot%\System32
				- Parent process is 
					- smss.exe (remember it kills its instance shortly after starting wininit.exe)
				- Number of instances
					- one
				- User Account
					- Local System
					- NT AUTHORITY\SYSTEM
			- Windows Initialisation Process
			- launches within Session 0
				- services.exe
					- Service Control Manager
				- lsass.exe
					- Local Security Authority
				- **lsaiso.exe**
					- Associated with Credential Guard and KeyGuard
					- This will only be seen if Credential Guard is enabled
		- **SCM (Service Control Manager) or services.exe**
			- https://en.wikipedia.org/wiki/Service_Control_Manager
				- Path: 
					- %systemroot%\system32
				- Parent: 
					- wininit.exe
				- Instances:
					- One
				- User Account:
					- Local System
					- NT AUTHORITY\SYSTEM
			- Handles system services
				- loading services
				- Interacting with services
				- Starting and stopping services
			- Maintains a database that can be queried using a Windows built-in utility, `sc.exe`
			- Information regarding services stored in registry is located in:
				- `HKLM\System\CurrentControlSet\Services`
			- This process also loads device drivers marked as auto-start into memory
			- Upon successful user logon, services.exe is responsible for setting the value of the "Last Known Good" control set (Last Known Good Configuration) to that CurrentControlSet
				- `HKLM\System\Select\LastKnownGood`
			- `services.exe` is the parent of other key processes:
				- `svchost.exe`
				- `spoolsv.exe`
				- `msmpeng.exe`
				- `dllhost.exe`
		- **wininit.exe > services.exe > svchost.exe**
		- https://en.wikipedia.org/wiki/Svchost.exe
				- Path
					- %systemroot%\system32\
				- Parent:
					- services.exe
				- Number of instances:
					- MANY!
				- User Account: 
					- Varies
					- (SYSTEM, Network Service, Local Service)
					- Depends on the svchost.exe instance
					- Win10 sometimes the instances may run as the logged-in user
				- Image
			- Service Host 
				- Host Process for Windows Services
			- Responsible for hosting and managing Windows services
			- The services that run in this process are implemented as DLLs
			- The DLL to implement is stored in:
				- `HKLM\SYSTEM\CurrentControlSet\Services\'SERVICE-NAME'\Parameters`
					- `ServiceDLL` subkey
			- When looking at various services in ProcessHacker (SystemInformer) take note of a services properties
				- The binary path will always have a `-k` in it
				- Showing that it is a legitimate `svchost.exe` process that is called
			- `-k` parameter
			- `C:\WINDOWS\system32\svchost.exe -k DcomLaunch -p`
				- Grouping similar services to share the same process
				- Concept was based on the OS design and implemented to reduce resource consumption
				- Started from Win10 v1703
				- Services grouped into host processes changed
				- For machines that run on more than 3.5GB of memory, each service will run its own process
			- Since `svchost.exe` will have multiple running processes on any Win system, this process has thus been made a target for malicious use.
				- Adversaries will create malware to masquerade as this process and try to hide amongst the legitimate svchost.exe processes
				- They can name the malware svchost.exe or misspell it a little, like `scvhost.exe`
				- Trying to get under the radar essentially
				- Another tactic is to install/call a malicious service (DLL)
				- https://www.hexacorn.com/blog/2015/12/18/the-typographical-and-homomorphic-abuse-of-svchost-exe-and-other-popular-file-names/ - article
		- `lsass.exe`
		- https://en.wikipedia.org/wiki/Local_Security_Authority_Subsystem_Service
				- PATH:
					- %SystemRoot\System32
				- Parent:
					- wininit.exe
				- Number of instances:
					- One
				- User Account:
					- Local System
					- NT AUTHORITY\SYSTEM
			- Local Security Authority Subsystem Service
			- Responsible for enforcing the security policy on the system
			- Verifies users logging on to a Windows computer or server, handles password changes, and creates access tokens
			- It also writes to the Windows Security Log
			- It creates security tokens for SAM (Security Account Manager), AD, and NETLOGON.
			- It uses authentication packages specified in
				- `HKLM\System\CurrentControlSet\Control\Lsa`
			- Another target for adversaries
				- **mimikatz** can be used to dump credentials, or threat actors may mimic this process to hide in plain sight
					- Changing the spelling of the malicious service/program only slightly 
			- https://yungchou.wordpress.com/2016/03/14/an-introduction-of-windows-10-credential-guard/
		- **winlogon.exe**
		- https://en.wikipedia.org/wiki/Winlogon
				- Path:
					- %SystemRoot%\System32\
				- Parent:
					- smss.exe (but recall that smss.exe will kill its process instance once netlogon.exe loads)
				- Number of instances:
					- >=1
				- User Account
					- Local System
					- NT AUTHORITY\SYSTEM
			- Windows Logon process
			- Responsible for handling the Secure Attention Sequence (SAS)
				- The ALT+CTRL+DEL combo to enter uname and pword :) 
			- Also responsible for loading the user profile
			- Loads the users **`NTUSER.DAT`** into `HKCU` and **userinit.exe** loads the user's shell. 
			- https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc939862(v=technet.10)?redirectedfrom=MSDN
			- It is also responsible for locking the screen, running any screensavers, along with other functions
		- **explorer.exe**
			- Path:
				- %SystemRoot%\explorer.exe
			- Parent:
				- Created by userinit.exe which exits
			- Number of instances 
				- One or more (per interactively logged-in user)
			- User Account:
				- Logged-in User(s)
			- Windows Explorer
			- Gives the user access to their folders and files
			- Also provides functionality for features such as the Start Menu and Taskbar
			- Winlogon.exe runs userinit.exe which launches the value in:
				- `HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\Shell`
			- Userinit.exe exits after spawning explorer.exe
				- Meaning that the parent-process is non-existent :) 
			- explorer.exe will have numerous child-processes