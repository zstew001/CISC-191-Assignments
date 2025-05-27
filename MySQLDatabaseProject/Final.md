## Final Project CISC 191
## Challenges I ran into with this project:
### 1. Issues with failure to import lines from TSV file. Temp fix by importing data via whitespace separation combined with print statements to check which lines were being missed. This led to the realization that the file format provided wasn't actually "TSV". I was able to run the file through a google docs script to convert whitespaces to tabs based on ASCII vals.
### 2. Significant amounts of duplicates of each table unless the auto_stats DB was truncated between each use of the program. This was probably not a significant issue but I chose to find a fix to prevent duplicate data entries(more user friendly in my opinion).
### 3. Issues with null values causing incorrect data placement within tables when attempting to Stringify each piece of data being picked up by the GUI. Solved this by changing method to StringBuilder. 

### DBUtils class contains core program logic. Connects to MySQL, creates tables using MySql commands, and imports data from TSV file to fill auto_stats DB tables.
### SliderPanel class creates the UI frame, sliders for mpg/horsepower, and user input textbox for car_name.
### AutoStatsViewer loads and formats the Swing GUI elemends from SliderPanel. Also contains the logic for fetching info from auto_stats and populating the UI elements with desired info.
### Main provides the filepath for desired TSV file, calls from DBUtils and AutoStatsViewer to load the program.

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.sql.*;

public class DBUtils {
    public static Connection connectAndSetupDatabase() throws Exception {
        String dbURL = "jdbc:mysql://localhost:3306/";
        String user = "testuser123";
        String password = "***********"; // Removed password from github upload for personal privacy reasons. -It exists on my personal machine.

        Connection conn = DriverManager.getConnection(dbURL, user, password);
        Statement stmt = conn.createStatement();
        stmt.executeUpdate("CREATE DATABASE IF NOT EXISTS auto_stats");
        stmt.executeUpdate("USE auto_stats");

        // Final UNIQUE clause due to issue with data being duplicated in MySQL auto_stats DB.
        String createTableSQL = """
            CREATE TABLE IF NOT EXISTS auto_stats (
                id INT AUTO_INCREMENT PRIMARY KEY,
                mpg FLOAT,
                cylinders INT,
                displacement FLOAT,
                horsepower FLOAT,
                weight FLOAT,
                acceleration FLOAT,
                model_year INT,
                origin INT,
                car_name VARCHAR(100),
                UNIQUE(mpg, cylinders, displacement, horsepower, weight, acceleration, model_year, origin, car_name)
            )
            """;
        stmt.executeUpdate(createTableSQL);
        return conn;
    }

