References:
https://pwn.college/computing-101/your-first-program/

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
	- imul
	- inc
	- dec
	- neg
	- not
	- and
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
	- 