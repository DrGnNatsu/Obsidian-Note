#DSA #Sort 
___
# How does it work?
==Simulation Link==: [Simulation link w3schools.com](https://www.w3schools.com/dsa/dsa_algo_insertionsort.php)
1. Take the first value from the unsorted part of the array.
2. Move the value into the correct place in the sorted part of the array.
3. Go through the unsorted part of the array again as many times as there are values.
___
# Insertion sort implement?
To implement the Insertion Sort algorithm in a programming language, we need:
1. An array with values to sort.
2. An outer loop that picks a value to be sorted. For an array with `n` values, this outer loop skips the first value and must run `n - 1` times.
3. An inner loop that goes through the sorted part of the array to find where to insert the value. If the value to be sorted is at index `i`, the sorted part of the array starts at index 00 and ends at index `i−1`.
```java
public int[] insertionSort(int[] arr) {
	int n = arr.length;  
	for (int i = 1; i < n; i++) {  
	    int key = arr[i];  
	    int j = i - 1;  
	    while (j >= 0 && arr[j] > key) {  
	        arr[j + 1] = arr[j];  
	        j = j - 1;  
	    }  
	    arr[j + 1] = key;  
	  
	}  
	return arr;
}
```
Time-Complexity: $O(n^2 = n^2 /2)$
Space-Complexity: $O(1)$
___
# Improvement of  the Insertion Sort
Shifting Elements Instead of Swapping: In the provided implementation, elements are shifted to the right to make space for the current element (currentValue) instead of swapping elements repeatedly. This reduces the number of assignments, making the algorithm more efficient.
```java
public static int[] insertionSort(int[] arr) {
	int n = arr.length;  
	for (int i = 1; i < n; i++) {  
	    int insertIndex = i;  
	    int currentValue = arr[i];  
	    for (int j = i - 1; j >= 0; j--) {  
	        if (arr[j] > currentValue) {  
	            arr[j + 1] = arr[j];  
	            insertIndex = j;  
	        } else {  
	            break;  
	        }  
	    }  
	    arr[insertIndex] = currentValue;  
	}  
	return arr;
}
```