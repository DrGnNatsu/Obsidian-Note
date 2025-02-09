#DSA #Sort 
___
# How does it work?
==Simulation Link==: [Simulation link w3schools.com](https://www.w3schools.com/dsa/dsa_algo_bubblesort.php)
1. Go through the array, one value at a time.
2. For each value, compare the value with the next value.
3. If the value is higher than the next one, swap the values so that the highest value comes last.
4. Go through the array as many times as there are values in the array.
___
# Bubble sort implement?
To implement the Bubble Sort algorithm in a programming language, we need:
1. An array with values to sort.
2. An inner loop that goes through the array and swaps values if the first value is higher than the next value. This loop must loop through one less value each time it runs.
3. An outer loop that controls how many times the inner loop must run. For an array with n values, this outer loop must run n-1 times.
```java
public int[] bubbleSort(int[] arr) {
    int n = arr.length;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // swap arr[j] and arr[j+1]
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    return arr;
}
```
Time-Complexity: $O(n^2)$
Space-Complexity: $O(1)$
___
# Improvement of  the Bubble Sort
Swapped Flag: The swapped flag is used to detect if any elements were swapped during the inner loop iteration. If no elements were swapped, the array is already sorted, and the algorithm can terminate early, avoiding unnecessary iterations.
```java
public static int[] bubbleSort(int[] arr) {
    int n = arr.length;
    for (int i = 0; i < n - 1; i++) {
        boolean swapped = false;
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // Swap arr[j] and arr[j+1]
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                swapped = true;
            }
        }
        // If no two elements were swapped by inner loop, then break
        if (!swapped) break;
    }
    return arr;
}
```