#This is my code for the WordsFrequency program.

```java

import java.util.Scanner;
/**
 * The WordFrequency class contains a method to determine frequency of words in an array and
 * a main method to allow words to be input, assigned to an array then printed to the console
 * along with their frequency of occurrence.
 *
 * @author Zachary Stewart
 * @version v1.0
 * @since 2/7/2025
 */
public class WordFrequency{
    /**
     * getWordFrequency method determines the frequency of word occurrence based on input vars.
     * @param wordsList String array to be processed by the method
     * @param listSize int value for total elements in the array
     * @param currWord memory locations of the input words
     * @return the frequency of occurrence for each word processed
     */
    public static int getWordFrequency(String[] wordsList, int listSize, String currWord){
        int frequency = 0;

        for(int i=0; i<listSize; i++){//for loop to determine amount of times to run based on listSize
            if(wordsList[i].equalsIgnoreCase(currWord)){
                frequency++;//if statement to determine frequency of processed words
            }

        }
        return frequency;

    }

    /**
     * Main program to allow input and create a String array object based on user input of words.
     */
    public static void main(String[] args){
        Scanner keyboard = new Scanner(System.in);
        int listSize = 0;//initialize listSize
        System.out.println("Enter number of words to be processed: ");
        listSize = keyboard.nextInt();//assign input number to listSize
        keyboard.nextLine();//clear carriage return

        String[] wordsList = new String[listSize];//creating wordsList array with listSize as argument
        for(int i=0; i<wordsList.length; i++){
            wordsList[i] = keyboard.nextLine();
        }

        for(int i=0; i<listSize; i++){
            String currWord = wordsList[i];
            int wordCount = getWordFrequency(wordsList, listSize, currWord);//int var to assign to word frequency for each word
            System.out.println(currWord + " " + wordCount);//print statement to print each word and its frequency

        }

    }



}
```
