---
tags:
  - "#ppl"
---
References: [[C5 - Syntax Analysis]]
___
# Linear vs Non-linear CFG

| Linear CFG                                                                            | Non-linear CFG                                                                                                                                           |
| ------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Production rules have **at most one non-terminal (variable)** on the right-hand side. | Production rules have **more than one non-terminal** on the right-hand side. We need to consider the implementation strategies: leftmost, rightmost, ... |

In CFGs that are not linear, a derivation may involve sentential forms with multiple variables.
*Example*
1. $S \rightarrow AB$
2. $A \rightarrow aaA$
3. $A \rightarrow \lambda$
4. $B \rightarrow Bb$
5. $B \rightarrow \lambda$
Language generated: $L(G) = \{a^{2n}b^m: n \ge 0, m \ge 0\}$ 
Example: $w = aaaab$

| Rules LM                | Current String LM | Rules RM                | Current String RM | Call            |
| ----------------------- | ----------------- | ----------------------- | ----------------- | --------------- |
| $S \rightarrow AB$      | $AB$              | $S \rightarrow AB$      | $AB$              | Sentential form |
| $A \rightarrow aaA$     | $aaAB$            | $B \rightarrow Bb$      | $ABb$             | Sentential form |
| $A \rightarrow aaA$     | $aaaaAB$          | $B \rightarrow \lambda$ | $Ab$              | Sentential form |
| $A \rightarrow \lambda$ | $aaaaB$           | $A \rightarrow aaA$     | $aaAb$            | Sentential form |
| $B \rightarrow Bb$      | $aaaaBb$          | $A \rightarrow aaA$     | $aaaaAb$          | Sentential form |
| $B \rightarrow \lambda$ | $aaaab$           | $A \rightarrow \lambda$ | $aaaab$           | Sentence        |

**COMPARING LM and RIGHT MOST**:
- Number of steps: may equals or not equals
- Derivation Process: Different
- Start and End string is the same.
___
# Derivation and Parse Tree
___
## Derivation
A **derivation** is a sequence of productions.
Example: $S \rightarrow L \rightarrow L \rightarrow L$
## Parse Tree (**Derivation Tree**)
A derivation can be drawn as a tree:
- The start symbol is the tree's root.
- For a production $X \rightarrow Y_1 L Y_n$, add children $Y_1 L Y_n$ to node $X$. (Slide 5)

A **parse tree** (or derivation tree) is a tree representation of the **syntactic structure** of a string according to a CFG. It illustrates how the start symbol is transformed into the string by applying production rules.
### Definition - Parse Tree
Let $G = (V, T, S, P)$ be a CFG. An ordered tree is a **derivation tree** for $G$. If It has the following properties (Slide 8):
1. The **root** is labeled $S$.
2. Every **leaf** has a label from $T \cup \{\lambda\}$.
3. Every **internal vertex** has a label from $V$.
4. If a vertex has a label $A \in V$, and its children are labeled $a_1, a_2, \ldots, a_n$, then $P$ must contain a production $A \rightarrow a_1 a_2 \ldots a_n$.
5. A leaf labeled $\lambda$ has no siblings.
### Examples
Illustrating derivation steps corresponding to parse tree construction.
![[Parse Tree.png]]
### Left-most vs. Right-most Derivations
- **Leftmost derivation**: At each step, replace the **leftmost** non-terminal.
- **Rightmost derivation**: At each step, replace the **rightmost** non-terminal.
### Derivation and Parse Tree Relationship
- Right-most and left-most derivations have the **same parse tree** (100% the same).
- The difference lies in **the order** in which branches are added.
### Partial Derivation Trees
- If $t_G$ iI any partial derivation tree for $G$ whose root is labeled $S$, then the yield of $t_G$ is a **sentential form** of $G$. (Slide 30)
- **Yield**: The string formed by the leaves of the tree (reading order matters). (Slide 25 illustrates yield calculation).
### Sentential Form
Let $G = (V, T, S, P)$ be a CFG. Then for every $w \in L(G)$, there exists a derivation tree of $G$ whose **yield is $w$**. Conversely, the yield of any derivation tree is in $L(G)$. (Slide 30)
Sometimes, derivation order doesn't matter, resulting in the **Same derivation tree** (Slide 31).