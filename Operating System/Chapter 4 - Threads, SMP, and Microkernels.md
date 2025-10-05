#os 
___
# Threads: Resource ownership and execution
---
## Processes and Threads
Processes have two characteristics:
- **Resource ownership:** Process includes a virtual address space (memory) to hold the process image - the process image is the collection of program, data, stack, and attributes defined in the process control block.
- **Scheduling/execution:** Follow an execution path (the flow of the code - instruction in the codebase) that may be interleaved with other processes.
These two characteristics are treated independently by the operating system.
The unit of dispatching is referred to as a **thread** or a **lightweight process**. The unit of resource ownership is referred to as a **process** or **task**.
## Multithreading
The ability of an OS to support multiple, concurrent paths of execution within a single process. 
- The Java runtime environment is a single process with multiple threads.
- Multiple processes, each of which supports multiple threads, are found in Windows, Solaris, and many modern versions of UNIX.
![[Processes and Threads.png]]
## Single Thread Approaches
- MS-DOS supports a single-user process and a single thread.
- Some UNIX, support multiple user processes but only support one thread per process.
## Processes
- A virtual address space that holds the process image
- Protected access to 
	- Processors
	- Other processes
	- Files
	- I/O resources
## Once or More Threads in Process
Each thread has
- An execution state (running, ready, blocked, etc.)
- Saved thread context when not running
- An execution stack (process stack, including the user stack, stores dynamic state, and the system stack is allocated by the OS)
- Some per-thread static storage for local variables
- Access to the memory and resources of its process (All threads of a process share this)
## One View...
A way to view a thread is as an independent program counter operating system **bo sung** a process.
## Threads vs. Processes
![[Single Vs. Multi.png]]
These threads know each other by using the shared User Address Space.
## Benefits of Threads
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
The state is associated with a change in thread state.
- Spawn (another thread)
- Block
	- Issue: Will blocking a thread block other, or all threads
- Unblock
- Finish (thread)
	- Deallocate register context and stacks
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

## Adobe PageMaker

## Categories of Thread Implementation
- User Level Thread (ULT)
- Kernel Level Thread (KLT), also called.
	- Kernel-supported threads
	- Lightweight processes
## User-Level Threads
- All thread management is done by the application.
- The kernel is not aware of the existence of threads
## Relationships Between ULT Thread and Process States
![[Relationships Between ULT Thread and Process States.png]]
The picture describes the relationship between process B and the two self-threads 1, 2.  The thread can change the state when process B is running. Other state of the process B, it freezes the state of the Threads.
## Kernel-Level Threads
- Kernel maintains context information for the process and the threads (No thread management done by the application)
- Scheduling is done on a thread basis.
- Windows is an example of this approach.
## Advantages of KLT
- The kernel can simultaneously schedule multiple threads from the same process on multiple processors.
- If one thread in a process is blocked, the kernel can schedule another thread of the same process.
- Kernel routines themselves can be multithreaded.
## Disadvantages of KLT
The transfer of control from one thread to another within the same process requires a mode switch to the kernel.
## Combined Approaches
- Thread creation is done in the user space.
- The bulk of scheduling and synchronization of threads by the application 
- An example is Solaris.
## Relationship Between Threads and Processes

# Symmetric Multiprocessing (SMP)
---
## Traditional View
Traditionally, the computer has been viewed as a sequential machine. 
- A processor executes instructions one at a time in sequence.
- Each instruction is a sequence of operations
Two popular approaches to providing parallelism 
- Symmetric MultiProcessors (SMPs)
- Clusters (ch 16)
## Categories of Computer Systems
- Single Instruction Single Data (SISD) stream: A Single processor executes a single instruction stream to operate on data stored in a single memory
- Single Instruction Multiple Data (SIMD) stream: Each instruction is executed on a different set of data by different processors
- Multiple Instruction Single Data (MISD) stream (Never implemented): A sequence of data is transmitted to a set of processors, each of which executes a different instruction sequence.
- Multiple Instruction Multiple Data (MIMD): A set of processors simultaneously executes different instruction sequences on different data sets.
## Parallel Processor Architectures
Cluster:
- Many supercomputers are using the visualization methods to create many VPS
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
# Microkernel
---
## Microkernel
- A microkernel is a small OS core that provides the foundation for modular extensions.
- Big question is how small must a kernel be to qualify as a microkernel – Must drivers be in user space?
- In theory, this approach provides a high degree of flexibility and modularity. 
## Kernel Architecture 
## Microkernel Design: Memory Management
Low-level memory management - Mapping each virtual page to a physical page frame: Most memory management tasks occur in user space.
## Microkernel Design: Interprocess Communication
- Communication between processes or threads in a microkernel OS is via messages. 
- A message includes: 
	- A header that identifies the sending and receiving process and
	- A body that contains direct data, a pointer to a block of data, or some control information about the process. 
## Microkernel Design: I/O and interrupt management 
Within a microkernel, it is possible to handle hardware interrupts as messages and to include I/O ports in address spaces. 
	*A particular user-level process is assigned to the interrupt, and the kernel maintains the mapping.* 
## Benefits of a Microkernel Organization
- Uniform interfaces on requests made by a process. 
- Extensibility 
- Flexibility 
- Portability 
- Reliability 
- Distributed System Support 
- Object Oriented Operating Systems 
## Different Approaches to Processes 
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

