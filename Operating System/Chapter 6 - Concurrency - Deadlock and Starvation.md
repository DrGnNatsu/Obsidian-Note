---
tags:
  - "#os"
---
# Principles of Deadlock
---
## Deadlock
- A set of processes is **deadlocked** when each process in the set is blocked, awaiting an event that can only be triggered by another blocked process in the set. (*permanently blocked*)
- Typically involves processes competing for the same set of resources.
- There is **no efficient solution** to this problem.

> **Real-world analogy**: A four-way intersection where four cars arrive at the same time. Each car waits for the car on its right to proceed. No one can move. This is a deadlock.
> ![[Deadlock.png]]

**Example of Deadlock:**
![[Deadlock Example.png]]
**Deadlock-inevitable region** (**fatal region**): If paths of both P and Q go to this region, deadlock is definitely guaranteed. The reason is that at this moment, P has successfully gotten A and is ready to get B. Q has successfully gotten B and is ready to get A. (*P is going to ask for B to continue running, but Q is holding it. In addition, Q requires A, but at this time, it belongs to P*) 
-> Then, deadlock will happen since none of them can continue running.

**Example of no deadlock**
![[Example No Deadlock.png]]
## Resource Categories
Two general categories of resources:
- **Reusable Resources**: Can be used by only one process at a time and are not depleted by use. Examples include processors, memory, files, databases, and semaphores.
	- Deadlock occurs if each process holds one reusable resource and requests another. If the execution of 2 processes is $p_0,p_1,q_0,q_1,p_2,q_2$ -> deadlock occurs.
	  ![[Example of Two Processes Competing for Reusable Resources.png]]
	- Another example of deadlock with a reusable resource has to do with requests for main memory. Suppose the space available for allocation is 200 Kbytes, and the following sequence of requests occurs.
	  ![[Example of Two Processes Competing for Reusable Resources 2.png]]
- **Consumable Resources**: Can be created (produced) and destroyed (consumed). Examples include interrupts, signals, and messages. Typically, there is no limit on the number of consumable resources of a particular type.
	- Deadlock can occur if a `Receive` message is blocking and processes are waiting for messages from each other.
	  ![[Example of Two Processes Competing for Consumable Resources.png]]
## Resource Allocation Graphs
A directed graph that depicts a state of the system of resources and processes. 
![[Pasted image 20251010153150.png]]
Within a resource node, a dot is shown for each instance of that resource.

---
### Resource Allocation Graphs of Deadlock
![[Examples of Resource Allocation Graphs.png]]
- Figure (c): There is only one unit each of resources Ra and Rb. Process P1 holds Rb and requests Ra, while P2 holds Ra but requests Rb.
- Figure (d): Has the same topology, but there is no deadlock because multiple units of each resource are available.

Back to the example of 4 cars, here is the resource allocation graph for the deadlock case.
## Conditions for Possible Deadlock
For a deadlock to occur, four conditions must be met simultaneously:
1. **Mutual Exclusion**: Only one process may use a resource at a time.
2. **Hold-and-Wait**: A process may hold allocated resources while awaiting the assignment of others.
3. **No Preemption**: No resource can be forcibly removed from a process holding it. (no Priority) - No process force to get out of the queue.
4. **Circular Wait**: A closed chain of processes exists, such that each process holds at least one resource needed by the next process in the chain. (100 % has a deadlock).
## Dealing with Deadlock
There are three general approaches for dealing with deadlock:
1.  **Deadlock Prevention**: Design a system in such a way that the possibility of deadlock is excluded by negating one of the four necessary conditions.
2.  **Deadlock Avoidance**: Make a dynamic decision on whether the current resource allocation request will, if granted, potentially lead to a deadlock.
3.  **Deadlock Detection**: Grant resource requests whenever possible and periodically check for the presence of deadlock. If detected, perform recovery.
___
# Deadlock Prevention
---
## Deadlock Prevention Strategy
- **Indirect method**: Prevent one of the first three conditions at the same time (Mutual Exclusion, Hold-and-Wait, No Preemption).
- **Direct method**: Prevent the Circular Wait condition.
- **Attacking Mutual Exclusion**: Generally not possible, as some resources are inherently non-shareable. (Remove multitasking)
- **Attacking Hold-and-Wait**: Require a process to request all of its required resources at one time. This is inefficient as it may hold resources for a long time without using them. (Some processes need many different resources)
- **Attacking No Preemption**: If a process holding resources is denied a further request, it must release its original resources. 
- **Attacking Circular Wait**: Define a linear ordering of resource types. A process can only request resources in an increasing order of enumeration.

