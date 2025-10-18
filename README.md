using System;
using System.Collections.Generic;
using System.Linq;

// 1. OOP PRINCIPLES: Student Class
// Defines a custom object to hold data, demonstrating good object-oriented design.
public class Student
{
    public string Name { get; private set; }
    private int[] _scores;

    // Constructor
    public Student(string name, int numAssignments)
    {
        Name = name;
        _scores = new int[numAssignments];
    }

    // Setter for a specific score
    public void SetScore(int assignmentIndex, int score)
    {
        if (assignmentIndex >= 0 && assignmentIndex < _scores.Length)
        {
            _scores[assignmentIndex] = score;
        }
    }

    // Method to calculate the average using a FOR loop pattern
    public double CalculateAverage()
    {
        int sum = 0;

        // Implementation of a standard 'for' loop pattern
        for (int i = 0; i < _scores.Length; i++)
        {
            sum += _scores[i];
        }

        if (_scores.Length == 0) return 0;
        return (double)sum / _scores.Length;
    }
}

public class LoopProgram
{
    private const int NumStudents = 2; // Can be easily changed
    private const int NumAssignments = 3; // Can be easily changed

    public static void Main(string[] args)
    {
        Console.WriteLine("==============================================");
        Console.WriteLine("    Week 09: Student Grade Loop Analyzer");
        Console.WriteLine("==============================================");

        // Prepare a List to hold our Student objects (good OOP practice)
        List<Student> classList = new List<Student>();

        // 2. NESTED LOOP APPLICATION (Input/Processing)
        // Outer loop: Iterates over each student
        for (int i = 0; i < NumStudents; i++)
        {
            Console.WriteLine($"\n--- Entering Data for Student #{i + 1} ---");
            Console.Write("Enter student name: ");
            string name = Console.ReadLine();

            Student currentStudent = new Student(name, NumAssignments);

            // Inner loop: Iterates over each assignment for the current student
            for (int j = 0; j < NumAssignments; j++)
            {
                int score = 0;
                bool valid = false;

                // INNOVATION (Extra Feature): Input validation using a simple loop
                while (!valid)
                {
                    Console.Write($"Enter score for Assignment {j + 1} (0-100): ");
                    string input = Console.ReadLine();
                    
                    if (int.TryParse(input, out score) && score >= 0 && score <= 100)
                    {
                        valid = true;
                    }
                    else
                    {
                        Console.WriteLine("Invalid input. Please enter a score between 0 and 100.");
                    }
                }
                
                currentStudent.SetScore(j, score);
            }

            classList.Add(currentStudent);
        }

        Console.WriteLine("\n==============================================");
        Console.WriteLine("           F I N A L   R E S U L T S");
        Console.WriteLine("==============================================");

        double highestAverage = -1;
        string topStudentName = "N/A";

        // 3. FOREACH LOOP PRACTICE (Output/Analysis)
        // Iterates through the list of Student objects easily.
        foreach (Student student in classList)
        {
            double average = student.CalculateAverage(); // The method internally uses a 'for' loop
            Console.WriteLine($"Student: {student.Name}, Average Score: {average:F2}");

            // Loop pattern for finding the highest value
            if (average > highestAverage)
            {
                highestAverage = average;
                topStudentName = student.Name;
            }
        }

        Console.WriteLine("\n----------------------------------------------");
        Console.WriteLine($"Top Student: {topStudentName} with an average of {highestAverage:F2}");
        Console.WriteLine("----------------------------------------------");

        // INNOVATION: Nested Loop for Pattern Output (Visual Flair)
        Console.WriteLine("\n** Creative Loop Pattern **");
        PrintAsteriskTriangle(4);
    }

    // 4. IMPLEMENT VARIOUS FOR LOOP PATTERNS (Nested for loop helper)
    // Code Quality: Separating complex logic into a clean method.
    public static void PrintAsteriskTriangle(int height)
    {
        for (int i = 1; i <= height; i++) // Outer loop: controls rows
        {
            for (int j = 0; j < i; j++) // Inner loop: controls stars per row (j < i makes it a triangle)
            {
                Console.Write("* ");
            }
            Console.WriteLine();
        }
    }
}
