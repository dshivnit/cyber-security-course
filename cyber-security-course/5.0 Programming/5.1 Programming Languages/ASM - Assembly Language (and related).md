References:
https://pwn.college/computing-101/your-first-program/
https://pwn.college/computing-101/hello-hackers/
https://open.umn.edu/opentextbooks/textbooks/733 
https://cs.brown.edu/courses/cs033/docs/guides/x64_cheatsheet.pdf
https://en.wikibooks.org/wiki/X86_Assembly/X86_Architecture

All roads lead to the CPU:

- Not mandatory, although `.s` is the usual extension used for assembly files (ie `first-assembly.s`)

- Source Code
	- Python, Javascript, Java
- Intermediate Language Bytecode
	- Interpreter or JIT (Just In Time)
- Binary-encoded Instructions
	- CPU

- Source Code
	- C, C++, Rust
- Intermediate Language Bytecode
	- Compiler
- Binary-encoded Instructions
	- CPU

- Logic Gates
	- AND (&) Gate
		- Two inputs
		- If both inputs are TRUE
			- the output is TRUE
		- If any input is FALSE
			- the output is FALSE
	- OR Gate
		- Two inputs
		- If either one is TRUE
			- The output is TRUE
		- If both inputs are TRUE
			- The output is TRUE
		- If both inputs are FALSE
			- The output is FALSE
	- XOR Gate
		- If only one input is TRUE
			- The output is TRUE
		- If both inputs are the same (either TRUE, or FALSE)
			- The output is FALSE
	- NOT Gate
		- One input
		- If the input is TRUE
			- The output is FALSE
		- If the input is FALSE
			- The output is TRUE

- Voltages
	- TRUE
	- FALSE

- Binary
	- `01001100 01101001 01110110 01100101 00100000 01101100 01101111 01101110 01100111 00101100 00100000 01100001 01101110 01100100 00100000 01010000 01110010 01101111 01110011 01110000 01100101 01110010 00101110 00100000 00111010 00101001`
	- Decimal / Base 10
		- Has digits from 0-9
	- Binary / Base 2
		- Has digits 0 and 1
	- Octal 
	- Hexadecimal (A-F)
	- American Standard Code for Information Exchange (ASCII) 
	  https://www.ascii-code.com/
	- UTF-8
	- Computers speak in Binary, why? Consider the logic gates described earlier.

- Bytes into Words (please excuse the capitalisation of the character "b/B" here.. In data transfers, a small b is a bit, and a big B is a byte - don't forget that. Here we're just talking about bytes, Bytes :) )
	- Remember that a Byte is is 8 bits
	- Nibble
		- Half of a byte (4bits)
	- Byte - 1 byte, 8 bits
	- Half word / "word" - 2 bytes, 16 bits
	- Double word (dword) - 4 bytes, 32 bits
	- Quad word (qword) - 8 bytes, 64 bits

---
- #### NEED TO TOUCH ON THIS FURTHER ####
- Numbers (to touch on this)
	- Integer Overflow
	- Integer Underflow
- How to differentiate between positive and negative numbers? 
	- Two's complement
- Signed Numbers
- Unsigned Numbers
---

- Assembly is called assembly because it is assembled, and not compiled, into Binary Code

- CPUs are concerned with three types of data:
	- Data given to it directly in form or as part of an instruction
	- Data that it is actively working on (Data that it is close at hand)
		- In its registers
	- Data in storage
		- Memory

Some Operations
- Add some data together
- Subtract some data
- Multiply some data
- Divide some data
- Move some data into or out of storage/memory
- Compare two pieces of data with each other
- Test some other properties of data

Assembly Dialects (CPU architecture dependent, every architecture has its own variant)
- x86
- arm
- ppc
- mips
- risc-v
- pdp-11
- .... .... ... 

Registers (short notes, please excuse the style of note taking here - will fix this section later sometime)
- Short-term memory in a way
- Register File
	- Sits right in the CPU
	- Data flows from System Memory, through CPU Cache's, and then into the Register File
	- Or directly from the Instruction into the Register File
	- Registers are very fast, temporary storage stores for data
	- Several 'general' purpose registers
	- 32bit and 64bit CPUs will have a different amount of registers
	- and when working with tools like x64dbg, you'll see the difference (need to work with that more, much more)
- 32bit Registers (x86)
	- eax, ecx, edx, ebs, **esp, ebp**, esi, edi
- 64bit Registers (amd64)
	- rax, rcx, rdx, rbx, **rsp, rbp**, rsi, rdi, r8, r9, 10, r11, r12, r13, r14, 15
	- The lower 32 bits of `rax` can be accessed using `eax`
		- The lower 16-bits using `ax`
		- And the lower 8-bits using `al` 
	- Lower register bytes access is applicable to *almost all* registers.
- arm Registers
	- r0, r1, r2, r3, r4, r5, r6, r7, r8, r9, r10, r11, r12, **r13, r14**
- Address for the next instruction for the CPU is kept in:
	- x86 - eip
	- x64 (amd64) - rip
	- arm - r15
