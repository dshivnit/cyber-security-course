https://tryhackme.com/room/windowseventlogs

- Windows Event Logs are not text files that can be viewed using a text editor. 
- The raw data can be translated into XML using the Windows API 
- The events are stored in proprietary binary format with a `.evt` or `.evtx` extension. 
	- `.evtx` file extensions normally reside in `C:\Windows\System32\winevt\Logs`

- Elements of a Windows Event Log
	- System Logs
		- Events associated with OS segments
		- Could include
			- hardware changes
			- device drivers
			- system changes
			- other activities related to the device
	- Security Logs
		- Events connected to logon and logoff activities on a device
		- The system's audit policy specifies the events
		- Excellent source for analysts to investigate attempted or successful unauthorised activity
	- Application Logs
		- Related to applications installed on a system
		- Main pieces include
			- application errors
			- events
			- warnings
	- Directory Service Events
		- AD (Active Directory) changes and activities, mainly on DCs (Domain Controllers)
	- File Replication Service Events
		- Associated with Windows Servers during the sharing of Group Policies and logon scripts to DCs from where they may be accessed by the users through the client servers
	- DNS Event Logs
		- DNS servers use these logs to record domain events
	- Custom Logs
		- Logged by applications that require custom data storage
		- Allows applications to control the log size or attach other parameters, such as ACLs, for security purposes

- Event Types of an Event Log
	- https://learn.microsoft.com/en-us/windows/win32/eventlog/event-types
	- Error
		- Indicates a significant problem such as a loss of data or loss of functionality
	- Warning
		- An event that is not necessarily significant, but may indicate a possible future problem
			- ie, when disk space is low
		- If an application can recover from an event without loss of functionality or data
	- Information
		- Describes the successful operation of an application, driver, or service
			- ie like when a network driver loads successfully
	- Success Audit
		- Records an audited security access attempt that is successful 
			- ie a User's successful attempt to log on to the system 
	- Failure Audit
		- Records an audited security attempt that fails
			- ie a User tries to access a network drive and fails

- Methods to access these Event Logs on a Windows System
	- Event Viewer (GUI-based)
	- Wevutil.exe (CLI-based)
	- Get-WinEvent (PowerShell cmdlet)

- Event Viewer
	- A Microsoft Management Console (MMC) snap-in
	- Alongside your usual properties such as creation date of the log, modified, last accessed - log properties will define maximum set log size and what action to take once criteria has been met
		- This concept is known as **log rotation**
		- These rules/criteria are normally defined by corporations 
	- "Clear Log"
		- There can be legitimate reasons to use this function, such as during security maintenance
		- However, adversaries will likely attempt to clear the logs to go undetected
		- **Note:** 
			- This is the only method to remove the event logs for any given event provider
	- Event ID
		- Predefined numerical value that maps to a specific operation or event
			- Based on the log source
		- Not necessarily unique
			- As again, they are based on the log source (vendor/provider of the log)
	- Connecting to another computer
		- Right-click on `Event Viewer (Local)` on the left pane, at the top of the list of event log providers
			- Click on `Connect to Another Computer`
	- *Handy to note*
		- *Applications and Services Logs > Microsoft > Windows > Powershell > Operations*
			- *Event ID 4104*
				- *Task Category: Execute a Remote Command*

- **wevutil.exe**
- https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/wevtutil
	- Can be used to install and uninstall manifests, run queries, and to export, archive and clear logs
	- Example:
		- `wevtutil qe Application /c:3 /rd:true /f:text`
			- Reading three Application logs with reverse direction, and printing events in easy to read text.

