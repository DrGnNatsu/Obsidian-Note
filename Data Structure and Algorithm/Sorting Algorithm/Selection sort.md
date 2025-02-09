#DSA #Sort 
___
# How does it work?
==Simulation Link==: [Simulation link w3schools.com](https://www.w3schools.com/dsa/dsa_algo_insertionsort.php)
1. Go through the array to find the lowest value.
2. Move the lowest value to the front of the unsorted part of the array.
3. Go through the array again as many times as there are values in the array.
___
# Selection sort implement?
To implement the Selection Sort algorithm in a programming language, we need:
1. An array with values to sort.
2. An inner loop that goes through the array finds the lowest value and moves it to the front of the array. This loop must loop through one less value each time it runs.
3. An outer loop that controls how many times the inner loop must run. For an array with `n` values, this outer loop must run `n−1` times.
```java
public int[] selectionSort(int[] arr) {
	int n = arr.length;  
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        int temp = arr[minIndex];
        arr[minIndex] = arr[i];
        arr[i] = temp;
    }
	return arr;
}
```
Time-Complexity: $O(n^2 = n^2 /2)$
Space-Complexity: $O(1)$
