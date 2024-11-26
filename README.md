package defaultpackage;

import java.util.ArrayList;
import java.util.InputMismatchException;
import java.util.Scanner;

class Person {
    String name;
    int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

class Patient extends Person {
    String disease;

    public Patient(String name, int age, String disease) {
        super(name, age);
        this.disease = disease;
    }
}

public class Hospitalmanagementsystem {
    private static Scanner scanner;

	public static void main(String[] args) {
        scanner = new Scanner(System.in);
        ArrayList<Patient> patients = new ArrayList<>();

        while (true) {
            try {
                System.out.println("1. Add Patient");
                System.out.println("2. Delete Patient");
                System.out.println("3. Search Patient");
                System.out.println("4. Modify Patient");
                System.out.println("5. Exit");
                System.out.print("Enter your choice: ");
                int choice = scanner.nextInt();

                switch (choice) {
                    case 1:
                        System.out.print("Enter patient name: ");
                        String name = scanner.next();
                        System.out.print("Enter patient age: ");
                        int age = scanner.nextInt();
                        System.out.print("Enter patient disease: ");
                        String disease = scanner.next();
                        patients.add(new Patient(name, age, disease));
                        System.out.println("Patient added successfully!");
                        break;

                    case 2:
                        System.out.print("Enter patient name to delete: ");
                        String deleteName = scanner.next();
                        patients.removeIf(p -> p.name.equals(deleteName));
                        System.out.println("Patient deleted successfully!");
                        break;

                    case 3:
                        System.out.print("Enter patient name to search: ");
                        String searchName = scanner.next();
                        boolean found = false;
                        for (Patient patient : patients) {
                            if (patient.name.equals(searchName)) {
                                System.out.println("Patient Found:");
                                System.out.println("Name: " + patient.name);
                                System.out.println("Age: " + patient.age);
                                System.out.println("Disease: " + patient.disease);
                                found = true;
                                break;
                            }
                        }
                        if (!found) {
                            System.out.println("Patient not found!");
                        }
                        break;

                    case 4:
                        System.out.print("Enter patient name to modify: ");
                        String modifyName = scanner.next();
                        for (Patient patient : patients) {
                            if (patient.name.equals(modifyName)) {
                                System.out.print("Enter new age: ");
                                patient.age = scanner.nextInt();
                                System.out.print("Enter new disease: ");
                                patient.disease = scanner.next();
                                System.out.println("Patient modified successfully!");
                                break;
                            }
                        }
                        break;

                    case 5:
                        System.out.println("Exiting program...");
                        System.exit(0);

                    default:
                        System.out.println("Invalid choice!");
                }
            } catch (InputMismatchException e) {
                System.out.println("Invalid input. Please enter a valid value.");
                scanner.next();
            }
        }
    }
}
