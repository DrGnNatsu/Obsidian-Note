---
tags:
  - "#ppl"
  - "#semantic_analysis"
---
>[!important] 
>How does the compiler know the sentences have a meaning?
# Recall Last Lecture (Derivations and Parse Trees)
Grammar Example: $E \rightarrow E+E \mid E*E \mid (E) \mid a$
- The previous lecture covered building a **Derivation Tree** for strings like $a+a*a$.
- Derivations can be **leftmost** (replacing the leftmost non-terminal) or **rightmost**.
- For $E \rightarrow E+E \mid E*E \mid (E) \mid a$, the string $a+a*a$ has **two distinct leftmost derivations and, consequently, two distinct derivation trees** (page 6).
___
# Ambiguous Definition
A context-free grammar $G$ It is **ambiguous** if some string $w \in L(G)$ has:
1.  Two or more **derivation trees**.
2.  Two or more **leftmost derivations** (or rightmost). 
> [!question] Why is Ambiguity Bad?
Ambiguity is **bad for programming languages** because it leads to different interpretations (e.g., different evaluation results for the same expression).
- Example $2+2*2$ results in 6 (if addition binds looser) or 8 (if multiplication binds looser), depending on the parse tree. 
- **Goal**: Remove ambiguity!
## Fixing Ambiguity 
**Example** $E \rightarrow E+E \mid E*E \mid (E) \mid a$
> Ambiguity is fixed by imposing structural constraints, often based on operator precedence and associativity, which results in a **non-ambiguous grammar**.
![[Ambiguity CFG.png]]
**New Non-Ambiguous Grammar (Preserving Precedence where $*$ binds tighter than $+$):**
- Non-terminals: $\{E, T, F\} \in V$ (where E means Expression, T means Term, F means Factor)
> [!tip] Fixing ambiguity
If the precedence is higher, we can nest it inside the lower precedence.
- Rules (in order of priority, highest first):
    - $E \rightarrow E + T$ 
    - $E \rightarrow T$
    - $T \rightarrow T * F$
    - $T \rightarrow F$
    - $F \rightarrow (E)$
    - $F \rightarrow a$
This non-ambiguous grammar yields a **unique derivation tree** for the string $a+a*a$.
> [!note] Order of Associativity
> If we change $E \rightarrow E + T$ to $E \rightarrow T+ E$ The associativity is different, which means $a+b+c = (a+b)+c = a+(b+c)$
## Case Study: Ambiguous Grammar (Dangling Else)
The grammar structure $S \rightarrow \text{if } C \text{ then } S \mid \text{if } C \text{ then } S \text{ else } S \mid \text{OTHER}$ is ambiguous because an `else` can match the closest unmatched `then` or an outer `then`.
- Typically, the desired interpretation is that the `else` matches the **closest unmatched `then`**.
- This preference can be enforced in the grammar using constructs like **MIF** (Matched If-Then-Else) and **UIF** (Unmatched If-Then-Else). 
___
# Abstract Syntax Tree (AST)

## Definition
An **Abstract Syntax Tree (AST)** is a tree representation of the **abstract syntactic structure** of source code.
- Each node denotes a construct occurring in the source code.
- Its purpose is to **abstract away from the concrete syntax** (like parentheses, semicolons) and represent the **logical structure**.
- Eliminate non-necessary elements.
## Concrete Tree vs. AST
- A **Parse Tree** (Concrete Syntax Tree) shows *exactly* how the text was derived, including all syntactic details (like parentheses, single-successor nodes). (Slide 25)
- An **AST** retains only the **essential structure** of the input, making it more useful for semantic analysis. (Slide 26)

## Building an AST using Semantic Actions
- Typically done through **semantic actions** associated with grammar productions.
- This is called **syntax-directed translation**.
- **Semantic Actions**: Code associated with a production $X \rightarrow Y_1 \ldots Y_n \{\text{action}\}$ that executes when that production is used during parsing.

## Attributes and Actions
- **Semantic Actions:** Each grammar symbol may have **attributes** (a property of the construct).
    - For terminals, the attribute (e.g., `val`) is the associated lexeme (calculated by the lexer).
    - For non-terminals, the attribute is computed from the subexpressions' attributes.
- The action can refer to or compute symbol attributes.
> [!note] Meaning of the symbols
> Everything needs to be defined. Example: ‘+’ is not the plus operator; we need to define it.

## Example: Calculating Expression Value
Grammar: $E \rightarrow \text{int} \mid E + E \mid (E)$
Annotated with actions to compute the value (`.val` attribute):
- $E \rightarrow \text{int} \implies \{E.\text{val} = \text{int}.\text{val}\}$
- $E \rightarrow E_1 + E_2 \implies \{E.\text{val} = E_1.\text{val} + E_2.\text{val}\}$

## Semantic Actions: Dependencies
Semantic actions specify a system of equations whose order of execution is *not* specified by the action definition itself.
- If $E_3.\text{val} = E_4.\text{val} + E_5.\text{val}$, then $E_3.\text{val}$ **depends** on $E_4.\text{val}$ and $E_5.\text{val}$.
	- ==NOTE==: the $+$ is not the plus the operation ,so we write the above sentences “$E_3.\text{val}$ **depends** on $E_4.\text{val}$ and $E_5.\text{val}$.” not “$E_3.\text{val}$ **depends** on $E_4.\text{val}$ *PLUS* $E_5.\text{val}$.”
- The **parser must find the order of evaluation** that satisfies these dependencies.

## Dependency Graph
- A graph is built where each non-terminal node $E$ has a slot for its $\text{val}$ attribute, showing dependencies via dashed lines. (Slide 34)
___
# Summary
- Syntax analysis (**parsing**) extracts structure from tokens.
- Languages are specified by **context-free grammars (CFGs)**.
- A **parse tree** shows derivation; ambiguity exists if a string has multiple derivation trees (or multiple leftmost derivations).
- Ambiguity must be eliminated by hand, often by refining the grammar.
- **Abstract Syntax Trees (ASTs)** capture the essential logical structure, abstracting away concrete syntax.
- **Semantic actions** build ASTs by executing code associated with productions, requiring the parser to determine the correct evaluation order based on attribute dependencies.