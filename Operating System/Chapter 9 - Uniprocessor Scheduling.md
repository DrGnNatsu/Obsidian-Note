---
tags:
  - os
---
---
# Scheduling
- An OS must allocate resources amongst competing processes.
- The resource provided by a processor is **execution time**.
- The resource is allocated by means of a **schedule**.
## Overall Aim of Scheduling
- Processor scheduling aims to assign processes to be executed by the processor over time.
- This should be done in a way that meets system objectives, such as response time, throughput, and processor efficiency.
## Scheduling Objectives
The scheduling function should:
- Share time **”fairly”** (algorithm) among processes. (Time of each slot is equal.)
- Prevent starvation of a process.
- Use the processor efficiently.
- Have low overhead (management cost is low). The swapping process is high overhead.
- Prioritise processes when necessary (e.g. real-time deadlines).
## Types of Scheduling (Table 9.1)

| Type | Description |
| :--- | :--- |
| **Long-term scheduling** | The decision to add to the pool of processes to be executed. |
| **Medium-term scheduling** | The decision to add to the number of processes that are partially or fully in main memory. |
| **Short-term scheduling** | The decision as to which available process will be executed by the processor. |
| **I/O scheduling** | The decision as to which process's pending I/O request shall be handled by an available I/O device. |

## Nesting of Scheduling Functions
(See Diagram on Page 2 showing the hierarchy from Long-Term to Short-Term scheduling).
## Queuing Diagram
(See Figure 9.3 on Page 2 illustrating the flow of processes through Long, Medium, and Short-term scheduling queues).
# Long-Term Scheduling
- Determines which programs are admitted to the system for processing.
- It may be **first-come-first-served** or according to criteria such as priority, I/O requirements, or expected execution time.
- Controls the **degree of multiprogramming**.
- More processes imply a smaller percentage of time each process is executed.
# Medium-Term Scheduling
- Part of the **swapping function**.
- Swapping-in decisions are based on the need to manage the degree of multiprogramming.
# Short-Term Scheduling
- Known as the **dispatcher** (scheduler - manages the time of slots) (top of main memory - small program - schedules to the processor).
- Executes most frequently.
- Invoked when an event occurs:
    - Clock interrupts
    - I/O interrupts
    - Operating system calls
    - Signals
## Aim of Short-Term Scheduling
- The main objective is to allocate processor time to optimise certain aspects of system behaviour.
- A set of criteria is needed to evaluate the scheduling policy.
## Short-Term Scheduling Criteria
- **User-oriented**:
    - **Response Time**: Elapsed time between the submission of a request and there is output.
- **System-oriented**:
    - **Effective** and **efficient** utilisation of the processor.
## Performance Criteria
- **Performance-related**:
    - Quantitative, easily measured (e.g., response time, throughput).
- **Non-performance related**:
    - Qualitative, hard to measure.

## Interdependent Scheduling Criteria (Table 9.3)
| Criteria | Description |
| :--- | :--- |
| **Turnaround time** | Total time from submission to completion. Appropriate for batch jobs. |
| **Response time** | Time from submission until response begins. Better for interactive processes. |
| **Deadlines** | Maximizing percentage of deadlines met. |
| **Predictability** | Variation in response time should be minimal regardless of load. |
| **Throughput** | Number of processes completed per unit of time. |
| **Processor utilization** | Percentage of time the processor is busy. |
| **Fairness** | Absence of starvation; equitable treatment. |
| **Enforcing priorities** | Favors higher-priority processes. |
| **Balancing resources** | Keeping all resources busy. |
# Priorities
- Scheduler will always choose a process of higher priority over one of lower priority.
- Have multiple ready queues to represent each level of priority.
## Starvation
- **Problem**: Lower-priority processes may suffer starvation if there is a steady supply of high-priority processes.
- **Solution**: Allow a process to change its priority based on its age or execution history.
# Scheduling Algorithms
## Selection Function
- Determines which process is selected for execution.
- If based on execution characteristics, important quantities are:
    - $w$: time spent in the system so far, waiting.
    - $e$: time spent in execution so far.
    - $s$: total service time required by the process, including $e$.
## Decision Mode
Specifies the instants in time at which the selection function is exercised.
- **Nonpreemptive**: Once a process is running, it will continue until it terminates or blocks itself for I/O (can not get the resources when the process go to the READY state).
	- **Preemptive**: Currently running process may be interrupted and moved to the ready state by the OS. Preemption may occur when a new process arrives, on an interrupt, or periodically.
## First-Come-First-Served (FCFS)
- Non-Preemption
- Each process joins the Ready queue.
- When the current process ceases to execute, the **longest** process in the Ready queue is selected.
- A short process may have to wait a very long time before it can execute.
- Favours **CPU-bound** processes; I/O processes have to wait until the CPU-bound process completes.
## Round Robin (RR)
- Uses **preemption** based on a clock (also known as **time slicing**).
- Clock interrupt is generated at periodic intervals.
- When an interrupt occurs, the currently running process is placed in the ready queue, and the next ready job is selected.
- Support short process
- Effect of Size of Preemption Time Quantum: can be constant or a function
    - Short quantum: increased overhead.
    - Long quantum: degrades to FCFS.
- **Virtual Round Robin**: Modification to handle I/O bound processes better (See Figure 9.7).
## Shortest Process Next (SPN)
- **Nonpreemptive** policy.
- The process with the **shortest expected processing time** is selected next.
- Short process jumps ahead of longer processes.
- **Issues**:
    - Predictability of longer processes is reduced.
    - If the estimated time for the process is not correct, the OS may abort it.
    - Possibility of **starvation** for longer processes.
## Shortest Remaining Time (SRT)
- **Preemptive** version of the shortest process next policy.
- Must estimate processing time and choose the shortest.
- Tie case: uses FCFS
## Highest Response Ratio Next (HRRN)
- **Nonpreemptive**
- Need to recompute after finishing.
- Choose the next process with the greatest ratio:
$$Ratio = \frac{\text{time spent waiting} + \text{expected service time}}{\text{expected service time}}$$
## Feedback Scheduling (penalty)
- Penalize jobs that have been running longer.
- Don't know remaining time process needs to execute.
- Variations exist, simple version **pre-empts** periodically, similar to round robin.
- Can lead to **starvation** → Using the quantum function to increase time slot after each priority queue
## Fair-Share Scheduling
- User's application runs as a collection of processes (threads).
- User is concerned about the performance of the **application**.
- Need to make scheduling decisions based on **process sets**.
# Traditional UNIX Scheduling
- **Multilevel feedback** using round robin within each of the priority queues.
- If a running process does not block or complete within 1 second, it is preempted.
- Priority is based on process type and execution history.
## Scheduling Formula
$$P_j(i) = \frac{CPU_j(i-1)}{2} + P_j(i-1) \quad \text{(simplified concept)}$$
$$P_j(i) = \text{Base}_j + \frac{CPU_j(i)}{2} + \text{nice}_j$$
## Bands
- Priorities are recomputed once per second.
- **Base priority** divides all processes into fixed bands of priority levels:
    - Swapper (highest)
    - Block I/O device control
    - File manipulation
    - Character I/O device control
    - User processes (lowest)