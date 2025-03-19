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
					2. **Big endian (MIPS): MSB is stored at lowest address.**
					3. No one is better based on the assumption.

| 7        | 6        | 5        | 4        |                |
| :------- | :------- | -------- | -------- | -------------- |
| **0xCE**     | **0xFA**     | **0xFE**     | **0xCA**     | **Little endian**  |
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
		- M updates the WORD (101) data to new value (2025).
___
# Data Transfer Instructions
- Assembly instruction format![[Assembly Instruction.png]]
- Opcode: 
	- Size of data: 1 byte, 2 bytes (half of word), 4 bytes (a word)
	- Behaviors: load or store
- Register
	- Load: destination
	- Store: source
- Memory Operand: offset (base register)
	- Offset: short integer number
	- Byte address: each address identifies an 8-bit byte 
	- “words” are aligned in memory (address must be multiple of 4)
___
# Memory Operand
$$
Memory\;Address=<offset>\;+\;value(base\;register)
$$
![[Memory Operand.png]]
**Given Data:**
- **Register Information**:
    - `$s0` stores the value **8**.
    - We need to determine the memory operand to access the byte storing **0x9A**.
**Solution:**
1. **Find the address of 0x9A in the memory map:**
    - Looking at the table, **0x9A is stored at address 12**.
2. **Calculate the offset from $s0 (which stores 8):**
    - Offset = Address of **0x9A** - Value in `$s0`
    - Offset = **12 - 8 = 4**
3. **Memory Operand Representation:**
    - The memory operand is represented as **offset(base register)**.
    - Since the base register is `$s0` and the offset is `4`, the memory operand is:**`4($s0)`**
**Final Answer:**
The memory operand used to access the byte storing the value **0x9A** is: **`4($s0)`**
**Another Solution:** we can use the `$zero`, always have the base value is 0 ⇒  the memory operand is:**`12($zero)`**
___
# Load Instruction
**Remind**: “load” means copying data from memory to a 32-bit register. 
- Instructions:
	- lw: load word 
		- eg.: lw $s0, 100($s1) # copy 4 bytes from memory to $s0 
		- If the word is 100 + $ s1 it is 
			- 100 + $ s1: 0x12
			- 101 + $ s1: 0x34
			- 102 + $ s1: 0x56
			- 103 + $ s1: 0x78
			- The MIPS is **Big endian**: MSB is at lowest address ⇒ $ s0: 0x12345678
	- lh: load half - sign extended 
		- eg.: lh $ s0, 100($ s1) # copy 2 bytes to $s0 and extend signed bit 
		- The address of the right and left half must be an even number. (constraints)
		- 100 + $ s1: 0xCA
		- 101 + $ s1: 0xFE
		- ⇒ 0xCAFE = 1100-1010-1111-1110 (base 2) ⇒ $ s0 = 0xFFFFCAFE (we replicate the MSbit - complements of the number - so we duplicate the 0)
		- Xem hình trong attachments
	- lhu: load half unsigned - zero extended 
		- eg.: lhu $ s0, 100($ s1) # copy 2 bytes to $s0 and extend signed bit 
		- The address of the right and left half must be an even number. (constraints)
		- 100 + $ s1: 0xCA
		- 101 + $ s1: 0xFE
		- ⇒ 0xCAFE = 1100-1010-1111-1110 (base 2) ⇒ $ s0 = 0x0000CAFE
	- lb: load byte - sign extended - No constraints
	- lbu: load byte unsigned - zero extended  - No constraints
	- Special case: lui - load upper immediate 
		- eg.: lui $ s0, 0x1234 # $s0 = 0x12340000
		- Copy the intermediate number to the left half, and the other numbers are zero.
