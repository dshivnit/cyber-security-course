Developed by Victor M. Alvarez and VirusTotal
https://github.com/virustotal/yara
https://tryhackme.com/r/room/yara

- A tool aimed at (but not limited to) helping malware researchers to identify and classify malware samples. With YARA you can create descriptions of malware families (or whatever you want to describe) based on textual or binary patterns. 
	- Each description (aka rule), consists of a set of strings and a boolean expression which determine its logic.
	- Example:
		```yara
			rule silent_banker : banker
			{
				meta:
					description = "This is just an example"
					threat_level = 3
					in_the_wild = true

				strings:
					$a = {6A 40 68 00 30 00 00 6A 14 8D 91}
					$b = {8D 4D B0 2B C1 83 C0 27 99 6A 4E 59 F7 F9}
					$c = "UVODFRYSIHLNWPEJXQZAKCBGMT"

				condition:
					$a or $b or $c
			}
		```
	- The above is telling YARA that any file containing on of the three strings must be reported as `silent_banker`. 
	- More complex and powerful rules can be created by using wild-cards, case-insensitive strings, regular expressions, special operators and many other features that you'll find explained in YARA's documentation (https://yara.readthedocs.io/en/latest/)

- Yara can identify information based on both binary and textual patterns - such as hexadecimal and strings contained within a file
	- Rules are used to label these patterns
	- Example - Yara rules are frequently written to determine if a file is malicious or not, based upon the features - or patterns - it presents. 
		- Strings are a fundamental component of programming languages. Applications use strings to store data such as text.
			- `print("Hello World!")`
		- We could write a Yara rule to search for "hello world" in every program on our operating system if we want - and it would pick up what it can pick up. 

*Why does Malware use Strings?*
- *Malware tends to use strings to store textual data*
- *Some examples of the data that various malware types store within strings:*
	- *Type - Ransomware*
	- *Data - 12t9YDPgwueZ9NyMgw519p7AA8isjr6SMw*
	- *Description - Bitcoin Wallet for ransom payments*
		- *https://tryhackme.com/r/room/malmalintroductory (will be going through this at a later stage)*

- YARA rules are only as effective as your understanding of the patterns you want to search for
- Using a rule is simple, every `yara` command requires two arguments to be valid, these are:
	- The rule file we create
	- Name of file, directory, or process ID to use the rule for
- Every rule  must have a name and condition. 
	- If we wanted to use "myrule.yar" on directory "some-dir", we would invoke this command:
		- `yara myrule.yar some-dir`
	- Note that .yar is the standard file extension for all Yara rules.
- Every rule requires a name and a condition to be valid.

Writing YARA Rules
https://yara.readthedocs.io/en/stable/writingrules.html
- YARA rules have a syntax that resembles C. 
- Each rule in YARA starts with the keyword `rule` followed by a rule identifier. 
- Identifiers must follow the same lexical conventions of the C programming language, they can contain any alphanumeric character and the underscore character, but the first character cannot be a digit. 
- Rule identifiers are case sensitive and cannot exceed 128 characters
- There are keywords that are reserved and won't be able to be used as an identifier (refer to the link above)
- Two sections in a rule:
	- Strings definition
		- This can be omitted if the rule doesn't rely on any string
	- Strings condition
		- This is always required
	- Each string has an identifier that starts with `$` character followed by a sequence of alphanumeric characters (and underscores)
		- These identifiers can be used in the condition section to refer to the corresponding string
		- Strings can be defined in text, or hexadecimal form - as shown here:
			```yara
			rule Example
			{
				strings:
					$my_text_string = "text goes here"
					$my_hex_string = { E2 34 A1 C8 23 FB }

				condition:
					$my_text_string or $my_hex_string
			}
			```
	- Text strings are enclosed in double quotes (like in C)
	- Hex strings are enclosed in curly brackets
		- Decimal numbers are not allowed in hexstrings
	- Comments
		- `/* comment here multi-line */`
		- `// single line comment` 
	- Strings
		- There are three types of strings in YARA
			- hexadecimal strings
			- text strings
			- regular expressions

Some Conditions:
- Desc
	- Short for description
	- Summarises what your rule checks for
	- Similar to commenting
- Meta
	- Reserved for descriptive information by the author of the rule
	- Anything within this and the `Desc` section does not influence the rule itself
	- Similar to commenting
- Strings
	- Strings can be used to search for specific text or hexadecimal in files or programs
		```yara
		rule helloworld_checker{
			strings:
				$hello_world = "Hello World!"
		}
		```
	- Remember that a condition is always needed too!
- Conditions
	- `$hello_world`
	- If any file has the string "Hello World!" then the rule will match
	- Case-sensitive. Bear that in mind
	- The condition `any of them` can be implemented here, as below:
		```yara
		rule hellow_worldchecker{
			strings:
				$hello_world = "Hello World!"
				$hello_world lowercase = "hello world"
				$hello_world_uppercase = "HELLO WORLD"
				
			condition:
				any of them
		}
		```
	- Operators
		- Such as <= or >= or != can be applied as well
		- if you have `#hello_world <= 10`
			- The rule will match if there are less than or equal to ten occurrences of the "Hello World!" string
			- *I haven't tested this but I think the # would need to be a $*
	- Combining Keywords
		- You can use
			- and
			- not
			- or
		- To combine multiple conditions. 
		- Say if you wanted to check if a file has a string and is of a certain size
			```yara
				condition:
					$hello_world and filesize < 10KB
			```
			- As with programming, the rule will match ONLY if both conditions are true
			- 
- Weight
	- *will have to further expand on this sometime...*

Integrating with Other Libraries
- Frameworks like the two below allows one to improve the technicality of YARA rules by a fair bit
	- Cuckoo Sandbox
		- https://github.com/cuckoosandbox/cuckoo
		- Automated malware analysis environment
		- Allows one to generate Yara rules based upon the behaviours discovered from Cuckoo the Sandbox
		- As this environment executes malware - you can create rules on specific behaviours such as runtime strings and what not
	- Python's PE Module
		- https://pypi.org/project/pefile/
		- Allows one to create Yara rules from the various sections and elements of the Windows Portable Executable (PE) Structure

Yara Tools
- There are predesigned rules that can be implemented
- Sometimes you may find yourself in a situation where you've encountered something unknown, which your stack of security tools can't or didn't detect. Tools like LOKI (below) can be used - you would need to add your own rules based on your threat intelligence gathered or findings from an incident response engagement (forensics)
- Some like in here: https://github.com/InQuest/awesome-yara
- LOKI
	- https://github.com/Neo23x0/Loki/blob/master/README.md
	- A free open-source IOC scanner created and written by Florian Roth
	- Detection is based on four methods:
		- File Name IOC Check
		- Yara Rule Check
		- Hash Check
		- C2 Back Connect Check
	- There are additional checks as well
	- **However, upon checking, the Loki project is now in inactive maintenance mode.**
	- 
- THOR
	- https://www.nextron-systems.com/thor-lite/
	- Florian's newest multi-platform IOC and YARA scanner
	- Precompiled for Windows, Linux and MacOS. 
	- Geared towards **corporate customers**
	- Thor Lite is the free version
- FENRIR
	- https://github.com/Neo23x0/Fenrir
	- Third tool created by Neo23x0 (Forial Roth)
	- Created to address the issue from its predecessors, where requirements must be met for them to function
	- Fenrir is a bash script, it will only run on a system capable of running bash (which is Windows these days too)
- YAYA (Yet Another Yara Automation)
	- Created by the EFF (Electronic Frontier Foundation) and released in Sept 2020
	- "YAYA is a new open-source tool to help researchers manage multiple YARA rule repositories. YAYA starts by importing a set of high-quality YARA rules, and then lets researchers add their own rules, disable specific rulesets, and run scans of files."
	- Only runs on LINUX

Creating YARA rules with yargen
- Also created by Florian Roth
	- https://github.com/Neo23x0/yarGen
- YarGen is a generator for YARA rules
	- "The main principle is the creation of yara rules from strings found in malware files while removing all strings that also appear in goodware files. Therefor yarGen includes a big goodware strings and opcode database as ZIP archives that have to be extracted before the first use."
- If a malicious file goes undetected, and an incident occurs as a result - we will need to amend some rules to be able to pick up the undetected threat again in the future
- One can manually open the file and attempt to sift through lines upon thousands of lines of code to find possible strings that can be used in our newly created YARA rule. 
	- `strings <'file-name'> | wc -l`
		- Will identify how many strings would be in the file and count them out
	- Going through each of those strings, line by line, is ridiculous 
- Using YarGen we can generate a rule based on what the tool finds in the file that is being inspected
	- `python3 yarGen.py -m <'path-to-file-to-inspect'> --excludegood -o <'path-to-destination-output-file'>`
		- `-m` is the path to the files you want to generate rules for
		- `--excludegood` force to exclude all goodware strings (strings found in legitimate software and can increase false positives)
		- `-o` location and name that you want to for the output from the YarGen Generator, the rule that will be created
	- Make sure that your generated .yar file is sitting with the rest of the .yar files that Loki would be using to scan

yarAnalyzer
https://github.com/Neo23x0/yarAnalyzer/
- Also created by Florian Roth!
- Creates statistics on a yara rule set and files in a sample directory
- Place some signatures with .yar in the signatures folder and then run yarAnalyser on a certain sample directory like:
	- `yarAnalyzer.py -p <'/path-to-dir/path'> -s /signatures` 
- Refer to the link above for further instructions (*will be looking at this in more detail later*)

Valhalla
https://www.nextron-systems.com/valhalla/
- Online Yara feed created and hosted by Nextron-Systems (... Also Florian Roth)
- "Valhalla boosts your detection capabilities with the power of thousands of hand-crafted high-quality YARA rules."
- 