#os 
___
RELATIVE RESOURCES: [[Chapter 2 - Operating System Overview]]
**Process states** that characterise the behaviour of processes.
**Data structures** used to manage processes.
# Requirements of OS
___
Fundamental Task: Process Management - Interleaving
![[Multiprogramming.png]]
The OS must:
- **Interleaving** the execution of multiple processes: maximise the CPU power
- Allocate resources to processes (the process is always greedy), and protect the resources of each process from other processes.
⇒ Optimise resources (too many resources in a specific process waste resources), Optimise the time
- Enable Processes to share and exchange information.
- Enable synchronisation among processes
## The OS manages the Execution of Applications
___
The resources are made available to multiple applications.
The processor is switched among multiple applications.
The Processor and IO devices can be used efficiently.
### Process
Consists of three components:
- Program code
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
### Process Control Block (PCB)
**Always load to the main memory - first steps need to do**
Contains the process elements
Create and manage by OS
Allows support for multiple processes
### Trace of the Process
The behavior of an individual process is shown by listing the sequence of instructions that are executed, called a **trace**.
**Dispatcher** is a small program which switches the processor from one process to another
# Process States
___
## Two-States Process Model
![[Two-state Process Model.png]]
- When you double-click to run the app:
	- The app will go to the state Not-running state (check the resources that are enough to run - if not, stop immediately).
## Queuing Diagram
![[Queue Diagram.png]]
When you click the app, the app will go into the ready queue, and wait to be processor execute
## Process Birth and Death

## Process Creation
The OS builds a data structure to manage the process
- Traditionally, the OS created all processes
	- But it can be useful to let a running process create another
- This action is called **process spawning**
	- **Parent Process** is the original, creating process
	- **Child Process** is the new process
	- Parents can keep connected with the child to synchronise. If the OS kill the parent, the child becomes an **orphan process**
	- **Zombie Process**: Cannot delete data, or the process does not clean up all the data.
## Process Termination
## Five-State model

![[Five-State Process Model.png]]
New: the App waits to check
Ready: Check finish and satisfaction, and wait to process
Running: The Processor processes it
Blocked: The app needs to wait for the disk, and I/O to get the data
## Using Two Queues
![[Two Queues.png]]
![[Multiple Blocked Queue.png]]
## Suspended Process
- The processor is faster than the I/O, so all processes could be waiting for I/O
	- *Swap these processes to disk to free up more memory and use the processor on more processes.*
	- 
- The blocked state becomes the **suspended state** when swapped to disk
- Two new states
	- Blocked/Suspend: wait in the secondary memory to get data
	- Ready/Suspend: finish and still in the secondary memory
![[Suspended Process.png]]
- New → Ready Suspend: The User wants to run the program, the OS tries to run that. All the conditions are satisfied, but it does not have enough main memory. It will run it in the Virtual Memory, the OS believes that the RAM will be free up soon
- Ready → Ready Suspend: New process is a higher priority than the queue process
- Running → Ready Suspend: Process consumes a part of memory. When the CPU processes, it may split the process into two different parts and put them in different types of memory. Maybe the process in the fast memory requests the data in the slow memory, to the CPU kicks it out to the Ready Suspended.
## Reason For Process Suspension
# Data Structures
___
## Processes and Resources
## OS Control Structures
- For the OS to manage processes and resources, it must have information about the current status of each process and resource.
- Tables are constructed for each entity, and the operating system manages
## Memory Tables
Memory tables are used to keep track of both main and secondary memory.
Must include this information:
- Allocation of main memory to processes
- Allocation of secondary memory to processes
- Protection attributes for access to shared memory regions
- Information needed to manage virtual memory
## I/O Tables
Used by the OS to manage the I/O devices and channels of the computer.
The OS needs to know
- Whether the I/O device is available or assigned
- The status of the I/O operation
- The location in the main memory is being used as the source or destination of the I/O transfer
## File Tables
These tables provide information about:
- Existence of files
- Location on secondary memory
- Current Status
- other attributes.
Sometimes this information is maintained by a file management system
## Process Table
To manage processes, the OS needs to know details of the processes
- Current state
- Process ID
- Location in memory
- etc
Process control block: **Process image** is the collection of programs: Data, stack, and attributes
## Process Attributes
We can group the process control block information into three general categories:
- Process identification
- Processor state information
- Process control information
### Process identification
Each process is assigned a *unique numeric identifier.*
Many of the other tables controlled by the OS may use process identifiers to cross-reference process tables.
### Processor State Information
This consists of the contents of the processor registers.
- User-visible registers
- Control and status registers
- Stack pointers
Program status word (PSW):
- contains status information
- Example: the EFLAGS register on Pentium processors
### Process control information
 This is the additional information needed by the OS to control nd coordinate the various active processes.

