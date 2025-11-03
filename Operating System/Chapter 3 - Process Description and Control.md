---
tags:
  - os
---
___
RELATIVE RESOURCES: [[Chapter 2 - Operating System Overview]]
**Process states** that characterise the behaviour of processes.
**Data structures** used to manage processes.
___
# Process Representation and Control
## Requirements of OS
- **Fundamental Task: Process Management** - Interleaving

![[Multiprogramming.png]]

The OS must:
- **Interleave** the execution of multiple processes: maximise the CPU power
- Allocate resources to processes (the process is always greedy), and protect the resources of each process from other processes. ⇒ Optimise resources (too many resources in a specific process waste resources) and the time
- Enable Processes to share and exchange information.
- Enable synchronisation among processes
## The OS manages the Execution of Applications
 - Resources are made available to multiple applications.
- The processor is switched among multiple applications.
- The processor and I/O devices can be used efficiently.
## What is a Process? ([[Chapter 2 - Operating System Overview]])
## Process Elements
- A process is comprised of:
    - Program code (possibly shared)
	- Set of data: defined in the code: declare the variables (fixed-size data), or a static array
	- Number of attributes describing the state of the process
- While the process is running, it has several elements, including:
	- ID (identifier): can be reused (1→ 1000: system) (10000→ : user)
		- Example: HTTP process: ID + port
	- State: Let OS know it's running, ...
	- Priority: Know the priority 
	- PC
	- Memory Pointers
	- Context data
	- IO status information
	- Accounting information
## Process Control Block (PCB)
> **Always load to the main memory - first steps need to do**
- Contains the process elements
- Create and manage by OS
- Allows support for multiple processes
## Trace of the Process
- The behavior of an individual process is shown by listing the sequence of instructions that are executed. This list is called a **Trace**.
- **Dispatcher**: A small program that switches the processor from one process to another.
___
# Process States

## Two-States Process Model
![[Two-state Process Model.png]]
- A process may be in one of two states:
    - **Running**
    - **Not-running**
- Ex: When you double-click to run the app: The app will go to the state Not-running state (check the resources that are enough to run - if not, stop immediately).
## Queuing Diagram
![[Queue Diagram.png]]
When you click the app, the app will go into the ready queue, and wait to be processor execute
## Process Birth and Death

| **Reasons for Process Creation**       | **Reasons for Process Termination** |
| ---------------------------------- | ------------------------------- |
| New batch job                      | Normal Completion               |
| Interactive Login                  | Memory unavailable              |
| Created by OS to provide a service | Protection error                |
| Spawned by an existing process     | Operator or OS Intervention     |
## Process Creation
- The OS builds a data structure to manage the process
- Traditionally, the OS created all processes: But it can be useful to let a running process create another
- This action is called **process spawning**
	- **Parent Process** is the original, creating process
	- **Child Process** is the new process
	- Parents can keep connected with the child to synchronise. If the OS kill the parent, the child becomes an **orphan process**
	- **Zombie Process**: Cannot delete data, or the process does not clean up all the data.
## Process Termination
- There must be some way that a process can indicate completion. 
- This indication may be:
	- A HALT instruction generating an interrupt alert to the OS. 
	- A user action (e.g. log off, quitting an application)
	- A fault or error 
	- Parent process terminating
## Five-State model

![[Five-State Process Model.png]]
- **New**: The process is being created.
- **Ready**: The process is waiting to be assigned to a processor.
- **Running**: Instructions are being executed.
- **Blocked**: The process is waiting for some event to occur.
- **Exit**: The process has finished execution.
## Using Two Queues
![[Two Queues.png]]
![[Multiple Blocked Queue.png]]
## Suspended Process
- The processor is faster than the I/O, so all processes could be waiting for I/O
	- *Swap these processes to disk to free up more memory and use the processor on more processes.*
