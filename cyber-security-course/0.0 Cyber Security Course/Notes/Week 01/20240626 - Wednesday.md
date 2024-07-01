##---------------------------------
- (please bear in mind that these notes are made on the fly and some topics/items may have been missed, and also, they're more directed in my thought process, thinking, but hopefully will be helpful where it can be! :) )

- Weekly recap and heartbeat
- AppSec event
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

Admin Groups
	Windows - Administrators
	Linux/Unix - wheel (or something like that)

-
- 


##---------------------------------
Tools:
- Putty
- SH? (double-check this)
- VIM - text editor 1337
- TryHackMe.com
- HackTheBox
- Kalia (LInux on the fly OS)
	- Look up others
- 
##---------------------------------
TO DO and Terminologies:
- Check out **Pirates of Silicon Valley (Movie/Doco)**
	- Set aside for a later time

- WSL - Windows Subsystem for Linux
	- Done

- Shell - comes from referencing a nut, hard shell on the outside, and inside is the kernel
- Kernel is the main part of the operating system
	- The two above have been noted
	
- A kernel in Windows is NT OS (New Technology OS)
- MACH used in MacOS
- The shell is the interface that speaks with the kernel

- Check out who created the Mouse and the GUI
	- In relation to Xerox? Palta Alto (something like that)
	  Noted in the main todo's
	  
- Binaries
	- Contain a list of utilities/functions
	- Example: "ls" , "cat"
		- Simple definition and Win/Linux default PATH's described in the Terminologies page
		  
- Check out that Everything Tool to check out descriptions of the various utilities
	  Pretty neat, kind of like Finder in MacOS, real fast to search for stuff when compared to your usual File Explorer in Windows
	  Noted in the Tools page
  
- Piping - check it
		Some notes added in Terminologies
		
- Check out Multics
	  Brief recap on this historical OS in terminologies
- Alexander Graham Bell - Invented the telegram/telephone
	- Check him out
	- Turned into AT&T (from Bell technologies or something like this? )
	- Check out the story
	- And the anti-trust laws that had taken place
		  Added to random todo's
		  
- Internet Explorer v5 and 6
	- Anti-trust issues check it out
	- Web 2.0
	- The good ol' compatibility issue days!!!! >_<
			- Added to Random Todo's
	
- Have a look at the "GO" dev language
	- Made by Google
	  Added to Random Todo's
	  
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
				  Added to Random todo's
			  
- Check out Samsung KNOX in more detail
- https://xkcd.com/927/ check it out from Josh
	- Use VirusTotal first, lol, ;) nah jokes trust you Josh
		  Added to Random Todo's
		  
- Check out the different types of SHELLS
	- Bourne/born again shell (bash)
		  A list of shell varieties has been added in the Terminologies page
		  
- Check out angular.js (came out of personal projects from workers at Google)
	  Added to random todo's
	  
- Sunsetting a project - announcement date > sunset time > then the actual killing of the project
	  Note added in Terminologies
	  
- Check out FlutterFlow programming language (Clark)
	  Programming Languages page has now been created in this Vault
	  This will be expanded in the days to come
	  
- Look into a cheatsheet for useful bash commands (and also Windows Powershell)
		Done and shared with the class.
		
- Brad: https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard
	  Have taken a note of this in Linux OS Page and in the Cheat Sheets page
	  
- ICMS - Spark/Telecom - used SSH or something or rather to do something; see what you can find
	  ????
	  Added to Random todo's
	  
- TP2? - still being used by VF? have a look or ask around
	  Noted
	  
- Technical Debt - check more
	  noted in Terminologies
	  
- Blockchains - Append-only database
	- Kris' blockchain analogy with Banks having the ability to manipulate balances wherein blockchain's would prevent such mischievous acts
		  Definition has been added to Terminologies page
		  
- Hyperledger (IBM) - check this out 
	  Added for further research
	  
