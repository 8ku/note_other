# c#

## static

不使用 static 的默认为 auto。

- **auto**：由程序自动控制变量的生命周期，通常是变量在被触发时被分配，结束时释放
- **static**：按程序的生命周期来分配释放变量，在程序初始化时被分配，程序退出时释放，按程序的生命周期来分配释放变量，而不是变量自己的生命周期。即**在程序运行期间一直占用内存空间。**

如果一个类经常被调用，就写成静态类，相反就不要写成静态类，以节省内存。

## params

参数数组，使用这个关键字你可以直接在调用时传入数组的值，而不需要在调用是重新构造一个数组再传入。

```c#
// 构造一个 int 类型的参数数组
public static void UserParams(params int[] list)
{
  for (int i = 0; i< list.Lengh; i++)
  {
    Console.Write(list[i] + " "); //输出在一行中
  }
  Console.WriteLine(); //把该方法的结果输出在新一行中
}

// 构造一个不限类型的数组 (object类型）
public static void UserParam2(params object[] list)
{
  for (int i = 0; i< list.Length; i++)
  {
    Console.Write(list[i] + " ");
  }
  Console.WriteLine();
}

// 调用方法
static void Main()
{
  UserParams(1,3,4,6);
  UserParams2(1,"2","we","为什么")；
}
```

## 调试

### 断点调试

在要打断点的行头点击，即可打断点，运行时，会在打断点的地方停下来。

### 异常处理

使用 try catch finally 语句来处理异常.

try用于预测可能出现的异常。捕获异常并对异常进行处理，就在catch中实现。不管异常发生与否，都会执行finally里面的语句。

```c#
static void Main()
        {
            while (true)
            {
                try //用于检测异常，当 try 中的语句发生异常时，用 catch 捕捉
                {
                    int num1 = Convert.ToInt32(Console.ReadLine()); 
                    break; //如果输入的是正确的形式, 即 try 语句正确执行, 用 break 跳出 while 循环；如果 try 报错，会进入 catch 块
                }
                catch
                {
                    Console.WriteLine("should be a number, please try again.");
                }

            }
        }
```



## 属性

可以给字段设置带处理的值，即在属性中处理字段，并输出结果给字段。这让字段的设置更灵活。

- 只读属性：只有 get ，没有 set
- 只写属性：只有 set ，没有 get（很少出现）
- value关键字：用户定义由 set 访问器分配的值

```c#
class TimePeriod
    {
        private double hours; //设置一个字段接收实参的值
        public double Hours
        {
            get { return hours; } // get 返回属性值
            set // set 分配新值
            {
                if (value > 0 && value < 24)
                {
                    hours = value;
                    Console.WriteLine($"Time is hours: {hours}");
                }
                else
                {
                    hours = value;
                    Console.WriteLine($"{hours} must be between 0 and 24.");
                }
            }
        }
    }
    class baku
    {
        static void Main()
        {
            TimePeriod t = new TimePeriod(); //构造
            t.Hours = 11; //调用 TimePeriod 类中的 Hours字段，给 hours 赋值
        }
    }
```

### C# 7.O get set 的变化

可以作为 expression-bodied 成员实现，不使用 return.

```c#
class SaleItem
    {
        string _name;
        decimal _cost;

        public SaleItem(string name,decimal cost)
        {
            _name = name;
            _cost = cost;
        }

        public string Name
        {
            get => _name;
            set => _name = value;
        }

        public decimal Price
        {
            get => _cost;
            set => _cost = value;
        }
    }


    class Program
    {
        static void Main()
        {
            SaleItem item = new SaleItem("Shoes",19.95m);
            Console.WriteLine($"{item.Name}: sells for {item.Price:c2}");
        }
    }
```

### 自动实现的属性(如果字段中没有逻辑，可以简化)

```c#
public class SaleItem
{
   public string Name 
   { get; set; }

   public decimal Price
   { get; set; }
}

class Program
{
   static void Main()
   {
      var item = new SaleItem{ Name = "Shoes", Price = 19.95m };
      Console.WriteLine($"{item.Name}: sells for {item.Price:C2}");
   }
}
```



