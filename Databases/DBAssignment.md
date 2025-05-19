## The most challenging portion of this lab was writing the program without access to the root@localhost:3306 MySQL database I created. (Outside of class hours, the database isn't accessible?)
### One thing I tried to implement in this lab is try-catching the possible exceptions instead of throwing them so a user could see specific error messages if the program fails to connect/update the record on MySQL.

```Java
import java.sql.*;
public class JavaDatabase {
    public static void main(String[] args){
        String url = "jdbc:mysql://localhost/testdb";
        String user = "testuser";
        String pass = "DarthRevan7@";

        try (Connection conn = DriverManager.getConnection(url, user, pass)) {
            String sql = "INSERT INTO Student (SSN, First_Name, Middle_Name, Last_Name, DOB, Street, Phone, Zipcode, deptID) "
                + "VALUES ('111222333', 'Philip', 'David Charles', 'Collins', '1951-01-30', 'NA', 'NA', 'NA', '1234')";

            try (Statement statement = conn.createStatement()) {
                statement.executeUpdate(sql);
                System.out.println("Database updated successfully.");
            } catch (SQLException e) {
                System.out.println("Error inserting record: " + e.getMessage());
            }

            String updateSql = "UPDATE Student SET Zipcode = '92126' WHERE SSN = '111222333'";

            try(Statement stmt = conn.createStatement()){
                int rowsChanged = stmt.executeUpdate(updateSql);
                if(rowsChanged>0){
                    System.out.println("Zipcode updated successfully.");
                }

            }catch (SQLException e){
                System.out.println("Unable to update record: " + e.getMessage());
            }

        }catch (SQLException e) {
            System.out.println("Connection error: " + e.getMessage());
        }
    }
}

```
### No output to share on this lab as I completed it outside of class time and was unable to test the program using MySQL.
