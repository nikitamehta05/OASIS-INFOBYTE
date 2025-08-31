TASK 1.Number Guessing Game

      import java.util.Random;
      import java.util.Scanner;
      
      public class NumberGuessingGame {
          public static void main(String[] args) {
              Scanner scanner = new Scanner(System.in);
              Random random = new Random();
      
              int totalScore = 0;
              int round = 1;
              int maxAttempts = 7;
              boolean playAgain = true;
      
              System.out.println("Welcome to the Number Guessing Game!");
      
              while (playAgain) {
                  int numberToGuess = random.nextInt(100) + 1;
                  int attemptsLeft = maxAttempts;
                  boolean guessedCorrectly = false;
      
                  System.out.println("\n Round " + round + " - Guess the number between 1 and 100.");
                  System.out.println(" You have " + maxAttempts + " attempts.");
      
                  while (attemptsLeft > 0) {
                      System.out.print("Enter your guess: ");
                      int userGuess;
      
                      // Check for valid integer input
                      if (!scanner.hasNextInt()) {
                          System.out.println(" Invalid input! Please enter a number.");
                          scanner.next(); // clear invalid input
                          continue;
                      }
      
                      userGuess = scanner.nextInt();
                      attemptsLeft--;
      
                      if (userGuess == numberToGuess) {
                          int points = 10 * (attemptsLeft + 1);  // Reward based on attempts left
                          totalScore += points;
                          System.out.println(" Correct! You guessed the number in " + (maxAttempts - attemptsLeft) + " attempts.");
                          System.out.println(" You earned " + points + " points this round.");
                          guessedCorrectly = true;
                          break;
                      } else if (userGuess < numberToGuess) {
                          System.out.println("Too low! Try again. Attempts left: " + attemptsLeft);
                      } else {
                          System.out.println("Too high! Try again. Attempts left: " + attemptsLeft);
                      }
                  }
      
                  if (!guessedCorrectly) {
                      System.out.println("You've used all attempts! The number was: " + numberToGuess);
                  }
      
                  System.out.println("Total Score: " + totalScore);
                  round++;
      
                  // Ask to play again
                  System.out.print("\nDo you want to play another round? (yes/no): ");
                  scanner.nextLine(); // consume newline
                  String response = scanner.nextLine().trim().toLowerCase();
                  playAgain = response.equals("yes") || response.equals("y");
              }
      
              System.out.println("\nThanks for playing! Final Score: " + totalScore);
              scanner.close();
          }
      }


