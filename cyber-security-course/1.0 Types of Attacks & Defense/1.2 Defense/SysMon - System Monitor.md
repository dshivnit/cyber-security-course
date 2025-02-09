https://tryhackme.com/room/sysmon

- Used to monitor and log events on Windows 
- Commonly used by enterprises as part of their monitoring and loggin solutions
- It's a part of the Sysinternals package
- Similar to Windows Event Logs with further details and granular control

- A Windows system service and device driver that once it has been installed on a system, it will remain resident across system reboots to monitor and log system activity to the Windows event log
	- It provides detailed information about
		- process creations
		- network connections
		- and changes to file creation time
- Gathers detailed and high-quality logs as well as event tracing that assists in identifying anomalies in the environment
- Commonly used with SIEMs

- Events within Sysmon are stored in:
	- `Applications and Services Logs/Microsoft/Windows/Sysmon/Operational`

Sysmon Config Overview
- A config file is required in order to tell the binary how to analyse the events that it is receiving
- One can be created, or downloaded..
	- One example from SwiftOnSecurity
		- https://github.com/SwiftOnSecurity/sysmon-config
- Includes 29 different types of EventIDs

- Some important EventIDs:
	- Event ID 1 : Process Creation
		- As its name depicts, this event will look for any processes that have been created
		- Can be used to look for known suspicious processes or processes with typos that could be considered anomalous 
		- You can exclude processes such as `svchost.exe` one that is generated quite a fair bit! 
			- So you can fine-tune the kind of results that come up in the config it sounds like
	- Event ID 3 : Network Connection
		- This event will look for events that occur remotely
		- Will include files and sources of suspicious binaries as well as opened ports
	- Event ID 7 : Image Loaded
		- Looks for DLLs loaded by processes 
			- Useful for when hunting for DLL injection and DLL hijacking attacks
		- CAUTION : Causes high system load
		- Uses the Image, Signed, ImageLoaded and Signature XML tags
	- Event ID 8 : CreateRemoteThread
		- Monitors for processes injecting code into other processes
		- Used for legitimate tasks and applications
		- Can also be used by malware to hide malicious activity
		- Uses the SourceImage, TargetImage, StartAddress, and StartFunction XML tags
	- Event ID 11 : File Created
		- Logs events when files are created (heh) or overwritten on the endpoint
		- Uses TargetFilename XML tag
	- Event ID 12 / 13 / 14 : Registry Event
		- Looks for changes or modifications in the registry
		- Malicious activity could include persistence and credential abuse
		- Uses TargetObject XML tags
	- Event ID 15 : FileCreateStreamHash
		- Looks for files created in an alternate data stream
		- Common technique by threat actors to hide malware
	- Event ID 22 : DNS Event
		- Logs all DNS queries and events for analysis
		- Common way to deal with this is to exclude all trusted domains that you know very well (which would otherwise cause NOISE)
		- Once the common/baseline domains have been excluded, you can then look out for anomalies 

Installation of Sysmon
- Via Sysinternals or the Microsoft website
Starting Sysmon
- via Powershell or CMD prompt
	- As admin of course
