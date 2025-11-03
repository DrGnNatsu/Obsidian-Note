---
tags:
  - "#os"
---
___
Mutual Exclusion: Loại trừ tương hỗ
- To find the resource while still collaborating.
- Ex: In the lab, we have 30 computers and 50 students
	- Op1: Wait until they finish, and I will use
	- Op2: Collab with someone
- That means sometimes collaborates, sometimes competes.
___
# Principles of Concurrency
___
## Multiple Processes
 - Central to modern OS is managing multiple processes through:
    - Multiprogramming
    - Multiprocessing
    - Distributed Processing
- **Big Issue is Concurrency**: Managing the interaction of all these processes.
## Concurrency
Concurrency arises in: 
- Multiple applications: Sharing time 
- Structured applications: Extension of modular design 
- OS structure (OS implemented as a set of processes or threads)
## Key terms

| Term                 | Description                                                                                                                                                                                                                                                          |
| :------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **atomic operation** | A sequence of one or more statements that appears indivisible; no other process can see an intermediate state or interrupt the operation. No middle state: finish or finish                                                                                          |
| **critical section** | A section of code within a process that requires access to shared resources and must not be executed while another process is in a corresponding section. The process only stay there for a specific period of time                                                  |
| **deadlock**         | A situation where two or more processes are unable to proceed because each is waiting for the other. Ex: go into the memory, then go out, not do something.                                                                                                          |
| **livelock**         | A situation where two or more processes continuously change their states in response to changes in others without doing any useful work.                                                                                                                             |
| **mutual exclusion** | The requirement that when one process is in a critical section accessing shared resources, no other process may access any of those shared resources.                                                                                                                |
| **race condition**   | A situation where the final result depends on the relative timing of multiple threads/processes reading/writing a shared data item. Using race to detect who will go into the critical section when we have many processes that want to access the critical section. |
| **starvation**       | A situation where a runnable process is overlooked indefinitely by the scheduler.                                                                                                                                                                                    |

## Interleaving and Overlapping Processes
**Concurrency - Multi-tasking - multiprogramming - interleaving**: Two processes run at the same time, but when we specify a period of time, *only one is running*.
**Parallel - Multiprocessing - Overlapping**: Two processes run at the same time. When we specify a period of time, many processes are running.
### Difficulties of Concurrency
- **Sharing of global resources**: Safely managing access to shared global resources is difficult.
- **Optimal resource allocation**: It is difficult for the OS to manage the allocation of resources optimally.
- **Locating programming errors**: Errors are hard to locate because results are often non-deterministic and difficult to reproduce.
> This makes debugging concurrency-related bugs extremely difficult, as they are not always reproducible and may only occur under specific timing conditions.
### Enforce Single Access
If a rule enforces that only one process can enter the function (mutual exclusion), P1 runs, P2 blocks until P1 completes, then P2 resumes.
## Race Condition
A race condition occurs when:
- Multiple processes or threads read and write shared data items.
- The final result depends on the specific order of execution of the processes.
- The output depends on which process "wins the race" to modify the data last.
> For example, if one process reads a shared variable, is interrupted, and a second process modifies that same variable, the first process will resume its work with stale, incorrect data, leading to a corrupted result.
## Operating System Concerns
The OS must:
- Keep track of the various processes.
- Allocate and de-allocate resources (processor time, memory, files, I/O devices).
- Protect the data and resources of each process from interference by other processes.
- Ensure that the process execution results are independent of the processing speed.
## Process Interaction
![[Relationship.png]]
- Three-level interaction:
	- Process unaware of each other:
		- Word vs Facebook → Competition
	- Process indirectly aware of each other:
		- Word vs Excel → Collaboration
	- Processes are directly aware of each other
		- Parent and child process: you get first, and I can use it
Three main control problems arise from process competition:
1.  **Need for Mutual Exclusion**:
2.  **Deadlock**
3.  **Starvation**
## Requirements for Mutual Exclusion
1. Only **one process** can be in its **critical section at a time** for a resource 
2. A process halted in its noncritical section must not interfere with others.
3. It must not be possible for a process requiring access to a critical section to be delayed indefinitely (no deadlock or starvation).
4. When no process is in a critical section, any process that requests entry must be permitted to enter without delay.
5. A process must not be delayed access to a critical section if no one else is using it.
	1. The OS treats all processes the same, regardless of size, speed, or big computation.
	2. They have the same limited time in the critical section.
6.  A process remains inside its critical section for a finite time only.
	1. The finite time used to lock other processes 
	2. Ex: Account back (money = critical section) and transaction = processes
		- If we have parallel transactions, withdraw and transfer money. 
		- The bank system will lock the money and execute transactions.
		- The back system will check every time it execute the transactions
---
# Mutual Exclusion: Hardware Support
## Disabling Interrupts
- Works only on **Uniprocessors**.
- Mutual exclusion can be guaranteed by disabling interrupts. A process will continue to run without being preempted until it enables interrupts again.
	- Example: The process interrupts in the critical section 
