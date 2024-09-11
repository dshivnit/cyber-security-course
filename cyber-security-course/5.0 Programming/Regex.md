- Regular Expressions
- Tools for finding or matching patterns in strings.
- Special sequences used to find or match patterns in strings. 
- These sequences use metacharacters and other syntax to represent sets, ranges or specific characters. 
	- ie `[0-9]` matches the range of numbers between 0 and 9
	- ie `humor|humour` matches both of the strings given, being 'humor' and 'humour'
- Basics:
	- Expressions start and end with a `/`
		- The below examples may not include these .. 
	- `^` Start of string, or start of line in multi-line pattern
	- `$` End of string, or end of line in multi-line pattern
	- `\` escape character - put this in-front of a special character so that the character's specialness doesn't engage..
	- Quantifiers
		- `*` - 0 or more
		- `+` - 1 or more
		- `?` - 0 or 1
	- Metacharacters
	- Character sets
		- `[bcf]at` - would mean that the characters within the square brackets would be included when searching strings for `*at` 
	- Ranges
		- `[a-z]at` - would include the entire alphabet when searching a string for `*at` 
		- Can be partial ranges, capitalised ranges, number ranges, symbol ranges
			- `[a-f]` or `[g-p`]
			- `[A-Z]`
			- `[0-9]`
			- `[!@#$%]`
		- Mixed
			- `[a-zA-Z0-9]`
		- A four letter word:
			- `[a-z][a-z][a-z][a-z]`
			- `[a-z]{4}`
		- A word with four letters or more
			- `[a-z]{4,}`
		- A word between 2 and 4 letters
			- `[a-z]`
		- Note that a range only specifies multiple alternatives for a single character in a pattern
	- Special characters
	- Flags
		- `g` - global
			- Don't return after first match
		- `i` - case-insensitive
			- Case insensitive match
		- `m` - multi-line
			- `^` and `$` match start/end of line
		- `y` - sticky
			- Anchor to start of pattern, or at the end of the most recent match
		- `u` - unicode
			- Match with full unicode
		- `v` - vnicode
			- Enable all unicode and character set features
		- `s` - single line
			- Dot matches newline
		- `d` - indices
			- The regex engine returns match indices
	- Expressions start with `/` and end with `/` 
	- Flags would go at the end of an expression
	- ie `/word/g`
- Practical applications of Regex:
	- Form input validation
	- Web scraping
	- Search and replace operations
	- Filtering information from large text files (such as LOGS!)
- Terminologies:
	- pattern
	- string
	- digit
	- letter
	- symbol
	- space
	- character
	- 
- Tools:
	- Regex101
	- Essential for experimenting with regex patterns in a supportive environment.
	  - Building and testing patterns to ensure desired criteria is matched
---

*(below taken from THM - thanks `concatenate`!)*
`\d` matches a digit, like `9`  
`\D` matches a non-digit, like `A` or `@`  
`\w` matches an alphanumeric character, like `a` or `3`  
`\W` matches a non-alphanumeric character, like `!` or `#`  
`\s` matches a whitespace character (spaces, tabs, and line breaks)  
`\S` matches everything else (alphanumeric characters and symbols)

Note: Underscores `_` are included in the `\w` metacharacter and not in `\W`. That means that `\w` will match every single character in `test_file`.

Often we want a pattern that matches many characters of a single type in a row, and we can do that with repetitions. For example, `{2}` is used to match the preceding character (or metacharacter, or charset) two times in a row. That means that `z{2}` will match exactly `zz`.

Here's a reference for each repetition along with how many times it matches the preceding pattern:

`{12}` - **exactly 12** times.  
`{1,5}` - **1 to 5** times.  
`{2,}` - **2 or more** times.  
`*` - **0 or more** times.  
`+` - **1 or more** times.

---
Examples:
- `[A-Z]+[0-9]*`
	- 1 or more A-Z characters (emphasis on at least **1** here!)
	- 0 or more numbers (emphasis on **0** here!)
- Check this site out for more practice, knowledge around how regex works
	- https://regexlearn.com/
- This site has various formats (Python, PHP, MySQL, Javascript etc) and is a useful quick-reference:
	- https://regexlearn.com/

References:
- https://quickref.me/regex
- https://www.sitepoint.com/learn-regex/
- https://regex101.com/
- https://regexlearn.com/
- https://tryhackme.com/r/room/catregex