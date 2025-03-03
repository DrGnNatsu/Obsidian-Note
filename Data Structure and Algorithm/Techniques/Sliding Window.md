#DSA #Technique #SlidingWindow
Sliding Window problems involve moving a fixed or variable-size window through a data structure, typically an array or string, to solve problems efficiently based on continuous subsets of elements. This technique is used when we need to find subarrays or substrings according to a given set of conditions.
___
# What is Sliding Window?
***Sliding Window Technique*** is a method used to efficiently solve problems that involve defining a ***window*** or ***range*** in the input data (arrays or strings) and then moving that window across the data to perform some operation within the window. This technique is commonly used in algorithms like finding subarrays with a specific sum, finding the longest substring with unique characters, or solving problems that require a fixed-size window to process elements efficiently.
___
# How to use the Sliding Window Technique?
## Fixed size Sliding Window
The general steps to solve these questions by follows:
- Find the size of the window required, say K.
- Compute the result for 1st window, i.e. include the first K elements of the data structure.
- Then use a loop to slide the window by 1, and keep computing the result window by window.
## Variable size Sliding Window
The general steps to solve these questions are as follows:
- Find the size of the window required, say K.
- Compute the result for 1st window, i.e. include the first K elements of the data structure.
- Then use a loop to slide the window by 1, and keep computing the result window by window
___
# Identify Sliding Window Problem
- These problems generally require finding the Maximum/Minimum ***Subarray***, ***Substrings*** which satisfy some specific condition.
- The size of the subarray or substring ***K*** will be given in some of the problems.
- These problems can easily be solved in $O(n^2)$ time complexity using nested loops, using a sliding window, we can solve these in $O(n)$Time Complexity.
- ***Required Time Complexity:*** $O(n)$ or $O(nlog(n))$
- ***Constraints:*** N ⇐ 106, If N is the size of the Array/String.
