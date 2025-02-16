https://tryhackme.com/r/room/digitalforensicsfundamentals
https://tryhackme.com/room/introductoryroomdfirmodule

Digital Forensics Methodology
- NIST (National Institute of Standards and Technology) define a general process for every case. 
- NIST works on frameworks for different areas of technology, including cybersec, where they introduce the process of digital forensics in four phases:
	- Collection
		- Identifying all devices from which data can be collected is essential
		- Important to ensure that the original data isn't tampered with when collecting evidence, and maintaining proper documentation containing items' collected is important as well
	- Examination
		- Data would normally need to be filtered due to the extent of how much there can be and how much of it would be relevant in the case at hand
	- Analysis
		- Correlating the data with multiple devices and pieces of evidence to be able to draw conclusions
		- Aims to extract the activities relevant to the case chronologically
	- Reporting
		- Lastly, a detailed report is prepared
		- Contains the investigations methodology, detailed findings from collected evidence, and possibly recommendations in moving forward
		- This report would then be presented to law enforcement and executive management
		- Important to include executive summaries as part of the report, considering the level of understanding of all the receiving parties

Different types of Digital Forensics
- All with their own collection and analysis methodologies
	- Computer Forensics
		- The most common type
	- Network Forensics
		- Covers investigation beyond individual devices - the entire network, network traffic logs, etc
	- Database Forensics
		- Critical data stored in dedicated DBs
		- DB Forensics investigates any intrusion into these DBs that result in data modification or exfiltration
	- Memory Forensics
		- Physical memory - much deeper dive into seeing if anything can be recovered from it
	- Mobile Forensics
		- Call records, SMSs, GPS locations, etc
	- Malware Forensics
	- Email Forensics
		- Common communication method between professionals
	- Cloud Forensics
	- Disk Forensics

Evidence Acquisition
- Proper Authorisation
	- The Forensics Team should gain authorisation from the relevant authorities before collecting any data
	- Evidence collected without prior approval may be inadmissible in court
	- Evidence normally would contain private and sensitive data of an organisation or individual - sticking within the boundaries of the law is important in making sure that the Team have the proper authority and go-ahead to look into this data prior to doing so (ie a Search Warrant)
- Chain of Custody
	- Process for documenting the evidence owners
	- Chain of Custody document
		- Contains details on all of the evidence:
			- Description of the evidence (name, type, etc)
			- Name of individuals who collected the evidence
			- Date and time of collection
			- Storage location for each piece of evidence
			- Access times and the individual record who accessed the evidence
	- We don't want the said evidence to go walkies, now do we..
	- The Chain of Custody document can prove the integrity and reliability of the evidence admitted in court. 
- Use of Write Blockers
	- While collecting data from devices taken from a crime scene, or that are a part of an investigation - some of the tools that the Digital Forensics Team may use can inadvertently alter timestamps of the files being accessed from said evidence (like an HDD)
	- Using a Write Blocker can help prevent that from happening
	- Keeping the evidential HDD in its original state as the write blocker can block any alteration to the target device whilst investigating it

Windows Forensics
- Various OSs could be used - the THM I'm looking at right now is focusing on Windows, however:
- Disk Image
	- Taking a disk image of the device that is being investigated is important - as it will save the HDD contents in a state that it was in upon collection - thus the team(s) involved can make copies of it for further analysis and so on
- Memory Image
	- Contains data inside the RAM of the device being investigated
	- Memory image should be prioritised and taken first from the system (as it is volatile)
- Tools:
	- FTK Imager
		- Widely used tool for taking disk images of Windows OSs
	- Autopsy
		- Open-source digital forensics platform
		- Can import an acquired disk image into this tool, and it will carry out an extensive analysis of the image
			- Keyword search
			- Deleted file recovery
			- File metadata
			- Extension mismatch detection
			- and more
	- Dumpit
		- Offers the utility of taking a memory image from a Win machine
		- Creates memory images using CLI and few commands
		- Memory image can be taken in different formats
	- Volatility
		- Open-source tool for analysing memory images
		- Each artifact can be analysed using a specific plugin
		- Supports various OSs
	- There other tools (more to describe on this later)

DFIR - Digital Forensics and Incident Response
- Covers the collection of forensic artifacts from digital devices such as computers, media devices, and smartphones to investigate an incident
- Helps teams to identify footprints left by an attacker when a security incident occurs - use them to determine the extent of compromise in an environment, and restore the environment to the state it was before the incident occurred. 