---
# Deadlock Avoidance
---
## Deadlock Avoidance Strategy
- A decision is made dynamically whether the current resource allocation request will, if granted, potentially lead to a deadlock. (simulation, if the OS grants the resources to the process, check if the system has a deadlock or not)
- This requires knowledge of future process resource requests.
- Two main approaches:
	- **Process Initiation Denial - New Process**: Do not start a process if its demands might lead to deadlock.
	- **Resource Allocation Denial - Existing Process (Banker's Algorithm)**: Do not grant an incremental resource request to a process if this allocation might lead to an unsafe state.
---
## Process Initiation Denial
A process is only started if the maximum claim of all current processes plus those of the new process, can be met. 

Consider a system of $n$ processes and $m$ different types of resources. Let us define the following vectors and matrices:
![[Process Initiation Denial.png]]
The matrix **Claim (C)** gives the maximum requirement of each process for each resource. The matrix **Allocation (A)** gives the current allocation to each process. The following relationships hold:
1.  $R_j = V_j + \sum_{i=1}^{n} A_{ij}$, for all j
    *   All resources are either available (V) or allocated (A).
2.  $C_{ij} \le R_j$, for all i, j
    *   No process can claim more than the total amount of resources in the system.
3.  $A_{ij} \le C_{ij}$, for all i, j
    *   No process is allocated more resources of any type than the process originally claimed to need.
With these quantities defined, we can define a deadlock avoidance policy. A new process $P_{n+1}$ is started only if:
$$R_j \ge C_{(n+1)j} + \sum_{i=1}^{n} C_{ij}, \quad \text{for all } j$$
That is, a process is only started if the maximum claim of all current processes plus the maximum claim of the new process can be met. This strategy is hardly optimal because it assumes the worst-case scenario: that all processes will make their maximum claims simultaneously.
Assumes the worst: that all processes will make their maximum claims together -> Not optimal.

---
## Banker's Algorithm (Resource Allocation Denial)
- State of the system is the current allocation of resources to process
- A state is **safe** if there is at least one sequence of process executions that allows all processes to run to completion.
- A state is **unsafe** if no such sequence exists. An unsafe state is not a deadlock, but it *may* lead to one.
- The Banker's Algorithm ensures the system never enters an unsafe state. When a request is made, the system pretends to grant it, then checks if the resulting state is safe. If it is, the request is granted; otherwise, the process must wait.

**Example:** The total amount of resources R1, R2, and R3 are 9, 3, and 6 units, respectively. In the current state allocations have been made to the four processes, leaving 1 unit of R2 and 1 unit of R3 available. Is this a safe state?
![[Banker's Algorithm.png]]

| Ký hiệu   | Tên bảng          | Ý nghĩa                                                     |
| --------- | ----------------- | ----------------------------------------------------------- |
| **C**     | Claim matrix      | Mức tài nguyên **tối đa** mà mỗi tiến trình có thể yêu cầu. |
| **A**     | Allocation matrix | Lượng tài nguyên **đang được cấp phát** cho mỗi tiến trình. |
| **C − A** | Need matrix       | Lượng tài nguyên **còn cần thêm** để tiến trình hoàn tất.   |
| **R**     | Resource vector   | Tổng số lượng tài nguyên hiện có trong hệ thống.            |
| **V**     | Available vector  | Số tài nguyên **hiện còn khả dụng** (chưa cấp phát cho ai). |
To answer this question, we ask an intermediate question: Can any of the four processes be run to completion with the resources available? That is, can the difference between the maximum requirement and current allocation for any process be met with the available resources? In terms of the matrices and vectors, the condition to be met for process i is:
$$C_{ij}-A_{ij}\leq V_j,\quad \text{for all j}$$
- This is not possible for P1, which has only 1 unit of R1 and requires 2 more units of R1, 2 units of R2, and 2 units of R3.
- However, if we assign one unit of R3 to process P2, then P2 has its maximum required resources allocated and can run to completion and return resources to ‘available’ pool

Can any of the remaining processes can be completed? **Note that P2 is completed**.
![[Banker's Algorithm 2.png]]
- Suppose we choose P1, allocate the required resources, complete P1, and return all of P1’s resources to the available pool.

**After P1 completed**
![[Banker's Algorithm 3.png]]
- Next, we can complete P3

**P3 completed**
![[Banker's Algorithm 4.png]]
- Thus, the state defined originally is a safe state.

**Another example:** This time we suppose that P1 makes the request for one additional unit each of R1 and R3. Is this safe?
![[Banker's Algorithm Deadlock.png]]
## Deadlock Avoidance
- When a process requests a set of resources
	- **Assume** that the request is granted
	- Update the system state accordingly
- Then determine if the result is a safe state. 
	- If safe, grant the request.
	- If not, block the process until it is safe to grant the request.
### Deadlock Avoidance Logic
![[Pasted image 20251010194936.png]]
![[Pasted image 20251010194948.png]]
![[Pasted image 20251010195006.png]]
### Deadlock Avoidance Advantages
- It is not necessary to preempt and rollback processes, as in deadlock detection
- It is less *restrictive* than deadlock prevention.
### Deadlock Avoidance Restrictions
- The *maximum resource requirement* must be stated in advance 
- Processes under consideration must be *independent* and with *no synchronization requirements*
- There must be a *fixed number of resources to allocate*
- No process may exit while holding resources

# Deadlock Detection
---
### Deadlock Detection Strategy
- ==Deadlock prevention and avoidance strategies can be very conservative==, limiting access to resources and restricting processes.
- ==Deadlock detection strategies are the opposite==; they grant resource requests whenever possible.
- The system does not check for deadlock before granting a resource. Instead, the OS periodically performs an algorithm to check for the presence of deadlock.

***
### A Common Detection Algorithm
*   Use a Allocation matrix and Available vector as previous.
*   Also use a request matrix **Q**
    *   Where $Q_{ij}$ indicates that an amount of resource *j* is requested by process *i*.
*   First 'un-mark' all processes that are not deadlocked.
    *   Initially that is all processes.

### Detection Algorithm
1.  Mark each process that has a row in the Allocation matrix of all zeros.
2.  Initialize a temporary vector **W** to equal the Available vector.
3.  Find an index *i* such that process *i* is currently unmarked and the *i*th row of **Q** is less than or equal to **W**.
    *   i.e. $Q_{ik} \le W_k$ for $1 \le k \le m$.
    *   If no such row is found, terminate.

### Detection Algorithm cont.
4.  If such a row is found,
    *   mark process *i* and add the corresponding row of the allocation matrix to **W**.
    *   i.e. set $W_k = W_k + A_{ik}$, for $1 \le k \le m$.
    *   Return to step 3.
*   A deadlock exists if and only if there are unmarked processes at the end.
*   Each unmarked process is deadlocked.

***

### Recovery Strategies Once Deadlock Detected
- Abort all deadlocked processes.
- Back up each deadlocked process to some previously defined checkpoint, and restart all process.
- Successively abort deadlocked processes until deadlock no longer exists.
- Successively preempt resources until deadlock no longer exists.

---
# Dining Philosophers Problem
---
### The Problem
- Devise a ritual (algorithm) that will allow the philosophers to eat.
- No two philosophers can use the same fork at the same time (mutual exclusion).
- No philosopher must starve to death (avoid deadlock and starvation ... literally!).

### Solutions Presented in the Slides
- **A first solution using semaphores**: A solution is presented where each philosopher waits on `fork[i]` and then `fork[(i+1) mod 5]`. This can lead to deadlock.
- **Avoiding deadlock**: A second solution is presented that adds a `semaphore room = {4}`. This ensures at most four philosophers can attempt to pick up forks, preventing deadlock.
- **Solution using Monitors**: A solution using a monitor is shown, which encapsulates the fork state and logic (`get_forks`, `release_forks`) to manage access.

---
# Concurrency Mechanisms
---
### UNIX Concurrency Mechanisms
- **Pipes**: A circular buffer allowing two processes to communicate on the producer-consumer model. It is a first-in-first-out queue, written by one process and read by another. Two types: Named and Unnamed.
- **Messages**: A block of bytes with an accompanying type. UNIX provides `msgsnd` and `msgrcv` system calls. Associated with each process is a message queue, which functions like a mailbox.
- **Shared Memory**: A common block of virtual memory shared by multiple processes. Permission is read-only or read-write, determined on a per-process basis. Mutual exclusion must be provided by the processes using the shared memory.
- **Semaphores**: SVR4 uses a generalization of the `semWait` and `semSignal` primitives. Associated with the semaphore are queues of processes blocked on that semaphore.
- **Signals**: A software mechanism that informs a process of the occurrence of asynchronous events. Similar to a hardware interrupt, without priorities.

### Linux Kernel Concurrency Mechanism
Includes all the mechanisms found in UNIX plus:
- **Atomic operations**: Operations that execute without interruption and without interference. Two types: Integer operations and Bitmap operations.
- **Spinlocks**: Only one thread at a time can acquire a spinlock. Any other thread will keep trying (spinning) until it can acquire the lock.
- **Semaphores**: Similar to UNIX SVR4 but also provides an implementation for its own use. Three types of kernel semaphores: Binary, counting, and reader-writer semaphores.
- **Barriers**: To enforce the order in which instructions are executed, Linux provides the memory barrier facility.

### Solaris Thread Synchronization Primitives
In addition to the concurrency mechanisms of UNIX SVR4:
- **Mutual exclusion (mutex) locks**: Used to ensure only one thread at a time can access the resource protected by the mutex. The thread that locks the mutex must be the one that unlocks it.
- **Semaphores**: Solaris provides classic counting semaphores.
- **Readers/writer locks**: Allows multiple threads to have simultaneous read-only access to an object. It also allows a single thread to access the object for writing at one time, while excluding all readers.
- **Condition variables**: Used to wait until a particular condition is true. Condition variables must be used in conjunction with a mutex lock.

### Windows concurrency mechanisms
Important methods of synchronization are:
- **Executive dispatcher objects (using Wait functions)**: The wait functions allow a thread to block its own execution until specified criteria have been met. Dispatcher objects include Events, Mutexes, Semaphores, and Timers.
- **user mode critical sections**: Similar mechanism to mutex except that critical sections can be used only by the threads of a single process. If the system is a multiprocessor, it will attempt to acquire a spin-lock first.
- **slim reader-writer locks**: Added in Windows Vista. A user mode reader-writer lock that enters the kernel to block only after attempting to use a spin-lock. 'Slim' as it normally only requires allocation of a single pointer-sized piece of memory.
- **condition variables**: Added in Windows Vista. The process must declare and initialise a `CONDITION_VARIABLE`. Used with either critical sections or SRW locks.