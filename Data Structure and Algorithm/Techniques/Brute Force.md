#DSA #Technique #BruteForce #When #Why
___
# What is the Brute Force Algorithm?
A brute force algorithm is a simple, comprehensive search strategy that systematically explores every option until a problem’s answer is discovered. It’s a generic problem-solving approach employed when the issue is small enough to make an in-depth investigation possible. However, because of their high temporal complexity, brute force techniques are inefficient for large-scale problems.

## Key Takeaways
- ***Methodical Listing:** Brute force algorithms investigate every potential solution to an issue, usually in an organised and detailed way. This involves attempting each option in a specified order.
- **Relevance:** When the issue space is small and easily explorable quickly, brute force is the most appropriate method. The temporal complexity of the algorithm becomes unfeasible for larger issue situations.
- ***Not using optimisation or heuristics:*** Brute force algorithms don’t use optimisation or heuristic approaches. They depend on testing every potential outcome without ruling out any using clever pruning or heuristics

## Features of the Brute Force Algorithm
- It is an intuitive, direct, and straightforward technique of [problem-solving](https://www.geeksforgeeks.org/how-to-approach-a-coding-problem/) in which all the possible ways or all the possible solutions to a given problem are enumerated.
- Many problems are solved in daily life using the brute force strategy, such as exploring all the paths to a nearby market to find the shortest path](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/).
- Arranging the books in a rack using all the possibilities to optimise the rack spaces, etc.
- Daily life activities use a brute force nature, even though [optimal algorithms](https://www.geeksforgeeks.org/optimization-techniques-set-1-modulus/) are also possible.

## Applications of Brute Force Algorithm
- **String Matching**: Brute force string matching checks for the occurrence of a substring by comparing it with all possible substrings of the main string.
- **Combinatorial Problems:** Problems like generating permutations, combinations, and subsets can be solved using brute force by exploring all possible configurations.
- **Optimisation Problems:** Finding the maximum or minimum of a function by evaluating it at all possible points, such as the knapsack problem or travelling salesman problem.

## Why Use Brute Force?
1. **Simplicity:** It’s easy to implement and understand.
2. **Completeness:** It guarantees finding a solution if one exists.
3. **Baseline:** It provides a baseline solution against which more complex algorithms can be compared.

## When to avoid Brute Force?
1. The problem size is large.
2. Real-time or near-real-time solutions are required.
3. More efficient algorithms are available (e.g., dynamic programming, greedy algorithms).

___
# Pros and Cons of Brute Force
| Pros                                                                                                                                                                                                                                                                                                                                                                                   | Cons                                                                                                                                                                                                                                                                                                                                                                                                                           |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| - The brute force approach is a guaranteed way to find the correct solution by listing all the possible candidate solutions for the problem.<br>- It is a generic method and not limited to any specific domain of problems.<br>- The brute force method is ideal for solving small and simpler problems.<br>- It is known for its simplicity and can serve as a comparison benchmark. | - The brute force approach is inefficient. For real-time problems, algorithm analysis often goes above the ***O(N!)*** order of growth.<br>- This method relies more on compromising the power of a computer system to solve a problem than on a good algorithm design.<br>- Slow.<br>- Brute force algorithms are not constructive or creative compared to algorithms that are constructed using some other design paradigms. |