    public static void importTSVData(Connection conn, String tsvFile) {
        String insertSQL = """
            INSERT IGNORE INTO auto_stats (mpg, cylinders, displacement, horsepower, weight, acceleration, model_year, origin, car_name)
            VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?)
            """;

        try (PreparedStatement stmt = conn.prepareStatement(insertSQL);
             BufferedReader br = new BufferedReader(new FileReader(tsvFile))) {

            String line;
            while ((line = br.readLine()) != null) {
                line = line.trim();
                if (line.isEmpty()) continue;

                String[] data = line.split("\\t"); // Initial split method only worked with whitespace as separation indicator prior to debug changes. Ask professor why this was the case if possible.
                if (data.length < 9) continue;

                try {
                    stmt.setObject(1, parseFloat(data[0]));
                    stmt.setInt(2, (int) Float.parseFloat(data[1].trim()));
                    stmt.setFloat(3, Float.parseFloat(data[2].trim()));
                    stmt.setObject(4, parseFloat(data[3]));
                    stmt.setFloat(5, Float.parseFloat(data[4].trim()));
                    stmt.setFloat(6, Float.parseFloat(data[5].trim()));
                    stmt.setInt(7, (int) Float.parseFloat(data[6].trim()));
                    stmt.setInt(8, (int) Float.parseFloat(data[7].trim()));
                    stmt.setString(9, data[8].replace("\"", "").trim()); //Issue with car_name string vals caused inconsistency re. car_name table data read.
                    stmt.executeUpdate();
                } catch (Exception ignored) {

                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
    // Forced to use this method to handle null value fields. Removes whitespaces surrounding each input String, checks if value is null/NA and the method returns null if check returns true, else parses value as Float.
    private static Float parseFloat(String value) {
        value = value.trim();
        return value.equalsIgnoreCase("NA") ? null : Float.parseFloat(value);
    }
}

import javax.swing.*;
import java.awt.*;

public class SliderPanel extends JPanel {
    private final JTextField carNameField = new JTextField(10);
    private final JSlider mpgSlider = new JSlider(0, 60, 30);
    private final JSlider hpSlider = new JSlider(0, 300, 150);

    public SliderPanel(Runnable onChange) {
        setLayout(new GridBagLayout());
        GridBagConstraints gbc = new GridBagConstraints();

        //Labels
        gbc.insets = new Insets(5, 5, 0, 5);
        gbc.gridy = 0;

        gbc.gridx = 0;
        gbc.anchor = GridBagConstraints.CENTER;
        add(new JLabel("Car Name:"), gbc);

        gbc.gridx = 1;
        add(new JLabel("MPG:"), gbc);

        gbc.gridx = 2;
        add(new JLabel("Horsepower:"), gbc);

        //Input
        gbc.insets = new Insets(0, 5, 5, 5);
        gbc.gridy = 1;

        //TextField for car_name
        gbc.gridx = 0;
        gbc.fill = GridBagConstraints.HORIZONTAL;
        gbc.anchor = GridBagConstraints.CENTER;
        add(carNameField, gbc);
        carNameField.addActionListener(e -> onChange.run());

        //Slider for mpg
        gbc.gridx = 1;
        mpgSlider.setMajorTickSpacing(15);
        mpgSlider.setPaintTicks(true);
        mpgSlider.setPaintLabels(true);
        mpgSlider.addChangeListener(e -> onChange.run());
        add(mpgSlider, gbc);

        //Slider for horsepower
        gbc.gridx = 2;
        hpSlider.setMajorTickSpacing(75);
        hpSlider.setPaintTicks(true);
        hpSlider.setPaintLabels(true);
        hpSlider.addChangeListener(e -> onChange.run());
        add(hpSlider, gbc);
    }

    public int getMPG() {
        return mpgSlider.getValue();
    }

    public int getHorsepower() {
        return hpSlider.getValue();
    }

    public String getCarNameFilter() {
        return carNameField.getText().trim();
    }
}

import javax.swing.*;
import java.awt.*;
import java.sql.*;

public class AutoStatsViewer extends JFrame {
    private final JTextArea resultArea = new JTextArea();
    private final JTextField queryField = new JTextField("ALL");
    private final SliderPanel sliderPanel;
    private final Connection conn;

    public AutoStatsViewer(Connection conn) throws SQLException {
        super("Auto Stats Viewer");
        this.conn = conn;

        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setSize(700, 450);
        setLayout(new BorderLayout(5, 5));

        JButton runBtn = new JButton("Run Query");
        runBtn.addActionListener(e -> runTextQuery());

        JPanel top = new JPanel(new BorderLayout(5, 5));
        top.add(new JLabel("Query:"), BorderLayout.WEST);
        top.add(queryField, BorderLayout.CENTER);
        top.add(runBtn, BorderLayout.EAST);

        resultArea.setEditable(false);
        add(top, BorderLayout.NORTH);
        add(new JScrollPane(resultArea), BorderLayout.CENTER);

        sliderPanel = new SliderPanel(this::runSliderQuery);
        add(sliderPanel, BorderLayout.SOUTH);

        runTextQuery();
    }


    private void runTextQuery() {
        if (!"ALL".equalsIgnoreCase(queryField.getText().trim())) {
            JOptionPane.showMessageDialog(this, "Only 'ALL' supported.");
            return;
        }
        try (Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery("SELECT * FROM auto_stats")) {
            showResults(rs);
        } catch (SQLException ex) {
            showError(ex.getMessage());
        }
    }

    private void runSliderQuery() {
        String carNameFilter = sliderPanel.getCarNameFilter();
        boolean hasCarNameFilter = !carNameFilter.isEmpty();

        StringBuilder sql = new StringBuilder("SELECT * FROM auto_stats WHERE mpg >= ? AND horsepower >= ?"); // Had to switch to StringBuilder method here. Wasn't covered in class but learned last semester. Ask professor alternative method to do this if possible.
        if (hasCarNameFilter) {
            sql.append(" AND car_name LIKE ?");
        }
        sql.append(" LIMIT 100");

        try (PreparedStatement ps = conn.prepareStatement(sql.toString())) {
            ps.setFloat(1, sliderPanel.getMPG());
            ps.setFloat(2, sliderPanel.getHorsepower());
            if (hasCarNameFilter) {
                ps.setString(3, "%" + carNameFilter + "%");
            }
            try (ResultSet rs = ps.executeQuery()) {
                showResults(rs);
            }
        } catch (SQLException ex) {
            showError(ex.getMessage());
        }
    }

    private void showResults(ResultSet rs) throws SQLException {
        StringBuilder sb = new StringBuilder(); // Tried converting each datatype to String then parsing prior to this implementation, caused issues with duplicates prior to fixing DBUtils data duplication error.
        ResultSetMetaData md = rs.getMetaData();
        int cols = md.getColumnCount();
        while (rs.next()) { // Logic: While ResultSet has new data to read, append ColumnName, append Separation var, append info in ColumnName as String, Read/Append info between columns.
            for (int i = 1; i <= cols; i++) {
                sb.append(md.getColumnName(i)).append(": ").append(rs.getString(i)).append("  ");
            }
            sb.append("\n"); // New line after each row of data. Tried to print each line to the feed but didn't work.
        }
        resultArea.setText(sb.toString());
    }

    private void showError(String msg) {
        JOptionPane.showMessageDialog(this, msg, "Error", JOptionPane.ERROR_MESSAGE);
    }
}

import java.sql.*;
public class Main {
    public static void main(String[] args) {
        try {
            Connection conn = DBUtils.connectAndSetupDatabase();
            DBUtils.importTSVData(conn, "C:\\CS 191\\Final.txt");
            javax.swing.SwingUtilities.invokeLater(() -> {
                try {
                    new AutoStatsViewer(conn).setVisible(true);
                } catch (SQLException e) {
                    throw new RuntimeException(e);
                }
            });
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```