TASK 2 Online ExamINATION

                  import java.awt.*;
                  import java.awt.event.*;
                  import javax.swing.*;
                  
                  public class OnlineExam extends JFrame implements ActionListener {
                      CardLayout card;
                      JPanel mainPanel;
                  
                      JTextField loginUsername;
                      JPasswordField loginPassword;
                      JButton loginButton;
                  
                      JTextField profileUsername;
                      JPasswordField profilePassword;
                      JButton updateProfileButton, logoutButton1;
                  
                      JLabel questionLabel, timerLabel;
                      JRadioButton[] options = new JRadioButton[4];
                      ButtonGroup bg;
                      JButton nextButton, submitButton, logoutButton2;
                      Timer timer;
                  
                      String currentUser = "admin";
                      String currentPass = "admin123";
                      int timeLeft = 60; // seconds
                      int currentQuestion = 0;
                      int score = 0;
                  
                      // Java-based MCQs
                      String[][] questions = {
                          {"Which keyword is used to inherit a class in Java?",
                           "super", "this", "extends", "implements", "3"},
                          {"Which method is the entry point of a Java program?",
                           "start()", "main()", "run()", "init()", "2"},
                          {"Which of these is not a Java keyword?",
                           "final", "include", "static", "try", "2"},
                          {"Which company originally developed Java?",
                           "Oracle", "Microsoft", "IBM", "Sun Microsystems", "4"},
                          {"What is the default value of an uninitialized boolean in Java?",
                           "true", "1", "null", "false", "4"}
                      };
                  
                      public OnlineExam() {
                          setTitle("Online Examination System");
                          setSize(600, 400);
                          setDefaultCloseOperation(EXIT_ON_CLOSE);
                          setLocationRelativeTo(null);
                  
                          card = new CardLayout();
                          mainPanel = new JPanel(card);
                  
                          mainPanel.add(loginPanel(), "Login");
                          mainPanel.add(profilePanel(), "Profile");
                          mainPanel.add(examPanel(), "Exam");
                  
                          add(mainPanel);
                          card.show(mainPanel, "Login");
                          setVisible(true);
                      }
                  
                      private JPanel loginPanel() {
                          JPanel panel = new JPanel(new GridLayout(4, 1));
                          loginUsername = new JTextField();
                          loginPassword = new JPasswordField();
                          loginButton = new JButton("Login");
                          loginButton.addActionListener(this);
                  
                          panel.setBorder(BorderFactory.createTitledBorder("Login"));
                          panel.add(new JLabel("Username:"));
                          panel.add(loginUsername);
                          panel.add(new JLabel("Password:"));
                          panel.add(loginPassword);
                          panel.add(loginButton);
                  
                          return panel;
                      }
                  
                      private JPanel profilePanel() {
                          JPanel panel = new JPanel(new GridLayout(5, 1));
                          profileUsername = new JTextField(currentUser);
                          profilePassword = new JPasswordField(currentPass);
                          updateProfileButton = new JButton("Update Profile");
                          logoutButton1 = new JButton("Logout");
                          updateProfileButton.addActionListener(this);
                          logoutButton1.addActionListener(this);
                  
                          panel.setBorder(BorderFactory.createTitledBorder("Update Profile"));
                          panel.add(new JLabel("New Username:"));
                          panel.add(profileUsername);
                          panel.add(new JLabel("New Password:"));
                          panel.add(profilePassword);
                          panel.add(updateProfileButton);
                          panel.add(logoutButton1);
                  
                          return panel;
                      }
                  
                      private JPanel examPanel() {
                          JPanel panel = new JPanel(new BorderLayout());
                  
                          JPanel topPanel = new JPanel(new BorderLayout());
                          timerLabel = new JLabel("Time: 01:00", JLabel.RIGHT);
                          logoutButton2 = new JButton("Logout");
                          logoutButton2.addActionListener(this);
                          topPanel.add(new JLabel("Exam Panel"), BorderLayout.WEST);
                          topPanel.add(timerLabel, BorderLayout.CENTER);
                          topPanel.add(logoutButton2, BorderLayout.EAST);
                  
                          JPanel centerPanel = new JPanel(new GridLayout(6, 1));
                          questionLabel = new JLabel("Question?");
                          bg = new ButtonGroup();
                          for (int i = 0; i < 4; i++) {
                              options[i] = new JRadioButton();
                              bg.add(options[i]);
                              centerPanel.add(options[i]);
                          }
                  
                          JPanel bottomPanel = new JPanel();
                          nextButton = new JButton("Next");
                          submitButton = new JButton("Submit");
                          nextButton.addActionListener(this);
                          submitButton.addActionListener(this);
                          bottomPanel.add(nextButton);
                          bottomPanel.add(submitButton);
                  
                          centerPanel.add(questionLabel);
                          panel.add(topPanel, BorderLayout.NORTH);
                          panel.add(centerPanel, BorderLayout.CENTER);
                          panel.add(bottomPanel, BorderLayout.SOUTH);
                  
                          return panel;
                      }
                  
                      void loadQuestion() {
                          if (currentQuestion < questions.length) {
                              bg.clearSelection();
                              String[] q = questions[currentQuestion];
                              questionLabel.setText("Q" + (currentQuestion + 1) + ": " + q[0]);
                              for (int i = 0; i < 4; i++) {
                                  options[i].setText(q[i + 1]);
                              }
                          } else {
                              endExam();
                          }
                      }
                  
                      void checkAnswer() {
                          String correct = questions[currentQuestion][5];
                          for (int i = 0; i < 4; i++) {
                              if (options[i].isSelected() && (i + 1) == Integer.parseInt(correct)) {
                                  score++;
                              }
                          }
                      }
                  
                      void startTimer() {
                          timer = new Timer(1000, e -> {
                              timeLeft--;
                              int min = timeLeft / 60;
                              int sec = timeLeft % 60;
                              timerLabel.setText(String.format("Time: %02d:%02d", min, sec));
                              if (timeLeft <= 0) {
                                  timer.stop();
                                  endExam();
                              }
                          });
                          timer.start();
                      }
                  
                      void endExam() {
                          if (timer != null) timer.stop();
                          JOptionPane.showMessageDialog(this, "Exam finished. Score: " + score + "/" + questions.length);
                          resetSession();
                      }
                  
                      void resetSession() {
                          currentQuestion = 0;
                          score = 0;
                          timeLeft = 60;
                          card.show(mainPanel, "Login");
                      }
                  
                      public void actionPerformed(ActionEvent e) {
                          if (e.getSource() == loginButton) {
                              String u = loginUsername.getText().trim();
                              String p = new String(loginPassword.getPassword()).trim();
                              if (u.equals(currentUser) && p.equals(currentPass)) {
                                  loginUsername.setText("");
                                  loginPassword.setText("");
                                  card.show(mainPanel, "Profile");
                              } else {
                                  JOptionPane.showMessageDialog(this, "Invalid login");
                              }
                          }
                  
                          else if (e.getSource() == updateProfileButton) {
                              currentUser = profileUsername.getText().trim();
                              currentPass = new String(profilePassword.getPassword()).trim();
                              JOptionPane.showMessageDialog(this, "Profile Updated!");
                              card.show(mainPanel, "Exam");
                              loadQuestion();
                              startTimer();
                          }
                  
                          else if (e.getSource() == nextButton) {
                              checkAnswer();
                              currentQuestion++;
                              loadQuestion();
                          }
                  
                          else if (e.getSource() == submitButton) {
                              checkAnswer();
                              endExam();
                          }
                  
                          else if (e.getSource() == logoutButton1 || e.getSource() == logoutButton2) {
                              if (timer != null) timer.stop();
                              resetSession();
                          }
                      }
                  
                      public static void main(String[] args) {
                          SwingUtilities.invokeLater(OnlineExam::new);
                      }
                  }