- Get-WinEvent
- https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.diagnostics/get-winevent?view=powershell-5.1 **READ THROUGH THESE, real good examples**
	- PowerShell cmdlet
	- Gets events from event logs and event tracing log files on local and remote machines
	- Provides information on event logs and event log providers.
	- Ability to combine numerous events from multiple sources into a single command and filter using:
		- XPath queries
		- structured XML queries
		- and hash table queries. 
	- Replaces the Get-EventLog cmdlet
	- Example usage:
		- `Get-WinEvent -ListLog *`
		- `Get-WinEvent -ListProvider *`
		- `Get-WinEvent -LogName Application`
	- Log Filtering using `Where-Object`
		- `Get-WinEvent -LogName Application | Where-Object { $_.ProviderName -Match 'WLMS' }`
			- Note WLMS is Windows License Monitoring Service
		- When working with large event logs, it's inefficient to send objects down the pipeline to a `Where-Object` command
			- Using `FilterHashtable` parameter is recommended to filter event logs
			- ```
			```
			 Get-WinEvent -FilterHashtable @{ LogName='Application' ; ProviderName='Microsoft-Windows-WMI' }
			```
			- Hashtable Guidelines
			- https://learn.microsoft.com/en-us/powershell/scripting/samples/creating-get-winevent-queries-with-filterhashtable?view=powershell-7.5&viewFallbackFrom=powershell-7.1
				- Begin the hash table with an `@` sign
				- Enclose the hash table with curly brackets `{` and `}`
				- Enter one or more key-value pairs for the content of the hash table
				- Use an equal sign (`=`) to separate each key from its value
				- Don't need to use a semicolon if you separate each key/value with a new line
			- Accepted key/value pairs for the `-FilterHashtable` parameter
				- LogName (String)
				- ProviderName (String)
				- Path (String) - No wildcard
				- Keywords (Long) - No wildcard
				- ID (Int32) - No wildcard
				- Level (Int32) - No wildcard
					- 5 - Verbose
					- 4 - Informational
					- 3 - Warning
					- 2 - Error
					- 1 - Critical
					- 0 - LogAlways
				- StartTime (DateTime) - No wildcard
				- EndTime (DateTime) - No wildcard
				- UserID (SID) - No wildcard
				- Data (String) - No wildcard
				- `<named-data>` (String) - No wildcard
			- When building a query with a hash table - Microsoft recommends making the hash table one key-value pair at a time
				- Event Viewer can provide quick information on what you need to build your hash table
					- Log Name
					- Event ID
					- Level
					- Source - Being the Provider Name
			- A handy command (from THM):
			```
			Get-WinEvent -FilterHashtable @{LogName='Microsoft-Windows-PowerShell/Operational'; ID=4104} | Select-Object -Property Message | Select-String -Pattern 'SecureString'
			```

- X-Path Queries
- https://www.w3.org/TR/1999/REC-xpath-19991116/
- https://learn.microsoft.com/en-us/windows/win32/wes/consuming-events#xpath-10-limitations
- https://learn.microsoft.com/en-us/previous-versions/dotnet/netframework-4.0/ms256115(v=vs.100)
	- The W3C created XPath, or **XML Path Language** 
	- Provides a standard syntax and semantics for addressing parts of an XML document and manipulating strings, numbers and booleans
	- The Windows Event Log supports a subset of XPath 1.0
	- Example:
		```
		// The following query selects all events from the channel or log file where the severity level is less than or equal to 3 and the event occurred in the last 24 hour period (note the 86400000 is in milliseconds)

		XPath Query: *[System[(Level <= 3) and TimeCreated[timediff(@SystemTime) <= 86400000]]]
		```
	- XPath events start with `*` or `Event`
	- Event Viewer can assist in constructing queries 
	- Both `wevtutil` and `Get-WinEvent` support XPath Queries as event filters
		- Event Viewer
			- Bottom-half of the middle pane > Details > XML View
			- First part is the `event` or `*`
			- Then we have `System`
			- Then the `Provider Name`, `EventID` 
			- And so on
		- Get-WinEvent
			- `PS C:\Users\Administrator> Get-WinEvent -LogName Application -FilterXPath '*/System/EventID=100'`
				- Note the `-FilterXPath` is being used to filter log results in this case
			- `PS C:\Users\Administrator> Get-WinEvent -LogName Application -FilterXPath '*/System/Provider[@Name="WLMS"]'`
			- `Get-WinEvent -LogName Application -FilterXPath '*/System/EventID=101 and */System/Provider[@Name="WLMS"]'`
			- `Get-WinEvent -LogName Application -FilterXPath '*/System/Provider[@Name="WLMS"] and */System/TimeCreated[@SystemTime="2020-12-15T01:09:08.940277500Z"]'`
		- `wevtutil.exe`
			- `C:\Users\Administrator>wevtutil.exe qe Application /q:*/System[EventID=100] /f:text /c:1`
				- Note that we have used the `/q` parameter - which is an XPath query in `wevutil`
	- Queries for elements within `EventData`
		- `Get-WinEvent -LogName Security -FilterXPath '*/EventData/Data[@Name="TargetUserName"]="System"'`
			![](https://assets.tryhackme.com/additional/win-event-logs/xpath-7b.png)

- EventIDs
-  **Good Cheatsheet!** - https://static1.squarespace.com/static/552092d5e4b0661088167e5c/t/580595db9f745688bc7477f6/1476761074992/Windows+Logging+Cheat+Sheet_ver_Oct_2016.pdf
- Spotting the Adversary with Windows Event Log Monitoring - https://web.archive.org/web/20190115215749/https://apps.nsa.gov/iaarchive/customcf/openAttachment.cfm?FilePath=/iad/library/ia-guidance/security-configuration/applications/assets/public/upload/Spotting-the-Adversary-with-Windows-Event-Log-Monitoring.pdf&WpKes=aF6woL7fQp3dJiqyJL2LenrLxuHC7ztGtVNK3x
- Real good list of EventID's to look out for, from Microsoft - https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/plan/appendix-l--events-to-monitor
- MITRE ATT&CK - https://attack.mitre.org/
	- -------------------------------------------------------------------
	- You need to know what you're looking for when monitoring and hunting.
	- And there are a large number of EventIDs..
	- Some events will not be generated by default, and certain features will need to be enabled and configured on the endpoint
		- Such as PowerShell logging
		- Can be enabled via Group Policy, or the Registry
			- Some resources:
				- https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_logging_windows?view=powershell-7.5&viewFallbackFrom=powershell-7.1
					- Microsoft
				- https://cloud.google.com/blog/topics/threat-intelligence/greater-visibility/
					- From Google
				- https://docs.splunk.com/Documentation/UBA/5.0.4/GetDataIn/AddPowerShell
					- Splunk
		- Another feature to enable and configure is **Audit Process Creation**
			- Event ID 4688
			- This will allow **command-line process auditing**
			- `Local Computer Policy > Computer Configuration > Administrative Templates > System > Audit Process Creation`
				- https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/manage/component-updates/command-line-process-auditing#try-this-explore-command-line-process-auditing
- **Seek, learn, find out.**
