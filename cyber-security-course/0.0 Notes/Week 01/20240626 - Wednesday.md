##---------------------------------
- (please bear in mind that these notes are made on the fly and some topics/items may have been missed, and also, they're more directed in my thought process, thinking, but hopefully will be helpful where it can be! :) )

- Weekly recap and heartbeat
- Owasp event
	- Kris will get us tickets to this
	- September 5-6th September
	- Thur/Fri
	- https://appsec.org.nz/conference/
	- Experienced speakers presenting
	- Capture The Flag events that Kris wants us to participate in 
	- 
- WSL - Windows Subsystem for Linux

- MacOS
	- Command key + Spacebar = Spotlight
	- Open Terminal 
	- 

SHELLS
- Shell's speak with the Kernel
- In today's time usually a GUI (Graphical User Interface)
- In the past, it used to be a TTY (TeleTypeWriter)
- A TTY was literally a type writer > it would send commands off to the server >> the Server was just a name for a computer that is/was running a bunch of services somewhere else
- You may see TTY on the top of terminal (in MacOS) or PTTY (check this out at some stage)
	- Also PuTTY!
- The shell is a computer program which takes in a input, does some processing then gives an output
	- Input --> Processing --> Output
- Shell (or sh)
- BIN > Binaries Directory in Linux/Unix
	- Contains all the utilities used in an OS
- Piping
	- To pipe data
	-  |  this is the pipe symbol
- File System
	- Can be seen as a protocol
		- A set of rules for doing a certain thing
	- /Users
	- Root = should refer to the / in the file system
	- Root = can also be sometimes be used in User Admin to refer to a super user or admin on the filesystem/system

Different SHELLS (shell can also be considered a command interprenter)
- Sh
- ksh
- korn
- bsh
- zsh
- korn
- zsh (default shell for MacOS)
- bash - uBuntu and mainline Linux OS's

Unix/Linux directories
- bin - binaries (programs on the system)
- dev - devices
- etc - etcetera, config files live here
- home - for local user home directories
- opt
- sbin - superuser binaries folder
- tmp - used for applications/programs that need to temporarily store data
	- Don't put stuff in here
- usr - 
- var - various, usually where logs live
- sbin
	- 

Technical Debt:
- Companies always have deadlines
- They always have to take shortcuts when they're developing/building something
- These can lead to Technical Debt
- "Technical debt (also known as tech debt or code debt) describes what results when development teams take actions to expedite the delivery of a piece of functionality or a project which later needs to be refactored. In other words, it's the result of prioritizing speedy delivery over perfect code." (from productplan.com)

Knowledge Half-life
- Kris: Technical books have a half-life due to technology advancing at the rate that it is and new standards coming into place
- Half of what was relevant in the past, may or may not be relevant in the present

File Redirection (in bash):
- 

COMMANDS:
- pwd - print working directory
- cd - change directory (cd "argument/switch/parameter")
	- options (argument/switch/parameter)
		- usually have a dash or a double-dash and are the command's additional functions/options
	- single-dash (short) arguments are BSD switches
	- double-dash (long) arguments are GNU switches
- ALWAYS read the error
- when in /bin
	- aliasing a command
		- Example:
			- alias lsc="ls -a --color=always
		- You can make these alias changes permanent by configuring a profile config file (look into seeing where this is)
- dd
	- Disk Destroyer!
	- Copies a file and copies it to another location
	- Tread with CARE - you can mess up the original file if you are pointing the output to the input accidentally
- echo
	- "The Dolphin!"
		- The Dolphin!
	- echo "The Dolphin!" > hello.txt
		- This will save the output of echo into a file named hello.txt in the directory/PATH of where you typed the echo command
	- echo < hello.txt 
- mkdir
	- Make directories yao
	- Remember to always use the --help parameter if you are wanting to know more about the command, ie
		- mkdir --help
			- This will give you some of the documentation around the mkdir command and its various parameters that can be used
- mv
	- Move something yao!
- chmod
	- change perms (permissions) for a folder/file
	- drwx
		- directory (sometimes p? Is this only in MacOS?)
		- read
		- write
		- executable
- ping6
- umount
	- To safely unplug devices plugged into the machine/system
- fsck
	- file system check
	- chkdsk (in Windows)
- dmesg
	- useful for debugging start up (boot up) process in Unix/Linux based systems
- md5
	- message digest version 5
	- Made by Ron Rivest in 1991
	- Will be covered in more detail when we cover cryptography 
	- It is a Hashing Algorithm
	- one-way (you can't reverse the hash output)
		- You can make a potato into hash, but you can't make hash back into a potato
	- You'd need to use ctrl+d to tell the system you're finished with whatever input you want to hash (this is in the Unix/Linux shell)
	- scream for --help if stuck
	- MD5 checksum (used to verify the integrity of files :) )

Unix Shell
- ctrl+d - tells the system taht you're finished
- 

Admin Groups
	Windows - Administrators
	Linux/Unix - wheel (or something like that)

-
- 


##---------------------------------
Tools:
- Putty
- SH? (double-check this)
- VIM - text editor l337
- 
##---------------------------------
TO DO and Terminologies:
- Check out **Pirates of Silicon Valley (Movie/Doco)**
- WSL - Windows Subsystem for Linux
- Shell - comes from referencing a nut, hard shell on the outside, and inside is the kernel 
- Kernel is the main part of the operating system
- A kernel in Windows is NT OS (New Technology OS)
- MACH used in MacOS
- The shell is the interface that speaks with the kernel

- Check out who created the Mouse and the GUI
	- In relation to Xerox? Palta Alto (something like that)
- Binaries
	- Contain a list of utilities/functions
	- Example: "ls" , "cat"
- Check out that Everything Tool to check out descriptions of the various utilities
- Piping - check it
- Check out Multics
- Alexander Graham Bell - Invented the telegram/telephone
	- Check him out
	- Turned into AT&T (from Bell technologies or something like this? )
	- Check out the story
	- And the anti-trust laws that had taken place
- Internet Explorer v5 and 6
	- Anti-trust issues check it out
	- Web 2.0
	- The good ol' compatibility issue days!!!! >_<
- Have a look at the "GO" dev language
	- Made by Google
- Also a framework called "flutter"
	- Mainly for mobile development
	- Java and C++ 
	- Kris was using this back in 2019
		- Didn't take off as it should've
		- People are hesitant to adopt products of Google these days 
		- Google laid off a bunch of staff who were working with flutter
		- if a project doesn't take off massively, they will kill the project
		- there is a Google graveyard of projects that didn't make it
			- CHECK THAT OUT!
- Check out Samsung KNOX in more detail
- https://xkcd.com/927/ check it out from Josh
	- Use VirusTotal first, lol, ;) nah jokes trust you Josh
