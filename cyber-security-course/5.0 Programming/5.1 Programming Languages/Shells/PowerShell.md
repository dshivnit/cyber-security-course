What is PowerShell?
- Windows Scripting Language and shell environment using the .NET framework
- Allows PS to execute .NET functions directly from its shell
- Most PS commands, called cmdlets, are written in .NET
- Unlike other scripting languages and shell environments, the output of these cmdlets are objects - making PS somewhat object-oriented
- This means that running cmdlets allows you to perform actions on the output object (which makes it convenient to pass output from one cmdlet to another). The normal format of a cmdlet is represented using Verb-Noun
	- ie `Get-Command` 
		- Will list commands
- Common verts to use include:
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
	- `Get-Command`
		- You can use wildcards
			- `Get-Command Verb-*`
			- `Get-Command *-Noun`
			- 
	- `Get-Help`
	- `Get-Help Command-Name`
	- `Get-Help Get-Command -Examples`
	- `powershell -c Get-Service`
		- Will get you a list of the services on the machine and their states (running, stopped)
	- `Restart-Service -Name "ServiceName"`
		- Will restart the given service
	- `Stop-Service -Name "ServiceName`
		- Will stop the given service

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

- Creating Objects from Previous cmdlets
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

- Enumeration
	- Users
		- `Get-LocalUser`
		- `Get-LocalUser | Measure-Object`
			- Not sure why you'd want to do that but I was mucking around
		- `Get-LocalGroup`
		- Needing to find out how to see if passwords are disabled for users or not
	- Basic networking information
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

- Basic Scripting
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
	- 