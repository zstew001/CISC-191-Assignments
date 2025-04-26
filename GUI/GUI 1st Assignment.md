## This program takes input for weekly hours worked and hourly rate to calculate annual salary (52 week basis).
### My primary process for this program was to copy the salary calc button program from lecture and add an additional field for weekly hours worked.
### Additionally, I had to create a new variable for user input and replace the standard 40 hours with this variable in the calculation method. 

```java
/**
 * This program takes two user inputs using JTextField, and displays the yearly salary.
 * 
 *
 * @author Zachary Stewart
 * @version v1.0
 * @since 04/21/25
 */
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JTextField;

public class SalaryCalcButtonFrame extends JFrame implements ActionListener {
    private JLabel wageLabel;     // Label for hourly salary
    private JLabel weekLabel;     // Label for weekly hours worked
    private JLabel salLabel;      // Label for yearly salary
    private JTextField salField;  // Displays hourly salary
    private JTextField weekField; // Displays weekly hours worked
    private JTextField wageField; // Displays yearly salary
    private JButton calcButton;   // Triggers salary calculation

    /* Constructor creates GUI components and adds GUI components
    using a GridBagLayout. */
    SalaryCalcButtonFrame() {
        // Used to specify GUI component layout
        GridBagConstraints positionConst = null;

        // Set frame's title
        setTitle("Salary");

        // Set hourly and yearly salary labels
        wageLabel = new JLabel("Hourly wage:");
        weekLabel = new JLabel("Weekly hours worked:");
        salLabel = new JLabel("Yearly salary:");

        wageField = new JTextField(15);
        wageField.setEditable(true);
        wageField.setText("0");

        weekField = new JTextField(15);
        weekField.setEditable(true);
        weekField.setText("0");

        salField = new JTextField(15);
        salField.setEditable(false);

        // Create a "Calculate" button
        calcButton = new JButton("Calculate");

        // Use "this" class to handle button presses
        calcButton.addActionListener(this);

        // Use a GridBagLayout
        setLayout(new GridBagLayout());
        positionConst = new GridBagConstraints();

        // Specify component's grid location
        positionConst.gridx = 0;
        positionConst.gridy = 0;

        // 10 pixels of padding around component
        positionConst.insets = new Insets(10, 10, 10, 10);

        // Add component using the specified constraints
        add(wageLabel, positionConst);

        positionConst.gridx = 0;
        positionConst.gridy = 1;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(weekLabel, positionConst);

        positionConst.gridx = 0;
        positionConst.gridy = 2;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(salLabel, positionConst);

        positionConst.gridx = 1;
        positionConst.gridy = 0;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(wageField, positionConst);

        positionConst.gridx = 1;
        positionConst.gridy = 1;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(weekField, positionConst);

        positionConst.gridx = 1;
        positionConst.gridy = 2;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(salField, positionConst);

        positionConst.gridx = 0;
        positionConst.gridy = 3;
        positionConst.insets = new Insets(10, 10, 10, 10);
        add(calcButton, positionConst);
    }

    /* Method is automatically called when an event
    occurs (e.g, button is pressed) */
    @Override
    public void actionPerformed(ActionEvent event) {
        String userInputOne;   // User specified hourly wage
        String userInputTwo;   // User specified weekly hours
        int hourlyWage;        // Hourly wage
        int weeklyHours;       // Weekly hours worked
        // Get user's wage input
        userInputOne = wageField.getText();
        userInputTwo = weekField.getText();

        // Convert from String to an integer
        hourlyWage = Integer.parseInt(userInputOne);
        weeklyHours = Integer.parseInt(userInputTwo);

        // Display calculated salary
        salField.setText(Integer.toString(hourlyWage * weeklyHours * 52));
    }

    /* Creates a SalaryCalculatorFrame and makes it visible */
    public static void main(String[] args) {
        // Creates SalaryLabelFrame and its components
        SalaryCalcButtonFrame myFrame = new SalaryCalcButtonFrame();

        myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        myFrame.pack();
        myFrame.setVisible(true);
    }
}
```
## The following is the output of my program.
![Screenshot 2025-04-26 125801](https://github.com/user-attachments/assets/b0946de2-268d-478f-a248-09fe86e50da9)

