## 最大公约数

```csharp
int a = Convert.ToInt32(Console.ReadLine());
int b = Convert.ToInt32(Console.ReadLine());

//假设 a 为最小值；
int min = a;

//确定最小数
if(b<min){
  min = b;
}

//解法1
for(int i=min;i>0;i--){
  if(a%i==0 && b%i==0){
    Console.WriteLine(i);
    // 只需要输出最大的公约数，输出后跳出循环
    break;
  }
}

//解法2 碾转相除/欧几里得算法
while (a % min > 0){
	int y = a % min;
	a = min;
	min = y;
}
Console.WriteLine(min);
```

维基百科的一种解法（if while的用法不太懂）

```csharp
//包装成一个方法，不用判断 a 和 b 的大小
class MainClass
    {

        public static int GCD(int a, int b)
        {
          //不太看得懂
            if (0 != b) while (0 != (a %= b) && 0 != (b %= a)) ;
            return a + b;
        }

        static void Main()
        {
            Console.WriteLine("Input int a");
            int a = Convert.ToInt32(Console.ReadLine());
            Console.WriteLine("Input int b");
            int b = Convert.ToInt32(Console.ReadLine());

            Console.WriteLine(GCD(a, b));
        }
    }
```

