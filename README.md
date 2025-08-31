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