## Roles of PCB
The *most important data structure in an OS*: 
- It defines the state of the OS
- OS is always protected PCB; if it is broken, the program becomes unstable.
Process Control Block requires protection:
- A faulty routine could cause damage to the block, destroying the OS’s ability to manage the process.
- Any design change to the block could affect many modules of the OS
# Ways in which the OS uses these data structures to control process execution
## Modes of Execution
- Most processors support at least two modes of execution:
- User mode
	- Less-privileged mode
	- User programs typically execute in this mode 
	- Normal code, such as $2+2=4$
- System mode:
	- More-privileged mode
	- Kernel of the operating system
	- Ex: Create a new process, the malloc() function, and use the computer resources
## Process Creation
Once the OS decides to create a new process, it:
- Assigns a *unique process identifier*: sometimes the ID can be reused
- Allocates space for the process
- Initialises process control block
- Sets up appropriate linkages: link can be the address, stack, instruction
- Creates or expands other data structures: I/O, File table.
## Switching Processes
Several design issues are raised regarding process switching
- What events trigger a process switch? The dispatcher and “time interrupt” do this 
- We must distinguish between mode switching and process switching.
- What must the OS do to the various data structures under its control to achieve a process switch?
## Change of the process state
The steps in a process switch are:
1. Save the context of the processor, including the program counter and other registers: save two instructions (PC and instructor) in the processor.
2. Update the process control block of the process that is currently in the Running state
3. Move the process control block to the appropriate queue – ready; blocked; or ready/suspend.
4. Select another process for execution
5. Update the process control block of the process selected
6. Update memory-management data structures
7. Restore the context of the selected process
## Is the OS a Process?
- If the OS is just a collection of programs and if it is executed by the processor just like any other program, is the OS a process? Yes, it is a special program which controls other programs. The OS have two parts: Kernels and Services
- If so, how is it controlled? Who (what) controls it? Kerne, Services, and Process Switching
### Non-Processor Kernel
## Security Issue
An OS associates a set of privileges with each process.
- The highest level is administrator, supervisor, or root access.
A key security issue in the design of any OS is to prevent anything (user or process) from gaining unauthorised privileges on the system
- Especially, from gaining root access.
## System access threats
- Intruders
	- Masquerader (outsider)
	- Misfeasor (insider)
	- Clandestine user (outside or insider)
- Malicious software (malware)
## Countermeasures: Intrusion Detection
- Intrusion detection systems are typically designed to detect human intruders and malicious software behaviour.
- May be host or network-based
- Intrusion detection systems (IDS) typically comprise
	- Sensors
	- Analyzers
	- User Interface
## Countermeasures: Authentication
- Two Stages:
	- Identification
	- Verification
- Four Factors:
	- Something the individual **knows**
	- Something the individual **possesses**
	- Something the individual is **(static biometrics)**
	- Something the individual does **(dynamic biometrics)**
## Countermeasures: Access Control
- A policy governing access to resources
- A security administrator maintains an authorisation database
	- The access control function consults this to determine whether to grant access.
- An auditing function monitors and keeps a record of user accesses to system resources.
## Countermeasures: Firewalls
- Traditionally, a firewall is a dedicated computer that:
	- interfaces with computers outside a network
	- has special security precautions built into it to
	- protect sensitive files on computers within the network.


