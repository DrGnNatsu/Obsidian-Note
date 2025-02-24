___
# Instruction Set Architecture
**Remake**: $$CPU\;Times=\frac{IC\times CPI}{Clock\;Rate}$$


| CISC (Complex instruction set computer)                                                         | RISC (Ruducied Intruction Set Computer)                                                                       |
| :---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| Philosophy is IC &darr;                                                                         | Philosophy is CPI &darr;                                                                                      |
| Complex instruction: multiple operations (operand) / instruction. **CPI↑**. <br>($a+b\times c$) | Simple instruction: one operation. **IC↑**.  Less hardware resources ⇒ Integrate more cores and optimise.<br> |
| x86: Intel, AMD                                                                                 | Apple Silicon, ARM                                                                                            |
| Number of ISA is more                                                                           | Number of ISA is less                                                                                         |
| Instruction of length (bits): Variant                                                           | Instruction of length (bits): Fix                                                                             |
## Von Neumann Architecture
Contains three mains components:
- Main memory (M): stored all the data and the software application.
- Central Processing Unit (CPU): Arithmetic logic unit (CA) and Program Control Unit (CC): All of execution of the program are executed by CPU.
- I/O Equipment: (I, O).
Stored-program concept
Instruction Category:
- Arithmetic 
- Data Transfer
- Logical
- Conditional branch
- Unconditional jump
## Computer Components
![[CPU Components.png| 640 x 480]]
If your OS said that it is 32 bits, it means that your **System bus** is 32 bits.
1. **CPU**:
	1. Execution unit (ALU): the logic gate inside the computer
	2. Register:
		1. Special Purpose: PC: program counter: store the address of the next instruction.
		2. General Purpose: storing data and execution in order (MIPS: 32 bits)
2. **Memory:** cells: the fixed size in each cell (at the standard cell: 8 bits = 1 bytes/cell) 
	1. The address of each cell is fixed (physical location, determines itself). The size of the address depends on the system bus: 
		1. Ex: Standard MIPS: 32 bits ⇒Total main memory: $2^{32} \; cells\; (address)$  ⇒ 4 GB in total.
		2. WORD: include `n` bytes ⇒ MIPS: word = 4 bytes = The size of system bus. = 4 cells in the word but it only on the physical that means it contains in groups 
			1. Constraints: 
				1. 4 cells must be consecutive in address (next to each other)
				2. Any cell only belong to 1 WORD ⇒ $Lowest\;Address\;\vdots\;4 = 0$
			2. Ex: we have the address of the WORD is `0xCA|FE|FA|CE` that mean the address write in term of hexadecimal. The `CA` on the left is Most Significant byte (MSB) and `CE` is Least Significant Byte (LSB).
				1. The computer have two way to put that in to the WORD.
					1. Little endian (Intel): LSB is stored at lowest address.
					2. Big endian (MIPS): MSB is stored at lowest address.
					3. No one is better based on the assumption.

| 0xCE     | 0xFA     | 0xFE     | 0xCA     | Little endian  |
| :------- | :------- | -------- | -------- | -------------- |
| **0xCA** | **0xFE** | **0xFA** | **0xCE** | **Big endian** |
| **4**    | **5**    | **6**    | **7**    |                |

2. **Memory:** 
	2. Data is changed by time ⇐ What CPU will access
3. **I/O Module**: is the same access the CPU to main memory
___
# Instruction Execution Module
 ![[Instruction Execution Module.png]]
 - Instruction fetch: from the memory: because the data is in the main memory.
	 - PC increased 
	 - PC stores the address of the next instruction 
- Execution: decode and execute
___
# Standard MIPS Instruction
## MIPS Instruction set
- MIPS Architecture
- MIPS Assembly Instruction ⇔ MIPS Machine Instruction
- Assembly: 
```MIPS
add $t0, $s2, $t0
```
- Machine: 000000_10010_01000_01000_00000_100000
- Only **one operation** is performed per MIPS Instruction.
	- Ex: `a+b+c` need at least two operations
## Instruction Set Design Principle
- Simplicity favours regularity 
- Smaller is faster 
- Make the common case fast. 
- Good design demands good compromises.
## MIPS Instruction
1. Register: 32 32-bit registers (start with the $sign)
	1. $t0 - $t9: storing temporary value
	2. $s0 - $s7: save variables
	3. $a0 - $a3
	4. $v0 - $v1
	5. $gp, $fp, $sp, $ra, $at, $zero, $k0 - $k1.
2. Memory operand: $2^{30}$ memory words (4 byte each): accessed only by data transfer instructions
3. Short Integer Immediate (16 bits): -10, 20, 2020, ...
⇒ **Only three operand types! Nothing else!***
## $1^{st}$ Group: Arithmetic Instructions
Assembly instruction format:

| Opcode | Destination register | Source Register 1 | Source Register 2 |
| :----- | -------------------- | ----------------- | ----------------- |
- Destination Register: update the register by the result of the operand / store the result in that
- OP code:
	- add: DR = SR1 + SR2
	- sub: DR = SR1 - SR2
	- addi: SR2 is an intermediate (e.g. 20), DR = SR1 +SR2
- Three register operands.
Exercise:  what is the MIPS code for this equation f = g + h - i - 2
```asm
add $t0, $s0, $s1
addi $t1, $s2, 2
sub $s4, $t0, $t1
```
## $2^{nd}$ Group: Data Transfer Instructions
- **Copy Data**: by the way memory and registers in CPU
	- Register
	- Address: a value used to delineate data element within a memory array
- **Load (l)**: Copy data from memory to a register.
	- Copy data from M to R ( copy from address 8 to $s0: 2025 → 10)
		- P sends address 8 to M
		- M comes to WORD at address 8
		- M take value (10) in WORD address 8 to P
		- P assign new value (10) to $s0.
- **Store (s)**: Copy data from register to memory.
	- Copy data from R to M ( copy from R 2025 to address 4)
		- P sends the value in the R (2025) & address 4 in the M 
		- M comes to the WORD at address 4
		- M updates data of the WORD (101) to new value (2025).