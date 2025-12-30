---
tags:
  - os
---
# Terminology

![[Virtual Address Terminology.png]]
# Key Points in Memory Management
1. Memory references are **logical addresses** dynamically translated into **physical addresses** at run time. A process may be swapped in and out of main memory, occupying different regions at different times.
2. A process may be broken up into pieces that do not need to be located contiguously in main memory.
# Breakthrough in Memory Management
If both dynamic translation and non-contiguous memory allocation are present:
- All pages/segments of a process don't need to be in main memory during execution.
- Execution can proceed as long as the next instruction and necessary data locations are in main memory.
## Execution of a Process
- OS brings into main memory a few pieces of the program
- Resident set - portion of processes that is in the RAM.
- An interrupt is generated when an address is needed that is not in RAM.
- OS places it in a blocking states
- The piece of process containing the logical address is brought into main memory.
	- The OS issues a disk I/O Read request.
	- Another process runs while disk I/O occurs.
	- An interrupt signals completion, placing the affected process in the **Ready state**.
## Implications of this New Strategy
- More processes can be maintained in main memory.
- Only load *some* pieces of each process.
- High likelihood that a process will be in the Ready state due to increased multiprogramming.
- A process may become larger than all of the main memory.
# Real and Virtual Memory
- **Real memory**: Main memory (actual RAM).
- **Virtual memory**: Memory on disk.
- Virtual memory allows effective multiprogramming and relieves the user of the tight constraints of main memory.
## Principle of Locality
- Program and data references within a process tend to **cluster**.
- Only a few pieces are needed over a short period of time.
- This principle suggests that virtual memory works efficiently.
## Thrashing
- A state where the system spends most of its time swapping pieces rather than executing instructions.
	- Reason: Not enough main memory, running too many processes
- To avoid this, the OS guesses which pieces are least likely to be referenced in the near future, based on recent history.
# Paging System
![[Memory Management Format.png]]
## Paging vs. Segmentation Support
Hardware must support paging and/or segmentation. The OS manages the movement of pages/segments between secondary and main memory.
## Paging
- Each process has its own **page table**.
- Each Page Table Entry (PTE) contains the **frame number** corresponding to the page in RAM.
- PTEs require two extra bits: one to indicate if the page is in main memory, and one to track if the page has been modified (dirty bit).
## Address Translation (Paging)
- A virtual address is composed of a **Page Number** and an **Offset** within the page.
- The Page Number indexes the Page Table to find the **Frame Number**.
- The physical address is constructed by concatenating the Frame Number with the **Offset**.
![[Address Translation.png]]
## Page Tables Structure
- Page tables are stored in virtual memory; part of the running process's page table must be in main memory.
- **Two-Level Hierarchical Page Table**: Used to manage large virtual address spaces by having a root page table pointing to multiple user page tables.
	- Example: 32-bit = 4 bytes
		- Indexing table: 1024 records ⇒ 4Kb
		- Indexing 2: 1024 tables ⇒ 4Mb
		- Stored 4GBs data
### Drawbacks of Hierarchical Paging
- The size of the page table is proportional to the size of the **virtual address space**, even if only a small portion is used.
## Inverted Page Table
- Actually, it is a hash table (saves memory) ⇒ Create N-bit tables consume memory ⇒ m-bit hash map to reduce memory consumption.  
- An alternative to hierarchical tables, used in PowerPC, UltraSPARC, and IA-64.
- The page number portion of the virtual address is mapped via a hash value to an entry in the inverted table.
- A fixed proportion of real memory is required, regardless of address space size.
- Each entry includes: Page number, Process identifier, Control bits (valid, referenced, etc.), and a **Chain pointer** for collision resolution.
![[Inverted Table Page.png]]
# Translation Lookaside Buffer (TLB)
- To overcome having two physical memory accesses per reference (one for page table, one for data), a high-speed cache for page table entries is used.
- **TLB**: Contains recently used page table entries.
--- start-multi-column:  
```column-settings  
number of columns: 2  
largest column: right
```

