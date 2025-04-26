## This program takes a single user input using a JFormattedTextField (distance in miles), and displays converted outputs (distance in Km, meters, feet).
### I created this program by modifying the flight travel time program from lecture. 
### The main challenge was to add/position a new label, field, and reconfigure the actionPerformed method to calculate distance conversions.

```java

/**
 * This program takes a user input for distance (in miles) and outputs the distance in km, m, and feet.
 *
 * @author Zachary Stewart
 * @version v1.0 
 * @since 04/24/25
 */
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.text.NumberFormat;
import javax.swing.JButton;
import javax.swing.JFormattedTextField;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JTextField;

public class DistanceFrame extends JFrame implements ActionListener {
    private JButton calcButton;            // Triggers time calculation
    private JLabel distLabel;              // Label for distance input
    private JLabel kilomLabel;            // Label for kilometers
    private JLabel metersLabel;          // Label for meters
    private JLabel feetLabel;            // Label for feet
    private JTextField kilomField;        // Displays kilometers
    private JTextField metersField;      // Displays meters
    private JTextField feetField;        // Displays feet
    private JFormattedTextField distField; // Holds distance input

    /* Constructor creates GUI components and adds GUI components
    using a GridBagLayout. */
    DistanceFrame() {
        // Used to specify GUI component layout
        GridBagConstraints layoutConst = null;

        // Set frame's title
        setTitle("Distance Calculator");

        // Create labels
        distLabel = new JLabel("Distance (miles):");
        kilomLabel = new JLabel("Distance (kilometers):");
        metersLabel = new JLabel("Distance (meters)");
        feetLabel = new JLabel("Distance (feet)");

        // Create button and add action listener
        calcButton = new JButton("Calculate");
        calcButton.addActionListener(this);

        // Create kilometer field
        kilomField = new JTextField(15);
        kilomField.setEditable(false);

        // Create meters field
        metersField = new JTextField(15);
        metersField.setEditable(false);
        
        // Create feet field
        feetField = new JTextField(15);
        feetField.setEditable(false);

        // Create and set-up an input field for numbers (not text)
        distField = new JFormattedTextField(NumberFormat.getNumberInstance());
        distField.setEditable(true);
        distField.setText("0");
        distField.setColumns(15); // Initial width of 10 units

        // Use a GridBagLayout
        setLayout(new GridBagLayout());

        // Specify component's grid location
        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 10, 1);
        layoutConst.gridx = 0;
        layoutConst.gridy = 0;
        add(distLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 1, 10, 10);
        layoutConst.gridx = 1;
        layoutConst.gridy = 0;
        add(distField, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 5, 10, 10);
        layoutConst.gridx = 2;
        layoutConst.gridy = 0;
        add(calcButton, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 0, 1, 10);
        layoutConst.gridx = 1;
        layoutConst.gridy = 1;
        add(kilomLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(1, 0, 10, 10);
        layoutConst.gridx = 1;
        layoutConst.gridy = 2;
        add(kilomField, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 0, 1, 10);
        layoutConst.gridx = 2;
        layoutConst.gridy = 1;
        add(metersLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(1, 0, 10, 10);
        layoutConst.gridx = 2;
        layoutConst.gridy = 2;
        add(metersField, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 0, 1, 10);
        layoutConst.gridx = 3;
        layoutConst.gridy = 1;
        add(feetLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(1, 0, 10, 10);
        layoutConst.gridx = 3;
        layoutConst.gridy = 2;
        add(feetField, layoutConst);

    }

    /* Method is automatically called when an event
    occurs (e.g, Enter key is pressed) */
    @Override
    public void actionPerformed(ActionEvent event) {
        double totMiles;     // Distance to travel
        double kilometers;       
        double meters;
        double feet;

        // Get value from distance field
        totMiles = ((Number) distField.getValue()).doubleValue();

        // Check if miles input is positive
        if (totMiles >= 0.0) {
            kilometers = totMiles * 1.609;
            meters = totMiles * 1609;
            feet = totMiles * 5280;

            kilomField.setText(Double.toString(kilometers));
            metersField.setText(Double.toString(meters));
            feetField.setText(Double.toString(feet));
        }
        else {
            // Show failure dialog
            JOptionPane.showMessageDialog(this, "Enter a positive distance value!");
        }
    }

    /* Creates a DistanceFrame and makes it visible */
    public static void main(String[] args) {
        // Creates DistanceFrame and its components
        DistanceFrame myFrame = new DistanceFrame();

        myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        myFrame.pack();
        myFrame.setVisible(true);
    }
}
```
## The following is a screenshot of my output for this program.

![Screenshot 2025-04-26 133603](https://github.com/user-attachments/assets/9dda1ca2-71fa-4e84-a124-69fdba52a8dd)