- tharchive.org - wayback machine (check it out)
	- Issues accessing this page
	  They did also get sued in the days of Covid for copyright infringments (but this could have been a different outfit from thearchive.org group
	  There is however blog.thearchive.org which reads, "THE BATTLE CONTINUES!"
	  Virustotal says it's safe)
		  Added to Random Todo's
		  
- YouTube Downloader - for referencing to a video online, grab a local copy of it and upload it on to your online platform should you need to refer to it (to prevent broken links in the future - in the event that vid goes down)

- [https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository "https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository") - check this out from Josh and secure the previous repo versions
	  Noted, read, and saved for when the time arises.
	  Bit of a process this one
	  
- To look into in mucho more detalio
	- TOR
		  already done
	- I2P 
		  Noted, done.
		  
- From Mark O'Gorman:
	- initscripts is an example of something going out of date. the initscripts start up system has been replaced in most operating systems by systemd.
	  Look into these terms in more detail
		  Cheatsheet created
		  Some notes defined in Terminologies
		  Done, for now. 
	  
  - Find out which profile in bash needs to be updated to save alias changes to commands
	    Pretty sure this should be the .bash_profile from memory
		    Added to main Todo's page for now
	    
  - Great power comes with great responsibility. 
		I choose Mark Manson's version
			With great responsibility comes great power. 
			
  - Look into seeing if the --help can be run on commands that have an alias variation made in the shell
	    Noted in the main todos
	    
  - Look into these
	  - CLSID
		  - A globally unique identifier that identifies a COM class object. (learn.microsoft.com)
		  - A serial number that represents a globally unique identifier for any application component in Windows
		    (NordVPN)
				    This has been noted in Terminologies for now, with the idea of expanding it at a later date
	  - UUID's
		    Noted in Terminologies for now
		    
  - Check out symbolic links for when in bash or similar shell
	  - Similar to shortcuts
		    Noted in Terminologies and also to look further into in ToDos
  - 
  - Look into the details of sbin and it's commands in more detail
	    Cheat sheets updated with the Unix Filesystem Cheat Sheet
	    
  - CloudFlare DNS:
	  - 1.1.1.1
		    noted - in my head.
		    
  - Text Editor:
	  - CHECK IT OUT .... wtf was I thinking here, too much bs
	    
  - Continue with Network+ modules
	  - IPv6 should not be far away..?
		    Yes.
		    
  - List up (in this Vault) the most useful and common commands for all OS's
	  - Reference to online cheat sheets where possible (always reference - be good)
			    THIS IS A WIP
			    
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
			This has been noted in the Cryptography section
			
	- Look into symbolic links in a unix/linux shell further
		- this one confused me in the past and still does, gg - git good
			  Symbolic links will be looked into further when I get to that part of bash again.
- jabberd
	- Instant messaging system back in the days (check it for the sake of looking into days past)
		  Noted in random todo's
		  
- Look into Unix Permissions further (chmod'aring all dae)
	- User
	- Group
	- Other
		  Done in the past, reviewed again, but will elaborate further later
		  
- Pi-hole - from Cameron - check it out | for RPi's
	  Added to random todo's list
	  
- Check out:
	- TryHackMe.com
	- HackTheBox (will have to adjust NoScript policies as well as with Brave and uBlock)
		- Search up Unitec as the University
				Done, WIP, still needing to search up Unitec as the University when I get to that stage
	
- Build your LinkedIn with certifications granted from the above online tools
	- (and the others as well, post a soft copy of the papers you have)
		  Noted in random todo's
		  
- Look into:
	- Kali  (LInux on the fly OS)
		- Look up others
			  Done, initial list given in OSes > Linux and Unix
			  
- Clean up Mailbox folders
	  Added to random todo's
	  
- DualLingo - GO GO FOR MANDARIN! (from Blair Hodson, chur!)
	  Added to random todo's
	  
- Read through rules for both of the Discord channels Kris shared today
	  Added to Todo's (so many bloody Discords..)
	  
- Install VirtualBox
		- Setup a VM of a variant of a Linux distro
		- Install OpenVPN
			  done whilst using WSL for now
		- Configure it to speak with the HackTheBox system
			- Hopefully this bypasses that 2-hour countdown (Kris mentioned something along the lines of this)
				  Diverted to using WSL for the time being running Ubuntu for now
	  Noted in Todo's will tend to this at a later stage as I want some VMs set up to familiarise with various GUI's and shells.
  
- Add the AppSec Event to the Calendar
	- https://appsec.org.nz/conference/
	- OWASP New Zealand Day 2024
		3 - 6 September 2024
		Auckland University of Technology (AUT) City Campus
			Added to calendar etc etc
##---------------------------------