- The blocked state becomes the **suspended state** when swapped to disk
- Two new states
	- **Blocked/Suspend**: wait in the secondary memory to get data
	- **Ready/Suspend**: finish and still in the secondary memory
![[Suspended Process.png]]
- New → Ready Suspend: The User wants to run the program, the OS tries to run that. All the conditions are satisfied, but it does not have enough main memory. It will run it in the Virtual Memory, the OS believes that the RAM will be free up soon
- Ready → Ready Suspend: New process is a higher priority than the queue process
- Running → Ready Suspend: Process consumes a part of memory. When the CPU processes, it may split the process into two different parts and put them in different types of memory. Maybe the process in the fast memory requests the data in the slow memory, to the CPU kicks it out to the Ready Suspended.
## Reason For Process Suspension

| **Reason**               | **Comment**                                                                                                                                                      |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Swapping**                 | The OS needs to release sufficient main memory to bring in a process that is ready to execute.                                                                   |
| **Other OS Reason**          | OS suspects process of causing a problem.                                                                                                                        |
| **Interactive User Request** | e.g., debugging or in connection with the use of a resource.                                                                                                     |
| **Timing**                   | A process may be executed periodically (e.g., an accounting or system monitoring process) and may be suspended while waiting for the next time.                  |
| **Parent Process Request**   | A parent process may wish to suspend execution of a descendent to examine or modify the suspended process, or to coordinate the activity of various descendants. |
___
# Data Structures
## OS Control Structures
- For the OS to manage processes and resources, it must have information about the current status of each process and resource.
- Tables are constructed for each entity, and the operating system manages
	- **Memory Tables**: Track main and secondary memory.
    - **I/O Tables**: Manage I/O devices and channels.
    - **File Tables**: Information about files.
    - **Process Tables**: Manage processes. 
### Memory Tables
Memory tables are used to keep track of both main and secondary memory.
Must include this information:
- Allocation of main memory to processes
- Allocation of secondary memory to processes
- Protection attributes for access to shared memory regions
- Information needed to manage virtual memory
### I/O Tables
Used by the OS to manage the I/O devices and channels of the computer. The OS needs to know
- Whether the I/O device is available or assigned
- The status of the I/O operation
- The location in the main memory is being used as the source or destination of the I/O transfer
### File Tables
These tables provide information about:
- Existence of files
- Location on secondary memory
- Current Status
- other attributes.
Sometimes this information is maintained by a file management system
### Process Table
To manage processes, the OS needs to know details of the processes
- Current state
- Process ID
- Location in memory
- etc
Process control block: **Process image** is the collection of programs: Data, stack, and attributes
#### Process Control Block (PCB)
- The most important data structure in an OS.
- Contains all process elements and attributes.
- Defines the state of the OS.
- Requires protection, as a fault could destroy the OS's ability to manage the process.
- **Process Image**: The collection of program, data, stack, and attributes.
##### Information in a PCB
- **Process Identification**: Unique numeric ID, user IDs, etc.
- **Processor State Information**: Contents of processor registers (user-visible, control/status, stack pointers), PSW.
- **Process Control Information**: Scheduling info, memory management, resource ownership, etc.
###### Process identification
Each process is assigned a *unique numeric identifier.*
Many of the other tables controlled by the OS may use process identifiers to cross-reference process tables.
###### Processor State Information
This consists of the contents of the processor registers.
- User-visible registers
- Control and status registers
- Stack pointers
Program status word (PSW):
- contains status information
- Example: the EFLAGS register on Pentium processors
###### Process control information
 This is the additional information needed by the OS to control and coordinate the various active processes.
##### Roles of PCB
The *most important data structure in an OS*: 
- It defines the state of the OS
- OS is always protected PCB; if it is broken, the program becomes unstable.
Process Control Block requires protection:
- A faulty routine could cause damage to the block, destroying the OS’s ability to manage the process.
- Any design change to the block could affect many modules of the OS
---
# Ways in which the OS uses these data structures to control process execution
## Modes of Execution
- Most processors support at least two modes of execution:
- **User mode**: Less-privileged. User programs execute here.
	-  Normal code, such as $2+2=4$
