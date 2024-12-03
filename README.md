import java.io.*;
import java.util.Scanner;

public class DocumentConverter {
    
    // Convert text file content to uppercase
    public static void convertToUppercase(String inputFilePath, String outputFilePath) throws IOException {
        try (BufferedReader reader = new BufferedReader(new FileReader(inputFilePath));
             BufferedWriter writer = new BufferedWriter(new FileWriter(outputFilePath))) {
             
            String line;
            while ((line = reader.readLine()) != null) {
                writer.write(line.toUpperCase());
                writer.newLine();
            }
        } catch (IOException e) {
            throw new IOException("Error during uppercase conversion: " + e.getMessage(), e);
        }
    }

    // Convert text file content to lowercase
    public static void convertToLowercase(String inputFilePath, String outputFilePath) throws IOException {
        try (BufferedReader reader = new BufferedReader(new FileReader(inputFilePath));
             BufferedWriter writer = new BufferedWriter(new FileWriter(outputFilePath))) {
             
            String line;
            while ((line = reader.readLine()) != null) {
                writer.write(line.toLowerCase());
                writer.newLine();
            }
        } catch (IOException e) {
            throw new IOException("Error during lowercase conversion: " + e.getMessage(), e);
        }
    }

    // Convert text file content to CSV (each word separated by commas)
    public static void convertToCSV(String inputFilePath, String outputFilePath) throws IOException {
        try (BufferedReader reader = new BufferedReader(new FileReader(inputFilePath));
             BufferedWriter writer = new BufferedWriter(new FileWriter(outputFilePath))) {
             
            String line;
            while ((line = reader.readLine()) != null) {
                String[] words = line.split("\\s+"); // Split by spaces
                writer.write(String.join(",", words)); // Join words with commas
                writer.newLine();
            }
        } catch (IOException e) {
            throw new IOException("Error during CSV conversion: " + e.getMessage(), e);
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Welcome to the Document Converter Project!");

        // Get input file path from user
        System.out.println("Enter the input file path:");
        String inputFilePath = scanner.nextLine();

        // Check if file exists
        File inputFile = new File(inputFilePath);
        if (!inputFile.exists() || !inputFile.isFile()) {
            System.out.println("Input file does not exist or is not a valid file.");
            scanner.close();
            return;
        }

        // Get conversion choice
        System.out.println("Select the conversion format:");
        System.out.println("1. Uppercase");
        System.out.println("2. Lowercase");
        System.out.println("3. CSV");
        int choice = scanner.nextInt();
        scanner.nextLine(); // Consume newline

        // Get output file path from user
        System.out.println("Enter the output file path:");
        String outputFilePath = scanner.nextLine();

        try {
            // Perform the conversion based on user choice
            switch (choice) {
                case 1:
                    convertToUppercase(inputFilePath, outputFilePath);
                    System.out.println("Conversion to uppercase completed.");
                    break;
                case 2:
                    convertToLowercase(inputFilePath, outputFilePath);
                    System.out.println("Conversion to lowercase completed.");
                    break;
                case 3:
                    convertToCSV(inputFilePath, outputFilePath);
                    System.out.println("Conversion to CSV completed.");
                    break;
                default:
                    System.out.println("Invalid choice!");
            }
        } catch (IOException e) {
            System.out.println("An error occurred: " + e.getMessage());
        } finally {
            scanner.close(); // Always close the scanner
        }
    }
}
