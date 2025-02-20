https://tryhackme.com/room/kape
Kroll Artifact Parser and Extractor

- KAPE parses and extracts Windows forensics artifacts
- It can reduce time needed to respond to an incident by providing forensic artifacts from a live system or a storage device much earlier than the imaging process completes
- Primary Purposes
	- Collect files
	- Process the collected files as per its given instructions/configuration

- Uses the concept of targets and modules
	- Targets can be defined as the forensic artifacts that need to be collected
	- Modules are the programs that process the collected artifacts and extract information from them

- First Pass (queue)
	- Copies files that it can from the system
	- Providing the files aren't locked by the OS
- Second Pass (queue)
	- Files here are processed using a different technique that uses raw disk reads to bypass the OS locks and copies the files
	- The copied files are saved with original timestamps and metadata and stored in a similar directory structure

- KAPE then processes collected data via the use of modules
- Modules can be independent binaries that run on the collected data and process them to extract information
	- ie KAPE collects and copies the Prefetch file to our target destination during the collection phase
	- Running a Prefetch Parser (PECmd) module on this target will extract the prefetch file and save it in a CSV file

- KAPE can extract targets from a live system, a mounted image, or the F-response utility
- KAPE doesn't need to be installed, it's portable - can be used from network locations or from USB drives

- Targets are identified with the `.tkape` file extension
	- They contain information about the artifact, such as the path, category and file masks to collect
	- the `.tkape` file tells KAPE what files to collect
		- Such as `.pf` when considering prefetch files from `C:\Windows\prefetch` or `C:\Windows.old\prefetch`
	- The `Windows.old` directory keeps files retained after Windows has finished an update (is now on a new version)
	- There can be useful information contained in there as well sometimes

- Compound targets
	- These are targets that are compounds of multiple other targets
	- KAPE is often used for quick triage collection and analysis
	- The purpose of KAPE will not be fulfilled if we have to collect each artifact individually
	- `Compound Targets` help collect multiple targets by giving a single command
	- Examples:
		- `!BasicCollection`
		- `!SANS_triage`
		- `KAPEtriage`
	- Compound targets can be viewed in the path `KAPE\Targets\Compound`

!Disabled
- Contains Targets that you want to keep in the KAPE instance but don't want them to appear in the active targets list

!Local
- If you have created some Targets that you don't want to sync with the KAPE Github repository - you can place them in this directory
- These can be Targets that are specific to your environment
- Similarly, anything not present in the Github repository when we update KAPE will be moved to the !Local directory

Module Options (`.mkape` files)
- Modules run specific tools against the provided set of files
- Their goal is not to copy files from one place to another but rather run some command store the output
	- Usually in the form of a `.csv` or `.txt` file
- the `.mkape` file will tell KAPE about the executable that has to be run, the command line parameters for it to follow from the executable file/binary, the output export format (.csv or .txt) and the filename to export to
- If the executable (such as ipconfig.exe for example) isn't on the machine that we want to run it on, then the `/bin` directory comes into play

- The `bin` directory
- Contains executables that we want to run on the system but are not natively present on most systems
- KAPE will run executables either form the `bin` directory or the complete path
- An example of files to be kept in the `bin` directory are Eric Zimmerman's tools
- Which are generally not present on a Windows system

`gkape.exe` - GUI variant
`kape.exe` - CLI variant
Keep in mind that KAPE is a CLI-based tool as is (many options/parameters that can be utilised)

Example command:
`.\kape.exe --tsource C: --tdest C:\Users\THM-4n6\Desktop\Practice --target KapeTriage --mdest C:\Users\THM-4n6\Desktop\Practice2 --module !EZParser --gui`
- The same command can be run in CLI without the `--gui` tag

Batch Mode:
- `_kape.cli`
- Kept in the directory that contains the KAPE binary
- when `kape.exe` is run, KAPE will if there is a `_kape.cli` file and will execute commands that are mentioned in it
- Useful for when you need someone else to run KAPE for you
- Keeping all commands in a single line
- All the person will need to do is to run `kape.exe` as an administrator