- Finding evidence of attacker activity in the network and sifting false alarms from actual incidents
- Robustly removing the attacker, so their foothold from the network no longer remains
- Identifying the extent and timeframe of a breach
	- This helps in communicating with relevant stakeholders
- Finding the loopholes that led to the breach
	- What needs to be changed to avoid the breach in the future
- Understanding attacker behaviour to pre-emptively block further intrusion attempts by the attacker
- Sharing information about the attacker with the community

Digital Forensics
	- These professionals are experts in identifying forensic artifacts or evidence of human activity in digital devices
Incident Response
- Incident responders are experts in cybersecurity and leverage forensic information to identify the activity of interest from a security perspective
DFIR Professionals
- These pro's know about Digital Forensics and Cybersecurity and combine these domains to achieve their goals
- DFIR domains are often combined because they are highly interdependent
- DF takes its goals and scope from the IR process
- IR leverages knowledge gained from DF and defines the extent of the forensic investigation

Artifacts
- Artifacts are pieces of evidence that point to an activity performed on a system
- They are collected to support a hypthesis or claim about attacker activity

Evidence Preservation
- The integrity of evidence collected must be maintained
- There are best practices which have been established as standards in the industry
- Note - any forensic analysis contaminates the evidence
	- Evidence is first collected, and then write-protected
	- A copy of the write-protected evidence is then used for analysis
	- This process ensures that the original artifact(s) is not contaminated and remains safe while analyzing
- If the copy that is being investigated gets corrupted, then the team(s) can return and make a new copy from the original artifact(s)

Chain of Custody
- When evidence is collected, it must be made sure that it is kept in secure custody
- Any person(s) not related to the investigation must not possess the evidence, or it will contaminate the chain of custody of the evidence
	- Contaminated artifacts lessen the integrity of data and will weaken the case being built

Order of Volatility
- RAM for example
	- Is lost when the computer is shut down
- It is vital to understand the order of volatility of the different evidence sources to capture and preserve accordingly
- Prioritize!

Timeline Creation:
- Once artifacts have been collected and their integrity maintained
	- They need to be presented understandably to fully use the information contained in them
- A timeline of events needs to be created for efficient and accurate analysis
	- The timeline of events will put all activities in a chronological order
- Provides perspective to the investigation and helps collate information from various sources to create a story of how things happened

Tools
- Eric Zimmerman's
- https://ericzimmerman.github.io/#!index.md
	- A security researcher who has written a few tools to help perform forensic analysis on the Windows platform
- KAPE
- https://www.kroll.com/en/services/cyber-risk/incident-response-litigation-support/kroll-artifact-parser-extractor-kape
	- Kroll Artifact Parser and Extractor
	- Also by Zimmerman
	- Automates the collection and parsing of forensic artifacts and can help create a timeline of events
	- A live data acquisition and analysis tool which can be used to acquire registry data
	- Primarily CLI, but also with a GUI
	- 
- Autopsy
- https://www.autopsy.com/
	- Open-source forensics platform that assists in analyzing data from digital media like mobile devices, hard drives, and removable drives
	- Plugins can assist in speeding up the forensic process, extract and to present valuable information from raw data sources
- Volatility
	- Assists in performing memory analysis for memory captures from both Windows and Linux OSes
	- Can extract valuable information from the memory of a machine under investigation
- Redline
	- Incident response tool developed by FireEye
	- Gathers forensic data from a system and helps with collected forensic information
- Velociraptor
	- Advanced endpoint-monitoring, forensics, and response platform
	- Open-source, yet powerful
- FTK Imager

---

Windows Forensics
https://tryhackme.com/room/windowsforensics1

