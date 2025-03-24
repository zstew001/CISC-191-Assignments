### This Program exhibits the use of a try-catch block to catch a custom negative input exception.
## Create stepsToMiles class that throws an exception for any negative input.
## Create exception object within stepsToMiles class that provides the correct exception message.
## If exception isn't caught, return int value for steps/2000 as miles. 
## Create Main method and include input/try-catch block to test steps to miles and catch potential exceptions.

```Java

import java.util.Scanner;

public class Exceptions {
  public static double stepsToMiles(int steps) throws Exception {
  if (steps < 0) {
  throw new Exception("Exception: Negative step count entered.");
  }
  return steps / 2000.0;
  }

  public static void main(String[] args) {
  Scanner keyboard = new Scanner(System.in);
  int steps = keyboard.nextInt();

  try {
  double miles = stepsToMiles(steps);
  System.out.printf("%.2f", miles);
  System.out.print("\n");
  } catch (Exception e) {
  System.out.println(e.getMessage());
  }
  }
}

```
![Screenshot 2025-03-23 213950](https://github.com/user-attachments/assets/5ef3f9b1-7ba7-44fc-b65a-c6a64a9699f9)
