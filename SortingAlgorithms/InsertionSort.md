### My main challenge with this lab was preventing off-by-one errors and tracking comparisons and swaps correctly.
## Originally, I made comparisons and swaps boolean vars and attempted to make a separate loop which tracked the occurrence of each instance where they indicated a true value.
## However, this didn't work so I changed the tracking method to int vars and made them increment within the while loop upon each occurrence.
## I also had difficulty printing each iteration of the array upon a comparison/swap occurrence, so I had to make a printInfo method to handle this separately(similar to the printInfo method from previous lecture section).

```java


/**
 * This program reads an array of integers and uses an insertion sort algorithm
 * to organize the array in ascending order numerically.
 *
 * @author Zachary Stewart
 * @version v1.0
 * @since 05/01/2025
 */
import java.util.Scanner;

public class insertionSort{
    public static void main(String[] args){
        Scanner keyboard = new Scanner(System.in);
        int size = keyboard.nextInt();
        int[] array = new int[size];
        int comparisons = 0;
        int swaps = 0;

        for(int i=0; i<size; i++){
            array[i] = keyboard.nextInt();
        }
        printInfo(array);
        System.out.println();

        for(int i=1; i<size; i++){
            int temp = array[i];
            int j = i-1;
            boolean swap = false;

            while(j>=0 && array[j]>temp){
                array[j+1] = array[j];
                j--;
                comparisons++;
                array[j+1] = temp;
                swap = true;
                swaps++;
            }

            if(j>=0){
                comparisons++;
            }
            
            printInfo(array);
        }

        System.out.println();
        System.out.println("Comparisons: " + comparisons);
        System.out.println("Swaps: " + swaps);

    }
    /**
     * The printInfo method uses an enhanced for loop to read the array and print it's
     * individual elements in a single line.
     * @param array user input integer array.
     */
    public static void printInfo(int[] array){
        for(int nums: array){
            System.out.print(nums + " ");
        }
        System.out.println();
    }
}
```
## The following is a screenshot of my output.

![Screenshot 2025-05-04 083909](https://github.com/user-attachments/assets/be8b0c59-3278-4681-a70c-f7c046c171f2)

