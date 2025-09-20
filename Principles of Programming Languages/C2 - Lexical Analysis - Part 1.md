#ppl 
___
# Lexical Analysis
___
*First phase* of the general translator
![[FE Overview.png]]
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
- Translate into the derivation tree (process of derivation). Step-by-step instructions to produce the instruction again
**Semantic Analysis:** Check type relations + consistent rules (grammar we already defined)
**Symbol Table:** contains all the units/instances that the Lexical Analysis generate
## Why separate lexical analysis from parsing?
- Simplication of design: simplify both the lexical analysis and the syntax analysis
- Efficiency: specialised techniques can be applied to improve lexical analysis
- Portability: only the scanner needs to communicate with the outside
## Lexical Analyser
- The first phase of a compiler.
- Scans the input string in the source program, identifies the **patterns of lexemes**, and converts them into *tokens*.
- **Non-Token elements**: whitespaces, tabs, newlines
- **Lexeme**: a *sequence*(order) of characters that together form a pattern and is recognised as a token. (units/instances)
	- Ex: `if()` is the pattern of lexemes, the character like `i` is the lexeme.
- **Pattern**: defines the *general rule* for what sequences of characters are valid.
- A **token** is a *kind of lexeme* that has a *valid pattern*. 
	- Satisfy two conditions: a valid pattern and lexemes
	-  In a programming language: identifier, integer, keyword, whitespace, …
	- Form: $<token-name, attribute-value>$
**Input:** source program → **Output**: Tokens
![[Lexical Analyser.png]]
Roles:
- Identify lexemes: a substring of the source program that belongs to a grammar unit
- Return tokens: a lexical category of lexemes
- Ignore spaces such as blank, newline, tab
- Record the position of tokens that are used in the next phases
## Why do we need a Lexical Analyser?
![[Lexical Parser.png]]
# Building a Lexical Analyser
___
## State Diagram
- State diagrams are representations of a class of mathematical machines called finite automata.
	- Making a transition between states
- Finite automata can be designed to recognise members of regular languages.
- The tokens of a programming language are a regular language, and a lexical analyser is a finite automaton.

# Finite Automata: DFA & NFA
___
- Finite Automata returns: **Accepts or rejects** the sequence of characters, concepts of the state diagram 
- 
