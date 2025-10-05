# QuizaApp
A console-based quiz application built in Java that tests users programming knowledge. Features include a Question class to store quiz data, MCQ with 4 options each, input validation, automatic scoring system, and real-time feedback. Users receive their final score with percentage and performance rating based on correct answers.
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Question {
    private String question;
    private List<String> options;
    private int correctAnswer;

    public Question(String question, List<String> options, int correctAnswer) {
        this.question = question;
        this.options = options;
        this.correctAnswer = correctAnswer;
    }

    public String getQuestion() {
        return question;
    }

    public List<String> getOptions() {
        return options;
    }

    public int getCorrectAnswer() {
        return correctAnswer;
    }

    public boolean checkAnswer(int userAnswer) {
        return userAnswer == correctAnswer;
    }
}

public class QuizApp {
    private List<Question> questions;
    private int score;
    private Scanner scanner;

    public QuizApp() {
        questions = new ArrayList<>();
        score = 0;
        scanner = new Scanner(System.in);
        loadQuestions();
    }

    private void loadQuestions() {
        // Question 1
        List<String> q1Options = new ArrayList<>();
        q1Options.add("HyperText Markup Language");
        q1Options.add("HighText Machine Language");
        q1Options.add("HyperText Making Language");
        q1Options.add("None of the above");
        questions.add(new Question("What does HTML stand for?", q1Options, 1));

        // Question 2
        List<String> q2Options = new ArrayList<>();
        q2Options.add("James Gosling");
        q2Options.add("Dennis Ritchie");
        q2Options.add("Bjarne Stroustrup");
        q2Options.add("Guido van Rossum");
        questions.add(new Question("Who created Java?", q2Options, 1));

        // Question 3
        List<String> q3Options = new ArrayList<>();
        q3Options.add("8");
        q3Options.add("16");
        q3Options.add("32");
        q3Options.add("64");
        questions.add(new Question("How many bits are in a byte?", q3Options, 1));

        // Question 4
        List<String> q4Options = new ArrayList<>();
        q4Options.add("Structured Query Language");
        q4Options.add("Simple Question Language");
        q4Options.add("System Quality Language");
        q4Options.add("Standard Query Logic");
        questions.add(new Question("What does SQL stand for?", q4Options, 1));

        // Question 5
        List<String> q5Options = new ArrayList<>();
        q5Options.add("Object-Oriented Programming");
        q5Options.add("Only One Programming");
        q5Options.add("Open Operating Protocol");
        q5Options.add("Operational Optimization Process");
        questions.add(new Question("What does OOP stand for?", q5Options, 1));

         // Question 6
        List<String> q6Options = new ArrayList<>();
        q6Options.add("8");
        q6Options.add("6");
        q6Options.add("7");
        q6Options.add("5");
        questions.add(new Question("Number of primitive datatypes in Java?", q6Options, 1));
    }

    public void startQuiz() {
        System.out.println("\nWELCOME TO THE ONLINE QUIZ APP");
        System.out.println("Answer the following questions:\n");

        for (int i = 0; i < questions.size(); i++) {
            Question q = questions.get(i);
            displayQuestion(i + 1, q);
            
            int userAnswer = getUserAnswer();
            
            if (q.checkAnswer(userAnswer)) {
                System.out.println("✓ Correct!\n");
                score++;
            } else {
                System.out.println("✗ Wrong! The correct answer was option " + q.getCorrectAnswer() + "\n");
            }
        }

        displayResults();
        scanner.close();
    }

    private void displayQuestion(int questionNumber, Question q) {
        System.out.println("Question " + questionNumber + ": " + q.getQuestion());
        List<String> options = q.getOptions();
        for (int i = 0; i < options.size(); i++) {
            System.out.println((i + 1) + ". " + options.get(i));
        }
    }

    private int getUserAnswer() {
        int answer = 0;
        boolean validInput = false;

        while (!validInput) {
            System.out.print("Your answer (1-4): ");
            try {
                answer = scanner.nextInt();
                if (answer >= 1 && answer <= 4) {
                    validInput = true;
                } else {
                    System.out.println("Please enter a number between 1 and 4.");
                }
            } catch (Exception e) {
                System.out.println("Invalid input! Please enter a number.");
                scanner.nextLine(); // Clear the buffer
            }
        }
        return answer;
    }

    private void displayResults() {
        System.out.println("\nQUIZ COMPLETED!");
        System.out.println("Your Score: " + score + " out of " + questions.size());
        
        double percentage = (double) score / questions.size() * 100;
        System.out.println("Percentage: " + String.format("%.2f", percentage) + "%");
        
        System.out.println("\nPerformance Rating:");
        if (percentage >= 80) {
            System.out.println("Excellent!");
        } else if (percentage >= 60) {
            System.out.println("Good Job!");
        } else if (percentage >= 40) {
            System.out.println("Fair");
        } else {
            System.out.println("Need Improvement!");
        }
    }

    public static void main(String[] args) {
        QuizApp quiz = new QuizApp();
        quiz.startQuiz();
    }
}
