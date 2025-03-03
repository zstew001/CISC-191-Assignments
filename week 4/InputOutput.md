```java

import java.util.Scanner;
import java.io.File;
import java.io.FileNotFoundException;
/**
 * The InputOutput class takes information from a file and changes the name of the file.
 *
 * @author Zachary Stewart
 * @version v1.0
 * @since 2/28/2025
 */
public class InputOutput {
    public static void main(String[] args) throws FileNotFoundException{
        Scanner keyboard = new Scanner(System.in);//create scanner obj for file path
        String fileName = keyboard.nextLine();//assign scanner obj to a String var
        keyboard.nextLine(); //clear carriage return
        File file = new File(fileName);//create new file obj
        Scanner fileChange = new Scanner(file);//create new scanner obj with file as arg
        
        while(fileChange.hasNextLine()){
            String photoName = fileChange.nextLine();
            String photoInfo = fileChange.replace("_photo.jpg", "info.txt");
            System.out.println(photoInfo);
            //while loop to replace info from input file
        }
        keyboard.close();
        fileChange.close();
        //close both scanner obj
    
    } 
    
}
```