- You load data into registers with assembly
	- `mov`
		- Move
	- `mov rax, 0x539`
	- `mov rbx, 1337`
	- Immediate Value - data specified directly in the instruction
- `mov rax, 0x539`
- `mov rbx, rax`
	- This will set both `rax` and `rbx` to `0x539` (what Jan (sp?) from pwn.college calls 1337)
- `mov` does not destroy the source of the data, it copies it
Extending Data (NEED TO TOUCH ON THIS MUCH MORE)
- `movsx rax, eax`
	- `movsx` does a 'sign-extending' move. 
	- Preserves Two's Complement value
		- (copies the top bit to the rest of the register)
		- So you can still work with both the positive full number of the value, and its negative representation as well
- The registers have different sizes

- mov example
	- `mov rax, 1337`
	- `mov` - operator, or, instruction(s)
	- `rax` - operands, which represent additional data (in this case, the specification of `rax` as a destination)
	- `1337`
		- the value we want to store there, also known as the source?

- Some Register Arithmetic
- https://github.com/yrp604/rappel
	- Most instructions, the first specified register stores the result
	- add
	- sub
	- mul
		- unsigned multiply
	- imul
		- signed multiply
	- div
		- 10/3 = 3 (rounded down)
		- special instruction that can divide 128-bit dividend by a 64-bit divisor while storing both the quotient and the remainder - using only one register as an operand
			- `rax = rdx:rax / reg`
			- `rdx = remainder`
				- `rdx:rax` means that `rdx` will be the upper 64-bits of the 128-bit dividend and `rax` will be the lower 64-bits of the 128-bit dividend
			- You must be careful about what is in `rdx` and `rax` before you call `div` 
				```asm
				; 64-bit division example (I had to claude.ai this... Makes sense though!)
				mov rax, 1000000 ; Dividend 
				xor rdx, rdx ; Clear rdx 
				mov rcx, 42 ; Divisor 
				div rcx ; Divides rdx:rax by rcx 
				;Result: rax = quotient, rdx = remainder
				```
			- Note that `rdx` here is the remainder, aka, the modulo (`%`) result. And `rax` would be the result of the division that took place (rounded down!)
			- MODULO continued (examples with a faster operation method - apparently using `div` is slow)
				- "if we have `x & y`, and `y` is a power of 2, such as `2^n`, the result will be the lower `n` bits of `x`."
				- "Therefore, we can use the lower register byte access to efficiently implement modulo"
					- For example, if we had to solve this:
						```asm
						rax = rdi % 256
						rbx = rsi % 65536
						```
					- 2 ^ 8 = 256, so the lowest byte (8-bit). Which for `rdi` would be `dil`
					- 2 ^ 16 = 65536, so the lowest 16-bit of `rsi` would be `si` 
						```asm
						.intel_syntax noprefix
						.global _start
						_start:
						mov rax, 0
						mov rbx, 0 # I did this just to clear both registers.. Probably not needed?
						mov al, dil # moving the lowest 8-bit of rdi into the lowest 8-bit of rax
						mov bx, si
						```
					- And that's that!
	- inc
	- dec
	- neg
	- not
	- and
		- You can find out if a register is holding an odd or even number! By:
			- `and reg-name, 1`
				- This will test the LSb (least-signifcant bit, the rightmost bit in the 64-bit register, position 0)
					- If it returns a one with the above instruction, then the  number is odd
					- *But for checking even/odd, we only care about that single rightmost bit of the entire number, since a number is odd if and only if its least significant bit is 1, regardless of all other bits.*
	- or
	- xor
	- shl
		- `shl rax, 10` 
		- shift rax's bits left by 10 (filling with 10 zero's to the right)
	- shr
		- `shr rax, 10`
		- shift rax's bits right by 10, (filling with 10 zero's to the left)
	- sar
		- `sar rax, 10`
		- shift rax's bits right by 10, with sign-extension to fill the now 'missing' bits
	- ror
		- `ror rax, 10`
		- rotate the bits of rax right by 10
		- `rol rax, 10`
		- rotate the bits of rax left by 10
	- xchg reg1 reg2
		- swaps the values between the two registers

Special Registers
- You cannot directly read from or write to `rip`
	- Contains the memory address of the next instruction to be executed (ip = Instruction Pointer)
- You should be careful with `rsp`
	- Contains the address of a region of memory to store temporary data (sp = Stack Pointer)
- *More to come*

- Normally - there are between 10 and 20 'general purpose' registers that code can use for any reason, and up to a few dozen other ones that are used for special purposes


FAULTS
- Segmentation Fault