**TLB Hit**: Frame number retrieved directly, physical address formed.

--- end-column ---

**TLB Miss**: Page number indexed into the Process Page Table. If the page is not in memory, a page fault occurs. The TLB is then updated.

--- end-multi-column

![[Translation Lookaside Buffer.png]]
![[Operation of TLB.png]]
# Page Size Impact
- **Smaller page size**: Less internal fragmentation, but more pages required per process, leading to larger page tables stored in virtual memory.
- **Larger page size**: Secondary memory works better transferring large blocks, but increases page faults as pages spread out further from recent references. 
![[Paging Behaviour.png]]
> [!note] Explanation:
> **1. Effect of Page Size (The Curve)**
> 	- **Small Pages:** **Low Fault Rate.** (High number of pages fit in RAM $\rightarrow$ tightly captures the "Working Set" / Locality).
> 	- **Increasing Page Size:** **Fault Rate Rises.** (Locality is weakened; pages contain "distant" code that isn't needed immediately, wasting RAM space).
> 	- **Huge Pages (Point P):** **Fault Rate Drops.** (As page size $\approx$ process size, the entire process fits in memory, eliminating faults).
>**2. Effect of Allocation (Frame Count)**
> 	- For a fixed page size, increasing the **Number of Frames** allocated to a process **decreases** the page fault rate.

## Protection and Sharing
- Segmentation naturally lends itself to implementing protection and sharing policies.
- Each segment entry holds a base address and length, allowing controlled access.
- Sharing is achieved by allowing multiple processes to reference the same segment.
# Operating System Software

## Fetch Policy
- Determines when a page should be brought into memory.
- ***Demand Paging***: Brings a page into main memory only when a reference is made to a location on that page. This leads to many page faults when a process first starts. Cần mới load
- ***Prepaging***: Brings in more pages than needed at one time. It is more efficient to bring in pages that reside contiguously on the disk. (Not to be confused with "swapping"). Load đại 
## Placement Policy
- Determines where in real memory a process piece is to reside.
- This is important in a segmentation system. For paging or combined systems, the hardware performs the address translation.

> [!important] Have page faults occur? 
>  NO page faults

> [!note] Definition
> Frame is empty, and put the page in it.
## Replacement Policy
- When all frames in main memory are occupied, this policy determines which page currently in memory is to be replaced.
- The goal is to remove the page least likely to be referenced in the near future, typically predicted based on past behaviour (principle of locality).
- Page faults
> [!note] definition
> The frame contains a page, and the OS replaces the new page in it.
### Frame Locking
- If a frame is ***locked***, the page in it may not be replaced.
- This is used for critical parts of the OS, key control structures, and I/O buffers. A lock bit is associated with each frame.
### Basic Replacement Algorithms
- ***Optimal*** (1): Replaces the page for which the time to the next reference is the longest. Impossible to implement perfectly as it requires future knowledge.
	- Based on an assumption
	- Replace the file that is not being used in the future. Thay thế file không dùng xa nhất.
- ***Least Recently Used (LRU)*** (2): Replaces the page that has not been referenced for the longest time. Difficult to implement as it requires tagging each page with the time of its last reference.
	- Thay thế file không dùng lâu nhất
- ***First-in, first-out (FIFO)*** (4): The page that has been in memory the longest is replaced.
- ***Clock Policy*** (3): A common approximation of LRU. It uses an additional "use bit" for each frame. When a page is referenced, its use bit is set to 1. To replace a page, the OS circularly scans the frames. If a frame's use bit is 1, it is flipped to 0. The first frame encountered with a use bit of 0 is replaced.
	- Thằng nào dùng nhiều thì có thêm một mạng.
	- PF xảy ra thì từ 1 thành 0
	- Page được reference thì 0 thành 1
	- Thằng nào 0 thì cút
	- Nếu không có 0 thì dùng FIFO.
![[Replacement Algorithm.png]]
### Page Buffering
- Replaced pages are not immediately discarded but are added to one of two lists: a ***free page list*** (if unmodified) or a ***modified page list***. This allows a page to be quickly reclaimed if it's needed again soon, and allows modified pages to be written to disk in batches.
### Replacement Policy and Cache Size
- Main memory size is getting larger, and the locality of applications is decreasing.
	- So, cache sizes have been increasing.
- With large caches, the replacement of pages can have a performance impact
	- Improve performance by supplementing the page replacement policy with a policy for page placement in the page buffer.
- **Two-Handed Clock**: Uses two pointers (front-hand and back-hand) scanning the page list to potentially improve performance over a single clock.
- **Page Buffering**: LRU/Clock policies can be supplemented by buffering modified pages to reduce expensive disk writes.
## Resident Set Management
- The OS must decide how many pages to allocate to each process (its ***resident set***).
	- The smaller the amount of memory allocated to each process, the more processes that can reside in memory.
	- A small number of pages loaded increases page faults.
	- Beyond a certain size, further allocations of pages will not affect the page fault rate.
- ***Resident Set Size***: 
    - ***Fixed-allocation***: A process is given a fixed number of frames.
    - ***Variable-allocation***: The number of pages allocated to a process varies over its lifetime.
- ***Replacement Scope***: 
    - ***Local***: The replacement policy chooses only from among the resident pages of the process that generated the page fault.
	    - Replace the page in the scope (fix the number of frames)
	    - Decide ahead of time the amount of allocation to give a process. If the allocation is too small, there will be a high page fault rate. If allocation is too large, there will be too few programs in main memory ⇒ Increased processor idle time or increased swapping.
    - ***Global***: The policy considers all unlocked pages in main memory for replacement.
	    - Place the page into the frame (add more frames)
	    - Easiest to implement: adopted by many operating systems.
	    - The operating system keeps a list of free frames
	    - A free frame is added to the resident set of processes when a page fault occurs
	    - If no free frame, it replaces one from another process
		    - Therein lies the difficulty … which to replace
![[Resident Set Management.png]]
## Cleaning Policy
- Determines when a modified page should be written out to secondary memory.
- ***Demand cleaning***: A page is written out only when it has been selected for replacement. Khi nào cần thì dọn
- ***Precleaning***: Pages are written out in batches before their frames are needed. This is often combined with page buffering. Dọn liên tục
- Best approach uses page buffering
- Replaced pages are placed in two lists 
- Modified and unmodified Pages in the modified list are periodically written out in batches 
- Pages in the unmodified list are either reclaimed if referenced again or lost when its frame is assigned to another page
## Load Control
- Determines the number of processes that will be resident in main memory (the ***multiprogramming level***).
- Too few processes lead to idle CPU time.
- Too many processes lead to ***thrashing***.
> [!note] Definition
> Long-term Scheduling: ensure there is enough space to ready state
> Middle-term Scheduling: check for suspend, ready, and block state
> Short-term Scheduling:
### Image Explanation
**1. The Relationship (The Curve)**
- **x-axis:** Degree of Multiprogramming (Number of processes).
- **y-axis:** CPU Utilization.
**2. Behavior**
- **Initial Rise:** More processes utilize idle CPU time during I/O waits.
- **Thrashing Point:** When memory is over-committed, processes do not have enough frames for their "Working Set."
- **The Crash:** High frequency of page faults causes the OS to spend all time swapping pages (Thrashing) rather than executing instructions.
Less number of processes - low performance, 
high number of processes - low performance, 
Load Control manage the number of processes to maximise the performance.
![[Processor and Performace.png]]
### Process Suspension
- If the degree of multiprogramming needs to be reduced, one or more resident processes must be suspended (swapped out).
- ***Suspension policies*** for choosing a process to suspend include:
    - Lowest priority process.
    - Faulting process (its working set is not in memory anyway).
    - Last process activated (least likely to have its working set resident).
    - Process with the smallest resident set.
    - Largest process.
    - Process with the largest remaining execution window.
