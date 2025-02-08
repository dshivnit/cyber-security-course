Find and Replace
```
:[range]s/{pattern}/{string}/[flags] [count]
```
- `:s/foo/bar`
	- Will replace all occurrences of 'foo' with 'bar' in the given line
- `:%s/foo/bar`
	- The `%` indicates a range from the first to the last line of the file

Copy
- `y$`
	- Copy (yank) everything from the cursor to the end of the line
	- 