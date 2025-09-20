#os
# Operating System
A program that executes application programs
An interface between applications and hardware
- Convenience: makes the computer more convenient to use: plug and play
- Efficiency: allows computer system resources to be used in an efficient manner
- Ability to evolve: permits effective development, testing, and introduction of new system functions without interfering with service.
Functions the same way as other computers: it is a program that is executed.
OS relinquishes control of the processor to run other programs
Kernel - Heart of the OS
- Portion of OS that is in the main memory
- Contains the most frequently used functions
## Layer of the Computer System
Application -> Utilities -> OS -> Computer Hardware
- Utilisation (middleware): Running on different OS -> environment, library, dependencies
## Uniprogramming
- Single running process: no threads
- The processor must wait for an IO instruction to complete before proceeding.
## Multiprogramming
- Multitasking
- When one job needs to wait for I/O, the processor can switch to the other job.

## Time Sharing
Using multiprogramming to handle multiple interactive jobs (real-time applications)
 - The processor’s time is shared among multiple users.
 - Multiple user processes simultaneously access the system

## Processes
Several definitions of a process:
- **A program in execution in the main memory**
- An instance of a program *in execution*.
- The entity that can be assigned to and executed on a processor
- A unit of activity characterised by a single sequential thread of execution, a current state, and an associated set of system resources
## Process
Consists of three components:
- An executable program
- Data needed by the program: static data
- Execution context of the program: all information the OS needs to manage the process
- Context: ID, attribute
- All the processes are in the stack

## Memory Management
- Process Isolation
- Automatic allocation and management
- Support for modular programming
- Protection and access control:
	- Many programs run in the memory
- Long-term storage

## Virtual Memory
- Allows programmers to address memory from a logical point of view (extend the RAM: maximum is double the physical RAM)
- Processes move between primary and secondary memory (using the hard disk to act as the RAM)
- Paging:
	- allows the process to be comprised of several fixed-size blocks, called pages (segment the code into different modules)
	- A virtual address is a page number and an offset within the page
	- Each page may be located anywhere in main memory
	- real address or physical address in main memory
![[Virtual Memory.png]]
## Scheduling and Resource Management
Scheduling: manage the process within the time slot
Resource Management: manage the resources for the process
- Fairness: give equal and fair access to all the processes
- Differential responsive:
	- Discriminate between different classes of jobs
	- High/low Priority: more resources
	- User/System
- Efficiency: maximise throughput, minimise response time, and accommodate as many users as possible
	- Balance resources and CPU time
## System Structure
- View the system as a series of levels (App → OS → Hardware) - Slides
- Each level performs a related subset of functions
- Each level relies on the next lower level to perform more primitive functions
- This decomposes a problem into several more manageable sub-problems
## Modern OS
- Mircokernel architecture
	- as opposed to monolithic
	- assigns only a few essential functions to the kernel
		- Address space management
		- Interprocess Communication (IPC): communicate between processes, create a process
		- Basic Scheduling
- Threads: processes in divided into a plurality of concurrent threads
## UNIX
