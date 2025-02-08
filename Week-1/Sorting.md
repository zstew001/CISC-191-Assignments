# This is my Code for Week 1 Assignment 1: Sorting

```java
import java.util.Scanner;
/**
 * The Sorting class contains 2 methods, one to Sort an array of integers and
 * return the sorted array as well as a main method to allow users to input a set
 * of integers to be sorted.
 *
 * @author Zachary Stewart
 * @version v1.0 
 * @since 2/6/2025
 */
public class Sorting{
    /**
     * The sortArray method takes an integer array and sorts it's elements in descending order.
     * @param myArr integer array to be sorted.
     * @param arrSize number of elements in the array to be sorted.
     */
    public static void sortArray(int[] myArr, int arrSize){
        for(int i=0; i<arrSize-1; i++){ //outer for loop to establish number of elements in the array to be processed
            for(int j=i+1;j<arrSize;j++){//inner for loop to determine the value of each array element
                if(myArr[i]<myArr[j]){//if statement to swap each element in the array - greatest value on left, lowest on right
                    int temp = myArr[j];
                    myArr[j] = myArr[i];
                    myArr[i] = temp;
                }            
            }
        }
    }

    /**
     * Main method asks user to input integer values to be placed in an array and sorted in descending order.
     */
    public static void main(String[] args){
        Scanner input = new Scanner(System.in);

        System.out.print("Enter the number of integers for the list: ");//text to prompt user 
        int arrSize = input.nextInt();//user input array size

        int[] myArr = new int[arrSize];//creating a new int array object with arrSize as argument
        for(int i=0; i<arrSize; i++){//for loop to allow input assignment of each integer
            myArr[i] = input.nextInt();
        }

        sortArray(myArr, arrSize);//call to sortArray method above

        for(int i: myArr){//enhanced for loop to pull integer i values from myArr array
            System.out.print(i + " ");//printed array elements in descending order
        }

    }
}
```java
