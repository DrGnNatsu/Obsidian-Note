---
tags:
  - ppl
---
___
# Recall: Computer Architecture
- The underlying architecture consists of:
    - **CPU**: Containing the Control Unit and the Logic Unit.
    - **Memory**: For storing data and instructions.
    - **Input/Output**: Interfaces for interaction.
# Code Generation Goals
There are two primary goals in code generation:
1.  **Correctness**: The generated code must accurately represent the source program's logic.
2.  **Speed**: The generated code should execute efficiently.

*Note*: Most complications in code generation arise from the effort to be fast as well as correct.
# Example: C-like Code
```c
int add(int a, int b) {
 int result = a + b;
 return result;
}

int main() {
 int x = 5, y = 10;
 int sum = add(x, y);
 print(sum);
 return 0;
}
```

# Procedure Activations
- The execution of an action within a procedure $P$ is called an **activation** of $P$.
- Each activation has its own **context** and **data**.
- The **lifetime** of an activation of $P$ includes:
    - All steps required to execute $P$.
    - All steps in procedures that $P$ calls.
- **Activation Tree**: A graphical representation of the flow of execution, where each node depicts a particular procedure activation.
# Activation Trees
- **Benefits**:
    - Represent the Runtime Call Relationships.
    - Track Recursion.

# Stack Machines
A stack machine is a computational model that uses a **stack data structure** to manage:
- Procedure activations.
- Local variables.
- Control flow (e.g., return addresses).
## Stack Machine Operations
- Each node in the activation tree corresponds to a **stack frame (activation record)** in the stack.
- Edges in the activation tree represent call and return operations.
- **Instruction Execution**:
    - Takes operands from the **top of the stack**.
    - Removes those operands.
    - Computes the required operation.
    - Pushes the result back onto the stack.
## Example: Stack Machine Instructions
Consider two instructions:
- `push i`: Place integer `i` on top of the stack.
- `add`: Pop two elements, add them, and push the result back.

**Program to compute 7 + 5:**
```
push 7
push 5
add
```

## Why use Stack Machines?
- Operations take operands from the same place and put results in the same place.
- This allows for a **uniform compilation scheme**.
# From Stack Machines to Microprocessor
- Compilers often generate code for a virtual **stack machine with an accumulator**.
- To run this on a real processor (like MIPS), we must **simulate** the stack machine instructions using MIPS instructions and registers.
## Simulating a Stack Machine
- **Accumulator**: Use MIPS register `$a0` to hold intermediate results.
- **Stack**: Use a portion of memory.
- **Stack Pointer (`$sp`)**: Manages the top of the stack. It keeps the address of the next location on the stack. The actual top of the stack data is at `$sp + 4`.
# MIPS Assembly Overview
- **Architecture**: RISC (Reduced Instruction Set Computer).
- **Arithmetic**: Uses registers for operands and results.
- **Memory Access**: Explicit load (`lw`) and store (`sw`) instructions.
- **Registers**: 32 general-purpose registers (32 bits each).
    - We specifically use: `$sp` (stack pointer), `$a0` (accumulator), `$t1` (temporary).
## Sample MIPS Instructions
- `lw reg1 offset(reg2)`: Load word from `address = reg2 + offset` into `reg1`.
- `sw reg1 offset(reg2)`: Store word from `reg1` to `address = reg2 + offset`.
- `add reg1 reg2 reg3`: `reg1 = reg2 + reg3`.
- `addiu reg1 reg2 imm`: `reg1 = reg2 + immediate` (unsigned addition).
- `li reg imm`: Load immediate value `imm` into `reg`.
## Example: Simulating `7 + 5` in MIPS
| Stack Machine Code | MIPS Assembly Code | Meaning |
| :--- | :--- | :--- |
| `acc <- 7` | `li $a0 7` | Load 7 into accumulator |
| `push acc` | `sw $a0 0($sp)`<br>`addiu $sp $sp -4` | Store acc on stack<br>Decrement stack pointer |
| `acc <- 5` | `li $a0 5` | Load 5 into accumulator |
| `acc <- acc + top_of_stack` | `lw $t1 4($sp)`<br>`add $a0 $a0 $t1` | Load value from stack to temp<br>Add temp to acc |
| `pop` | `addiu $sp $sp 4` | Increment stack pointer (pop) |
# The Activation Record (AR)
- An **Activation Record** is a block of memory allocated on the stack during a procedure's execution.
- It contains all information needed to manage a single activation.
- The structure includes:
    - **Return Address**: Where to go after function completion.
    - **Saved Frame Pointer**: Previous frame pointer.
    - **Function Parameters**: Arguments passed.
    - **Local Variables**: Variables local to the function.
    - **Saved Registers**: Registers preserved across calls.
## Managing the AR
- **Stack Discipline**: On function exit, `$sp` must be the same as on entry.
- **Frame Pointer (`$fp`)**: A stable reference point within the stack frame, distinct from the frequently changing stack pointer (`$sp`). It remains constant during execution to access locals/parameters easily.
## AR Layout Example
Consider a call to `f(x, y)`. The AR might look like:
```
| ...      |
| old fp   |
| y        |
| x        |
| return   | <-- FP points near here
| ...      | <-- SP changes below here
```
# Code Generation Strategy
- For each expression `e`, we generate MIPS code that:
    - Computes the value of `e` into `$a0`.
    - Preserves `$sp` and the stack contents.
- We define a function `cgen(e)` which outputs this code.
## Code Generation for Constants
To evaluate a constant `i`:
- `cgen(i) = li $a0 i`
- This simply loads the value into the accumulator and preserves the stack.
## Code Generation for Add (`e1 + e2`)
The code generation function `cgen(e1 + e2)` is defined recursively:
1.  **Generate code for `e1`**: `cgen(e1)` (Result is in `$a0`).
2.  **Push result**:
    - `sw $a0 0($sp)`
    - `addiu $sp $sp -4`
3.  **Generate code for `e2`**: `cgen(e2)` (Result is in `$a0`).
4.  **Load `e1` result**: `lw $t1 4($sp)` (Retrieve from stack).
5.  **Add**: `add $a0 $t1 $a0` (Add popped value to `$a0`).