Syscall (System Call) Instruction
- Programs interact with the OS via the CPU (some things here will be basic, but I'm covering all grounds as I go along :) )
- Linux has around 330 different syscalls
- Programs invoke a specific syscall by moving its syscall number in to the `rax` register and invoking the `syscall` instruction
- ie
	`mov rax, 60`
	`syscall`
	Exits the program cleanly. 60 is moved into rax, then syscall is invoked
- You can pass parameters into the syscall through registers as well - say for example if you wanted the program to exit with an exit code of 42
	- The first parameter to a syscall is passed via the `rdi` register. 
	- If you want a program to exit with an exit code of 42 for example:
		`mov rdi, 42`
		`mov rax, 60`
		`syscall`
	- You will, however, need an executable (referencing 42 as the exit code) in order to be able to this

Building an Executable
- One will need to:
	- write the assembly in a file (either in an `.S` or `.s` syntax)
	- Assemble the binary into an executable *object file* (using the `as` command)
	- Link one or more executable object files into a final executable binary (using the `ld` command)
- One will need to prepend a directive at the beginning of the assembly code, say for example if we're using the Intel Assembly Syntax:
```asm.s
.intel_syntax noprefix
mov rdi, 42
mov rax, 60
syscall
```
- `.intel_syntax noprefix` will tell the assembler that you will be using the Intel Assembly Syntax, specifically the variant where you don't have to add extra prefixes to every instruction (more on this later) 
- Assemble the code using the `as` assembler (if the instructions working with are in a file called `asm.s`)
	- `as -o asm.o asm.s`
	- The source code in `asm.s` is assembled into binary code, and an object filed named `asm.o` is created (outputted)
	- Albeit that the object file has assembled binary code in it, it isn't ready to be run yet. 
	- It needs to be linked first.

Linking Executables
- In usual production, there will be source code that is compiled and assembled into object files, however, there are normally numerous amounts of these object files. 
- Source code files in a program are compiled into their own object files. They are then linked together, into a single executable file. 
- Even if there is only one object file, we still need to link it to create the final executable, `exe` file. 
- This is done with the `ld` (from the term **l**ink e**d**itor) command:
- `ld -o exe asm.o`
- an exe is created!
- Now, for the time being we're only testing exit codes, so if you run this `./exe` nothing will happen
- But if you check for exit/error codes
	- `echo $?`
	- 42 is returned :) (which is the exit code we set the program to use when exiting earlier)

