## 检测输入

### 检测用户输入的是否为数字

用`try catch`

```c#
namespace Csharp01
{
    class MainClass
    {
        public static void Main()
        {
            string userInput;
            Console.WriteLine("Please input a number");
            userInput = Console.ReadLine();
            int number = GetNumber(userInput);          
        }

        public static int GetNumber(string s) {
            while (true) {
                try
                {
                    int number = Convert.ToInt32(s);
                    return number;
                }
                catch {
                    Console.WriteLine("Please input number");
                    s = Console.ReadLine();
                }
            }
        }
    }
}

```

