## This program is an altered version of the previous insertion sort program which sorts a user input integer array and prints the sorted array. Additionally, this program tracks the occurrence of comparisons and swaps.
### The primary challenge in this program was correctly tracking comparisons and swaps. The specified output in the assignment asks to track swaps but doesn't provide an expected output for swaps.
### Attached below is an image of the mathematical logic behind the correct amount of swaps that should occur. I verified my math based on the fact that O(nlog(n)) time complexity with n=6 is ~4.67
![IMG_2551](https://github.com/user-attachments/assets/16a84ed9-bd64-4928-92d6-746e11d4efbc)

```java
import java.util.Scanner;

/**
 * The MergeSort class uses the merge sort algorithm to sort a user input array
 * of integers, track the number of comparisons and swaps, and sort the array in
 * ascending order.
 * @author Zachary Stewart
 * @version 1.0
 * @since 05/04/2025
 */
public class MergeSort {
    static int comparisonCount = 0;
    static int swapCount = 0;
    public static void merge(int[] numbers, int i, int j, int k) {
        int mergedSize = k - i + 1;
        int[] mergedNumbers = new int[mergedSize];
        int mergePos = 0;
        int leftPos = i;
        int rightPos = j + 1;

        while (leftPos <= j && rightPos <= k) {
            comparisonCount++; 
            if (numbers[leftPos] <= numbers[rightPos]) {
                mergedNumbers[mergePos++] = numbers[leftPos++];
            } else {
                mergedNumbers[mergePos++] = numbers[rightPos++];
                swapCount += (j - leftPos + 1); 
            }
        }

        while (leftPos <= j) {
            mergedNumbers[mergePos++] = numbers[leftPos++];
        }

        while (rightPos <= k) {
            mergedNumbers[mergePos++] = numbers[rightPos++];
        }

        for (int m = 0; m < mergedSize; ++m) {
            numbers[i + m] = mergedNumbers[m];
        }
    }

    public static void mergeSort(int[] numbers, int i, int k) {
        int j;

        if (i < k) {
            j = (i + k) / 2;
            mergeSort(numbers, i, j);
            mergeSort(numbers, j + 1, k);
            merge(numbers, i, j, k);
        }
    }

    public static void main(String[] args) {
        Scanner keyboard = new Scanner(System.in);
        int size = keyboard.nextInt();
        int[] numbers = new int[size];

        for (int i = 0; i < size; ++i) {
            numbers[i] = keyboard.nextInt();
        }

        System.out.print("Unsorted: ");
        for (int num : numbers) {
            System.out.print(num + " ");
        }
        System.out.println();

        mergeSort(numbers, 0, numbers.length - 1);

        System.out.print("Sorted: ");
        for (int num : numbers) {
            System.out.print(num + " ");
        }
        System.out.println();

        System.out.println("Comparisons: " + comparisonCount);
        System.out.println("Swaps: " + swapCount);
    }
}
```
### Below is an image of my output.
![Screenshot 2025-05-04 215955](https://github.com/user-attachments/assets/75f33d78-de4c-4246-a75d-7007054b32a9)