___
# Store Instructions
- **Remind**: “store” means copying data from a register to memory. 
- Instructions: 
	- sw: store word - must be a 4-digit 4 number. (constraints)
	- eg.: sw $ s0, 100($ s1) # copy 4 bytes in $s0 to memory 
	- sh: store half - **two least significant bytes** - must be an even number. (constraints)
		- eg.: sh $ s0, 100($s1) # copy 2 bytes in $s0 to memory 
	- sb: store byte - **the least significant byte** 
		- eg.: sb $ s0, 100($s1) # copy 1 bytes in $s0 to memory
___
# 3rd Group: Logical instructions
 - Instruction format: The same as arithmetic instructions
 - Bitwise manipulation
	 - Process operands bit by bit

| Operation   | C Operation | MIPS opcode | Explain                                                                                              | Example                      |
| ----------- | ----------- | ----------- | ---------------------------------------------------------------------------------------------------- | ---------------------------- |
| Shift left  | >>          | sll         | Shift the value in the first source to the left and fill the least significant positions with 0 bits | $s0, $s1, 4 # $s0 = $s1 << 4 |
| Shift right | <<          | srl         | Shift the value in the first source to the right and fill the most significant positions with 0 bits | $s0, $s1, 4 # $s0 = $s1 >> 4 |
| AND         | &           | and, andi   |                                                                                                      |                              |
| OR          | \|          | or, ori     |                                                                                                      |                              |
| NOT         | ~           | nor         |                                                                                                      |                              |
## Shift Operation
Shift left (sll) :
- The maximum number of bits we can shift is 31 bits.
- Special case: sll by bits multiplies by $2^i$
Shift right (srl):
- The maximum number of bits we can shift is 31 bits.
- Special case: srl by bits divides by $2^i$(unsigned number only)
## AND Operation
Bitwise AND two source operands 
- and: two source registers 
	- e.g., and $s0, $s1, $s2 # $s0 = $s1 & $s2 
- andi: the second source is a short integer number (16 bit) 
	- 16 high-significant bits of the result are 0s 
	- e.g., andi $s0, $s1, 100 # $ s0 = {16’b0,$s1(5:0)&100} 
- Useful to mask bits in a register:
	- Select some bits and clear others to 0
## OR Operation
Bitwise OR two source operands 
- or: two registers 
	- e.g., or $s0, $s1, $s2 # $s0 = $s1 | $s2 
- ori: the second source is a short integer number (16 bit) 
	- Copy 16 high-significant bits from the first source to the destination. 
	- e.g., ori $s0, $s1, 100 # $ s0 = {$ s1(31:16),$ s1(15:0)|100} 
- Useful to include bits in a word:
	- Set some bits to 1, leave others unchanged.
## NOT Operation
Don’t have a “not” instruction in MIPS ISA:
- 2-operand instruction 
- Useful to invert all bits in a register 
Can be done by the nor operator, a 3-operand instruction 
- a NOR b = NOT (a OR b) 
- NOT a = NOT (a OR 0) = a NOR 0 
- e.g., nor $s0, $s0, $zero 
- What else?
___
# 4th Group: Conditional Branch Instructions
- Branch to a label if a condition is true; otherwise, continue sequentially. 
- Only two standard conditional branch instructions 
	- beq $rs, $rt, L1 # branch if equal 
		- If (rs == rt), go to L1 
	- bne $rs, $rt, L1 
		- If (rs != rt), go to L1 
- Label: a given name format: `<label>: <instruction>`
![[Branch Instructions.png ]]
___
# 5th Group: Unconditional Jump Instructions
Immediately jump to a label:
- Without any condition checked 
- Three standard unconditional jumps:

# Set-on-less than instruction
Used for comparing less than or greater than: Results (destination registers) are always 0 (false) or 1 (true) 
- slt $rd, $rs, $rt: if (rs < rt) rd = 1; else rd = 0; 
- slti $rt, $rs, immediate: if (rs < immediate) rt = 1; else rt = 0; 
- sltu $rd, $rs, $rt: Values are unsigned numbers 
- sltui $rt, $rs, immediate: Values in registers & immediate are unsigned numbers
