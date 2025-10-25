---
tags:
  - "#os"
---
# The Need for Memory Management
- Memory is cheap today, and getting cheaper, but applications demand more.
- Memory Management involves swapping blocks of data from secondary storage.
- Memory I/O is slow compared to a CPU; the OS must cleverly time swapping to maximize CPU efficiency.
> Memory needs to be allocated to ensure a reasonable supply of ready processes to consume available processor time.
# Memory Management Requirements
- Relocation
- Protection
- Sharing
- Logical organization
- Physical organization
## Requirements: Relocation
- The programmer *does not know* where the program will be placed in memory when it is executed.
- It may be swapped to disk and returned to main memory at a different location (relocated).
- Memory references must be translated to the actual physical memory address.
![[Addressing.png]]

| Term | Description |
| :--- | :--- |
| **Frame** | Fixed-length block of main memory. |
| **Page** | Fixed-length block of data in secondary memory (e.g., on disk). |
| **Segment** | Variable-length block of data that resides in secondary memory. |
Frame-size = Page-size
## Requirements: Protection
- Processes should not be able to reference memory locations in another process without permission.
- Impossible to check absolute addresses at compile time; must be checked at run time.
## Requirements: Sharing
- Allow several processes to access the same portion of memory.
- Better to allow each process access to the same copy of the program rather than have its own separate copy.
## Requirements: Logical Organization
- Memory is organized linearly (usually).
- *Programs are written in modules* that can be written and compiled independently. (FOR DEV ONLY)
- Different degrees of protection (read-only, execute-only) can be given to modules.
- Segmentation helps in sharing modules among processes.
## Requirements: Physical Organization
- Cannot leave the programmer with the responsibility to manage memory.
- Memory available might be insufficient.
- Overlaying (assigning the same memory region to various modules at different times) is time-consuming to program.
- The programmer *does not know* how much space will be available.
___
# Partitioning

## Types of Partitioning
- Fixed Partitioning
- Dynamic Partitioning
- Simple Paging
- Simple Segmentation
- Virtual Memory Paging
- Virtual Memory Segmentation
## Fixed Partitioning
- An early method of managing memory (pre-virtual memory).
- **Equal-size partitions**: Any process $\le$ The Partition size can be loaded. The OS can swap processes out if none are ready.
- **Unequal Size Partitions**: Lessens problems but doesn't completely solve them. Reduces internal fragmentation by using smaller partitions for smaller programs.
### Fixed Partitioning Problems
- A program may not fit in a partition (requiring overlays).
- Main memory use is inefficient (internal fragmentation).
- Any program, no matter how small, occupies an entire partition.
### Placement Algorithm (for Unequal Size)
- **Equal-size**: Trivial (no options).
- **Unequal-size**:
    - Assign the process to the **smallest partition** it will fit in.
    - Queue for each partition.
    - Aims to minimize wasted memory within a partition.
## Dynamic Partitioning
- Partitions are of **variable length and number**.
- Process is allocated **exactly as much memory as required**.
### Dynamic Partitioning Problems (External Fragmentation)
- Memory external to all processes is fragmented.
- Can be resolved using **compaction** (OS moves processes to be contiguous), which wastes CPU time.
### Dynamic Partitioning Placement Algorithms
- **First-fit algorithm**: Scans from the beginning, chooses the first available block that is large enough. (Fastest).
- **Best-fit algorithm**: Chooses the block that is **closest in size** to the request (leaves the smallest fragmentation). (Worst performer overall).
- **Next-fit**: Scans memory from the location of the **last placement**. Tends to allocate at the end of memory.
___
# Buddy System
- The entire space available is treated as a single block of $2^U$.
- If the request size $s$ falls within $2^{U-1} < s \le 2^U$ The entire block is allocated.
- Otherwise, the block is split into two equal buddies. Process continues until the smallest suitable block is generated.

## Relocation
- When a program is loaded, actual (absolute) memory locations are determined.
- Different absolute memory locations are used during execution if the process moves partitions (due to swapping or compaction).

## Addresses
- **Logical**: Reference independent of current memory assignment.
- **Relative**: Address expressed relative to some known point.
- **Physical or Absolute**: Actual location in main memory.

### Registers Used during Execution
- **Base register**: Starting address for the process.
- **Bounds register**: Ending location of the process.
- These values are set when the process is loaded or swapped in.
- The base register value is added to a relative address to get an absolute address, which is then checked against the bounds register.

## Paging
- Partition memory into small equal **fixed-size chunks**:
    - Process chunks are called **pages**.
    - Memory chunks are called **frames**.
- The OS maintains a **page table** for each process, containing the frame location for each page.
- A memory address consists of a **page number** and an **offset** within the page.
(See Figure 7.12(a) on page 7 illustrating logical-to-physical address translation in Paging).

## Segmentation
- A program can be subdivided into **segments**.
- Segments may vary in length (but there is a maximum segment length).
- Addressing consists of a **segment number** and an **offset**.
- Similar to dynamic partitioning.
(See Figure 7.12(b) on page 7 illustrating logical-to-physical address translation in Segmentation).

(See Figure 7.11 on page 7 comparing logical addresses in Partitioning, Paging, and Segmentation).
(See Figure 7.10 on page 7 showing Page Table Data Structures).