- **System mode**: More-privileged. The kernel of the OS executes here.
	- Ex: Create a new process, the malloc() function, and use the computer resources
## Process Creation
- When the OS decides to create a new process (e.g., via `fork()`):
    1.  Assigns a *unique process identifier*: sometimes the ID can be reused
    2.  Allocates space for the process.
    3.  Initializes the process control block.
    4.  Sets up appropriate linkages (e.g., to parent process, address, stack, instruction)
    5.  Creates or expands other data structures:  I/O, File table.
## Switching Processes
Several design issues are raised regarding process switching
- What events trigger a process switch? The dispatcher and “time interrupt” do this 
- We must distinguish between mode switching and process switching.
- What must the OS do to the various data structures under its control to achieve a process switch?
>  A process switch may occur any time the OS has gained control from the currently running process. Possible events include:

| Mechanism           | Cause            | Use                                         |
| :------------------ | :--------------- | :------------------------------------------ |
| **Interrupt**       | External event   | Reaction to an asynchronous external event  |
| **Trap**            | Error/exception  | Handling of an error or exception condition |
| **Supervisor Call** | Explicit request | Call to an operating system function        |

## Change of the process state
- The steps in a process switch are:
	1. Save the context of the processor (program counter, registers).
	2. Update the PCB that is currently in the Running state.
	3. Move the PCB to the appropriate queue (ready, blocked, eady/suspend, .etc.).
	4. Select another process for execution.
    5. Update the PCB of the selected process.
    6. Update memory-management data structures.
    7. Restore the context of the selected process.
## Is the OS a Process?
- **Non-process Kernel**: The kernel executes outside of any process. OS code is executed as a separate entity in privileged mode.
- **Execution Within User Processes**: The OS executes software within the context of a user process.
- **Process-based Operating System**: The OS is implemented as a collection of system processes.
- If the OS is just a collection of programs and if it is executed by the processor just like any other program, is the OS a process? Yes, it is a special program which controls other programs. The OS have two parts: Kernels and Services
- If so, how is it controlled? Who (what) controls it? Kernel, Services, and Process Switching
### Non-Processor Kernel
- Execute kernel outside of any process 
- The concept of process is considered to apply only to user programs. Operating system code is executed as a separate entity that operates in privileged mode
### Execution within User Process
- Operating system software within context of a user process 
- No need for Process Switch to run OS routine
### Process-based operating system 
- Implement the OS as a collection of system process
## Security Issue
- An OS associates a set of privileges with each process (e.g., administrator/root).
- A key security issue is to prevent unauthorized privilege escalation.
- **System Access Threats**: Intruders (Masquerader, Misfeasor, Clandestine user) and Malicious software.
## System access threats
- Intruders
	- Masquerader (outsider)
	- Misfeasor (insider)
	- Clandestine user (outside or insider)
- Malicious software (malware)
### Countermeasures: Intrusion Detection
- Intrusion detection systems are typically designed to detect human intruders and malicious software behaviour.
- May be host or network-based
- Intrusion detection systems (IDS) typically comprise
	- Sensors
	- Analyzers
	- User Interface
### Countermeasures: Authentication
- Two Stages:
	- Identification
	- Verification
- Four Factors:
	- Something the individual **knows**
	- Something the individual **possesses**
	- Something the individual is **(static biometrics)**
	- Something the individual does **(dynamic biometrics)**
### Countermeasures: Access Control
- A policy governing access to resources
- A security administrator maintains an authorisation database
	- The access control function consults this to determine whether to grant access.
- An auditing function monitors and keeps a record of user accesses to system resources.
### Countermeasures: Firewalls
- Traditionally, a firewall is a dedicated computer that:
	- interfaces with computers outside a network
	- has special security precautions built into it to
	- Protect sensitive files on computers within the network.


