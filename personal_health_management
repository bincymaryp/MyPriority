package org.example;
import javax.swing.*;
import java.awt.Color;
import javax.swing.JLabel;
import java.awt.*;
import java.awt.event.*;
import java.util.HashMap;
import java.util.Map;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Timer;
import java.util.TimerTask;

public class LoginPage extends JFrame {
    private CardLayout cardLayout;
    private JPanel cardPanel;
    private LoginPanel loginPanel;
    private SignUpPanel signUpPanel;
    private DashboardPanel dashboardPanel;
    private AppointmentPanel appointmentPanel;
    private DietPlanPanel dietPlanPanel;
    private PrescriptionPanel prescriptionPanel;
    private MessagePanel messagePanel;
    private Map<String, User> users;
    private JLabel backgroundLabel;
    private User currentUser;
    private Timer waterReminderTimer;

    public LoginPage() {
        users = new HashMap<>();
        users.put("test", new User("Test User", "test", "password", "70", "170", "30", "Male"));

        setTitle("MyPriority");
        setSize(800, 600);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);

        ImageIcon backgroundImage = new ImageIcon("C:/Users/Bincy/IdeaProjects/personal_health/src/main/Resource/backimg.jpg");
        backgroundLabel = new JLabel(backgroundImage);
        backgroundLabel.setLayout(new BorderLayout());
        setContentPane(backgroundLabel);

        JLabel titleLabel = new JLabel("MyPriority");
        titleLabel.setFont(new Font("Arial", Font.BOLD, 36));
        Color customColor = new Color(0, 0, 71);
        titleLabel.setForeground(customColor);
        titleLabel.setHorizontalAlignment(JLabel.CENTER);
        titleLabel.setVerticalAlignment(JLabel.TOP);
        backgroundLabel.add(titleLabel, BorderLayout.NORTH);

        cardLayout = new CardLayout();
        cardPanel = new JPanel(cardLayout);
        cardPanel.setOpaque(false);

        loginPanel = new LoginPanel();
        signUpPanel = new SignUpPanel();
        dashboardPanel = new DashboardPanel();
        appointmentPanel = new AppointmentPanel();
        dietPlanPanel = new DietPlanPanel();
        prescriptionPanel = new PrescriptionPanel();
        messagePanel = new MessagePanel();

        cardPanel.add(loginPanel, "Login");
        cardPanel.add(signUpPanel, "SignUp");
        cardPanel.add(dashboardPanel, "Dashboard");
        cardPanel.add(appointmentPanel, "Appointment");
        cardPanel.add(dietPlanPanel, "DietPlan");
        cardPanel.add(prescriptionPanel, "Prescription");
        cardPanel.add(messagePanel, "Message");

        backgroundLabel.add(cardPanel, BorderLayout.CENTER);

