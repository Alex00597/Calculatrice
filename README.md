# Calculatrice
using System;

namespace CalculatorLibrary
{
        public class Calculator
        {
            public static double DoOperation(double num1, double num2, string op)
            {
                double result = double.NaN; // Default value is "not-a-number" which we use if an operation, such as division, could result in an error.

                // Use a switch statement to do the math.
                switch (op)
                {
                    case "a":
                        result = num1 + num2;
                        break;
                    case "s":
                        result = num1 - num2;
                        break;
                    case "m":
                        result = num1 * num2;
                        break;
                    case "d":
                        // Ask the user to enter a non-zero divisor.
                        if (num2 != 0)
                        {
                            result = num1 / num2;
                        }
                        break;
                    // Return text for an incorrect option entry.
                    default:
                        break;
                }
                return result;
            }

        }
        class Program
        {
            static void Main(string[] args)
            {
                bool endApp = false;
                // Display title as the C# console calculator app.
                Console.WriteLine("Calculatrice en C#\r");
                Console.WriteLine("------------------------\n");

                while (!endApp)
                {
                    // Declare variables and set to empty.
                    string numInput1 = "";
                    string numInput2 = "";
                    double result = 0;

                    // Ask the user to type the first number.
                    Console.Write("Ecrivez un nombre, puis appuyer sur entrée: ");
                    numInput1 = Console.ReadLine();

                    double cleanNum1 = 0;
                    while (!double.TryParse(numInput1, out cleanNum1))
                    {
                        Console.Write("Ce caractére n'est pas valide, veuillez entrée un nombre: ");
                        numInput1 = Console.ReadLine();
                    }

                    // Ask the user to type the second number.
                    Console.Write("Ecrivez un autre nombre, puis appuyer sur entrée: ");
                    numInput2 = Console.ReadLine();

                    double cleanNum2 = 0;
                    while (!double.TryParse(numInput2, out cleanNum2))
                    {
                        Console.Write("Ce caractére n'est pas valide, veuillez entrée un nombre: ");
                        numInput2 = Console.ReadLine();
                    }

                    // Ask the user to choose an operator.
                    Console.WriteLine("Choisir une opération dans la liste suivante:");
                    Console.WriteLine("\ta - Addition");
                    Console.WriteLine("\ts - Soustraction");
                    Console.WriteLine("\tm - Multiplication");
                    Console.WriteLine("\td - Division");
                    Console.Write("Ton choix ? ");

                    string op = Console.ReadLine();

                    try
                    {
                        result = Calculator.DoOperation(cleanNum1, cleanNum2, op);
                        if (double.IsNaN(result))
                        {
                            Console.WriteLine("Erreur mathématique.\n");
                        }
                        else Console.WriteLine("Le résultat: {0:0.##}\n", result);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("Oh non! une erreur s'est produite.\n - Details: " + e.Message);
                    }

                    Console.WriteLine("------------------------\n");

                    // Wait for the user to respond before closing.
                    Console.Write("Appuyer sur'n'et entrer pour fermer la page, ou appuyer sur entrer pour continuer: ");
                    if (Console.ReadLine() == "n") endApp = true;

                    Console.WriteLine("\n"); // Friendly linespacing.
                }
                return;
            }
        }
    }
