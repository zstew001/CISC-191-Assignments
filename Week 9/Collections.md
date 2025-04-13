## Thought process: 
### Deque via LinkedList
### Could use a for loop which reads values from input String and throws an error to user with message regarding invalid type.
### i.e. "Incorrect input, please only use lower case letters. i.e. "a, b, c...""(tried this, it's difficult to implement).
### Otherwise, create a check if input is a char, then only add that to deque and force it toLowerCase.(what I ended up using).
### Last, while loop to iterate when deque list exists and is storing values. Then check if first and last are equal until no more values exist to compare, then print result. 




```java

import java.util.Deque;
import java.util.LinkedList;
import java.util.Scanner;
/**
 * This program reads a line of input text, then outputs whether or not the input
 * is a palindrome.
 *
 * @author Zachary Stewart
 * @version v1.0
 * @since 4/10/25
 */
public class Palindrome{

    public static void main(String[] args){
    
        Scanner keyboard = new Scanner(System.in);
        String input = keyboard.nextLine();
        
        Deque<Character> deque = new LinkedList<>();
        
        for(int i=0; i<input.length(); i++){
            char c = input.charAt(i);
            if(Character.isLetter(c)){
                deque.addLast(Character.toLowerCase(c));
                
            }
        
        }
        
        boolean isPalindrome = true;
        
        while(deque.size() > 1){
            if(deque.removeFirst() != deque.removeLast()){
                isPalindrome = false;
            }
        
        }
        
        if(isPalindrome){
            System.out.println("Yes, " + input + " is a palindrome.");
        }
        else{
            System.out.println("No, \"" + input + "\" is not a palindrome.");
        
        
        }
        
    
    }
}

```
