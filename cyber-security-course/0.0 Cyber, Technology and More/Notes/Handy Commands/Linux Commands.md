Aliases
- Create an alias
	- `alias shortname='official command'`
	- Usage example:
		- `alias ll='ls -l'`
		- `ll`
- List configured aliases
	- `alias -p`
- Remove an alias
	- `unalias <alias-name>`

Grep
- Searching a directory (this will give you the file that the result is in as well)
	- `grep -r 'pattern-to-search' <directory-path>`
		- Usage:
			- `grep -r '@' office365/`
- Finding email addresses
- `grep -Eo ‘[a-zA-Z0–9._%+-]+@[a-zA-Z0–9.-]+\.[a-zA-Z]{2,}’`
- `grep -r -E -o "\b[a-zA-Z0-9.-]+@[a-zA-Z0-9.-]+.[a-zA-Z0-9.-]+\b" .`

CLI JSON Processor (https://jqlang.org/manual/)
- `cat <poershell.json-file> | jq`
	- Parse all JSON into a nice output
- `cat <powershell.json-file> | jq '{Field1Name, Field2}'`
	- Print some fields out from the entries based upon the field names that you can see from the nice output previously
- `cat powershell.json-file | jq -s -c 'sort_by(.Timestamp) | .[] | {Field}'`
- `cat powershell.json | jq -s 'sort_by(.Timestamp) | .[]' | grep -e 'sq3.exe' -e 'cd ' -C 5`

- `hping3`

