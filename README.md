# Sorting
AP CSA Sorting Algorithms
Here is a list of algorithms:
1. [Bubble Sort](./bubblesort.html)
2. [Selection Sort](./selectionsort.html)
4. [Insertion Sort](./insertionsort.html)
5. [Quick Sort](quicksort.html)
6. [Heapify](heapify.html)
7. [Heap Sort](heapsort.html)
8. [Merge Sort](mergesort.html)

# Java Sorting Algorithms

Below is a minimalistic implementation of various sorting algorithms in Java. 
```java
import java.util.Arrays;

public class SortingAlgorithms {

    // Utility method to print arrays
    public static void printArray(int[] arr, String message) {
        System.out.println(message + Arrays.toString(arr));
    }

    // 1. BUBBLE SORT
    // Time Complexity: O(n²), Space Complexity: O(1)
    public static void bubbleSort(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    // Swap arr[j] and arr[j+1]
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
    }

    // 2. SELECTION SORT
    // Time Complexity: O(n²), Space Complexity: O(1)
    public static void selectionSort(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            // Find the minimum element in unsorted array
            int minIdx = i;
            for (int j = i + 1; j < n; j++) {
                if (arr[j] < arr[minIdx]) {
                    minIdx = j;
                }
            }
            // Swap the found minimum element with the element at index i
            int temp = arr[minIdx];
            arr[minIdx] = arr[i];
            arr[i] = temp;
        }
    }

    // 3. INSERTION SORT
    // Time Complexity: O(n²), Space Complexity: O(1)
    public static void insertionSort(int[] arr) {
        int n = arr.length;
        for (int i = 1; i < n; i++) {
            int key = arr[i];
            int j = i - 1;

            // Move elements of arr[0..i-1] that are greater than key
            // to one position ahead of their current position
            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j = j - 1;
            }
            arr[j + 1] = key;
        }
    }

    // 4. QUICK SORT
    // Time Complexity: O(n log n) average, O(n²) worst, Space Complexity: O(log n)
    public static void quickSort(int[] arr, int low, int high) {
        if (low < high) {
            // Partition the array and get the pivot position
            int pivotPos = partition(arr, low, high);

            // Sort elements before and after the pivot
            quickSort(arr, low, pivotPos - 1);
            quickSort(arr, pivotPos + 1, high);
        }
    }

    // Helper method for quickSort - partitions the array and returns pivot position
    private static int partition(int[] arr, int low, int high) {
        // Choose the rightmost element as pivot
        int pivot = arr[high];
        
        // Index of smaller element
        int i = low - 1;
        
        for (int j = low; j < high; j++) {
            // If current element is smaller than the pivot
            if (arr[j] < pivot) {
                i++;
                
                // Swap arr[i] and arr[j]
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
        
        // Swap arr[i+1] and arr[high] (pivot)
        int temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;
        
        return i + 1;
    }

    // 5. HEAPIFY (procedure to maintain heap property)
    // This is a utility function for Heap Sort
    private static void heapify(int[] arr, int n, int i) {
        int largest = i; // Initialize largest as root
        int left = 2 * i + 1; // Left child
        int right = 2 * i + 2; // Right child

        // If left child is larger than root
        if (left < n && arr[left] > arr[largest]) {
            largest = left;
        }

        // If right child is larger than largest so far
        if (right < n && arr[right] > arr[largest]) {
            largest = right;
        }

        // If largest is not root
        if (largest != i) {
            int swap = arr[i];
            arr[i] = arr[largest];
            arr[largest] = swap;

            // Recursively heapify the affected sub-tree
            heapify(arr, n, largest);
        }
    }

    // 6. HEAP SORT
    // Time Complexity: O(n log n), Space Complexity: O(1)
    public static void heapSort(int[] arr) {
        int n = arr.length;

        // Build heap (rearrange array)
        for (int i = n / 2 - 1; i >= 0; i--) {
            heapify(arr, n, i);
        }

        // Extract elements from heap one by one
        for (int i = n - 1; i > 0; i--) {
            // Move current root to end
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;

            // Call heapify on the reduced heap
            heapify(arr, i, 0);
        }
    }

    // 7. MERGE SORT
    // Time Complexity: O(n log n), Space Complexity: O(n)
    public static void mergeSort(int[] arr, int left, int right) {
        if (left < right) {
            // Find the middle point
            int mid = left + (right - left) / 2;

            // Sort first and second halves
            mergeSort(arr, left, mid);
            mergeSort(arr, mid + 1, right);

            // Merge the sorted halves
            merge(arr, left, mid, right);
        }
    }

    // Helper method for mergeSort - merges two subarrays
    private static void merge(int[] arr, int left, int mid, int right) {
        // Find sizes of two subarrays to be merged
        int n1 = mid - left + 1;
        int n2 = right - mid;

        // Create temp arrays
        int[] L = new int[n1];
        int[] R = new int[n2];

        // Copy data to temp arrays
        for (int i = 0; i < n1; i++) {
            L[i] = arr[left + i];
        }
        for (int j = 0; j < n2; j++) {
            R[j] = arr[mid + 1 + j];
        }

        // Merge the temp arrays
        
        // Initial indexes of first and second subarrays
        int i = 0, j = 0;
        
        // Initial index of merged subarray
        int k = left;
        
        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                arr[k] = L[i];
                i++;
            } else {
                arr[k] = R[j];
                j++;
            }
            k++;
        }

        // Copy remaining elements of L[] if any
        while (i < n1) {
            arr[k] = L[i];
            i++;
            k++;
        }

        // Copy remaining elements of R[] if any
        while (j < n2) {
            arr[k] = R[j];
            j++;
            k++;
        }
    }

    // MAIN METHOD to demonstrate all sorting algorithms
    public static void main(String[] args) {
        // Arrays to be sorted by each algorithm
        int[] arr1 = {64, 34, 25, 12, 22, 11, 90};
        int[] arr2 = {64, 34, 25, 12, 22, 11, 90};
        int[] arr3 = {64, 34, 25, 12, 22, 11, 90};
        int[] arr4 = {64, 34, 25, 12, 22, 11, 90};
        int[] arr5 = {64, 34, 25, 12, 22, 11, 90};
        int[] arr6 = {64, 34, 25, 12, 22, 11, 90};
        int[] arr7 = {64, 34, 25, 12, 22, 11, 90};

        System.out.println("Original array: " + Arrays.toString(arr1));
        
        // 1. Bubble Sort
        bubbleSort(arr1);
        printArray(arr1, "1. Bubble Sort:    ");
        
        // 2. Selection Sort
        selectionSort(arr2);
        printArray(arr2, "2. Selection Sort: ");
        
        // 3. Insertion Sort
        insertionSort(arr3);
        printArray(arr3, "3. Insertion Sort: ");
        
        // 4. Quick Sort
        quickSort(arr4, 0, arr4.length - 1);
        printArray(arr4, "4. Quick Sort:     ");
        
        // 5 & 6. Heap Sort (using heapify)
        heapSort(arr5);
        printArray(arr5, "5 & 6. Heap Sort:  ");
        
        // 7. Merge Sort
        mergeSort(arr6, 0, arr6.length - 1);
        printArray(arr6, "7. Merge Sort:     ");
    }
}
```

## Compilation and Execution

Save the above code to a file named `SortingAlgorithms.java`, then compile and run:

```bash
javac SortingAlgorithms.java
java SortingAlgorithms
```

## Expected Output

```
Original array: [64, 34, 25, 12, 22, 11, 90]
1. Bubble Sort:    [11, 12, 22, 25, 34, 64, 90]
2. Selection Sort: [11, 12, 22, 25, 34, 64, 90]
3. Insertion Sort: [11, 12, 22, 25, 34, 64, 90]
4. Quick Sort:     [11, 12, 22, 25, 34, 64, 90]
5 & 6. Heap Sort:  [11, 12, 22, 25, 34, 64, 90]
7. Merge Sort:     [11, 12, 22, 25, 34, 64, 90]
```
