```java
// ===== Code from file Person.java =====
public class Person {
   private int ageYears;
   private String lastName;

   public void setName(String userName) {
      lastName  = userName;
   }

   public void setAge(int numYears) {
      ageYears = numYears;
   }

   // Other parts omitted

   public void printAll() {
      System.out.print("Name: " + lastName);
      System.out.print(", Age: "  + ageYears);
   }
}
// ===== end =====

// ===== Code from file Student.java =====
public class Student extends Person {
   private int idNum;

   public void setID(int studentId) {
      idNum = studentId;
   }

   public int getID() {
      return idNum;
   }
}
// ===== end =====

// ===== Code from file StudentDerivationFromPerson.java =====
public class StudentDerivationFromPerson {
   public static void main(String[] args) {
      Student courseStudent = new Student(); //creation of new Student object called courseStudent
      courseStudent.setName("Smith");   //calling setName() method to assign name to courseStudent object
      courseStudent.setAge(20);   //calling setAge() method to assign age to courseStudent object
      courseStudent.setID(9999);   //calling setID() method to assign ID number to courseStudent object
      courseStudent.printAll();   //calling printAll() method to print student name and age
      System.out.println(", ID: " + courseStudent.getID()); //separate println statement to print ID number(formatting included)

   }
}
// ===== end =====
```
