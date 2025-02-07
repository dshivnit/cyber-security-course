https://pwn.college/computing-101/debugging-refresher/
https://sourceware.org/gdb/current/onlinedocs/gdb.html/index.html
https://web.archive.org/web/20250101052732/https://users.umiacs.umd.edu/~tdumitra/courses/ENEE757/Fall15/misc/gdb_tutorial.html
https://www.brendangregg.com/blog/2016-08-09/gdb-example-ncurses.html
https://github.com/pwndbg/pwndbg/blob/dev/FEATURES.md
https://hugsy.github.io/gef/commands/aliases/
https://apps.p.ost2.fyi/learning/course/course-v1:OpenSecurityTraining2+Dbg1012_IntroGDB+2024_v1/home

---

**Running through "Debuggers 1012: Introductory GDB"**
(https://apps.p.ost2.fyi/learning/course/course-v1:OpenSecurityTraining2+Dbg1012_IntroGDB+2024_v1/home)

Compiling Test Programs fibber.c and echo.c
```C
// fibber.c
#include <stdio.h>

unsigned int fibbonacci(unsigned int n){
        if(n <= 1){
                return n;
        }
        else{
                return (fibbonacci(n-1) + fibbonacci(n-2));
        }
}

int main(){
        unsigned int n = 10;

        printf("First %d elements of the Fibbonacci sequence: ", n);

        for(unsigned int i = 0; i < n; i++){
                printf("%d ", fibbonacci(i));
        }
        printf("\n");
        return 0;
}
```
- Created the above `fibber.c` file
- Compiled it
	- `gcc -ggdb fibber.c -o fibber_bin`
		- `-ggdb`
			- Adds GDB debugging symbols to the binary
			- Confirm it executes by running the bin file that is created (`fibber_bin`)
```C
// echo.c - A simple program to take input on the command line and echo it back out
#include <stdio.h>
void main(int argc, char ** argv){
        if(argv[1] != NULL && argv[1] != ""){
                printf("You entered %s for argv[1]\n", argv[1]);
        } else {
                printf("You didn't enter an argv[1]\n");
        }
}
```
- Created the above echo.c file
- Compiled it with:
	- `gcc -ggdb echo.c -o echo_bin`
	- Confirmed `echo_bin` is running

Loading a Binary from Disk
- Loading binary from filesystem: Option 1
	- Load `fibber_bin` in GDB with `gdb --quiet ./fibber_bin`: 
		- Loads the binary in quiet mode
		- Otherwise you get the gdb banner
- Loading binary from filesystem: Option 2
	- Run `gdb -q`, then load the executable to be run with the `file <path-to-executable>` command
- Quitting GDB
	- `(gdb) quit`
	- or `ctrl+d`

Commands: run, start, continue
- Running (or re-running) a program
	- The `run` (short '`r`') command will run the program just the same as if you had invoked it from the CLI
		- `(gdb) r`
			- Runs the program.
- Running a program that requires CLI requirements
	- If the program requires CLI arguments, they can be passed after the run command, the same way they would be if you were invoking the program from the terminal
		- `(gdb) r yo`
- Starting a program and breaking at its entry point
	- Start command is like run, except that it sets a breakpoint on the entry point of the program
		- `(gdb) start`
	- You can also specify arguments if needed by the program - after the `start` command
		- `(gdb) start yo`
- Continuing execution of a program stopped at a breakpoint
	- `continue` or '`c`'
		- `(gdb) c`

Code Breakpoints: Setting, Listing and Deleting
- Setting Code Breakpoints
	- Breakpoints can be set with the `break` or ('`b`') command
		- `(gdb) break main`
		- `(gdb) b fibbonacci`
			- This one is interesting in this scenario with the fibber code above
- Listing Code Breakpoints
	- Breakpoints can be listed with either `info breakpoints` or `info break` or `info b`
		- `(gdb) break main`
		- `(gdb) break fibbonacci`
		- `info b`
- Unsetting Code Breakpoints
	- `clear <address>` command can remove a breakpoint at the address, specified either by a symbol name, or a `*` followed by an absolute memory address
		- `clear *0x0000555555555155`
		- `info break`
		- `clear main`
		- `info break`
	- `delete <breakpoint-number-from-info-breakpoints>` (short `'d'`) will delete the specific breakpoint given by a number taken from the `info break` output
- Note that the memory addresses can change from where breakpoints are initially pointed out. Reason being is that the debugger has no idea where in memory the actual code, when being run/executed, will reside in memory until it has started running. Also, the OS may randomize where the executable is loaded into memory - a mechanism called **Address Space Layout Randomization (ASLR)** - which is designed to assist in mitigating some security vulnerabilities. 
	- So , after an executable has started, the debugger will be able to display exactly the real addresses for the executable after it has been loaded in memory and started. 

Code Breakpoints: Disabling and Enabling
https://web.archive.org/web/20221203080449/http://www.sourceware.org/gdb/current/onlinedocs/gdb/Disabling.html
- Disabling Breakpoints:
	- Once you have a breakpoint number from `info break` you can `disable` it (via calling upon its number in `info b`)
- Enabling Breakpoints
	- `enable <breakpoint-number>`

Examining Source Code
- Listing Source Code Lines
- https://web.archive.org/web/20220606212422/https://sourceware.org/gdb/current/onlinedocs/gdb/List.html#List
	- Only relevant to situations in which you have the source code for the program being debugged, and if it was built with symbols enabled 
		- The `-g` or `-ggdb` flags to `gcc`
	- It will not be useful when reverse engineering opaque binaries
	- `list`
		- Will show you source code surrounding the current location you are stopped at
	- `list <function-name>`
		- Will show source code before and after the given function
	- `list <source-file-name>:<line-number>`
		- Will show source code before and after the given line in the given file

Examining Assembly
- One-time Disassembly Display
- https://web.archive.org/web/20221127202729/https://sourceware.org/gdb/current/onlinedocs/gdb/Machine-Code.html
	- `diassemble` or `disas`
		- will show assembly surrounding the current location where you are stopped at
	- `disassemble <address-or-symbol-name>`
		- Disassembles the memory specified by the address or symbol name
	- `disassemble /r`
		- Gives the raw bytes which make up the instructions
	- `disassemble /m`
		- Mixes source code and assembly in the output
	- `x`
		- Examine memory command
		- Can display some number of instructions at a given address, form is
			- `x/10i <address>`
- Continuously-updating Disassembly Display
	- `display` and one of it's forms can ensure that every time a program stops, that some number of instructions ()
		- `display/10i <instruction-pointer / program-counter>`

Commands: x (examine), print, display
- Format Specifiers
	- 
---



`gdb` - GNU Debugger
- Start a program
	- `(gdb) starti`
- 