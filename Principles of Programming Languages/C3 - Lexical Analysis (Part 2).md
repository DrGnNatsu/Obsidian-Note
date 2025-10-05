#ppl 
___
# The Story so Far
---
- A finite automaton is a **collection of states** joined by transitions. 
- Some state is designed as the start state.
- The automaton processes a string by starting at the initial state and moving along the transitions according to the input symbols.
- If the automaton ends in an accepting state, it will accept the input; otherwise it will rejects the input.

# DFA Definition (Deterministic Finite Automata)
---
A deterministic finite automaton (DFA) is a 5-tuple $M=<Q,\Sigma,\delta,q_0,F>$, which is theoretical model of computation used to recognize patterns within input strings where
- $Q$ is the finite set of **states**.
- $\Sigma$ is the **input alphabet**.
- $\delta: Q \times \Sigma \rightarrow Q$ is the **transition function**.
- $q_0 \in Q$ is the **start state**.
- $F \subseteq Q$ is the set of **accepting states** (or **final states**).

# Why is a DFA Deterministic?
---
- A DFA always begins from **one unique start state**.
- In any given state, when it reads an **input symbol**, the **next state is uniquely determined**.
- For a particular input string, the **entire sequence of transitions is fixed**.
- Therefore, the computation is called a **deterministic computation**.

> At every step, a DFA has exactly one possible move for the given input.

# Alphabet and Formal Language
---
- An **alphabet** $\Sigma$ is a finite non-empty set of symbols. 
- A **word over** $\Sigma$ is a finite sequence of elements from $\Sigma$. The word is the string that only contains a sequence of symbols $\in \Sigma$
- The **empty word** (the empty sequence of elements) is denoted by $\epsilon$.
- ${\Sigma}^*$ denotes the set of all words over $\Sigma$. Including $\Sigma^*=\{\epsilon, \dots\}$
- ${\Sigma}^+={\Sigma}^* \setminus \{\epsilon\}$ denotes the set of all non-empty words over $\Sigma$. Including$\Sigma^*=\{ \dots\}$
- We write $|w|$  for the length of a word $w$, called cardinality/length of word $w$.
- A formal language (over alphabet $\Sigma$) is a subset of ${\Sigma}^*$ (chọn một số chuỗi trong ${\Sigma}^*$ theo luật nào đó.)

# DFA - Recognized Language
---
Let $M$ e a deterministic finite automaton, then the **language recognized by** $M$  is defined as $\mathcal{L}(M) = \{\, w \in \Sigma^* \mid w \text{ is accepted by } M \,\}.$ 

# Formal Language & Regular Expression
---
**Formal language:** A set of "words" (strings) built from those letters, following some rules. Example $L=\{w \in \{0,1\}^* \mid \text{ends with 1}\}$.

**Regular expression:** a compact, rule-based notation used to describe certain formal languages — specifically, those that can be recognized by a DFA. Example $(0 \mid 1)^*1$

# Operations on Language
---

# Transition Table
---
The transition table is a tabular representation of the transition function. It takes two arguments (a state and a symbol) and returns a state (the “next state”).

A transition table is represented by the following things
- Column correspond to input symbols.
- Rows correspond to states.
- Entries correspond to the next stage.
- The start state is denoted by an arrow with no source.
- The accept state is denoted by a star.
# Nondeterministic Finite Automata (NFA)
---
A nondeterministic finite automaton (NFA) is a 5-tuple $M=<Q,\Sigma,\delta,q_0,F>$ where
- $Q$ is the finite set of **states**.
- $\Sigma$ is the **input alphabet**.
- $\delta: Q \times (\Sigma \cup \{\epsilon\}) \rightarrow \mathcal{P}(Q)$ is the **transition function**. (mapping to the power set of $Q$)
- $q_0 \in Q$ is the **start state**.
- $F \subseteq Q$ is the set of **accept states** (or **final states**).
# Epsilon Moves in NFAs
---
- Another kind of transition: $\epsilon$ moves
- Machine can move from state A to state B without reading input.
- Only exist in NFAs

# $\epsilon$ - closure of a State
---
For a state $q \in Q$, we write $E(q)$ to denote the set of states that are reachable from $q$ via $\epsilon$-transition in $\delta$

> For NFA $M=<Q,\Sigma,\delta,q_0,F>$ and state $q \in Q$, state $p$ is in the $\epsilon$-closure $E(q)$ of $q$ if there is a sequence of states $q_0',...q_n'$ with 
> 1. $q_0'=q$
> 2. $q_i' \in \delta(q_{i-1}',\epsilon)$  for all $i \in \{1,...,n\}$
> 3. $q_n'=p$

$q\in E(q)$ **for every state** $q$

# NFA – Accepted Words
---

An NFA $M = \langle Q, \Sigma, \delta, q_0, F \rangle$ **accepts** the word $w = a_1 a_2 \ldots a_n$ if there exists a sequence of states $q'_0, q'_1, \ldots, q'_n \in Q$ such that:
- $q'_0 \in E(q_0)$  
- $q'_i \in \bigcup_{q \in \delta(q'_{i-1}, a_i)} E(q)$ for all $i \in \{1, \ldots, n\}$  
- $q'_n \in F$

# Comparing DFA and NFA
---

| Đặc điểm                                                                         | NFA                                     | DFA                      |
| -------------------------------------------------------------------------------- | --------------------------------------- | ------------------------ |
| Transition cho 1 input tại 1 state                                               | Có thể nhiều hoặc không                 | Chính xác 1              |
| ε-transition (nhảy không cần input)                                              | Có thể                                  | Không có                 |
| Cách hoạt động                                                                   | Máy có thể song song đi nhiều nhận,     | Luôn có 1 đường duy nhất |
| Accept word:. Chỉ cần **1 nhánh** đi đến state chấp nhận, còn lại đếch quan tâm. | Đường duy nhất phải đến state chấp nhận |                          |
# Convert NFA to DFA
![[NFA to DFA.png]]
*Construct the Transition Table of NFA*

| State             | a             | b     |
| ----------------- | ------------- | ----- |
| $\rightarrow q_0$ | $\{q_0,q_1\}$ | $q_0$ |
| $q_1$             | null          | $q_2$ |
| $q_2^*$           | null          | null  |
Problem: same event can go to many stages, and many of cells are null.

*Construct the Transition Table of DFA*

| State             | a             | b             |
| ----------------- | ------------- | ------------- |
| $\rightarrow q_0$ | $\{q_0,q_1\}$ | $q_0$         |
| $\{q_0,q_1\}$     | $\{q_0,q_1\}$ | $\{q_0,q_2\}$ |
| $\{q_0,q_2\}^*$   | $\{q_0,q_1\}$ | $q_0$         |
•  Treat $\{q_0,q_1\}$ as a new stage.
•  Convert the transition function $\delta(\{q_0,q_1\},a)=\delta(q_0,a) \cup \delta(q_1,a)=\{q_0,q_1\} \cup \emptyset=\{q_0,q_1\}$
•  $\delta(\{q_0,q_1\},b)=\delta(q_0,b) \cup \delta(q_1,b)=\{q_0\} \cup \{q_2\}=\{q_0,q_2\}$
•  $\delta(\{q_0,q_2\},a)=\delta(q_0,a) \cup \delta(q_2,a)=\{q_0,q_1\} \cup \emptyset=\{q_0,q_1\}$
•  $\delta(\{q_0,q_2\},b)=\delta(q_0,b) \cup \delta(q_2,b)=\{q_0\} \cup \emptyset=q_0$