- Check out the different types of SHELLS
	- Bourne/born again shell (bash)
	- 
- Check out angular.js (came out of personal projects from workers at Google)
- Sunsetting a project - announcement date > sunset time > then the actual killing of the project
- Check out FlutterFlow programming language (Clark)
- Look into a cheatsheet for useful bash commands (and also Windows Powershell)
- Brad: https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard
- ICMS - Spark/Telecom - used SSH or something or rather to do something; see what you can find
- TP2? - still being used by VF? have a look or ask around
- Technical Debt - check more
- Blockchains - Append-only database
	- Kris' blockchain analogy with Banks having the ability to manipulate balances wherein blockchain's would prevent such mischievous acts
- Hyperledger (IBM) - check this out 
- tharchive.org - wayback machine (check it out)
- YouTube Downloader - for referencing to a video online, grab a local copy of it and upload it on to your online platform should you need to refer to it (to prevent broken links in the future - in the event that vid goes down)
- [https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository "https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository") - check this out from Josh and secure the previous repo versions
- To look into in mucho more detalio
	- TOR
	- I2P 
- From Mark O'Gorman:
	- initscripts is an example of something going out of date. the initscripts start up system has been replaced in most operating systems by systemd.
	  Look into these terms in more detail
  - Find out which profile in bash needs to be updated to save alias changes to commands
  - Great power comes with great responsibility (a different way to look at things)
  - Look into seeing if the --help can be run on commands that have an alias variation made in the shell
  - Look into these
	  - CLSID's
	  - UUID's
  - Check out symbolic links for when in bash or similar shell
	  - Similar to shortcuts
  - Look into the details of sbin and it's commands in more detail
  - CloudFlare DNS:
	  - 1.1.1.1
  - Text Editor:
	  - CHECK IT OUT
  - Continue with Network+ modules
	  - IPv6 should not be far away..?
  - List up (in this Vault) the most useful and common commands for all OS's
	  - Reference to online cheat sheets where possible (always reference - be good)
  - md5
	- message digest version 5
	- Made by Ron Rivest in 1991
	- Will be covered in more detail when we cover cryptography 
	- It is a Hashing Algorithm
	- one-way (you can't reverse the hash output)
		- You can make a potato into hash, but you can't make hash back into a potato
	- You'd need to use ctrl+d to tell the system you're finished with whatever input you want to hash (this is in the Unix/Linux shell)
	- scream for --help if stuck
	- MD5 checksum (used to verify the integrity of files :) )
	- Look into symbolic links in a unix/linux shell further
		- this one confused me in the past and still does, gg - git good
- jabberd
	- Instant messaging system back in the days (check it for the sake of looking into days past)
- Look into Unix Permissions further (chmod'aring all dae)
	- User
	- Group
	- Other
- 
##---------------------------------