- Windows Registry
	- A collection of databases that contain the system's configuration data
		- Hardware
		- Software
		- User Information
	- Registry Hive
		- https://learn.microsoft.com/en-us/windows/win32/sysinfo/registry-hives
		- A group of keys, subkeys and values stored in a single file on the disk
		- A User Hive for example, contains specific registry information, :
			- Application settings
			- Desktop
			- Environment
			- network connections
			- printers
			- `HKEY_USERS`
	- Structure of Registry:
		- `HKEY_CURRENT_USER`
			- Contains the root of the configuration information for the user who is *currently* logged on
			- Folders, screen colours, control panel settings are stored here
			- Associated with the user's profile
			- Subkey of `HKEY_USERS` or `HKU`
			- Abbreviated as `HKCU`
		- `HKEY_USERS`
			- Contains all actively loaded user profiles on the computer
			- Abbreviation of `HKU`
		- `HKEY_LOCAL_MACHINE`
			- Contains configuration information particular to the computer (for any user)
			- Abbreviated `HKLM`
		- `HKEY_CLASSES_ROOT`
			- Subkey of `HKLM\Software`
			-  Information here makes sure that the correct program opens when you open a file by using Windows Explorer
			- `HKLM\Software\Classes` key
				- Contains default settings that can apply to all users on the local computer
			- `HKCU\Software\Classes` key
				- Contains settings that override the default settings and apply only to the interactive user
			- `HKCR` key
				- Provides a view of the registry that merges the information from the two sources/keys above
				- Also provides a view for earlier versions of Windows
			- Changes for the current interactive user must be made within the `HKCU\Software\Classes` key instead of within `HKCR`
			- Abbreviated to `HKCR`
		- `HKEY_CURRENT_CONFIG`
			- Contains information about the hardware profile that is used by the local computer at system startup
			  
- Accessing Registry Hives Offline
	- The majority of Registry Hives are located in:
		- `C:\Windows\System32\Config`
	- `DEFAULT` - mounted on `HKU\DEFAULT`
	- `SAM` - mounted on `HKLM\SAM`
	- `SECURITY` - mounted on `HKLM\Security`
	- `SOFTWARE` - mounted on `HKLM\Software`
	- `SYSTEM` -  mounted on `HKLM\System`
	  
