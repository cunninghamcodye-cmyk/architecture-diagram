# Calorie Count App
Calorie Count App


fusing System;
using System.Collections.Generic;

class Program
{
    // Define a class to represent a structural Meal object
    class Meal
    {
        public string Name { get; set; }
        public int Calories { get; set; }

        public Meal(string name, int calories)
        {
            Name = name;
            Calories = calories;
        }
    }

    static void Main()
    {
        // Initialize daily variables
        List<Meal> dailyMeals = new List<Meal>();
        int totalCalories = 0;
        int calorieGoal = 2000; // Default baseline target
        bool running = true;

        // Main program loop
        while (running)
        {
            Console.WriteLine("--- DAILY CALORIE TRACKER ---");
            Console.WriteLine("1. Add a Meal");
            Console.WriteLine("2. View Daily Summary");
            Console.WriteLine("3. Set Daily Calorie Goal");
            Console.WriteLine("4. Exit");
            Console.Write("Enter your choice (1-4): ");
            string userChoice = Console.ReadLine();

            switch (userChoice)
            {
                case "1":
                    // Get meal details
                    Console.Write("Enter meal name (e.g., Breakfast, Snack): ");
                    string mealName = Console.ReadLine();

                    // Input validation for calories
                    int mealCalories;
                    while (true)
                    {
                        Console.Write("Enter calories for this meal: ");
                        if (int.TryParse(Console.ReadLine(), out mealCalories) && mealCalories >= 0)
                        {
                            break;
                        }
                        Console.WriteLine("Invalid input. Please enter a positive number.");
                    }

                    // Create, store, and tally the new meal
                    Meal newMeal = new Meal(mealName, mealCalories);
                    dailyMeals.add(newMeal);
                    totalCalories += mealCalories;

                    Console.WriteLine("Meal added successfully!");
                    break;

                case "2":
                    // Display summary
                    Console.WriteLine("\n=== DAILY SUMMARY ===");
                    if (dailyMeals.Count == 0)
                    {
                        Console.WriteLine("No meals logged yet today.");
                    }
                    else
                    {
                        foreach (Meal item in dailyMeals)
                        {
                            Console.WriteLine($"- {item.Name}: {item.Calories} kcal");
                        }
                    }

                    Console.WriteLine("---------------------");
                    Console.WriteLine($"Total Calories Consumed: {totalCalories} / {calorieGoal} kcal");

                    // Give context relative to the goal
                    if (totalCalories > calorieGoal)
                    {
                        int surplus = totalCalories - calorieGoal;
                        Console.WriteLine($"You are {surplus} kcal OVER your daily goal.");
                    }
                    else
                    {
                        int remaining = calorieGoal - totalCalories;
                        Console.WriteLine($"You have {remaining} kcal REMAINING for the day.");
                    }
                    break;

                case "3":
                    // Adjust goal with validation
                    while (true)
                    {
                        Console.Write($"Current daily goal is {calorieGoal} kcal. Enter new goal: ");
                        if (int.TryParse(Console.ReadLine(), out int newGoal) && newGoal > 0)
                        {
                            calorieGoal = newGoal;
                            Console.WriteLine("Calorie goal updated!");
                            break;
                        }
                        Console.WriteLine("Invalid input. Please enter a valid number greater than 0.");
                    }
                    break;

                case "4":
                    // Quit the application
                    Console.WriteLine("Exiting tracker. Have a healthy day!");
                    running = false;
                    break;

                default:
                    Console.WriteLine("Invalid choice. Please select an option from 1 to 4.");
                    break;
            }

            Console.WriteLine(); // Print empty line for clean spacing
        }
    }
}
d
