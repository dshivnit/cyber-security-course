[[2.1.1.0 AMD CPUs]]

- AMD
- Intel
- Qualcomm
- Exynos
- MediaTek


- *Describe general basics*
	- CPU Cache
	- Current standards (in particular from AMD, X3D BABY!)
	- Performance Cores
	- Energy-saving Cores
	- Page Files
	

- Hyperthreading
	- Hyperthreading is a technology that enables a single processor to handle multiple tasks simultaneously, thereby improving performance.
	- Intel introduced it in 2002, becoming a standard feature in most of its processors
	(taken from www.keysight.com)
- Multithreading
	- A form of of parallelization or dividing up work for simultaneous processing. Instead of giving a large workload to a single core, threaded programs split the work into multiple software threads. These threads are processed in parallel by different CPU cores to save time. 
- Processes & Threads
	- The most significant difference between a process and a thread is that a process is defined as a task that is being completed by the computer, whereas a thread is a **lightweight** process that can be managed independently by a scheduler. 
	- Process(es)
		- A process is an active program (that is currently under execution)
		- It is more than the program code, as it includes the program counter, process stack, registers, program code etc. 
		- Compared to this, the program code is only the text section
		- When a program is triggered to execute, it does not run directly, it first determines the steps required for execution of the program
		- Following these steps of execution is referred to as a process
		- An individual process takes its own space in memory (RAM) and does not share this space with other processes 
		- Processes can be classified into two types namely - **child (clone) process** and **parent process**. 
			- Parent Process - the one responsible for creating other processes to perform multiple tasks at a time
			- Child Process - one that is created by another process (the parent)
	- Thread(s)
		- A lightweight process that can be managed independently by a scheduler. 
		- It improves the application performance using parallelism.
		- A thread shares information like the below:
			- data segment
			- code segment
			- files etc
		  With its peer threads while it contains its own:
			  - registers
			  - stack
			  - counter etc
		- A thread is basically a subpart of a large process
		- In a process, all threads within it are interrelated to each other
		- The most important feature of threads is that they share:
			- memory
			- data
			- resources etc
		  With their peer threads within a process that they belong to
		- All the threads within a process are required to be synchronised to avoid unexpected results

![](https://github.com/dshivnit/cyber-security-course/blob/main/cyber-security-course/99.99%20Images%20Used/TutorialsPointProcThrComparison.png?raw=true)

 (the above has been taken from tutorialspoint.com - https://www.tutorialspoint.com/difference-between-process-and-thread)
		  - All the threads within a process are required to be synchronised to avoid unexpected results
		  - By using threads, you can perform multiple tasks simultaneously within a single application, leading to improved performance and responsiveness. Threads are commonly used in applications that involve heavy computational tasks, network communication, and graphical user interfaces (from lenovo.com)
- 