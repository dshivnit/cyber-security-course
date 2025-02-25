- Log Analysis
	- Sysmon
	- Firewall
	- Endpoint Logs
		- EvtxEcmd (EZ Tool)
			- CLI tool that can create a CSV output of a SysMon .evtx (eventviewer) file
		- Timeline Explorer (EZ Tool)
			- GUI tool
			- Load CSVs
		- SysmonView
			- Export SysMon logs into an XML file via Event Viewer
			- You can then view correlated events related to a specific process
		- Event Viewer
	- Network Logs
		- Wireshark
		- Brim
- Event Correlation
	- Time/Date(s)
	- Source / Destination IPs
	- Source / Destination Ports
	- Actions Taken
	- Protocols Used
	- Process Name(s)
	- User Account(s)
	- Machine Name(s)
- Hashes
	- Get them for relevant artefacts 

`lnkparse`
- Good tool to be able to get information from shortcut files that come in as email attachments

Elastic
- Ensure these are options in the column table view (or whatever you want) to make searches/analysis more efficient!!!!!
	- process.parent.executable
	- The executable itself
	- process.args
	- host.hostname

Oletools Suite
- `olevba` - a tool for analyzing and extracting VBA macros from MS Office documents

Bypassing UAC processes
- `fodhelper.exe`
- `eventvwr.exe`
- `rundll32.dll`
- 1. **Fileless Attacks:** Attackers can leverage legitimate Windows utilities like `fodhelper.exe`, `eventvwr.exe`, or `sdclt.exe` to execute commands with elevated privileges without triggering a UAC prompt. These utilities have auto-elevate properties, meaning they do not require user interaction for elevation.
1. **DLL Hijacking:** Attackers can exploit vulnerable processes that load DLLs in an unsafe manner. By placing a malicious DLL in a location that the process checks first, the attacker can gain elevated privileges when the process loads the malicious DLL.
2. **Windows Installer (msiexec.exe):** The Windows Installer can be used to bypass UAC by launching an MSI package with elevated privileges. Attackers may use this to install malicious software without triggering a UAC prompt.
3. **Token Manipulation:** Attackers can manipulate access tokens to escalate privileges. For example, they may use a standard user’s token to impersonate an administrator and execute processes with elevated privileges.
4. **COM Object Hijacking:** COM objects (Component Object Model) are used extensively in Windows. Attackers can register a malicious COM object that gets called by a process with elevated privileges, allowing them to bypass UAC.
5. **Scheduled Tasks:**Attackers can create or modify scheduled tasks that run with elevated privileges. By doing so, they can execute their payloads with administrator rights without triggering UAC.