        loginPanel.setSignUpButtonListener(e -> cardLayout.show(cardPanel, "SignUp"));
        signUpPanel.setLoginButtonListener(e -> cardLayout.show(cardPanel, "Login"));
    }

    private void startWaterReminder() {
        if (waterReminderTimer != null) {
            waterReminderTimer.cancel();
        }
        waterReminderTimer = new Timer();
        waterReminderTimer.scheduleAtFixedRate(new TimerTask() {
            @Override
            public void run() {
                SwingUtilities.invokeLater(() -> {
                    JOptionPane.showMessageDialog(LoginPage.this,
                            "It's time to drink water!",
                            "Water Reminder",
                            JOptionPane.INFORMATION_MESSAGE);
                });
            }
        }, 0, 2 * 60 * 60 * 1000);
    }

    private void stopWaterReminder() {
        if (waterReminderTimer != null) {
            waterReminderTimer.cancel();
            waterReminderTimer = null;
        }
    }

    private class LoginPanel extends JPanel {
        private JTextField usernameField;
        private JPasswordField passwordField;
        private JButton loginButton;
        private JButton goToSignUpButton;

        public LoginPanel() {
            setLayout(new GridBagLayout());
            setOpaque(false);

            GridBagConstraints gbc = new GridBagConstraints();
            gbc.fill = GridBagConstraints.HORIZONTAL;
            gbc.insets = new Insets(5, 5, 5, 5);

            usernameField = new JTextField(20);
            passwordField = new JPasswordField(20);
            loginButton = new JButton("Login");
            goToSignUpButton = new JButton("Go to Sign Up");

            addField(this, "Username:", usernameField, gbc, 0);
            addField(this, "Password:", passwordField, gbc, 1);

            gbc.gridx = 1;
            gbc.gridy = 2;
            gbc.gridwidth = 1;
            gbc.anchor = GridBagConstraints.EAST;
            add(loginButton, gbc);

            gbc.gridx = 1;
            gbc.gridy = 3;
            add(goToSignUpButton, gbc);

            loginButton.addActionListener(e -> {
                String username = usernameField.getText();
                String password = new String(passwordField.getPassword());
                if (users.containsKey(username) && users.get(username).password.equals(password)) {
                    JOptionPane.showMessageDialog(LoginPage.this, "Login successful!");
                    currentUser = users.get(username);
                    cardLayout.show(cardPanel, "Dashboard");
                } else {
                    JOptionPane.showMessageDialog(LoginPage.this, "Invalid username or password!");
                }
            });
        }

        public void setSignUpButtonListener(ActionListener listener) {
            goToSignUpButton.addActionListener(listener);
        }
    }

    private class SignUpPanel extends JPanel {
        private JTextField nameField, usernameField, weightField, heightField, ageField;
        private JPasswordField passwordField;
        private JRadioButton maleRadio, femaleRadio;
        private JButton signUpButton;
        private JButton goToLoginButton;

        public SignUpPanel() {
            setLayout(new GridBagLayout());
            setOpaque(false);

            GridBagConstraints gbc = new GridBagConstraints();
            gbc.fill = GridBagConstraints.HORIZONTAL;
            gbc.insets = new Insets(5, 5, 5, 5);

            nameField = new JTextField(20);
            usernameField = new JTextField(20);
            passwordField = new JPasswordField(20);
            weightField = new JTextField(20);
            heightField = new JTextField(20);
            ageField = new JTextField(20);
            maleRadio = new JRadioButton("Male");
            femaleRadio = new JRadioButton("Female");
            ButtonGroup genderGroup = new ButtonGroup();
            genderGroup.add(maleRadio);
            genderGroup.add(femaleRadio);
            signUpButton = new JButton("Sign Up");
            goToLoginButton = new JButton("Go to Login");

            addField(this, "Name:", nameField, gbc, 0);
            addField(this, "Username:", usernameField, gbc, 1);
            addField(this, "Password:", passwordField, gbc, 2);
            addField(this, "Weight (kg):", weightField, gbc, 3);
            addField(this, "Height (cm):", heightField, gbc, 4);
            addField(this, "Age:", ageField, gbc, 5);

            JPanel genderPanel = new JPanel(new FlowLayout(FlowLayout.LEFT));
            genderPanel.add(maleRadio);
            genderPanel.add(femaleRadio);
            gbc.gridx = 0;
            gbc.gridy = 6;
            gbc.gridwidth = 2;
            add(new JLabel("Gender:"), gbc);
            gbc.gridx = 1;
            add(genderPanel, gbc);

            gbc.gridx = 1;
            gbc.gridy = 7;
            gbc.gridwidth = 1;
            gbc.anchor = GridBagConstraints.EAST;
            add(signUpButton, gbc);

            gbc.gridy = 8;
            add(goToLoginButton, gbc);

            signUpButton.addActionListener(e -> {
                String name = nameField.getText();
                String username = usernameField.getText();
                String password = new String(passwordField.getPassword());
                String weight = weightField.getText();
                String height = heightField.getText();
                String age = ageField.getText();
                String gender = maleRadio.isSelected() ? "Male" : (femaleRadio.isSelected() ? "Female" : "Not specified");

                if (users.containsKey(username)) {
                    JOptionPane.showMessageDialog(LoginPage.this, "Username already exists!");
                } else {
                    users.put(username, new User(name, username, password, weight, height, age, gender));
                    JOptionPane.showMessageDialog(LoginPage.this, "Sign up successful!");
                    cardLayout.show(cardPanel, "Login");
                }
            });
        }

        public void setLoginButtonListener(ActionListener listener) {
            goToLoginButton.addActionListener(listener);
        }
    }

    private class DashboardPanel extends JPanel {
        private JToggleButton waterReminderToggle;

        public DashboardPanel() {
            setLayout(new BorderLayout());
            setBackground(new Color(173, 216, 230)); // Light blue background

            JPanel menuPanel = new JPanel(new GridBagLayout());
            menuPanel.setOpaque(false);
            GridBagConstraints gbc = new GridBagConstraints();
            gbc.gridwidth = GridBagConstraints.REMAINDER;
            gbc.fill = GridBagConstraints.HORIZONTAL;
            gbc.insets = new Insets(10, 10, 10, 10);

            String[] buttonLabels = {
                    "Book an Appointment",
                    "Message the Doctor",
                    "Diet Plan",
                    "Prescription Update"
            };

            for (String label : buttonLabels) {
                JButton button = new JButton(label);
                button.setPreferredSize(new Dimension(200, 40));
                button.addActionListener(e -> {
                    if (label.equals("Book an Appointment")) {
                        cardLayout.show(cardPanel, "Appointment");
                    } else if (label.equals("Diet Plan")) {
                        if (currentUser != null) {
                            dietPlanPanel.updateDietPlan(currentUser);
                            cardLayout.show(cardPanel, "DietPlan");
                        } else {
                            JOptionPane.showMessageDialog(LoginPage.this, "Please log in to view your diet plan.");
                        }
                    } else if (label.equals("Prescription Update")) {
                        prescriptionPanel.loadPrescription();
                        cardLayout.show(cardPanel, "Prescription");
                    } else if (label.equals("Message the Doctor")) {
                        cardLayout.show(cardPanel, "Message");
                    }
                });
                menuPanel.add(button, gbc);
            }

            waterReminderToggle = new JToggleButton("Water Reminder: OFF");
            waterReminderToggle.addActionListener(e -> {
                if (waterReminderToggle.isSelected()) {
                    startWaterReminder();
                    waterReminderToggle.setText("Water Reminder: ON");
                } else {
                    stopWaterReminder();
                    waterReminderToggle.setText("Water Reminder: OFF");
                }
            });
            menuPanel.add(waterReminderToggle, gbc);

            add(menuPanel, BorderLayout.CENTER);

            JButton logoutButton = new JButton("Logout");
            logoutButton.addActionListener(e -> {
                currentUser = null;
                stopWaterReminder();
                waterReminderToggle.setSelected(false);
                waterReminderToggle.setText("Water Reminder: OFF");
                cardLayout.show(cardPanel, "Login");
            });
            add(logoutButton, BorderLayout.SOUTH);
        }
    }

    private class AppointmentPanel extends JPanel {
        private JTextField dateField;
        private JSpinner timeSpinner;
        private JTextField doctorField, hospitalField;
        private JButton bookButton, backButton;

        public AppointmentPanel() {
            setLayout(new GridBagLayout());
            setOpaque(false);

            GridBagConstraints gbc = new GridBagConstraints();
            gbc.fill = GridBagConstraints.HORIZONTAL;
            gbc.insets = new Insets(5, 5, 5, 5);

            dateField = new JTextField(10);

            SpinnerDateModel timeModel = new SpinnerDateModel();
            timeSpinner = new JSpinner(timeModel);
            JSpinner.DateEditor timeEditor = new JSpinner.DateEditor(timeSpinner, "HH:mm");
            timeSpinner.setEditor(timeEditor);

            doctorField = new JTextField(20);
            hospitalField = new JTextField(20);
            bookButton = new JButton("Book Appointment");
            backButton = new JButton("Back to Dashboard");

            addField(this, "Date (yyyy-MM-dd):", dateField, gbc, 0);
            addField(this, "Time:", timeSpinner, gbc, 1);
            addField(this, "Doctor Name:", doctorField, gbc, 2);
            addField(this, "Hospital Name:", hospitalField, gbc, 3);

            gbc.gridx = 1;
            gbc.gridy = 4;
            gbc.gridwidth = 1;
            gbc.anchor = GridBagConstraints.EAST;
            add(bookButton, gbc);

            gbc.gridy = 5;
            add(backButton, gbc);

            bookButton.addActionListener(e -> {
                String dateStr = dateField.getText();
                Date selectedTime = (Date) timeSpinner.getValue();
                String doctor = doctorField.getText();
                String hospital = hospitalField.getText();

                if (dateStr.isEmpty() || selectedTime == null || doctor.isEmpty() || hospital.isEmpty()) {
                    JOptionPane.showMessageDialog(LoginPage.this, "Please fill in all fields!");
                } else {
                    SimpleDateFormat timeFormat = new SimpleDateFormat("HH:mm");
                    String timeStr = timeFormat.format(selectedTime);

                    JOptionPane.showMessageDialog(LoginPage.this,
                            "Appointment booked successfully!\n" +
                                    "Date: " + dateStr + "\n" +
                                    "Time: " + timeStr + "\n" +
                                    "Doctor: " + doctor + "\n" +
                                    "Hospital: " + hospital);
                    cardLayout.show(cardPanel, "Dashboard");
                }
            });

            backButton.addActionListener(e -> cardLayout.show(cardPanel, "Dashboard"));
        }
    }

    private class DietPlanPanel extends JPanel {
        private JTextArea dietPlanArea;
        private JButton backButton;

        public DietPlanPanel() {
            setLayout(new BorderLayout());
            setOpaque(false);

            dietPlanArea = new JTextArea(20, 40);
            dietPlanArea.setEditable(false);
            JScrollPane scrollPane = new JScrollPane(dietPlanArea);

            backButton = new JButton("Back to Dashboard");
            backButton.addActionListener(e -> cardLayout.show(cardPanel, "Dashboard"));

            add(scrollPane, BorderLayout.CENTER);
            add(backButton, BorderLayout.SOUTH);
        }

        public void updateDietPlan(User user) {
            double bmi = user.calculateBMI();
            String dietPlan = generateDietPlan(user, bmi);
            dietPlanArea.setText(dietPlan);
        }

        private String generateDietPlan(User user, double bmi) {
            StringBuilder plan = new StringBuilder();
            plan.append("Diet Plan for ").append(user.name).append("\n\n");
            plan.append("Age: ").append(user.age).append(" years\n");
            plan.append("Weight: ").append(user.weight).append(" kg\n");
            plan.append("Height: ").append(user.height).append(" cm\n");
            plan.append("BMI: ").append(String.format("%.2f", bmi)).append("\n\n");

            if (bmi < 18.5) {
                plan.append("You are underweight. Here's a diet plan to help you gain weight healthily:\n\n");
                plan.append("1. Increase your calorie intake\n");
                plan.append("2. Eat more protein-rich foods\n");
                plan.append("3. Include healthy fats in your diet\n");
                plan.append("4. Have frequent meals and snacks\n");
            } else if (bmi >= 18.5 && bmi < 25) {
                plan.append("You have a healthy weight. Here's a diet plan to maintain your weight:\n\n");
                plan.append("1. Eat a balanced diet with plenty of fruits and vegetables\n");
                plan.append("2. Include lean proteins in your meals\n");
                plan.append("3. Choose whole grains over refined grains\n");
                plan.append("4. Stay hydrated and limit sugary drinks\n");
            } else {
                plan.append("You are overweight. Here's a diet plan to help you lose weight healthily:\n\n");
                plan.append("1. Reduce your calorie intake\n");
                plan.append("2. Increase your intake of fruits and vegetables\n");
                plan.append("3. Choose lean proteins and limit fatty foods\n");
                plan.append("4. Exercise regularly\n");
            }

            return plan.toString();
        }
    }

    private class PrescriptionPanel extends JPanel {
        private JTextArea prescriptionArea;
        private JButton backButton;

        public PrescriptionPanel() {
            setLayout(new BorderLayout());
            setOpaque(false);

            prescriptionArea = new JTextArea(20, 40);
            prescriptionArea.setEditable(false);
            JScrollPane scrollPane = new JScrollPane(prescriptionArea);

            backButton = new JButton("Back to Dashboard");
            backButton.addActionListener(e -> cardLayout.show(cardPanel, "Dashboard"));

            add(scrollPane, BorderLayout.CENTER);
            add(backButton, BorderLayout.SOUTH);
        }

        public void loadPrescription() {
            prescriptionArea.setText("Your Prescription:\n\n" +
                    "1. Dollo - 1 tablet twice daily\n" +
                    "2. CARBIN-Z - 1 capsule before bed\n" +
                    "3. Paracetamol- 2 tablets with meals\n\n" +
                    "Please follow the dosage instructions carefully.\n" +
                    "If you experience any side effects, contact your doctor immediately.");
        }
    }

    private class MessagePanel extends JPanel {
        private JTextArea messageArea;
        private JTextField inputField;
        private JButton sendButton;
        private JButton backButton;

        public MessagePanel() {
            setLayout(new BorderLayout());
            setOpaque(false);

            messageArea = new JTextArea(15, 30);
            messageArea.setEditable(false);
            JScrollPane scrollPane = new JScrollPane(messageArea);

            inputField = new JTextField(20);
            sendButton = new JButton("Send");
            backButton = new JButton("Back to Dashboard");

            JPanel inputPanel = new JPanel();
            inputPanel.add(inputField);
            inputPanel.add(sendButton);

            add(scrollPane, BorderLayout.CENTER);
            add(inputPanel, BorderLayout.SOUTH);
            add(backButton, BorderLayout.NORTH);

            sendButton.addActionListener(e -> {
                String message = inputField.getText();
                if (!message.isEmpty()) {
                    messageArea.append("You: " + message + "\n");
                    inputField.setText("");
                    messageArea.append("Doctor: Your message has been received. I'll respond as soon as possible.\n\n");
                }
            });

            backButton.addActionListener(e -> cardLayout.show(cardPanel, "Dashboard"));
        }
    }

    private void addField(JPanel panel, String label, JComponent field, GridBagConstraints gbc, int y) {
        gbc.gridx = 0;
        gbc.gridy = y;
        gbc.gridwidth = 1;
        gbc.anchor = GridBagConstraints.EAST;
        panel.add(new JLabel(label), gbc);

        gbc.gridx = 1;
        gbc.anchor = GridBagConstraints.WEST;
        panel.add(field, gbc);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            new LoginPage().setVisible(true);
        });
    }
}

class User {
    String name, username, password, weight, height, age, gender;

    public User(String name, String username, String password, String weight, String height, String age, String gender) {
        this.name = name;
        this.username = username;
        this.password = password;
        this.weight = weight;
        this.height = height;
        this.age = age;
        this.gender = gender;
    }

    public double calculateBMI() {
        double weightKg = Double.parseDouble(weight);
        double heightM = Double.parseDouble(height) / 100.0;
        return weightKg / (heightM * heightM);
    }
}
