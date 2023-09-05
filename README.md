# oibsip_taskno4
# oibsip_4
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;
import java.util.Timer;
import java.util.TimerTask;

public class OnlineExaminationSystem {
    private static Map<String, String> users = new HashMap<>();
    private static Map<String, String> profiles = new HashMap<>();
    private static Map<String, Integer> scores = new HashMap<>();
    private static String currentUser = null;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
		users.put("user1", "password1");
        users.put("user2", "password2");

        while (true) {
            if (currentUser == null) {
                System.out.println("\nWelcome to the Online Examination System");
                System.out.println("1. Login");
                System.out.println("2. Quit");
                System.out.print("Select an option: ");

                int choice = scanner.nextInt();
                scanner.nextLine(); // Consume newline

                switch (choice) {
                    case 1:
                        login(scanner);
                        break;
                    case 2:
                        System.out.println("Thank you for using the Online Examination System. Goodbye!");
                        scanner.close();
                        System.exit(0);
                    default:
                        System.out.println("Invalid option. Please try again.");
                }
            } else {
                System.out.println("\nOnline Examination Menu");
                System.out.println("1. Start Exam");
                System.out.println("2. Update Profile");
                System.out.println("3. Change Password");
                System.out.println("4. Close Session");
                System.out.println("5. Logout");
                System.out.print("Select an option: ");

                int choice = scanner.nextInt();
                scanner.nextLine(); // Consume newline

                switch (choice) {
                    case 1:
                        startExam(scanner);
                        break;
                    case 2:
                        updateProfile(scanner);
                        break;
                    case 3:
                        changePassword(scanner);
                        break;
                    case 4:
                        closeSession();
                        break;
                    case 5:
                        logout();
                        break;
                    default:
                        System.out.println("Invalid option. Please try again.");
                }
            }
        }
    }

    private static void login(Scanner scanner) {
        System.out.print("Enter your username: ");
        String username = scanner.nextLine();
        System.out.print("Enter your password: ");
        String password = scanner.nextLine();

        if (users.containsKey(username) && users.get(username).equals(password)) {
            currentUser = username;
            System.out.println("Login successful. Welcome, " + username + "!");
        } else {
            System.out.println("Login failed. Please check your username and password.");
        }
    }

    private static void startExam(Scanner scanner) {
        System.out.println("Starting the exam...");

        // Simulated timer for the exam (e.g., 30 minutes)
        Timer timer = new Timer();
        timer.schedule(new TimerTask() {
          
            public void run() {
                System.out.println("\nTime's up! Auto-submitting your exam...");
                submitExam();
                timer.cancel();
            }
        }, 30 * 60 * 1000); // 30 minutes in milliseconds

        // Simulated exam questions and answers
        int score = 0;
        System.out.println("MCQs (Select the correct option - A, B, C, or D):");
        System.out.println("1. What is the capital of France?");
        System.out.println("A. Paris");
        System.out.println("B. London");
        System.out.println("C. Berlin");
        System.out.println("D. Madrid");
        System.out.print("Your answer: ");
        String answer1 = scanner.nextLine().trim();
        if (answer1.equalsIgnoreCase("A")) {
            score++;
        }

        System.out.println("2. What is the largest planet in our solar system?");
        System.out.println("A. Earth");
        System.out.println("B. Mars");
        System.out.println("C. Jupiter");
        System.out.println("D. Venus");
        System.out.print("Your answer: ");
        String answer2 = scanner.nextLine().trim();
        if (answer2.equalsIgnoreCase("C")) {
            score++;
        }

        System.out.println("3. What is 7 multiplied by 9?");
        System.out.println("A. 49");
        System.out.println("B. 56");
        System.out.println("C. 63");
        System.out.println("D. 77");
        System.out.print("Your answer: ");
        String answer3 = scanner.nextLine().trim();
        if (answer3.equalsIgnoreCase("C")) {
            score++;
        }

        scores.put(currentUser, score);
        System.out.println("Exam submitted. Your score: " + score);
    }

    private static void updateProfile(Scanner scanner) {
        System.out.println("Update your profile:");
        System.out.print("Full Name: ");
        String fullName = scanner.nextLine();
        System.out.print("Email: ");
        String email = scanner.nextLine();

        profiles.put(currentUser, "Full Name: " + fullName + ", Email: " + email);
        System.out.println("Profile updated successfully.");
    }

    private static void changePassword(Scanner scanner) {
        System.out.print("Enter your current password: ");
        String currentPassword = scanner.nextLine();

        if (users.get(currentUser).equals(currentPassword)) {
            System.out.print("Enter your new password: ");
            String newPassword = scanner.nextLine();
            users.put(currentUser, newPassword);
            System.out.println("Password changed successfully.");
        } else {
            System.out.println("Incorrect current password. Password change failed.");
        }
    }

private static void submitExam() {
    // Here, you can perform any additional actions needed when the exam is submitted,
    // such as storing the user's exam responses, calculating the final score, etc.
    System.out.println("Exam submitted.");
}
    private static void closeSession() {
        System.out.println("Closing the session...");
        currentUser = null;
        System.out.println("Session closed.");
    }

    private static void logout() {
        currentUser = null;
        System.out.println("Logged out successfully.");
    }
}
