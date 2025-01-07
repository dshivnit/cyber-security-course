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
	- 