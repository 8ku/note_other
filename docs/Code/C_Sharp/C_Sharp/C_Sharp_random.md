# Random

猜数字

```csharp
class MainClass
    {
        static void Main()
        {
            Random random = new Random();
            int number = random.Next(0, 51);
            Console.WriteLine("I have a number,from 0 to 50, guess what number is ");
            while (true)
            {
                int userGuess = Convert.ToInt32(Console.ReadLine());
                if (userGuess < number)
                {
                    Console.WriteLine("more higher, please");
                }
                else if (userGuess > number)
                {
                    Console.WriteLine("more lower, please");
                }
                else
                {
                    Console.WriteLine("bingo!");
                    break;
                }
            }            
        }

    }
```