- `sysmon.exe -accepteula -i ..\Configuration\swift.xml`
	- Point the launch to a configuration script you have handy, such as the one mentioned earlier (https://github.com/SwiftOnSecurity/sysmon-config) and another one in this module being looked at is here (https://github.com/ion-storm/sysmon-config/blob/develop/sysmonconfig-export.xml)
- **Once Sysmon has started you can look at Event Viewer to monitor events**
- Events will be under:
	- `Applications and Services Logs/Microsoft/Windows/Sysmon/Operational`

This module will be covering anomalous activities present in threats such as 
- Ransomware
- Persistence
- Mimikatz
- Metasploit
- and C2

It will always come down to using an ample and efficient configuration file as it can do a lot of the *heavy lifting* for us.

Sysmon Best Practices
- Exclude > Include
	- Typically best to prioritize excluding events rather than including them 
	- Prevents you from accidentally missing crucial events and only seeing the events that matter the most
- CLI gives you further control
	- As is common with most applications!
	- `Get-WinEvent` or `wevutil.exe` to access and filter logs (there is another article on that in this book/repo somewhere)
	- As integration into SIEM and other tools takes place, the reliance on the above tools will not be so commonplace after a while
- Know your environment before implementation
	- Baseline processes
		- So you know what is 'normal' or can be considered to be

- Loading a config file:
	- `sysmon.exe -accepteula -i <path-to-file>\config.xml`

Filtering Events with Event Viewer
- Main filter that one would use is filtering by `EventID` along with keywords
- You can also choose to filter by writing XML but this can be a tedious process (!) that doesn't scale well..

Filtering Events with PowerShell
- `Get-WinEvent` along with `XPath` (refer to the other page - Event Viewer [[Windows Event Logs - Event Viewer - Get-WinEvent - wevutil.exe]])
- The above tools allow for further granular control and filtering whereas the Event Viewer GUI does not.
	- Main filters we will be considering in this scenario:
		- Filter by EventID
			- `*/System/EventID=<ID>`
		- Filter by XML Attribute/Name
			- `*/EventData/Data[@Name="<XML Attribute/Name">]`
		- Filter by Event Data
			- `*/EventData/Data=<Data>`
	- These filters can be brought together with various attributes and data to get the most control out of our logs
	- Example:
		- `Get-WinEvent -Path <path-to-log> -FilterXPath '*/System/EventID=3 and */EventData/Data[@Name="DestinationPort] and */EventData/Data=4444'`
		- `Get-WinEvent -Path C:\Users\THM-Analyst\Desktop\Scenarios\Practice\Filtering.evtx -Oldest -FilterXPath '*/System/EventID=3' -MaxEvents 1 | Select-Object -Property *`
			- Good way to get properties of the event returned and also a good way to filter it down to the most earliest event

Hunting Metasploit
- This scenario will be focusing on hunting the Metasploit Meterpreter Shell
- By default - Metasploit tends to use port `4444` (and `5555` can be considered)
- A document with some information around how malware and payloads interact with networks:
	- https://docs.google.com/spreadsheets/d/17pSTDNpa0sf6pHeRhusvWG6rThciE8CsXTSlDUAZDyo/edit
		- Hunting for Open Ports with PowerShell
		- Can use `XPath` to filter out events from `NetworkConnect` with `DestinationPort` 
			- `Get-WinEvent -Path <path-to-logfile> -FilterXPath '*/System/EventID=3 and */EventData/Data[@Name="DestinationPort"] and */EventData/Data=4444'`
 
Detecting Mimikatz Overview
- Mimikatz is a well-known credential dumper
- Known for mainly dumping LSASS (Local Security Authority Subsystem Service)
- Albeit that current Anti-Virus systems will pick up Mimikatz as its signatures are widely known - threat actors may still use it  to obfuscate or use droppers to get the file on to the device
- For the better part one will need **more advanced threat hunting techniques like searching for LSASS behaviour**
- Hunting Abnormal LSASS Behaviour
	- The ProcessAccess EventID (EventID 10)
	- Recall that excluding common processes like `svchost.exe` should be taken into consideration to cut down the amount of noise reported by Sysmon and the logs
		```
		<RuleGroup name="" groupRelation="or">  
		<ProcessAccess onmatch="include">  
	    <TargetImage condition="image">lsass.exe</TargetImage>  
		</ProcessAccess>  
		</RuleGroup>
		
		<RuleGroup name="" groupRelation="or">  
		<ProcessAccess onmatch="exclude">  
		<SourceImage condition="image">svchost.exe</SourceImage>  
		</ProcessAccess>  
		<ProcessAccess onmatch="include">  
		<TargetImage condition="image">lsass.exe</TargetImage>  
		</ProcessAccess>  
		</RuleGroup>
		```
- Detecting LSASS Behaviour with PowerShell
	- `Get-WinEvent -Path <path-to-log-file> -FilterXPath '*/System/EventID=10 and */EventData/Data[@Name="TargetImage"] and */EventData/Data="C:\Windows\system32\lsass.exe`

Hunting Malware Overview
- Two main kinds of malware that will be focused on are RATs and Backdoors
	- (in this scenario)
- RATs typically use a Client-Server model and comes with an interface for easy user administration
- Different from payloads like MSFVenom
	- Examples are `Xeexe` and `Quasar`
- Hunting RATs and C2 Servers
	```
	<RuleGroup name="" groupRelation="or">  
	<NetworkConnect onmatch="include">  
	<DestinationPort condition="is">1034</DestinationPort>  
	<DestinationPort condition="is">1604</DestinationPort>  
	</NetworkConnect>  
	<NetworkConnect onmatch="exclude">  
	<Image condition="image">OneDrive.exe</Image>  
	</NetworkConnect>  
	</RuleGroup>
	```
	- Be careful to not exclude well-used ports such as `53` (DNS) as this port can be exploited by threat actors
		- And similar ports
- Hunting for Common Back Connect Ports with PowerShell
	- Filtering on the `NetworkConnect` EventID (`3`)
	- Again, **if one is using a good configuration file with a reliable set of rules, it will do the majority of the heavy lifting and filtering to what you want**
	- `Get-WinEvent -Path <path-to-log-file> -FilterXPath '*/System/EventID=3 and */EventData/Data[@Name="DestinationPOrt"] and */EventData/Data=<port>'`

Hunting Persistence Overview
- Used by threat actors to maintain access to a system once that system has been compromised
- Focusing on registry modifications and startup scripts in this instance/scenario
- Look for File Creation events as well as Registry Modification events
- Hunting Startup Persistence
	- Perhaps looking for detections for a file being placed in the `\Startup\` or `\Start Menu` directories
	```
	<RuleGroup name="" groupRelation="or">  
	<FileCreate onmatch="include">  
	<TargetFilename name="T1023" condition="contains">\Start Menu</TargetFilename>  
	<TargetFilename name="T1165" condition="contains">\Startup\</TargetFilename>  
	</FileCreate>  
	</RuleGroup>
	```
	- Any changes to the Start Menu should be investigated.
- Hunting Registry Key Persistence
	```
	<RuleGroup name="" groupRelation="or">  
	<RegistryEvent onmatch="include">  
	<TargetObject name="T1060,RunKey" condition="contains">CurrentVersion\Run</TargetObject>  
	<TargetObject name="T1484" condition="contains">Group Policy\Scripts</TargetObject>  
	<TargetObject name="T1060" condition="contains">CurrentVersion\Windows\Run</TargetObject>  
	</RegistryEvent>  
	</RuleGroup>
	```

Detecting Evasion Techniques
- ADS - Alternate Data Streams
	- Sysmon comes with an EventID to detect newly created and accessed streams allowing, allowing quick detection of malware that uses ADS
- Injections
	- Thread Hijacking
	- PE Injection
	- DLL Injection
		- Backdooring DLLs
	- more
- Masquerading
- Packing/Compression
- Recompiling
- Obfuscation
- Anti-Reversing Technique
- Hunting ADS (Alternate Data Streams)
	- Event ID 15
		- EventID 15 will hash and log any NTFS Streams that are included within the Sysmon config file
		```
		<RuleGroup name="" groupRelation="or">  
		<FileCreateStreamHash onmatch="include">  
		<TargetFilename condition="contains">Downloads</TargetFilename>  
		<TargetFilename condition="contains">Temp\7z</TargetFilename>  
		<TargetFilename condition="ends with">.hta</TargetFilename>  
		<TargetFilename condition="ends with">.bat</TargetFilename>  
		</FileCreateStreamHash>  
		</RuleGroup>
		```
- Detecting Remote Threads
	- Remote threads can be used to evade detections in combination with other techniques
	- Remote threads are created using the Windows API `CreateRemoteThread` and can be accessed using `OpenThread` and `ResumeThread`. 
	- Can be used in multiple evasion techniques, like:
		- DLL injection
		- Thread hijacking
		- Process hallowing
	- `EventID 8`
		- (this being from the SwiftOnSecurity Sysmon config file)
	- Exclude common remote threads (reduce noise)
		```
		<RuleGroup name="" groupRelation="or">  
		<CreateRemoteThread onmatch="exclude">  
		<SourceImage condition="is">C:\Windows\system32\svchost.exe</SourceImage>  
		<TargetImage condition="is">C:\Program Files (x86)\Google\Chrome\Application\chrome.exe</TargetImage>  
		</CreateRemoteThread>  
		</RuleGroup>
		```
		- The above is evidently showing that powershell.exe is creating a remote thread and accessing notepad.exe 
			- A PoC and could in theory execute any other kind of executable or DLL
			- This is called a Reflective PE Injection (Reflective code loading - https://attack.mitre.org/techniques/T1620/)
- Detecting Evasion Techniques with PowerShell
	- Only need to filter the EventID in this instance as we are using the rules stated by the config file written by SwiftOnSecurity
	- `Get-WinEvent -Path <path-to-logfile> -FilterXPath '*/System/EventID=8'`
	- 