#DSA #Technique #Backtracking #When 
___
==**Reference link**==: [Backtracking](https://www.geeksforgeeks.org/backtracking-algorithms/)
___
# What is Backtracking?
**Backtracking** is an algorithmic problem-solving technique that involves incrementally finding a solution by experimenting with **different options** and **undoing** them if they lead to a **dead end**.

It is commonly used to explore multiple possibilities to solve a problem, such as searching for a path in a maze or solving puzzles like ***Sudoku***. When a dead end is reached, the algorithm backtracks to the previous decision point and explores a different path until a solution is found or all possibilities have been exhausted.
___
# How Does a Backtracking Algorithm Work?
A ***backtracking algorithm*** works by recursively exploring all possible solutions to a problem. It starts by choosing an initial solution, and then it explores all possible extensions of that solution. If an extension leads to a solution, the algorithm returns that solution. If an extension does not lead to a solution, the algorithm backtracks to the previous solution and tries a different extension.

The following is a general outline of how a backtracking algorithm works:
1. Choose an initial solution.
2. Explore all possible extensions of the current solution.
3. If an extension leads to a solution, return that solution.
4. If an extension does not lead to a solution, backtrack to the previous one and try a different one.
5. Repeat steps 2-4 until all possible solutions have been explored.
## Example of Backtracking Algorithm
***Example:*** Finding the shortest path through a maze
***Input:*** A maze is represented as a 2D array, where ***0*** represents an open space, and ***1*** represents a wall.
***Algorithm:***
1. Start at the starting point.
2. For each of the four possible directions (up, down, left, right), try moving in that direction.
3. If moving in that direction leads to the ending point, return the path taken.
4. If moving in that direction does not lead to the ending point, backtrack to the previous position and try a different direction.
5. Repeat steps 2-4 until the ending point is reached or all possible paths have been explored.
___
# When to Use a Backtracking Algorithm?
Backtracking algorithms are best used to solve problems that have the following characteristics:
- There are multiple possible solutions to the problem.
- The problem can be broken down into smaller subproblems.
- The subproblems can be solved independently.
___
# Applications of Backtracking Algorithm?
- Solving puzzles (e.g., Sudoku, crossword puzzles)
- Finding the shortest path through a maze
- Scheduling problems
- Resource allocation problems
- Network optimization problems
- Combinatorial problems, such as generating permutations, combinations, or subsets.