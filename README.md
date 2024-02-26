# Mastermind

using System;

namespace MastermindGame
{
    class Program
    {
        static void Main(string[] args)
        {
            // Generate random answer
            Random random = new Random();
            int[] answer = new int[4];
            for (int i = 0; i < 4; i++)
            {
                answer[i] = random.Next(1, 7);
            }

            // Game loop
            int attempts = 0;
            while (attempts < 10)
            {
                Console.WriteLine("Enter your guess (4 digits between 1 and 6):");
                string guessStr = Console.ReadLine();
                if (guessStr.Length != 4)
                {
                    Console.WriteLine("Invalid input. Please enter exactly 4 digits.");
                    continue;
                }

                int[] guess = new int[4];
                bool validGuess = true;
                for (int i = 0; i < 4; i++)
                {
                    if (!int.TryParse(guessStr[i].ToString(), out guess[i]) || guess[i] < 1 || guess[i] > 6)
                    {
                        validGuess = false;
                        break;
                    }
                }
                if (!validGuess)
                {
                    Console.WriteLine("Invalid input. Please enter digits between 1 and 6.");
                    continue;
                }

                // Check guess
                int plusCount = 0;
                int minusCount = 0;
                for (int i = 0; i < 4; i++)
                {
                    if (guess[i] == answer[i])
                    {
                        plusCount++;
                    }
                    else if (Array.IndexOf(answer, guess[i]) != -1)
                    {
                        minusCount++;
                    }
                }

                // Print result
                for (int i = 0; i < plusCount; i++)
                {
                    Console.Write("+");
                }
                for (int i = 0; i < minusCount; i++)
                {
                    Console.Write("-");
                }
                Console.WriteLine();

                // Check if guess is correct
                if (plusCount == 4)
                {
                    Console.WriteLine("Congratulations! You've guessed the number!");
                    break;
                }

                attempts++;
            }

            // If player couldn't guess the number
            if (attempts == 10)
            {
                Console.WriteLine("Sorry, you've run out of attempts. The answer was: " + string.Join("", answer));
            }
        }
    }
}