\_start
- This snippet of code indicates where in your program should begin from when ELF is executed.  (ELF - Executable and Linkable Format)
- Continuing to work with the code from above - this can be added as below:
```asm.s
.intel_syntax noprefix
.global _start
_start:
mov rdi, 42
mov rax, 60
syscall
```
- Assemble using the assembler (`as`)
- Link to an executable with the Link Editor (`ld`)
- The `.global_start` will direct the assembler (`as`) to make the `_start` label 'globally visible' at the 'linker level,' instead of just locally visible at the object file level 
- Since the Link Editor (`ld`) is the linker this particular directive (`.global _start`) is needed for the `_start:` label to be seen.
- (remember, I referenced a gem at the start of this page. **pwn.college** - check 'em out, amazing stuff on there :) )

Tracing Syscalls and Debugging
- Syscal Tracer - `strace`
- `strace` once given a program to run, will use Linux functionality to introspect and record every system call the program invokes, and the results of those syscalls
- `strace ./exe`
- the `execve` syscall is one that starts a new program
- the `exit` syscall is just that
- the `alarm` syscall (syscall number 37) will set a timer in the OS, and when that timer hits 0, the OS will terminate the program
	- The point of `alarm` is to kill the program when it is frozen.

Moving Between Registers
- `rsi`
	- Like `rdi`, `rsi` is a register where data can be parked, example:
		- `mov rsi, 42`
		- `mov rdi, rsi`
	- `mov` here is actually setting the data
	- Here, both `rdi` and `rsi` will be set to 42
	- Don't worry about the naming conventions - lel..

- Memory (RAM)
	- Address linearly
		- From: 0x10000 (for security reasons..)
		- To: 0x7fffffffffff (for architecture / OS purposes)
			- *Will need to refine this at some stage as learning progresses*
	- Each memory address references one-byte in memory
	- This means, 127 terabytes of addressable RAM..?
		- Virtually, not physically
		- 
	- There is too much memory to name every location (like we do with registers) 
		- They are referenced as numbers (numerical identifiers)
	- The Stack
		- A region of memory, that when a process starts up - a space in memory is created called the stack
		- You push things on to the stack, then you pop them off the stack
			```asm
			mov rax, 0xc001ca75
			push rax
			push 0xb0bacafe
			push rax
			```
		- (like mov, push leaves the value in the src register intact)
		```asm
		pop rbx # sets rbx to 0xc001ca75
		pop rcx # sets rcx to 0xb0bacafe
		```
		- Popped off in reverse order from how they were pushed
			- It logically pops the data that is sitting in the stack 'off' - but the actual data remains should you wanted to get back and access them...
			- Above we are popping whatever was pushed last into the stack, firstly into rbx (`0xc001ca75`) and then (`0xb0bacafe`) into rcx
				- But logically off the stack
		- Each entry is 64-bits
		- When you push onto the stack, the rsp decrease by 8
		- Pops add 8 to rsp
		- Temporary Data Storage
		- You can move data between registers and memory with `mov`
		- Registers point to a place in memory
			- `mov rax, 0x133337`
			- `mov [rax], rbx`
		- Equivalent to `push rcx`:
			- `sub rsp, 8 # subtracting 8 from rsp` 
			- `mov [rsp], rcx`
		- Each addressed memory location contains one byte:
			- An 8-byte write at address `0x133337` will write to addresses `0x133337` through to `0x13333f`
- Controlling Write Sizes
	- You can use partials to store/load fewer bits
	- Load 64 bits from addr `0x12345` and store the lower 32 bits to addr `0x133337`
		```asm
		mov rax, 0x12345
		mov rbx, [rax]
		mov rax, 0x133337
		mov [rax], ebx
		```
	- Store 8 bits from addr `0x12345` to `bh`
		```asm
		mov rax, 0x12345
		mov bh, [rax]
		```
- Memory Endianess
	- Data on most modern systems is stored backwards, bitewise, in little endian
	- Will have to watch this again (https://www.youtube.com/watch?v=HahXfnOsSUU), and again, and again.
	- `mov eax, 0xc001ca75 # sets rax to` 
		- c0 | 01 | ca (`ah`) | 75 (`al`)
	- `mov rcx, 0x10000` 
	- `mov [rcx], eax # stores data as`
		- 75 (`0x10000`) | ca (`0x10001`) | 01 (`0x10002`) | c0 (`0x10003`)
	- `mov bh, [rcx] # reads 0x75 first, and so on, backwards`
	- See how the data was stored backwards, coolcats (`c001ca75`) into `eax`? 
		- Essentially flipping it around
	- This happens for historical reasons.. 
		- Intel created the 8008 for a company called Datapoint in 1972
		- Datapoint used little endian for easier implementation of carry in arithmetic
		- Intel used little endian in 8008 for compatibility with Datapoint's processes
		- Every step in the evolution between 8008 and modern x86 maintained some level of binary compatibility with its processor 
	- Bytes are only shuffled for multi-byte stores and loads of registers to memory
	- Individual bytes never have their bits shuffled
		- Yes, writes to the stack behave just like any other write to memory
		- *Remember, this is a course from pwn.college - I'm note taking for the time being :) *
- Address Calculation
	- You can do some limited calculation for memory addresses
	- Use `rax` as an offset off some base address (in this case, the stack)
	```asm
	mov rax, 0
	mov rbx, [rsp+rax*8] # read a qword right at the stack pointer
	inc rax
	mov rcx, [rsp+rax*8] # read a qword to the right of the previous one
	```
	- You can get the calculated address with Load Effective Address (`lea`)
	```asm
	mov rax, 1
	pop rcx
	lea rbx, [rsp+rax*8] # rbx now holds the computed address for double-checking
	mov rbx, [rbx]
	```
	- Address calculation has limits
		- **reg+reg*(2 or 4 or 8)+value** is as good as it gets
- RIP - Relative Addressing
	- `lea` is one of the few instructions that can directly access the rip register
	```asm
	lea rax, [rip] # load the address of the next instruction into rax
	lea rax, [rip+8] # the address of the next instruction, plus 8 bytes
	```
	- You can also use `mov` to read directly from those locations
		- `mov rax, [rip] # load 8 bytes from the location pointed to by the address of the next instruction`
	- Or write there
		- `mov [rip], rax # write 8 bytes over the next instruction (CAVEATS APPLY)`
	- This is useful for working with data embedded near your code
	- This is what makes certain security features on modern machines possible
- Writing Immediate Values
	- You can also write immediate values
	- You must, however, specify their size:
		- This writes a 32-bit 0x1337 (padded with 0 bits) to address 0x133337
			```asm
			mov rax, 0x133337
			mov DWORD PTR [rax], 0x1337
			```
		- Depending on your assembler, it might expect DWORD instead of DWORD PTR
- Other Memory Regions
	- *to describe later..*

System Calls
https://blog.rchapman.org/posts/Linux_System_Call_Table_for_x86_64/
- An instruction that makes a call to the OS
- `syscall` triggers the system call specified by the value in `rax`
- Arguments in `rdi`, `rsi`, `rdx`, `r10`, `r8`, and `r9` retun value in `rax`
- Reading 100 bytes from stdin to the stack:
- `n = read(0, buf, 100);`
	```asm
	mov rdi, 0 # the stdin file descriptor
	mov rsi, rsp # read the data onto the stack
	mov rdx, 100 # the number of bytes to read
	mov rax, 0 # system call number of read()
	syscall # do the system call
	```
- `read` returns the number of bytes read via `rax`, so we can easily `write` them out:
- `write(1, buf, n);`
	```asm
	mov rdi, 1 # the stdout file descriptor
	mov rsi, rsp # write the data from the stack
	mov rdx, rax # the number of bytes to write (same as what we read in)
	mov rax, 1 # system call number of write()
	syscall # do the system call
	```
- System calls have  very well-defined interfaces that very rarely change
- There are over 300 syscalls in Linux, here are some examples:
- `int open(const char *pathname, int flags)`
	- Returns a file new descriptor of the open file (also shows up in /proc/self/fd!)
- `ssize_t read (int fd, void *buf, size_t count)` 
	- Reads data from the file descriptor
- `ssize_t write(int fd, void *buf, size_t count)`
	- Writes data to the file descriptor
- `pid_t fork()`
	- Forks off an identical child process.
	- Returns 0 if you're the child and the PID of the child if you're the parent
- `int execve(const char *filename, char **argv, char **envp)`
	- Replaces your process
- `pid_t wait(int *wstatus)`
	- Wait child termination, returns its PID, write its status into `*wstatus`

"String" Arguments
- ASCII bytes
- Syscalls take "string" arguments (for example, file paths)
- A string is a bunch of contiguous bytes in memory, followed by a `0` byte
- Building a file path for `open()` on the stack:
	```asm
	mov BYTE PTR [rsp+0], '/' # write the **ASCII** value of '/' onto the stack
	mov BYTE PTR [rsp+1], 'f'
	mov BYTE PTR [rsp+2], 'l'
	mov BYTE PTR [rsp+3], 'a'
	mov BYTE PTR [rsp+4], 'g'
	mov BYTE PTR [rsp+5], 0 # write the 0 byte that will terminate our string
	```
	- The stack would then somewhat look like this (remember this is in **ASCII**):
	- `rsp = 2f (/)` | `rsp+1 = 66 (f)` | `rsp+2 = 6c (l)` | `rsp+3 = 61 (a)` | `rsp+4 = 67 (g)` | `rsp+5 = 00 (\0)`
- Now we can `open()` the `/flag` file:
	```asm
	mov rdi, rsp # read the data on to the stack
	mov rsi, 0 # open the file read only (more on this later)
	mov rax, 2 # system call number of open()
	syscall # do the system call
	```
	- `open()` returns the file descriptor number in `rax`

Constant Arguments
- Some system calls require archaic "constants". 
- The argument flags must include one of the following access modes:
	- O_RDONLY
	- O_WRONLY
	- O_RDWR
	- These request opening the file read-only, write-only, or read/write respectively (the naming convention pretty much speaks for itself)
- Example:
	- `open()` has a flags argument to determine how the file will be opened. 
	- We can figure out the values of these arguments in C:
		```C
		#include <stdio.h>
		#include <fcntl.h>
		int main() {
			printf("O_RDONLY is: %d\n", O_RDONLY);
		}
		```
	- Returns:
		```bash
		./print_rdonly
		O_RDONLY is: 0
		```

And then Quit (the program :P ):
- As so:
	```asm
	mov rdi, 42 # our program's return code (eg, for bash scripts)
	mov rax, 60 # the system call number for exit()
	syscall # do the system call!
	```

Writing Output
- `write` syscall is `1`
- The `write` syscall needs to specify, via its parameters, what data to write and where to write it to.
- File Descriptors
	- Each process starts out with three FDs
		- FD 0 - Standard Input
			- The channel through which the process takes input
				- Your shell uses Standard Input (FD 0) to read the commands that you input
		- FD 1 - Standard Output
			- The channel through which processes output normal data, such as when you run a `cat` command on a file to read its contents, or use the `ls` command to list contents of a directory
		- FD 2 - Standard Error
			- The channel through which processes output error details
				- If you mistype a command, the shell will output over Standard Error - `this command does not exist` or something like that
- `write` system calls specify where to write the data to
	- ie, to which File Descriptor
- Example:
	- The first command to an `exit` system call could be the exit code (that we described before) - `mov rdi, 42` 
	- The first (but not only) parameter to `write` is the File Descriptor
- If you want to write to Standard Output (FD 1) you would set `rdi` to 1
- If you want to write to Standard Error (FD 2) you would set `rdi` to 2
- What to write
	- Registers don't fit a tonne of data, and to write a long story one would need to invoke the `write` system call multiple times. 
	- Relatively speaking, that would have a high performance cost
	- The CPU needs to switch from executing the instructions of your program to executing the instructions of Linux itself - do a bunch of housekeeping computation - interact with your hardware to get the actual pixels to show up on your screen - and then switch back....
		- This is slow. 
	- So we try to MINIMISE the number of times we invoke system calls
	- The solution to this would be to write multiple characters at the same time
	- The `write` system call does this by taking **two** parameters for the "**what**": a **where** (in memory) to start writing from and a **how many** characters to write. 
	- These parameters are passed as the second and third parameter to `write`. In the kind of C-syntax that we learned from `strace`(system call tracer.)- this could be:
		- `write(file_descriptor, memory_address, number_of_characters_to_write)`
	- Example:
		- If you wanted to write 10 characters from memory address `1337000` to Standard Output (FD 1), it would be:
		- `write(1, 1337000, 10)`
	- Specifying these parameters. Example continued:
		- Pass the **first** parameter of a system call, as we reviewed above, in the `rdi` register
		- **Second** parameter via the `rsi` register
			- The agreed-upon convention in Linux is that `rsi` is used as the second parameter to system calls
		- Third **parameter** via the `rdx` register
			- `rdi` (the register holding the first parameter) has such a similar name to `rdx` that it's really easy to mix up, and the naming is this way for historic reasons .
		- And the `write` syscall index into `rax` itself: `1` 

Control Flow (making decisions)
	https://www.youtube.com/watch?v=0a8NlF7z7Ro
	https://en.wikibooks.org/wiki/X86_Assembly/Control_Flow
- Assembly instructions are direct translations of binary code
	- The binary code lives in memory when the program is loaded
	- And is then passed directly into the CPU
- Example:
	- Program Binary Code | 0x400800 `pop rax` | `pop rbx` | `add rax, rbx` | `push rax` 
- The above in Hex would look like:
	- Program Binary Code | 0x400800 `58` | 0x400801 `5b` | 0x400802 `48 01 d8` | 0x400805 `50` 
- As you can see above, Assembly is a **direct translation** of Binary Code!
- x86 is what is called a Variable-Width architecture
	- (whereas ARM is a Fixed-Width architecture)

Control Flow - Jumps
- CPUs execute instructions in sequence until told not to 
- One way to interrupt the sequence is with a `jmp` instruction:
	```asm
		mov cx, 1337
		jmp STAY_LEET
		mov cx, 0
	STAY_LEET:
		push rcx
	```
- Would look like, firstly:
	- Program Binary Code | 0x400800 `mov cx, 1337` | `jmp STAY_LEET` | `mov cx, 0` | STAY_LEET `push rcx`
- Translated into Binary would look like:
	- Program Binary Code | 0x400800 `66 b9 37 13` (notice the little endian 37 13 for 1337) | 0x400804 `eb 04` (**skip 4 bytes** - hence the 04) | 0x400806 `66 b9 00 00` | STAY_LEET 0x40080a `51` 
- `jmp` skips X bytes and then resumes execution. 
	- `eb` is for the `jmp` instruction
	- `eb fe` will jump back to the start of the instruction (like `-2`)
		- `eb fe` is an infinite loop in x86
- `jmp` is useful for embedding data in the code

Control Flow - Conditional Jump
- Jumps can rely on conditions
	```asm
	mov cx, 1337
	jnz STAY_LEET
	mov cx; 0
	STAY_LEET:
	push rcx
	```
- The above would look like, firstly:
	- Program Binary Code | 0x400800 `mov cx, 0x1337` | `jmp STAY_LEET` | `mov cx, 0` | STAY_LEET `push_rcx`
- In Binary:
	- Program Binary Code | 0x400800 `66 b9 37 13` | 0x400804 `75 04` | 0x400806 `66 b9 00 00` | STAY_LEET 0x40080a `51`
- `jnz` - But jump if **what** is not zero...? 
	- What we checked last for equality
	- First check things, and then you take actions on the checked things
	- (*will continue this after the list of `jmp` conditions below*)
- Jump Conditions:
	- `je` - jump if equal
	- `jne` - jump if not equal
	- `jg` - jump if greater
	- `jl` - jump if less
	- `jle` - jump if less than or equal
	- `jge` - jump if greater than or equal
	- `ja` - jump if above (unsigned)
	- `jb` - jump if below (unsigned)
	- `jae` - jump if above or equal (unsigned)
	- `jbe` - jump if below or equal (unsigned)
	- `js` - jump if signed
	- `jns` - jump if not signed
	- `jo` - jump if overflow
	- `jno` - jump if not overflow
	- `jz`- jump if zero
	- `jnz` - jump if not zero

Control Flow - Conditions
- Conditional jumps check Conditions stored in the "flags" register: `rflags`
	- https://en.wikipedia.org/wiki/FLAGS_register
	- `rflags` hold a bunch of bits representing condition flags
- Flags are updated by:
	- Most arithmetic instructions
	- Comparison instruction `cmp` (**sub**, but discards result)
	- Comparison instruction `test` (**and**, but discards result)
- Main conditional flags:
	- **Carry Flag** CF: 
		- was the 65th bit 1 (the extra bit)?
		- "in this last 64-bit, 32-bit (or 8-bit) operation, was the extra bit, 1? Was the carry bit, 1?"
	- **Zero Flag** ZF: 
		- was the result 0? 
	- **Overflow Flag** OF: 
		- did the result "wrap" between positive to negative? 
	- **Signed Flag** SF: 
		- was the result's signed bit set (ie was it negative)?
- Common patterns:
	```asm
	cmp rax, rbx: ja STAY_LEET # unsigned rax > rbx. 0xffffffff >= 0
	cmp rax, rbx; jle STAY_LEET # signed rax <= rbx. 0xffffffff = -1 < 0
	test rax, rax; jnz STAY_LEET  # rax != 0
	cmp rax, rbx; je STAY_LEET # rax == rbx
	```
	- **Thanks to Two's Complement, only the *jumps themselves* have to be signedness-aware**
- Jump Conditions with `rflags` (same as above with an additional column)
	- `je` - ZF=1
	- `jne` - ZF=0
	- `jg` - ZF=0 and SF=OF
	- `jl` - SF!=OF
	- `jle` - ZF=1 or SF!=OF
	- `jge` - SF=OF
	- `ja` - CF=0 and ZF=0
	- `jb` - CF=1
	- `jae` - CF=0
	- `jbe` - CF=1 or ZF=1
	- `js` - SF=1
	- `jns` SF=0
	- `jo` - OF=1
	- `jno` - OF=0
	- `jz` - ZF=1
	- `jnz` ZF=0
- We don't tend to normally deal with the `rflags`  directly but use the semantic jump conditions more (as previously stated above prior to the addition of the `rflags` column)

Looping
- With our conditional jumps, we can implement a loop (think of the usual for, while etc)
- Example (this counts to 10):
	```asm
	mov rax, 0
	LOOP_HEADER:
	inc rax
	cmp rax, 10
	jb LOOP_HEADER # if rax is less than 10, jump back to LOOP_HEADER
	# now rax is 10
	```
- With looping and conditional control flow, we have almost everything we need to write anything we want

Control Flow - Function Calls
- Assembly code is split into functions with `call` and `ret`. 
- `call` - pushes `rip` (address of the next instruction after the call) and jumps away
- `ret` - pops `rip` and jumps to it
- Using a function that takes an **authenticated** value and returns **leetness**:
	```asm
	mov rdi, 0
	call FUNC_CHECK_LEET # pushing the value of rdi (0) on to FUNC_CHECK_LEET (below)
	mov rdi, 1
	call FUNC_CHECK_LEET # pushing the value of rdi (1) on to FUNC_CHECK_LEET (below)
	call EXIT

	FUNC_CHECK_LEET:
		test rdi, rdi
		jnz LEET # jump if rdi is not zero, call LEET (below)
		mov ax, 0  
		ret # otherwise return 0 and pop rip
		LEET:
		mov ax, 1337 
		ret # return 1337 and pop rip  

	FUNC_EXIT:
		???
	```
- In code:
	```C
	int check_leet(int authed) {
		if (authed) return 1337;
		else return 0;
	}
int main() {
	check_leet(0);
	check_leet(1);
	exit()
}
	```

Calling Conventions
- Calle and caller functions must agree on argument passing.
	- **Linux x86**
		- push arguments (in reverse order), then call (which pushes return addresses), return value in `eax` 
	- **Linux amd64**
		- `rdi`, `rsi`, `rdx`, `rcx`, `r8`, `r9`, return value in `rax`
	- **Linux arm**
		- `r0`, `r1`, `r2`, `r3` return value in `r0`
- Registers are *shared* between functions, so calling conventions should agree on what registers are **protected**. 
- **Linux amd64**
	- `rbx`, `rbp`, `r12`, `r13`, `r14`, `r15` are "**callee-saved**"
		- (the function you call keeps their values safe on the stack)
			- It will return these registers back in the same way that the function found them on the stack
				- After modifying them
				- Before returning these registers it will pop them off
		- Other registers are up for grabs
			- (within reason; eg - `rsp` must be maintained - temporary storage of things). 
			- Save their values (on the stack)
	- If you don't want `rcx` to be destroyed by function calls, then save it, on to the stack - push it, then pop it after you call the function
		- This is called caller-save registers

Building Programs
https://www.youtube.com/watch?v=IITocH-WGH4
- From Assembly to Binary
	```asm
	# .intel_syntax tells the assembler that we are using Intel assembly syntax
	# noprefix tells it that we will not prefix all register names with "%" (cause that looks silly, lol Yan)
	.intel_syntax noprefix
	.global _start
	start_:
	mov rdi, 42 # our program's return code (eg for bash scripts)
	mov rax, 60 # system call number of exit()
	syscall # do the system call
	```
- Assembly is named after the Assembler. Let's use the Assembler (but using the whole package this time, not just `as`)
	- `gcc -nostdlib -o filetocompile filetocompile.s`
		- `nostdlib` - this is NOT a C that uses C libraries
	- `file filetocompile`
	- You truncate one step here compared to the other way of compiling that was described earlier above (or way up above ...) that being having to use the Link Editor command `ld -o exe asm.o` for example
- Reading Assembly
	- **Disassemble** the program!
	- `objdump -M intel -d filetodisassemble`
- Extracting the Binary Code
	- gcc builds your Assembly into a full ELF (executable and linkable format) program
	- You can extract *just* your binary code:
		- `objcopy --dump-section .text=file-to-extract_binary_code file-to-extract`
		- This will then produce a file called 'file-to-extract_binary_code' 
		- You can read its contents by:
			- `hd file-to-extract_binary_code`
			- Which will then get you your binary code
			- `hd` here is HEX DUMP

Bugs in the Program
- Your program might have errors
- This has been prophesised for centuries (lol)
	- *"... an analysing process must equally have been performed in order to furnish the Analytical Engine with the necessary operative data; and that herein may also lie a possible source of error.* 
	  *Granted that the actual mechanism is unerring in its process, the cards may give it wrong orders"*
		  Ada Lovelace - Notes on the Analytical Engine (1843)
- Debugging bugs through the ages
	- The term "bug" to mean "fault" dates back a long time:
		- "*... difficulties arise-this thing gives out and \[it is\] then that "Bugs" - as such little faults and difficulties are called - show themselves*"
			  Thomas Edison - letter (1878)
- Popularly attributed to Grace Hopper for finding a moth in a computer - lol an actual bug... 
- To remove bugs, you need to debug them (thanks Yan)
- Debugging
	- Debugging is done with debuggers, such as `gdb`
	- Debuggers use (among other methods), a special debug instruction:
		```asm
		mov rdi, 42 // our program's return code (ie for bash scripts)
		mov rax, 60 // system call number for exit()
		int3 // trigger the debugger with a breakpoint
		syscall // do the system call
		```
	- When the `int3` breakpoint instruction executes, the debugged program is interrupted and you can inspect its state
	- Of course, the debugger itself can set breakpoints:
		- Overwrites the instruction at the breakpoint address with `int3`
		- Emulates its effects when the breakpoint is executed instead
	- (pwn.college Assembly Crash Course has an automatic debugger that has been provided for us/you/me - putting in an `int3` is the way to use it.)
	- Note: `int3` or interrupter 3 - will need to have an associated debugger attached. Otherwise the process is going to die

Memory
- Remember that memory is linear
- It goes from `0` to `0xffffffffffffffff` (massive)
- Dereferencing:
	- `mov rax, [some-memory-address]`
		- We can access the "thing" at a memory location 
- Also works with registers
	- `mov rax, [rdi]`
- In x86_64 you can access each of the word sizes when dereferencing an address - just like using bigger or smaller register accesses:
	- `mov al, [mem-address]` -- moves the least significant **byte** from the `mem-address` to `rax`
	- `mov ax, [mem-address]` -- moves the least significant **word** from `mem-address` to `rax`
	- `mov eax, [mem-address]` -- moves the least significant **double-word** from `mem-address` to `rax`
	- `mov rax, [mem-address]` -- moves the full **quad-word** from `mem-address` to `rax`
	- **REMEMBER, moving into `al` does not fully clear the upper bytes**
	- Also remember:
		- byte - 1-byte - 8-bits
		- word - 2-bytes -16-bits
		- double-word - 4-bytes - 32bits
		- quad-word - 8-bytes - 64 bits
- Little Endian
	- Recalling that memory is stored linearly
	- If we wanted to access the quad word at `0x1337`
		- `[0x1337] = 0x00000000deadbeef`
	- It would be laid out in memory like this - by little endian:
		- `[0x1337] = 0xef`
		- `[0x1337 + 1] = 0xbe`
		- `[0x1337 + 2] = 0xad`
		- `[0x1337 + 3] = 0xde]`
		- `[0x1337 + 7] = 0x00`
	- This means that we can access things next to each other using offsets
	- Say if you want the 5th byte from an address, you can access it like so:
		- `mov al, [mem-address+4]`
	- Offsets always start at 0, woo

The Stack
- The stack is a region of memory that can store values for later
- To store a value on the stack, we use the `push` instruction
- To retrieve a value from the stack, we use the `pop` instruction
- **The stack works on a LIFO (Last In, First Out) memory structure**
	- Meaning that the last value pushed, is the first value that is popped
	- Think about a stack of plates, one would take the top most plate first when wanting to use a plate. Same thing here with the stack when using `pop` 
- The `push` instruction will take the value in a register and push it onto the top of the stack
	- `pop rax` - will take the top (last pushed) value from the stack and put it into `rax`
	- `sub rax, rdi` - will subtract `rdi` from the value that is in `rax` (which in this case will be what was last in the stack)
	- `push rax` - will push the new value back into the stack
- `rsp` (The Registry Stack Pointer)
	- on x86, the `rsp` always stores the memory address of the top of the stack
		- ie - the memory address of the last value pushed
	- One can use `[rsp]` to access the value at the memory address in `rsp` 
	- For example
		```asm
		mov r8, [rsp]
		mov r9, [rsp+0x8]
		mov r10, [rsp+0x10]
		mov r11, [rsp+0x18]
		```
		- `[rsp]` - is the TOP of the stack!
		- `[rsp+0x8]` - 8 bytes up
		- `[rsp+0x10]` - 16 bytes up
		- `[rsp+0x18]` - 24 bytes up
		- These will be bytes, as we are working with QWORDS! 
			- (Quad-words = 64bits, or 8 bytes)
Other Resources
- `gdb` - the go-to debugging experience
- `strace` - lets you figure out how your program is interacting with the OS
	- A good first stop for debugging
- `Rappel` - lets you explore the effects of instructions
	- https://github.com/yrp604/rappel
	- Installable via https://github.com/zardus/ctf-tools
- Documentation of x86
	- Opcode listing by byte value:
		- http://ref.x86asm.net/coder64.html
	- Instruction documentation:
		- https://www.felixcloutier.com/x86/
	- Intel's x86_64 architecture manual:
		- http://www.intel.com/content/dam/www/public/us/en/documents/manuals/64-ia-32-architectures-software-developer-instruction-set-reference-manual-325383.pdf

