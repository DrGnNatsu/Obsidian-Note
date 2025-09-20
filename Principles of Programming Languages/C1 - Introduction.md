#ppl 
___
# Introduction
# Reason to study PPL
DSL: Internal DSL and External DSL: Domain-specific language: a type of programming language designed for a specific domain or purpose.
- External DSL: You need to build a compiler for that language.
	- Ex: SQL, Latex
- Internal DSL: 
GBL: global purpose languages
# Language Design
# Grading Scheme
# Course Policy
# Compilation Phases
## Implementation Methods
- Interpreters run your program
- Compilers translate your program

| **Compiler**                                                                                                        | **Interpreter**                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Take all the code → Convert code into Machine Language → Give to the system to process → Share output with the user | Take one instruction → Convert code into Machine code → Give to the system to process and generate output → Handle the second instruction |
| Cons: Do not know if the code is wrong                                                                              | Cons: Takes more time                                                                                                                     |
| Pros: Fast                                                                                                          | Pros: know if the code is wrong                                                                                                           |
## Why do we need a translator?
*Translator:* convert a high-level language to machine language
## Compilation Phases
![[Compilation Phases.png]]
**Lexical Analyser:** segment the unit/instance ( identify words)
- Reads the stream of characters and outputs tokens
- Ex: $7 + 3 = 10$
	- The 7, 3, 10 is just the digit
	- “+”, “=“ is the symbol
	- The analyser will separate it into units: “7”, ...
		- Check the validity of the unit (the validity of the unit based on the definition of the language)
**Syntax Analyser:** check whether the entire order of the unit is correct or not
- Check if the sequence is correct
- Ex: $7 \quad 3 + = 10$
	- Between the “+” must be two operands; the sequence is wrong
- Translate into the derivation tree (process of derivation). Step-by-step to produce the instruction again
**Intermediate Code (IC) Generator:**
- Intermediate Code (represented in the tree - abstract syntax tree)
**Code optimiser**: (plus not must) optimise the IC to make it as fast as possible. 
**Code generator**: Have some instructions to translate into the target language. 