TASK 3.ATM INTERFACE

                  import java.util.*;
                  
                  class Transaction {
                      String type;
                      double amount;
                      String recipient;
                      Date date;
                  
                      Transaction(String type, double amount, String recipient) {
                          this.type = type;
                          this.amount = amount;
                          this.recipient = recipient;
                          this.date = new Date();
                      }
                  
                      public String toString() {
                          if (recipient == null)
                              return type + " of $" + amount + " on " + date;
                          else
                              return type + " of $" + amount + " to " + recipient + " on " + date;
                      }
                  }
                  
                  class TransactionHistory {
                      private List<Transaction> transactions = new ArrayList<>();
                  
                      public void addTransaction(String type, double amount, String recipient) {
                          transactions.add(new Transaction(type, amount, recipient));
                      }
                  
                      public void showHistory() {
                          if (transactions.isEmpty()) {
                              System.out.println("No transactions yet.");
                          } else {
                              for (Transaction t : transactions) {
                                  System.out.println(t);
                              }
                          }
                      }
                  }
                  
                  class User {
                      String userId;
                      String userPin;
                      double balance;
                      TransactionHistory history;
                  
                      User(String userId, String userPin) {
                          this.userId = userId;
                          this.userPin = userPin;
                          this.balance = 1000.0; // default balance
                          this.history = new TransactionHistory();
                      }
                  
                      public boolean validatePin(String pin) {
                          return this.userPin.equals(pin);
                      }
                  }
                  
                  class Bank {
                      private Map<String, User> users = new HashMap<>();
                  
                      public Bank() {
                          // Add a default user
                          addUser(new User("12345", "6789"));
                      }
                  
                      public void addUser(User user) {
                          users.put(user.userId, user);
                      }
                  
                      public User getUser(String userId) {
                          return users.get(userId);
                      }
                  
                      public boolean userExists(String userId) {
                          return users.containsKey(userId);
                      }
                  
                      public void transfer(User sender, String recipientId, double amount) {
                          if (!userExists(recipientId)) {
                              System.out.println("Recipient account not found.");
                              return;
                          }
                  
                          if (sender.balance < amount) {
                              System.out.println("Insufficient balance.");
                              return;
                          }
                  
                          User recipient = getUser(recipientId);
                          sender.balance -= amount;
                          recipient.balance += amount;
                  
                          sender.history.addTransaction("Transfer", amount, recipientId);
                          recipient.history.addTransaction("Received", amount, sender.userId);
                  
                          System.out.println("Transfer successful!");
                      }
                  }
                  
                  public class ATM {
                      static Scanner sc = new Scanner(System.in);
                      static Bank bank = new Bank();
                  
                      public static void main(String[] args) {
                          System.out.println("Welcome to the ATM!");
                          System.out.print("Enter User ID: ");
                          String userId = sc.nextLine();
                          System.out.print("Enter PIN: ");
                          String pin = sc.nextLine();
                  
                          User user = bank.getUser(userId);
                          if (user != null && user.validatePin(pin)) {
                              System.out.println("Login successful!\n");
                              showMenu(user);
                          } else {
                              System.out.println("Invalid ID or PIN. Access denied.");
                          }
                      }
                  
                      public static void showMenu(User user) {
                          int choice;
                          do {
                              System.out.println("\n===== ATM Menu =====");
                              System.out.println("1. Transaction History");
                              System.out.println("2. Withdraw");
                              System.out.println("3. Deposit");
                              System.out.println("4. Transfer");
                              System.out.println("5. Quit");
                              System.out.print("Choose an option: ");
                              choice = sc.nextInt();
                  
                              switch (choice) {
                                  case 1:
                                      user.history.showHistory();
                                      break;
                                  case 2:
                                      withdraw(user);
                                      break;
                                  case 3:
                                      deposit(user);
                                      break;
                                  case 4:
                                      transfer(user);
                                      break;
                                  case 5:
                                      System.out.println("Thank you for using the ATM. Goodbye!");
                                      break;
                                  default:
                                      System.out.println("Invalid option.");
                              }
                          } while (choice != 5);
                      }
                  
                      public static void withdraw(User user) {
                          System.out.print("Enter amount to withdraw: $");
                          double amount = sc.nextDouble();
                          if (amount <= 0) {
                              System.out.println("Invalid amount.");
                          } else if (amount > user.balance) {
                              System.out.println("Insufficient balance.");
                          } else {
                              user.balance -= amount;
                              user.history.addTransaction("Withdraw", amount, null);
                              System.out.println("Withdraw successful. New balance: $" + user.balance);
                          }
                      }
                  
                      public static void deposit(User user) {
                          System.out.print("Enter amount to deposit: $");
                          double amount = sc.nextDouble();
                          if (amount <= 0) {
                              System.out.println("Invalid amount.");
                          } else {
                              user.balance += amount;
                              user.history.addTransaction("Deposit", amount, null);
                              System.out.println("Deposit successful. New balance: $" + user.balance);
                          }
                      }
                  
                      public static void transfer(User user) {
                          System.out.print("Enter recipient User ID: ");
                          String recipientId = sc.next();
                          System.out.print("Enter amount to transfer: $");
                          double amount = sc.nextDouble();
                          bank.transfer(user, recipientId, amount);
                      }
                  }