- Hives Containing User Information
	- Hives containing user information can be found in the User Profile directory
		- `C:\Users\<profile/user-name>`
			- `NTUSER.DAT` - mounted on `HKCU`
				- Located in `C:\Users\<profile/user-name>\`
			- `USRCLASS.DAT` - mounted on `HKCU\Software\CLASSES`
				- located in the directory `C:\Users\<profile/user-name>\Appdata\Local\Microsoft\Windows`
			- These two `.DAT` files are *hidden*
			  
- The AmCache Hive
	- Located in:
		- `C:\Windows\AppCompat\Programs\Amcache.hve`
	- Saves information on programs that were recently run on the system
	  
- Transaction Logs and Registry Backups:
	- Transaction Logs:
		- Transaction logs can be considered as the journal of the changelog of the registry hive
		- Windows often uses the transaction logs when writing data to registry hives
		- Meaning that transaction logs can often have the latest changes in the registry that haven't made their way to the registry hives themselves
		- Transaction log for each hive is stored as a `.LOG` file in the same directory as the hive itself, with the same name as the registry hive (with the `.LOG` extension though)
		- There can be multiple transaction logs for a registry hive, `.LOG .LOG1 .LOG2` etc
	- Registry Backups
		- Backups of the registry hives that are located in `C:\Windows\System32\Config` and are copied to `C:\Windows\System32\Config\RegBack`
		- Copied every 10 days
		- Good place to look if you think that some registry keys have been deleted or modified

- Data Acquisition
	- The process of imaging or copying a system or the required data to perform forensics on it
	- Keeping in mind that registry files are restricted files, so how can we make a copy of them?
		- Tools, such as
			- KAPE
			- Autopsy
			- FTK Imager
	- Bear in mind that these tools are used to *acquire* the needed registry hives

- Exploring Windows Registry
	- Tools will be needed, such as
		- Registry Viewer
			- https://www.exterro.com/ftk-product-downloads/registry-viewer-2-0-0
			- Only holds one hive at a time, and it can't take transaction logs
		- Zimmerman's Registry Explorer
			- https://ericzimmerman.github.io/#!index.md
			- Can load multiple hives simultaneously and add data from transaction logs into the hive to make a more *cleaner* hive with more up-to-date data
			- Also has a Bookmarks option, which can contain important registry keys usually sought out by investigators
		- RegRipper
			- Takes a registry hive as an input and outputs a report that extracts data from some of the forensically important keys and values in that hive
			- Output report is a text file and shows results in a sequential order
			- Doesn't take transaction logs into account.
			- Registry Explorer can be used to merge transaction logs with related registry hives before sending the output to RegRipper for processing

- System Information and System Accounts
	- OS Version
		- `SOFTWARE\Microsoft\Windows NT\CurrentVersion`
	- Control Sets
		- Configuration data used for controlling system startup are called Control Sets
		- Usually, in the `SYSTEM` hive - there will be ControlSet001 and ControlSet002
		- In most cases (most, not all), ControlSet001 will point to the Control Set that the machine booted with
		- ControlSet002 will be the `last known good` configuration
		- Locations:
			- `SYSTEM\ControlSet001`
			- `SYSTEM\ControlSet002`
	- Current Control Set
		- A volatile control set when the machine is live, called the CurrentControlSet
		- `HKLM\SYSTEM\CurrentControlSet`
		- `SYSTEM\Select\Current`
			- Which Control Set is being used as the CurrentControlSet
		- `SYSTEM\Select\LastKnownGood`
			- Will outline which Control Set is being used for the Last Known Good configuration
	- *Vital to establish this information before moving forward with the analysis.*
		- *Many artifacts will be collected from these Control Sets - keep that in mind*
	- Computer Name
		- `SYSTEM\CurrentControlSet\Control\ComputerName\ComputerName`
		- Ensure we are working on the machine that we are supposed to be working on (important for any analysis really)
	- Time Zone Information
		- `SYSTEM\CurrentControlSet\Control\TimeZoneInformation`
		- Important to establish what time zone the computer is located in 
		- Helps to establish a good understanding of the chronology of events as they happened
		- Important because some data in the computer will have their timestamps in the UTC/GMT zones and others in the local time zones. 
		- Knowledge of the local time zone helps in establishing a timeline when merging data from all sources
	- Network Interfaces and Past Networks
		- `SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces`
		- Each interface is represented with a GUID subkey
			- Contains values relating to the interface's TCP/IP configuration
			- Helps provide information like IP addresses, DHCP IP address, Subnet Masks, Default Router, DNS Servers, and more
		- Significant information as it will help ensure that we are performing forensics on a machine that we are supposed to be performing on
		- Past networks a machine was connected to can be found in:
			- `SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signature\Unmanaged`
			- `SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Signatures\Managed`
			- These keys contain past networks as well as the time they were connected
				- The last write time of the registry keys point to the last time these networks were connected
	- Autostart Programs
		- These keys include information about programs or commands that run when a user logs on
			- `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Run`
			- `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\RunOnce`
			- `SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce`
			- `SOFTWARE\Microsoft\Windows\CurrentVersion\policies\Explorer\Run`
			- `SOFTWARE\Microsoft\Windows\CurrentVersion\Run`
		- This registry key contains information about services
			- `SYSTEM\CurrentControlSet\Services`
				- If the `start` key is set to `0x02`, it means that this service will start at boot
	- SAM Hive and User Information
		- `SAM\Domains\Account\Users`
		- Contains
			- User account information
			- Login information
			- Group information
			- Relative Identifer (RID) of the user
			- Number of times the user logged in 
			- Last login time
			- Last password change
			- Password expiry
			- Password Policy
			- Password hint
			- Any group memberships

- Usage or Knowledge of Files/Folders
	- Recent Files
		- Stored in the NTUSER hive
		- `NTUSER.dat\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs`
		- Registry Explorer tool allows sorting of data contained in the registry keys quickly
			- Most Recently Used (MRU) at the top for example
		- Also the Recent Files key can contain keys for different file extensions, such as `.pdf`, `.jpg`, `.docx` for example
		- If looking for a particular one:
			- `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\.docx` 
		- Registry Explorer tools also lists the Last Opened Time of files
	- Office Recent Files
		- `NTUSER.DAT\Software\Microsoft\Office\VERSION`
		- Example:
			- `NTUSER.DAT\Software\Microsoft\Office\15.0\Word`
				- `15.0` refers to Office 2013
		- Different Office Releases:
			- https://learn.microsoft.com/en-us/microsoft-365-apps/deploy/install-different-office-visio-and-project-versions-on-the-same-computer#office-releases-and-their-version-number\
		- Office365 and later, Microsoft has now tied the location to the user's Live ID 
			- `NTUSER.DAT\Software\Microsoft\Office\VERSION\UserMRU\LIVEID_####\FileMRU`
	- ShellBags
		- When a user opens a folder, the folder opens in a specific layout
		- Users have the ability to change this layout so it meets their preferences
		- Layouts can be different for different folders
		- This information about the *Windows Shell* is sotred and can identify the MRU (Most Recently Used) files and folders
		- Since it's a setting that is different for each user, it is located within the User Hives - in these locations:
			- `USRCLASS.DAT\Local Settings\Software\Microsoft\Windows\Shell\Bags`
			- `USRCLASS.DAT\Local Settings\Software\Microsoft\Windows\Shell\BagMRU`
			- `NTUSER.DAT\Software\Microsoft\Windows\Shell\BagMRU`
			- `NTUSER.DAT\Softwware\Microsoft\Windows\Shell\Bags`
		- A tool from Zimmerman called **ShellBag Explorer** can be used to show information in an easy-to-use format
	- Open/Save and Last Visited DIalog MRUs:
		- When a file is opened or saved, a dialogue box appears prompting the user where to save or open that file from
		- Windows then remembers that location
		- `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePIDMRU`
		- `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedPidlMRU`
	- Windows Explorer Address / Search Bars
		- Another way to identify a user's recent activity is by looking at the paths entered into the Windows Explorer address bar or searches performed using these registry keys:
			- `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\TypedPaths`
			- `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\WordWheelQuery`

