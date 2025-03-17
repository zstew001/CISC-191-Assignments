```java

public class Course{

    private String courseNum;
    private String courseTitle;
    
    public void setCourseNum(String courseNum){
        this.courseNum = courseNum;    
    }
    
    public void setCourseTitle(String courseTitle){
        this.courseTitle = courseTitle;
    }
    
    public String getCourseNum(){
        return courseNum;
    }
    
    public String getCourseTitle(){
        return courseTitle;
    }
    
    public void printInfo(){
        System.out.println("Course Information: ");
        System.out.println("Course Number: " + getCourseNum());
        System.out.println("Course Title: " + getCourseTitle());
    }
}

public class OfferedCourse extends Course{

    private String instructorName;
    private String location;
    private String classTime;
    
    public void setInstructorName(String instructorName){
        this.instructorName = instructorName;
    }
    
    public void setLocation(String location){
        this.location = location;
    }
    
    public void setClassTime(String classTime){
        this.classTime = classTime;
    }
    
    public String getInstructorName(){
        return instructorName;
    }
    
    public String getLocation(){
        return location;
    }
    
    public String getClassTime(){
        return classTime;
    }
    
    @Override
    public void printInfo(){
        super.printInfo();
        
        System.out.println("Instructor Name: " + getInstructorName());
        System.out.println("Location: " + getLocation());
        System.out.println("Class Time: " + getClassTime());
    }


}

import java.util.Scanner;

public class DerivedClassesDemo{
    
    public static void main(String[] args){
        Scanner keyboard = new Scanner(System.in);
        
        Course course = new Course();
        OfferedCourse offeredCourse = new OfferedCourse();
        
        String courseNum = keyboard.nextLine();
        String courseTitle = keyboard.nextLine();
        
        String offeredCourseNum = keyboard.nextLine();
        String offeredCourseTitle = keyboard.nextLine();
        String instructorName = keyboard.nextLine();
        String location = keyboard.nextLine();
        String classTime = keyboard.nextLine();
        
        course.setCourseNum(courseNum);
        course.setCourseTitle(courseTitle);
        
        course.printInfo();
        
        offeredCourse.setCourseNum(offeredCourseNum);
        offeredCourse.setCourseTitle(offeredCourseTitle);
        offeredCourse.setInstructorName(instructorName);
        offeredCourse.setLocation(location);
        offeredCourse.setClassTime(classTime);
        
        offeredCourse.printInfo();
    
    
    }

}

![Screenshot 2025-03-16 192957](https://github.com/user-attachments/assets/fdda0523-90c2-46aa-8081-0ca7d543a377)
