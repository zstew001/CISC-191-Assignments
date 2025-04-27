### This program uses a JSpinner to take user input (Distance in miles) and convert it to kilometers.
## I created this program by redesigning the dog age to human age calculator from lecture.

# Note to Dr. Khan: I really enjoyed working on the GUI projects over the past few weeks. This was completely new material for me and it was very fun to tinker with layouts, positioning, and stylistic elements of UI programming.

```java

/**
 * This program uses a JSpinner to calculate miles to kilometers.
 *
 * @author Zachary Stewart
 * @version v1.0 
 * @since 04/25/25
 */

import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JSpinner;
import javax.swing.JTextField;
import javax.swing.SpinnerNumberModel;
import javax.swing.event.ChangeEvent;
import javax.swing.event.ChangeListener;

public class MilesToKilometersFrame extends JFrame implements ChangeListener {
    private JSpinner milesSpinner;    // Triggers miles to km calculation
    private JTextField kmField;        // Displays km
    private JLabel milesLabel;         // Label for miles
    private JLabel kmLabel;            // Label for kilometers

    /* Constructor creates GUI components and adds GUI components using GridBagLayout */
    MilesToKilometersFrame() {
        double initMiles = 0.0;  // Initial value
        double minMiles = 0.0;   // Minimum value
        double maxMiles = 10000.0; // Maximum value
        double stepVal = 0.1;    // Step increment

        GridBagConstraints layoutConst = null;
        SpinnerNumberModel spinnerModel = null;

        setTitle("Miles to Kilometers Converter");

        // Labels
        milesLabel = new JLabel("Enter distance (miles):");
        kmLabel = new JLabel("Distance (kilometers):");

        // Spinner for miles input
        spinnerModel = new SpinnerNumberModel(initMiles, minMiles, maxMiles, stepVal);
        milesSpinner = new JSpinner(spinnerModel);
        milesSpinner.addChangeListener(this);

        // Text field for kilometer output
        kmField = new JTextField(15);
        kmField.setEditable(false);
        kmField.setText("0.00");

        // Set layout
        setLayout(new GridBagLayout());

        // Positioning
        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 10, 1);
        layoutConst.anchor = GridBagConstraints.LINE_END;
        layoutConst.gridx = 0;
        layoutConst.gridy = 0;
        add(milesLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 1, 10, 10);
        layoutConst.fill = GridBagConstraints.HORIZONTAL;
        layoutConst.gridx = 1;
        layoutConst.gridy = 0;
        add(milesSpinner, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 10, 1);
        layoutConst.anchor = GridBagConstraints.LINE_END;
        layoutConst.gridx = 0;
        layoutConst.gridy = 1;
        add(kmLabel, layoutConst);

        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 1, 10, 10);
        layoutConst.fill = GridBagConstraints.HORIZONTAL;
        layoutConst.gridx = 1;
        layoutConst.gridy = 1;
        add(kmField, layoutConst);
    }

    /* Spinner calculation changes */
    @Override
    public void stateChanged(ChangeEvent event) {
        double miles = (Double) milesSpinner.getValue();
        double kilometers = miles * 1.60934;
        kmField.setText(String.format("%.2f", kilometers));
    }

    /* Main method to create a frame */
    public static void main(String[] args) {
        MilesToKilometersFrame myFrame = new MilesToKilometersFrame();
        myFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        myFrame.pack();
        myFrame.setVisible(true);
    }
}
```

### Below is a screenshot of the output of this program. 
## I changed the calculation from increments of 1 to increments of 0.1 as mileage is often tracked more specifically than years.

![Screenshot 2025-04-26 205315](https://github.com/user-attachments/assets/9c3ff629-44c0-4bb5-b76e-ae61677ce410)