- Evidence of Execution
	- UserAssist
		- Windows keeps track of applications launched by the user using Windows Explorer for statistical purposes in the User Assist registry keys
		- Programs run from the command line can't be found in the User Assist keys
		- User Assist key is in the NTUSER hive, mapped to each user's GUID
		- `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist\{GUID}\Count`
	- ShimCache
		- A mechanism used to keep track of application compatibility with the OS and tracks all applications launched on the machine
		- Main purpose is to ensure backward compatibility of applications
		- Also called Application Compatibility Cache (AppCompatCache)
		- `SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache`
		- Stores file name, file size, last modified time of the executables
		- An Eric Zimmerman tool called **AppCompatCache Parser** can be used to parse data and output it into a CSV file
		- This command can be used to run the AppCompatCache Parser tool/utility:
			- `AppCompatCacheParser.exe --csv <path-to-save-csvoutput> -f <path-to-HIVE> -c <control-set-to-parse>`
		- The output can be viewed with **EZViewer** - another one of Eric Zimmerman's tools
	- AmCache:
		- A hive related to ShimCache
		- `C:\Windows\appcompat\Programs\Amcache.hve`
		- Stores additional data to ShimCache, related to program executions
			- Execution path
			- Installation
			- Execution time
			- Deletion time
			- SHA1 hashes of executed programs
		- Information about the last executed programs can be found here in the hive:
			- `Amcache.hve\Root\File\{Volume GUID}\`
	- BAM/DAM
		- BAM - Background Activity Monitor
			- Keeps track on the activity of background applications
		- DAM - Desktop Activity Moderator
			- Part of MS Windows that optimizes the power consumption of the device
		- Both of these are part of Modern Standby systems in MS Windows
		- Contains information about last run programs, their full paths, and last execution time
			- `SYSTEM\CurrentControlSet\Services\bam\UserSEttings\{SID}`
			- `SYSTEM\CurrentControlSet\Services\dam\UserSettings\{SID}`
- External Devices/USB Device Forensics
	- Device Identification
		- These locations keep track of USB keys plugged into a system
		- These locations store the Vendor ID, Product ID, and Version of the USB device plugged in and can be used to identify unique devices
			- `SYSTEM\CurrentControlSet\Enum\USBSTOR`
			- `SYSTEM\CurrentControlSet\Enum\USB`
		- Will show when the device was first installed, last connected bits of information as well
		- The Registry Explorer tool presents information in these keys very well
	- First/Last Times
		- The following key tracks the first time the device was connected, the last time it was connected and the last time the device was removed from the system
			- `SYSTEM\CurrentControlSet\Enum\USBSTOR\Ven_Prod_version\USBSerial#\Properties\{83da6326-97a6-4088-9453-a19231573b29}\####`
			- The `####` can be replaced by the following digits to get the required information:
				- 0064 - First Connection Time
				- 0066 - Last Connection Time
				- 0067 - Last Removal Time
		- Registry Explorer will show this anywho
	- USB Device Volume Name
		- Device name of a connected device can be found here:
			- `SOFTWARE\Microsoft\Windows Portable Devices\Devices`
		- The GUID seen in this key can be compared with the Disk ID we see on other keys mentioned in device identification to correlate names with unique devices

---
