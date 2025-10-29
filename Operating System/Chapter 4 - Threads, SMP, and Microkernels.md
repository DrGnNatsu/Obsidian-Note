---
tags:
  - os
---
---
# Threads: Resource ownership and execution
## Processes and Threads
**Processes** have two characteristics are treated independently by the OS:
- **Resource ownership:** unit of resource ownership: a **process**/**task**
	- **Characteristics**: A process owns the resources necessary for the application to run.
	- **Components**: Associated elements include the virtual address space (holding the process image, data, code, and attributes defined in the PCB), memory containing code and data, open files, devices, and I/O channels
- **Scheduling/execution:** Follow an execution path (the flow of the code - instruction in the codebase) that may be interleaved with other processes.

**The Thread (Unit of Execution and Dispatching)**: This is the fundamental unit that is actually scheduled and dispatched by the OS (**lightweight process**)
- **Characteristics**: A thread is an independent path of execution within a process.
- **Components**: Associated elements include a thread execution state (Running, Ready, Blocked), an execution stack, and a saved thread context when it is not running (containing the program counter and stack pointer)
## Multithreading
The ability of an OS to support multiple, concurrent paths of execution within a single process.
- **Single Thread Approaches**: MS-DOS supports a single process with a single thread. Some UNIX versions support multiple processes but only one thread per process.
- **Multiple Threads per Process**: Found in Java run-time environments, Windows, Solaris, and modern UNIX versions. 
	- Advantages: Lower Overhead, Efficient Communication:

![[Processes and Threads.png]]

## Processes ([[Chapter 2 - Operating System Overview]])
- A virtual address space that holds the process image
- Protected access to 
	- Processors
	- Other processes
	- Files
	- I/O resources
## Once or More Threads in Process
Each thread typically has:
- An execution state (running, ready, blocked, etc.)
- Saved thread context when not running
- An execution stack (process stack, including the user stack, stores dynamic state, and the system stack is allocated by the OS)
- Some per-thread static storage for local variables
- **Shared Access**: Access to the memory and resources of its process (all threads of a process share this

> A way to view a thread is as an independent program counter OS a process.
## Threads vs. Processes
![[Single Vs. Multi.png]]

- **Single-Threaded Process Model**: One Control Block managing one thread/execution path.
- **Multithreaded Process Model**: One Process Control Block, but multiple Thread Control Blocks manage parallel execution paths within the shared address space. These threads know each other by using the shared User Address Space.
### Benefits of Threads
- Takes less time to create a new thread than a process. Creating the process takes many states; the thread is easier.
- Less time to terminate a thread than to terminate a process. The process takes the resource by the OS, and the thread takes the resource by using the shared resource inside the process.
- Switching between two threads takes less time than switching processes.
- Threads can communicate with each other without invoking the kernel.
## Thread Use in a Single-User System
- Foreground and background work
- Asynchronous processing
- Speed of execution
- Modular program structure
- Remote procedure calls
Example: The web server opens port 80 to listen to the client. If the client connects to the server, the server blocks the port and creates a thread to handle that client. The server can create as many threads as it can handle, as many as clients. 
## Threads
Several actions that affect all of the threads in a process
- The OS must manage these at the process level
Examples:
- Suspending a process involves suspending all threads of the process.
- Termination of a process terminates all threads within the process.
## Activities Similar to Processes
- Threads have execution states, and many synchronize with one another.
- We look at these 2 aspects of thread functionality in turn.
	- States
	- Synchronization
## Thread Execution States

| State Change Activity | Description                                                  |
| :-------------------- | :----------------------------------------------------------- |
| **Spawn**             | Creates another thread.                                      |
| **Block**             | An issue will block a thread block other, or *all*, threads. |
| **Unblock**           |                                                              |
| **Finish (thread)**   | Deallocate register context and stacks.                      |
## Example: Remote Procedure Call
Consider:
- A program that performs 2 remote procedure calls (RPCs)
- to two different hosts
- To obtain a combined result.
## RPC Using a Single Thread
![[RPC Single Thread.png]]
## RPC Using One Thread per Server 
![[RPC Multithread.png]]
## Multithreading on a Uniprocessor

## Categories of Thread Implementation
- User Level Thread (ULT): managed by the app itself through a **threads library** in user space
- Kernel Level Thread (KLT), also called.
	- Kernel-supported threads
	- Lightweight processes
### User-Level Threads
- **Management:** The kernel (OS) is unaware of the existence of the threads within the process. The library contains the code for creating, destroying, scheduling, and saving/restoring thread contexts
## Relationships Between ULT Thread and Process States
![[Relationships Between ULT Thread and Process States.png]]
The picture describes the relationship between process B and the two self-threads 1, 2.  The thread can change the state when process B is running. Other state of the process B, it freezes the state of the Threads.
### Kernel-Level Threads
- KLTs are threads maintained and managed directly by the OS kernel.
	- **Management:** The kernel is aware of and maintains the context for every thread. No thread management done by application.
		- Scheduling is done on a thread basis
	- **Efficiency:** Switching between KLTs requires a **mode switch** to the kernel, making the switch slower than a ULT switch.
	- **Concurrency:** KLTs allow multiple threads from the same process to execute simultaneously (in parallel) on a multiprocessor or multicore system
	- Windows is an example of this approach
#### Advantages of KLT
- The kernel can simultaneously schedule multiple threads from the same process on multiple processors.
- If one KLT blocks, the kernel can simply schedule another ready thread (from the same process or a different one) for execution. The entire process is **not blocked**
- Kernel routines themselves can be multithreaded.
#### Disadvantages of KLT
The transfer of control from one thread to another within the same process requires a mode switch to the kernel.
## Combined Approaches
- Thread creation is done in the user space.
- The bulk of scheduling and synchronization of threads by the application 
- An example is Solaris.
## Relationship Between Threads and Processes

| Thread/Process Ratio | Description                                                                                                                                                                                            |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **1:1**              | Each thread of execution is a unique process with its own address space and resources. Traditional UNIX implementations                                                                                |
| **M:1**              | A process defines an address space and dynamic resource ownership. Multiple threads may be created and executed within that process (managed by a UTL). Windows NT, Solaris, Linux, OS/2, OS/390, MACH |
| **1:M**              | A thread may migrate from one process environment to another. This allows a thread to be easily moved among distinct systems.                                                                          |
| **M:N**              | Combines attributes of M:1 and 1:M cases. Ra (Clouds), Emerald, TRIX                                                                                                                                   |

___
# Symmetric Multiprocessing (SMP)
## Traditional View
Traditionally, the computer has been viewed as a sequential machine. 
- A processor executes instructions one at a time in sequence.
- Each instruction is a sequence of operations
Two popular approaches to providing parallelism 
- Symmetric MultiProcessors (SMPs)
- Clusters 
## Categories of Computer Systems
- **Single Instruction Single Data (SISD)**: Single processor executes one instruction stream on data in single memory.
- **Single Instruction Multiple Data (SIMD)**: Each instruction executes on a different set of data by different processors. (See Parallel Processor Architectures diagram on page 6).
- **Multiple Instruction Single Data (MISD)**: Sequence of data transmitted to processors, each executing a different instruction sequence (Never implemented).
- **Multiple Instruction Multiple Data (MIMD)**: Processors simultaneously execute different instruction sequences on different data sets.
## Parallel Processor Architectures
Cluster: Many supercomputers are using the visualization methods to create many VPS
- **SIMD**: Master/Slave or Symmetric Multiprocessing (SMP).
- **MIMD**: Shared-Memory (tightly coupled) or Distributed-Memory (loosely coupled).
## Symmetric Multiprocessing
- Kernel can execute on any processor: Allowing portions of the kernel to execute in parallel
- Typically, each processor does self-scheduling from the pool of available processes or threads
## Typical SMP Organization

## Multiprocessor OS Design Considerations
The key design issues include
- Simultaneous concurrent processes or threads
- Scheduling
- Synchronization
- Memory Management
- Reliability and Fault Tolerance
___
# Microkernel

## Multiprocessor OS Design Considerations
Key design issues include:
- Simultaneous concurrent processes or threads.
- Scheduling.
- Synchronization.
- Memory Management.
- Reliability and Fault Tolerance.
## Microkernel
- A microkernel is a small OS core that provides the foundation for modular extensions.
- Key theoretical questions involve how small the kernel must be and whether drivers must reside in user space.
- Big question is how small must a kernel be to qualify as a microkernel – Must drivers be in user space?
- In theory, this approach provides a high degree of flexibility and modularity. 
### Kernel Architecture 
#### Microkernel Design: Memory Management
- Low-level memory management: Mapping each virtual page to a physical page frame.
- Most memory management tasks occur in **user space**..
#### Microkernel Design: Interprocess Communication (IPC)
- Communication between processes or threads in a microkernel OS is via **messages**.
- A message includes: 
	- A header identifying sender/receiver.
	- A body containing data, a pointer to data, or control information.
#### Microkernel Design: I/O and interrupt management 
Within a microkernel, it is possible to handle hardware interrupts as messages and to include I/O ports in address spaces. 
	*A particular user-level process is assigned to the interrupt, and the kernel maintains the mapping.* 
### Benefits of a Microkernel Organization
- Uniform interfaces on requests made by a process.
- Extensibility, Flexibility, Portability, Reliability.
- Distributed System Support.
- Object Oriented Operating Systems.
---
# Different Approaches to Processes 
Differences between different OS’s support of processes include
- How processes are named
- Whether threads are provided
- How processes are represented
- How process resources are protected
- What mechanisms are used for inter-process communication and synchronization
- How processes are related to each other 
## Windows Processes
Processes and services provided by the Windows Kernel are relatively simple and general-purpose
- Implemented as objects
- An executable process may contain one or more threads
- Both processes and thread objects have built-in synchronization capabilities 

## Relationship between Process and Resources
## Windows Process Object
## Windows Thread Object

## Thread States

## Solaris
Solaris implements multilevel thread support designed to provide flexibility in exploiting processor resources.  
- Processes include the user’s address space, stack, and process control block  
## Solaris Process
Solaris makes use of four separate thread-related concepts:  
- **Process**: includes the user’s address space, stack, and process control block.  
- **User-level threads**: a user-created unit of execution within a process.  
- **Lightweight processes (LWPs)**: a mapping between ULTs and kernel threads.  
- **Kernel threads**  
## Relationship between Processes and Threads
## Traditional Unix vs Solaris
## LWP Data Structure
- An LWP identifier  
- The priority of this LWP  
- A signal mask  
- Saved values of user-level registers  
- The kernel stack for this LWP  
- Resource usage and profiling data  
- Pointer to the corresponding kernel thread  
- Pointer to the process structure  
## Solaris Thread States
## Linux Tasks
A process, or task, in Linux is represented by a `task_struct` data structure.  
- This contains several categories, including:  
  - State  
  - Scheduling information  
  - Identifiers  
  - Interprocess communication  
  - And others  
## Linux Process/Thread Model

