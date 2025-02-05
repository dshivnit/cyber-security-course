- Debugging 
	- `gcc -g -o something something.c`
	- `objcopy --only-keep-debug something something.debug`
	- `gdb -s something.debug -e something`
	- In gdb type `info` and enter
		- This will give you the list of commands you can enter
	- *No idea what I'm doing at this stage, just thought I'd take note of this* 

There are several common ways to get the memory address of a function named `special()` from code that is already compiled:
	- Using GDB:
		`gdb ./program (gdb) print special`
	- Using objdump:
		`objdump -t ./program | grep special`
	- Using nm:
		`nm ./program | grep special`
-  