``` C
while (true) {
/* disable interrupts */;
/* critical section */;
/* enable interrupts */;
/* remainder */;
}
```
- **Major Drawbacks:**
	- System efficiency degrades because the processor is limited in its ability to interleave processes.
	- **This approach does not work on multiprocessor systems.** Disabling interrupts on one processor does not prevent other processors from accessing the shared resource.
## Special Machine Instructions
- These are hardware instructions that are performed as a single atomic operation, meaning they are not subject to interference from other processes.
- **Compare&Swap (CAS)**: Atomically compares the content of a memory location to a given value and, only if they are the same, modifies the content of that memory location to a new given value.
``` C
// The function below is an atomic operation
int compare_and_swap (int *word, int testval, int newval) {
	int oldval;
	oldval = *word
	if (oldval == testval) *word = newval;
	return oldval;
}
/* program mutualexclusion */
const int n = /* number of processes */;
int bolt;
void P(int i) {
	while (true) {
		while (compare_and_swap(bolt, 0, 1) == 1) //Race begin
		/* do nothing */;
		/* critical section */;
		bolt = 0; //Restart race
		/* remainder */;
	}
}

void main() {
	bolt = 0;
	parbegin (P(1), P(2), ... ,P(n));
}
```
- **Exchange**: Atomically swaps the contents of a register and a memory location.
``` C
// The function below is an atomic operation
void exchange (int *register, int *memory) {
	int temp;
	temp = *memory;
	*memory = *register;
	*register = temp;
}
/* program mutualexclusion */

int const n = /* number of processes */;
int bolt;
void P(int i) {
	while (true)
		int keyi = 1;
		do exchange (&keyi, &bolt) // Race begin
		while (keyi != 0);
		/* critical section */
		bolt = 0; //Restart race
		/* remainder */
	}

}

void main() {
	bolt = 0;
	parbegin (P(1), P(2), ..., P(n));
}
```
## Hardware Mutual Exclusion: Advantages & Disadvantages
- **Advantages**: Applicable to any number of processes (single or multiprocessor), simple to verify, supports multiple critical sections.
- **Disadvantages**:
	- **Busy-waiting**: A process repeatedly checks a condition in a loop, consuming processor time without performing useful work.
	- **Starvation** is possible because the selection of the next process to enter the critical section is not necessarily fair.
	- **Deadlock** is possible: multiple resources 
# Semaphores
---
## Semaphore (Data Structure)
- A semaphore is an integer value used for signaling among processes. Operations must be **atomic**: `initialize`, `Decrement (semwait)`, and `increment (semSignal)`.
	- **Binary Semaphore**: Value is restricted to zero or one (used like a lock).
	- **Strong Semaphores**
	- **Weak Semaphores
- It’s the number of resource values, it can be negative:
	- Example: I have 3 resources, a requests consume 3 → it becomes 0, and the second requests consume 2 → it becomes -2 (but it means that we do not have -2, but we need to wait 2 resources to execute the requests in the queue)
- Only three **atomic** operations are permitted on a semaphore:
	1. **Initialize**: Set the semaphore to a non-negative value.
	2.  **semWait (or P)**: Decrements the semaphore value. If the value becomes negative, the process executing the `semWait` is blocked. 
		1. It is a race.
	3.  **semSignal (or V)**: Increments the semaphore value. If the value is not positive, a process blocked by a `semWait` operation is unblocked.
``` C
struct semaphore {
	int count;
	queueType queue;
};
void semWait(semaphore s) { 
	s.count--;
	if (s.count < 0) { // We dont have enough resources
		/* place this process in s.queue */;
		/* block this process */;
	}
}
void semSignal(semaphore s) {
	s.count++;
	if (s.count<= 0) { // We don’t have enough resources, we have the process in the queue, we need to execute the queue first
	/* remove a process P from s.queue */;
	/* place process P on ready list */;
	}
}
```
## Strong/Weak Semaphore
- The distinction lies in how processes are unblocked from the semaphore's queue.
- **Weak Semaphore**: Does not specify the order in which processes are removed from the queue. (Random pick up, may have starvation)
- **Strong Semaphore**: Uses a **FIFO (First-In-First-Out)** policy, ensuring that the process that has been blocked the longest is released from the queue first. This prevents starvation.
## Mutual Exclusion Using Semaphores
- This is the most common application of semaphores.
- A semaphore (often called a mutex) is initialized to 1.
- A process performs a `semWait` operation before entering its critical section.
- The process performs a `semSignal` operation after exiting its critical section.
## The Producer/Consumer Problem
- **Scenario**: One or more **producers** generate data and place it in a shared buffer. A single **consumer** removes items from the buffer one at a time.
	- Example: Chef and customers in the Kichi Kichi
	- If the line is free, the Chef can put the sushi
	- The customer takes the food until the line is empty
- Constraints: 
	- Only one producer or consumer may access the buffer at any one time (Critical Section)
	- Ensure the producer can not add data to the full buffer, and the Consumer can not remove data from an empty buffer.
