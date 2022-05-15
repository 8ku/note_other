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



## 随机生成

### 生成随机数

#### Linq 类

```c#
using System;
using System.Linq;

namespace Csharp01
{
    class MainClass
    {
        private static Random random = new Random();
        public static string methodRandom(int length)
        {
            const string characters = "abcdefghijklmnopqrstuvwxyz0123456789_";
            return new string(Enumerable.Repeat(characters, length).Select(s => s[random.Next(s.Length)]).ToArray());
        }

        public static void Main()
        {
            string finalString = methodRandom(15);
            Console.WriteLine(finalString);
        }
    }
}
```

#### RNGCryptoServiceProvider 类（生成加密随机数）

```c#
using System;
using System.Security.Cryptography;

namespace Csharp01
{
    class MainClass
    {
        static string method3(int length)
        {
            using (var crypto = new RNGCryptoServiceProvider())
            {
                var bits = (length * 6);
                var byte_size = ((bits + 7) / 8);
                var bytesarray = new byte[byte_size];
                crypto.GetBytes(bytesarray);
                return Convert.ToBase64String(bytesarray);
            }
        }

        static void Main(string[] args)
        {
            string finalString = method3(15);
            Console.WriteLine(finalString);
        }
    }
}
```

