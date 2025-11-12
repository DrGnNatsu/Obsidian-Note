---
tags:
  - data_mining
---

# What Is Frequent Pattern Analysis?

## Frequent Pattern Definition
A **frequent pattern** is a pattern (a set of items, subsequences, substructures, etc.) that occurs frequently in a data set.
- First proposed by Agrawal, Imielinski, and Swami [AIS93] in the context of frequent itemsets and association rule mining.
- **Motivation**: Finding inherent regularities in data (e.g., "What products were often purchased together?—Beer and diapers?!").
- **Applications**: Basket data analysis, cross-marketing, catalog design, sale campaign analysis, Web log analysis, and DNA sequence analysis.
## Why Is Frequent Pattern Mining Important?
Frequent patterns are an intrinsic property of datasets and form the foundation for many data mining tasks:
- Association, correlation, and causality analysis.
- Sequential, structural (e.g., sub-graph) patterns.
- Pattern analysis in spatiotemporal, multimedia, time-series, and stream data.
- Classification (discriminative, frequent pattern analysis).
- Cluster analysis (frequent pattern-based clustering).
- Data warehousing (iceberg cube and cube-gradient).
- Semantic data compression (fascicles).

# Basic Concepts: Frequent Patterns
## Itemset
- **Itemset**: A set of one or more items.
- **k-itemset $X = \{X_1, \ldots, X_k\}$**.
- **Support Count (Absolute Support)**: Frequency/occurrence of an itemset $X$.
- **Relative Support ($s$)**: Fraction of transactions containing $X$ (probability that a transaction contains $X$).
	- Example: Sup(nuts) = 3 /5 ( three sets contain nuts / five sets)
- An itemset $X$ is **frequent** if its support is no less than a **minsup** threshold.
## Basic Concepts: Association Rules
Rules are of the form $X \Rightarrow Y$ (where $X$ and $Y$ are itemsets, $X \cap Y = \emptyset$).
- **Support ($s$)**: Probability that a transaction contains $X \cup Y$.
- **Confidence ($c$)**: Conditional probability that a transaction containing $X$ also contains $Y$.
If $\text{minsup} = 50\%$ and $\text{minconf} = 50\%$:
- Frequent Patterns found include: $\text{\{Beer, Diaper\}}: 3$, $\text{Beer}: 3$, $\text{Diaper}: 3$
- Association rules can be generated, e.g., $\text{Beer} \Rightarrow \text{Diaper}$ ($60\%$ support, $100\%$ confidence).
## Closed Patterns and Max-Patterns
Mining all patterns leads to a combinatorial explosion (e.g., $2^{100}$ patterns).
**Solution**: Mine **closed patterns** and **max-patterns** instead.
- **Closed Itemset $X$**: $X$ is frequent, and there exists **no super-pattern $Y \supset X$ with the same support as $X$**. (Page 8)
- **Max-pattern $X$**: $X$ is frequent, and there exists **no frequent super-pattern $Y \supset X$**. (Page 8)
- Closed patterns provide a lossless compression of frequent patterns.
**Exercise Example (Page 9)**: Given transactions $\langle a_1, \ldots, a_{100} \rangle$ and $\langle a_1, \ldots, a_{50} \rangle$ with $\text{min\_sup}=1$:
- Closed itemsets: $\{a_1, \ldots, a_{100}\}$ (sup: 1) and $\{a_1, \ldots, a_{50}\}$ (sup: 2).
- Max-pattern: $\{a_1, \ldots, a_{100}\}$ (sup: 1).
___
# Frequent Itemset Mining Methods
## Scalable Frequent Itemset Mining Methods
Approaches to efficiently find frequent itemsets:
1.  Apriori: A Candidate Generation-and-Test Approach.
2.  Improving the Efficiency of Apriori.
3.  FPGrowth: A Frequent Pattern-Growth Approach.
4.  Mining Close Frequent Patterns and Maxpatterns.
## 1. Apriori: A Candidate Generation & Test Approach ( thi)
- **Apriori Pruning Principle**: If any $k$-itemset is infrequent, its supersets should not be generated/tested. (Downward Closure Property: Any subset of a frequent itemset must also be frequent.)
	- Example: $\text{\{Beer, Diaper, Nuts\}}: \text{frequent}$ so $\text{\{Beer,  Nuts\}}: \text{frequent}$
- **Method**:
    1. Scan DB once for frequent 1-itemsets ($L_1$).
    2. **Generate** length $(k+1)$ candidates ($C_{k+1}$) from $L_k$.
    3. Remove the $(k-itemset)$ is not frequent
    4. **Test** candidates against the DB.
    5. Terminate when no new frequent set is found.
- **Implementation Example**: Shows candidate generation ($C_2, C_3$) and pruning steps based on the Apriori principle. Complete itemsets: {A}, {B}, {C}, {E}, {A, C}, {B, C}, ... all the satisfy $sup \geq sup_{min}$.
![[Aproiri Algo.png]]
- **Pseudo-Code**: Iteratively generate $C_{k+1}$ from $L_k$ and test against the database. (Page 29)
### Improving the Efficiency of Apriori
Major challenges addressed: multiple DB scans, huge candidate sets, tedious support counting.
Ideas: Reduce passes, shrink candidates, facilitate support counting.
- **Partitioning**: Scan the database twice. Scan 1 finds local frequent patterns in partitions ($DB_i$); Scan 2 consolidates results. (Page 36)
- **Reducing Candidates (Hash Tree)**: Store candidates in a hash-tree to efficiently count supports within a transaction using a subset function. (Pages 31, 32)
- **SQL Implementation**: Uses object-relational extensions (UDFs, Table functions) for efficient candidate generation and pruning. (Page 33)
## 2. FP-Growth: A Frequent Pattern-Growth Approach
- **Philosophy**: Grow long patterns from short ones using local frequent items only, **avoiding explicit candidate generation**. (Page 42)
- **Method**:
    1. Scan DB once to find frequent 1-itemsets and create the **FP-tree** structure (Page 43).
    2. **Recursively** grow patterns by constructing conditional pattern bases and conditional FP-trees for each frequent item.
- **Benefits of FP-tree Structure**: Completeness, Compactness (infrequent items pruned), Never needs repeated scans of the entire database. (Page 49)
- **Recursion**: Mining is done by recursively analyzing conditional FP-trees. (Page 47)
### Scalability Comparison
Graphs show FP-Growth runtime significantly lower than Apriori, especially as support threshold decreases (Page 53) and the dataset size increases (Page 54).
## 3. Mining Closed Frequent Patterns and Maxpatterns
- **CLOSET**: Mines **closed itemsets** using a pattern-growth approach, leveraging itemset merging and sub-itemset pruning. (Page 59)
- **MaxMiner**: Mines **max-patterns** by finding frequent items first, then checking support for potential supersets, pruning if a length-2 subset is not frequent. (Page 61)
___
# Which Patterns Are Interesting?—Pattern Evaluation Methods

## Interestingness Measure: Correlations (Lift)
- Simple support/confidence can be misleading (e.g., if an item is already very common).
- **Lift** measures dependency/correlation:
$$\text{lift}(X, Y) = \frac{P(X \cup Y)}{P(X)P(Y)}$$
- If $\text{lift} > 1$, the events are positively correlated (e.g., $\text{lift}(\text{Diaper} \rightarrow \text{Beer}) = 1.33$). (Page 64)

## Null-Invariant Measures
A table summarizing properties (like symmetry, inversion invariance) satisfied by various interestingness measures ($\phi$, $\lambda$, odds ratio, Gini index, **Confidence**, Lift, etc.). (Page 65)