---
tags:
  - "#os"
---
# Operating System
- A program that controls the execution of application programs.
- **OS as User/Computer Interface** The OS masks the details of the hardware from the programmer, providing a convenient interface and acting as a mediator for application programs to access facilities and services
- **OS as Resource Manager** The OS is responsible for controlling the use of a computer’s resources, including I/O, main and secondary memory, and processor execution time.
- **Goals**:
    - **Convenience**: Makes the computer more convenient to use.
    - **Efficiency**: Allows computer system resources to be used in an efficient manner.
    - **Ability to evolve**: Permits effective development, testing, and introduction of new system functions without interfering with service.
## OS Functionality
- Functions the same way as other computer software; it is a program that is executed.
- The operating system relinquishes control of the processor to run other programs.
- **Kernel**: The heart of the operating system.
    - The portion of the operating system that is in main memory.
    - Contains the most-frequently used functions.
## Layers of Computer System
Application -> Utilities -> OS -> Computer Hardware
- Utilisation (middleware): Running on different OS -> environment, library, dependencies
## Operating System Services
- **Program development**: Editors, compilers, and debuggers.
- **Program execution**: Process and thread scheduling.
- **Access to I/O devices**.
- **Access to filesystem(s)**.
- **Access to network(s)**.
- **Accounting**: Monitor performance, used for billing.
- **Error detection and response**: Handles internal and external hardware and software errors.
___
# Uniprogramming vs. Multiprogramming
## Uniprogramming
- Single running process: no threads
- The processor must wait for an IO instruction to complete before proceeding.
## Multiprogramming
- Multitasking
- When one job needs to wait for I/O, the processor can switch to the other job.
## Time Sharing
Using multiprogramming to handle multiple interactive jobs (real-time applications): slices the time into many slots to execute concurrently
 - The processor’s time is shared among multiple users.
 - Multiple user processes simultaneously access the system
> Key objective is to **minimize response time**

|                          | Batch Multiprogramming        | Time Sharing                  |
| :----------------------- | :---------------------------- | :---------------------------- |
| **Principal objective**  | Maximize processor use        | Minimize response time        |
| **Source of directives** | Job control language commands | Commands entered in real time |
___
# Processes
Several definitions of a process:
- **A program in execution in the main memory**
- An instance of a program *in execution*.
- The entity that can be assigned to and executed on a processor
- A unit of activity characterised by a single sequential thread of execution, a current state, and an associated set of system resources
Consists of three components:
1. An executable program
2. Data needed by the program: static data
3. Execution context of the program: all information the OS needs to manage the process
- Context: ID, attribute
- All the processes are in the stack
## Memory Management
- **Process isolation**: Prevent independent processes from interfering with each other.
- **Automatic allocation and management**: Dynamic allocation across the memory hierarchy.
- **Support for modular programming**.
- **Protection & access control**: Private & shared memory areas. 
- **Long-term storage** (non-volatile).
### Virtual Memory
- Allows programmers to address memory from a logical point of view (Virtual RAM: max is double the physical RAM)
- Processes move between primary and secondary memory (using the hard disk to act as the RAM)
- **Paging**:
	- Allows the process to be comprised of several fixed-size blocks, called **pages** 
		- Segment the code into different modules)
	- A virtual address is a page number and an offset within the page
	- Each page may be located anywhere in main memory
	- The real address or physical address in main memory
![[Virtual Memory.png]]
## Scheduling and Resource Management
**Scheduling**: manage the process within the time slot
**Resource Management**: manage the resources for the process
- **Fairness**: Give equal and fair access to all processes.
- **Differential responsiveness**: Discriminate between different classes of jobs
	- High/low Priority: more resources
	- User/System
- **Efficiency**: Maximize throughput, minimize response time, and accommodate as many users as possible.
	- Balance resources and CPU time
## System Structure
- View the system as a series of levels (App → OS → Hardware)
- Each level performs a related subset of functions
- Each level relies on the next lower level to perform more primitive functions
- This decomposes a problem into several more manageable sub-problems
## Operating System Design Hierarchy
H: high level, I: intermediate level, L: low level

| Level | Objects                                     | Level | Objects                                    |
| ----- | ------------------------------------------- | ----- | ------------------------------------------ |
| 6I    | Blocks of data, device channels             | 13H   | User programming environment               |
| 5I    | Primitive process, semaphores, ready list   | 12H   | User processes                             |
| 4L    | Interrupt-handling programs                 | 11H   | Directories                                |
| 3L    | Procedures, call stack, display             | 10H   | External devices (printer, displays, etc.) |
| 2L    | Evaluation stack, micro-program interpreter | 9H    | Files                                      |
| 1L    | Registers, gates, buses, etc.               | 8H    | Pipes                                      |
|       |                                             | 7I    | Segments, pages                            |
# Modern OS
## Modern Operating Systems
- **Symmetric multiprocessing (SMP)**: More than one processor, all processors are equal and share memory/I/O.
- **Distributed operating systems**: Provides the illusion of a single memory system across multiple machines.
- **Object-oriented design**: For adding modular extensions to a small kernel.
### Mircokernel architecture
- As opposed to a monolithic kernel, it assigns only a few essential functions to the kernel:
	- Address space management.
	- Interprocess Communication (IPC): communicate between processes, create a process
	- Basic Scheduling
-  **Threads**: A process is divided into a plurality of concurrent threads.
___
# UNIX
- Hardware is surrounded by the operating-system kernel.
- Comes with user services and interfaces (C compiler, shell, etc.).
- **Modern Unices**: System V (SVR4), BSD, Solaris, Linux, macOS.