- **Challenges**:
	- The producer must not add data to the buffer if it is full.
	- The consumer must not remove data from the buffer if it is empty.
	- Only one process (producer or consumer) may access the buffer at any given time.
**Incorrect Solution**
``` C
/* program producerconsumer */
int n;
binary_semaphore s = 1, delay = 0;
void producer() {
	while (true) {
		produce();
		semWaitB(s);
		append();	
		n++;
		if (n==1) semSignalB(delay);
		semSignalB(s);
	}
}

void consumer() {
	semWaitB(delay); // Chặn comsumer vô critical section khi không có data = there is data in the buffer
	while (true) {
		semWaitB(s);	
		take();	
		n--;
		semSignalB(s);
		consume();
		if (n==0) semWaitB(delay); // Empty buffer
	}
}

void main() {
	n = 0;
	parbegin (producer, consumer);
}
```
![[Critical Section (Fail).png]]
Problem:
- n: global variable, it is a critical section, but we do not protect it.
Fix:
- Create the local variable to protect it:
## Bounded Buffer Problem Solution
- The solution for a finite buffer uses three semaphores:
	1.  `s`: A binary semaphore for enforcing **mutual exclusion** on buffer access, initialized to 1.
	2.  `n`: A counting semaphore to count the number of **items in the buffer**, initialized to 0.
	3.  `e`: A counting semaphore to count the number of **empty spaces in the buffer**, initialized to the buffer size.
- The producer waits on `e` before producing and signals `n` after. The consumer waits on `n` before consuming and signals `e` after. Both wrap their buffer access with waits and signals on `s`.
# Monitors
---
## Monitors
- A monitor is a programming language construct that provides equivalent functionality to semaphores but is easier to control.
- **Chief Characteristics**:
	- Local data variables are accessible only by the monitor's procedures.
	- A process enters the monitor by invoking one of its procedures.
	- **Only one process can execute in the monitor at a time**, providing implicit mutual exclusion.
## Synchronization in Monitors
- Synchronization is achieved using **condition variables** within the monitor.
- **cwait(c)**: Suspends the execution of the calling process on condition `c`. The monitor is now available for another process.
- **csignal(c)**: Resumes the execution of some process blocked on condition `c`. If no process is blocked, the signal has no effect.
# Message Passing
---
## Message Passing
- This is a mechanism for inter-process communication that synchronizes actions and exchanges data. It is an alternative to shared variables.
- It relies on a pair of primitives:
	- `send(destination, message)`
	- `receive(source, message)`
- This approach works on both shared-memory and distributed systems.
## Synchronization
- Primitives can be **blocking (synchronous)** or **non-blocking (asynchronous)**.
	- **Blocking send**: The sending process is blocked until the message is received.
	- **Blocking receive**: The receiving process is blocked until a message arrives.
	- A combination of blocking send and blocking receive is known as a **rendezvous**.
- **Non-blocking send**: The sending process continues execution immediately after sending.
- **Non-blocking receive**: The receiver retrieves a message if available, but does not wait if one is not.
## Addressing
- **Direct Addressing**: The `send` primitive explicitly identifies the destination process. The `receive` primitive can specify the desired source process.
	- You can not send it if the receiver does not accept
- **Indirect Addressing**:
	- Messages are sent to a shared data structure called a **mailbox**.
	- Processes communicate by sending messages to and receiving messages from the mailbox.
## Mutual Exclusion for Messages
``` C
/* program mutualexclusion */
const int n = /* number of process */
void P(int i) {
	message msg;
	while (true) {
		receive (box, msg);
		/* critical section */; // one receives message, others wait
		send (box, msg);
		/* remainder */; // Start new race
	}
}
void main() {
	create mailbox (box);
	send (box, null);
	parbegin (P(1), P(2), . . . , P(n)); 
}
```
# Readers/Writers Problem
---
## The Readers/Writers Problem
- **Scenario**: A data area is shared among many processes.
	- Some processes only read the data area (**Readers**).
	- Some processes only write to the data area (**Writers**).
- **Conditions to satisfy**:
	1.  Any number of readers may simultaneously read the file.
	2.  Only one writer at a time may write to the file.
	3.  If a writer is writing to the file, no reader may read it.
- There are two main variations of the problem based on priority:
	- **Readers have Priority**: No reader will be kept waiting unless a writer has already obtained permission to write. A waiting writer may be starved by a continuous stream of new readers.
	- **Writers have Priority**: Once a writer is ready to write, no new readers are allowed to start reading. A waiting reader may be starved by a continuous stream of new writers.
``` C
/* program readersandwriters */
int readcount;
semaphore x = 1,wsem = 1;
void reader(){
	while (true){
		semWait (x);
		readcount++;
		if(readcount == 1) semWait (wsem);
		semSignal (x);
		READUNIT();
		semWait (x);
		readcount--;
		if(readcount == 0) semSignal (wsem);
		semSignal (x);
	}
}
void writer() {
	while (true) {
		semWait (wsem);
		WRITEUNIT();
		semSignal (wsem);
	}
}
void main() {
	readcount = 0;
	parbegin (reader,writer);
}
```