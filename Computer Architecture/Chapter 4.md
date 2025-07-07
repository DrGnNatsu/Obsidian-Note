___
pipeline⇒concurrently (sử dụng đồng thời cùng một tài nguyên) != parallel (sử dụng đồng thời nhưng khác tài nguyên)
# Introduction
Simplified: CPI = 1 (long cycle time = low clock rate = low frequency)
Realistic pipelined version: CPI >= 1 (short cycle time = high clock rate)
___
# Instruction Execution
1. PC instruction memory (cache), fetch instruction 
2. Access Register numbers -> to load register file (data), read registers 
3. Depending on the instruction class 
	1. Use the ALU to calculate 
		1. Arithmetic result done 
		2. Memory address for load/store 3.2 
		3. Branch target address 3.3 
	2. Access data memory for load/store 
	3. PC target address or PC + 4
___
# Execution Stages
1. Instruction fetch (IF): PC -> instruction address 
2. Instruction decode (ID): register operands, register file 
3. Execute (EXE): 
	1. Load/store: compute a memory address 
	2. Arithmetic/logical: compute an arithmetic/logical result 
4. Memory access (MEM): (can be skipped by some instructions such as add, sub, ...)
	1. Load: read from data memory 
	2. Store: write to data memory 
5. Write back (WB): Store the result of the register file (can be skipped by some instructions such as sw, sh, sb, ...)
___
# Datapath - Controller
- **Datapath**: contains information that is operated on by a functional unit 
	- Instruction memory: contains instructions (IF) 
	- Registers file: 32 32-bit registers (ID & WB) 
	- ALU: calculate arithmetic and logical operations (EXE) 
	- Data memory: contains data (MEM) 
- Control signals: used for the multiplexer selection or for directing the operation of a functional unit 
	- Control unit 
	- Multiplexer (selection block) - decide which source we will take.
![[Chapter4-10.jpg]]
# Instruction Fetch
- Main operations: fetching the next instruction from Instruction memory 
	- PC -> instruction address 
	- Instruction memory -> instruction (32 bits) 
	- PC <- PC + 4 (using the Add component) 
- Results: 
	- 32-bit machine instruction (Instruction) 
	- Address of the next instruction in the PC
![[Instruction Fecth.png]
# Instruction decode
- Main operations: Extract machine instructions 
	- R-format, branch, and store: rs, rt -> Registers -> values 
	- I-format: rs -> Registers -> values & immediate -> sign-extend
- Results: value 32-bit for the next stage
![[Instruction decode.png]]
# Instruction Execution
- Main operation:
	- Calculate the arithmetic operations/address of memory/register comparison. 
	- R-format and bne&beq: both operands collected from Registers
	- I-format (except bne & beq): one operand collected from Registers and one from the sign-extend
- Results: 
	- Arithmetic result/memory address (ALU ->result) 
	- Comparison result (zero-output)
![[Example Datapath.png]]
# Control block
# Performance Issue
- Simplified version (CPI = 1): Every instruction executed in only one cycle:
	- Longest delay determines the clock period. 
	- What is the longest instruction? 
		- Instruction memory → register file → ALU → data memory → register file 
	- Not feasible to vary the period for different instructions 
	- We will improve performance by pipelining.
==Pipeline== != ==Parallel==
Sequential model: the longest process displays a time cycle
Pipeline: instructions execute concurrently. The longest stage displays the cycle time.
- Ex: we have CS program: itit24, itit23, itit22, itit21 at the same time
Parallel: multiple resources, execute at the same time
# Pipelining Analogy
- Pipeline laundry:
	- Overlapping execution 
	- Improving performance (time for the entire group) 
- Four loads:
	- Speed-up = 2.3x
	- Not impressive 
- Non-stop (#loads ) 
	- Speed-up? 
	- Number of stages
- If we have an infinite persons needing the laundry process, the speed will approach 4.0 times.
![[Pipelining Analogy.png]]
==The factor affects the speed up (constraints):==
- Balanced stages (the time for each stage must be equal)
- More workloads
- A reasonable number of stages.
# Pipeline speed-up
$$\text{Speed-up} = \frac{\text{time of single-cycle}}{\text{time of pipelined}} = \frac{\text{time between instructions}_{\text{single-cycle}}}{\text{time between instructions}_{\text{pipelined}}}$$
- If **not balanced**, speedup is less
- Source of speedup
	- **Throughput** increased
	- **Latency** (time for each instruction) does not decrease
	  - Sometimes **increased**

#  Pipeline Register 
D-FlipFLop == Pipeline Register == Barrier
Purpose: hold the value for the next part
# Multi-Cycle Pipeline Diagram
- In the pipeline, if that instruction do not need to do some part of process but it should be wait. Because some different instruction using the the next part of instruction.
- Ex: `sub` do not need to use the DM but it still need to wait the `lw` use REG
![[Multi-Cycle Pipeline Diagram.png]]
# Single-Cycle Pipeline Diagram
**The last `lw` will store in the `$t4`**
![[Single-Cycle Pipeline Diagram.png]]