```java

import java.util.Scanner;

public class TaxTableTools {

   /** This class searches the 'search' table with a search argument and
       returns the corresponding value in the 'value' table. Variable
       'nEntries' has the number of entries in each table.
   */
   private int [] search =   {   0, 20000, 50000, 100000,  Integer.MAX_VALUE };
   private double [] value = { 0.0,  0.10,  0.20,   0.30,               0.40 };
   private int nEntries;

   // *********************************************************************** 

   // Default constructor 
   
   public TaxTableTools () {
      nEntries  = search.length;  // Set the length of the search table
   } 
   
   // *********************************************************************** 

   // Overloaded constructor
    public TaxTableTools(int[] search, double[] value){
        this.search = search;
        this.value = value;
        nEntries = search.length;
    }
   // FIXME: Add an overloaded constructor to load the search and value tables.
   // FIXME: Be sure to set the nEntries value, too.

   // *********************************************************************** 

   // Method to prompt for and input an integer
   
   public int getInteger(Scanner input, String prompt) {
      int inputValue = 0;
      
      System.out.println(prompt + ": ");
      inputValue = input.nextInt();
      
      return inputValue;
   } 

   // *********************************************************************** 

   // Method to get a value from one table based on a range in the other table

   public double getValue(int searchArgument) {
      double result;
      boolean keepLooking;
      int i;

      result = 0.0;
      keepLooking = true;
      i = 0;

      while ((i < nEntries) && keepLooking) {
         if (searchArgument <= search[i]) {
            result = value[i];
            keepLooking = false;
         }
         else {
            ++i;
         }
      } 

      return result;
   } 
}

import java.util.Scanner;

public class IncomeTaxMain {    
   public static void main(String [] args) { 
      final String PROMPT_SALARY = "\nEnter annual salary (-1 to exit)";
      Scanner scnr = new Scanner(System.in);
      int annualSalary;
      double taxRate;
      int taxToPay;
      int i;

      // Tables to use in the exercise are the same as in the TaxTableTools class
      // int [] salaryRange = {   0,  20000, 50000, 100000,  Integer.MAX_VALUE };
      // double [] taxRates = { 0.0,   0.10,  0.20,   0.30,               0.40 };

      // 2(a) Modify the salary and tax tables in the main method to use 
      // different salary ranges and tax rates.
      int []    salaryRange  = {   0,  30000,  60000,  Integer.MAX_VALUE };
      double [] taxRates     = { 0.0,  0.25,   0.35,               0.45 };

      // Access the related class
      // TaxTableTools table = new TaxTableTools();

      // 2(b)Use the just-created overloaded constructor to initialize 
      // the salary and tax tables.
      TaxTableTools table = new TaxTableTools(salaryRange, taxRates);

      // Get the first annual salary to process
      annualSalary = table.getInteger(scnr, PROMPT_SALARY);

      while (annualSalary >= 0) {
         taxRate = table.getValue(annualSalary);
         taxToPay= (int)(annualSalary * taxRate);     // Truncate tax to an integer amount
         System.out.println("Annual Salary: " + annualSalary + 
                            "\tTax rate: " + taxRate +
                            "\tTax to pay: " + taxToPay);

         // Get the next annual salary
         annualSalary = table.getInteger(scnr, PROMPT_SALARY);
      } 
   } 
}
```
