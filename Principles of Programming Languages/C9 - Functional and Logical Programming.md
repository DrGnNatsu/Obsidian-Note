---
tags:
  - ppl
---

___
# Main Programming Styles
In Software Engineering, there are two main programming styles:
1.  **Imperative** programming styles
2.  **Declarative** programming styles
## Imperative vs. Declarative
- **IMPERATIVE PROGRAMMING**:
    - A programmer describes **how** to solve a problem using instructions that change the program's **state**.
    - Execution is sensitive to the current state.
    - **State**: Data stored in variables, structures, or external sources.
    - **Program**: Collection of instructions (assignments, changes to mutable data).
- **DECLARATIVE PROGRAMMING**:
    - A programmer describes **what** relationships hold between various entities.
    - **Program**: Collection of definitions of functions or relations.
**Sample Problem Comparison (Calculating Sum):**
- Imperative style (Python): Uses loops and explicit state mutation (`sum += number`).
	- How to get the sum: we need to sum all of the elements step-by-step.
- Declarative style (SQL): Describes the desired result (`SELECT SUM(number) FROM numbers_table;`).
	- How to get the sum: just write the function sum
## Main Programming Styles Categorization
- **Two imperative styles**: Procedural Programming, Object-Oriented Programming.
- **Two declarative styles**: Functional Programming (with functions - relationships between functions), Logic Programming (with relations (entities) - relationships between classes).

# Functional Programming Languages

## Characteristics of Functional Programming
- First-class functions
- Higher-order functions
- Immutable data
- Pure functions
- Recursion
- Manipulation of lists
- Lazy Evaluation

>[!note] Meaning of functional programming
>Combines all functions to build new behaviour.
## What is functional programming?
- A style emphasising **function application** and **function composition**.
- Aims to **mimic mathematical functions** (a mapping from a domain set to a range set).
	- Example $f(x)=x^2+1$
	- $x$ is the domain set. The unique $x$ is only getting one value in the range set.
	- $f(x)$ is the range set
- Three components:
	- What are the variables? (LHS)
	- What is the functional requirement (function definition)? (RHS)
	- What is the function application (function call)? → How to use it and when we use it?
	
>[!important] Functional programming
>Just care about the input to get the output. Do not care about how to get that output.
## Functional Programming Language Types
- **First-order programming languages**: *Functions cannot be passed as arguments, returned from other functions, or assigned to variables*. Primary entities are basic data types (e.g., FORTRAN, COBOL, Assembly). 
	- The function name can not work as arguments
- **Higher-order programming languages**: Functions **can** be passed as parameters or returned as results (e.g., Lisp).
## Lisp Example
- **First Language** applies **Higher-Order Language**.
- Data objects: originally only **atoms** (numbers, symbols, strings) and **lists** (sequences of elements).
- List form: parenthesised collections of sublists and/or atoms, structured using `<data, pointer>` elements (linked lists). 
- Functions are defined using `(function_name parameter1 ... parameterN)` syntax, and functions can be referenced via `(LAMBDA ... expression)`. (Page 17)
- Higher-order functions demonstrated: `apply-twice` (takes a function as an argument) and `create-multiplier` (returns a function). (Pages 18, 19)
## Function Forms
Key concepts include: `lambda`, `map`, `reduce`, `compose`, `filter`, `any`, `all`, and `currying`.

# Logical Programming

## What is Logical Programming?
- **Definition**: A paradigm based on **formal logic**.
- Programs consist of **facts** and **rules**.

- Computation is the process of **querying the knowledge base**.
- **Key Features**: Declarative in nature, problem-solving through **logical inference**.
## Applications of Logical Programming
- Natural Language Processing (NLP) (Speech Recognition, Chatbots, Text Extraction, Document Classification, AutoCorrection, Language Translation) (Page 24).
- Expert systems.
- Robotics.
- Intelligent Tutoring Systems
- Game AI
## Core Concepts (Prologue)
- **Prologue** (): Popular language for logical programming, used for knowledge representation and reasoning.
- **Basic Structure**: Facts, Rules, Queries.
	- Facts: _“các mệnh đề luôn đúng, vô điều kiện.”_  Trong lập trình hàm (Functional Programming – FP), mục tiêu là viết ra các đoạn code **hoạt động giống như các mệnh đề luôn đúng** → **Dự đoán được, không thay đổi, luôn cho cùng một kết quả.**
		- Could be statements
		- Need to be declared
	- Rules: define the logical relationships between the facts.
	- Queries: a combination of facts and rules.
	- Example:
		- `parent(john, mary).` → John is the parent of Mary.
		- `ancestor(X, Y) :- parent(X, Y).` → X là tổ tiên của Y nếu X là cha/mẹ của Y.
			- General Structure: `Head:- Body.` Read: The head is true if the body is true.
		- `?- ancestor(john, mary).` → The queries will answer true or false based on facts and rules. In this case is true.
	- How do it works?
		- Prolog nhận truy vấn `ancestor(john, mary)`.
		- Nó tìm rule có dạng `ancestor(X, Y) :- ...`.
		- Quy tắc nói `ancestor(X, Y)` đúng nếu `parent(X, Y)` đúng.
		- Prolog kiểm tra `parent(john, mary)` → thấy fact này tồn tại.
		- Điểm khớp → rule đúng → trả về **true**.
- **Syntax**: Facts end with a period (`.`), rules use`:-` (implication), queries start with `?-`.
### Unification (Facts have variable undefined)
- Matching patterns in Prologue.
- Variables are **bound** during pattern matching.
- The flowchart illustrates the process: Query Input $\rightarrow$ Match $\rightarrow$ Successful Unification? $\rightarrow$ Return 'Yes' with bindings or 'No'. 
### Backtracking (Queries have variable undefined)
- Prologue systematically explores possible solutions using a search tree. If a path fails to satisfy a query, it **backtracks** to an earlier choice point to try an alternative solution. 
- Using the queries as the root node and travel from the first fact to the end.
## Example: Family Tree (Ancestry using Recursion)
- **Facts**: `parent(john, mary).`, `parent(mary, sarah).`
- **Rules (Recursive Definition)**:
    - `ancestor(X, Y) :- parent(X, Y).` (Base case)
    - `ancestor(X, Y) :- parent(X, Z), ancestor(Z, Y).` (Recursive step)
- **Query**: `?- ancestor(john, sarah).` (Result: Yes, due to $john \rightarrow mary \rightarrow sarah$).