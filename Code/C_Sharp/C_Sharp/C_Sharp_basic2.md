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

## 派生类构造方法

派生类调用基类的方法

```c#
// 派生类中，用 base 来调用基类的构造方法
// 如果不用 :base，默认会调用基类中的无参构造方法
public DerivedClass():base()
```



## 接口

使用 interface 关键字定义接口。

类与类之间叫**继承**，类与接口之间叫**实现**。

**接口类似于只有抽象成员的抽象基类。实现接口的任何类或结构都必须实现其所有成员。**

- 接口名称必须是有效的c#标识符名称，接口名称以大写字母 I 开头。
- 接口无法直接进行实例化
- 接口之间也可继承，继承接口和继承方法一样

- 接口可包含方法、属性、事件、索引器或这四种成员类型的任意组合。

- 接口不能包含常量、字段、运算符、实例构造函数、终结器或类型。 接口成员会自动成为公共成员，不能包含任何访问修饰符。不能是静态成员。
- 若要实现接口成员，实现类的对应成员必须是公共、非静态，并且具有与接口成员相同的名称和签名。
- 一个类或结构可以实现多个接口。一个类可以继承一个基类，还可实现一个或多个接口。

```c#
// 基类
class BaseClass
{
  public BCMethod()
  {
    
  }
}

// 定义接口
interface Ifly
{
  void Fly();
  void MethodA();
}

//继承接口
interface Ib:Ifly
{
  void MethodC();
}

// 实现接口
public class MyClass:Ib,BaseClass
{
  public void Fly() //实现接口必须把接口内的所有成员实现，这个方法属于 IFly 接口
  {
    
  }
  public void MethodA() //这个方法属于 IFly 接口
  {
    
  }
  
  public void MethodC() //这个方法属于 Ib 接口(如果一个接口属于另一个基类接口，实现该接口时，必须也实现其基类接口)
  {
    
  }
}
```

## 继承的一个例子

```c#
public class A
    {
        public virtual void Fun1(int i)
        {
            Console.WriteLine(i);
        }

        public void Fun2(A a)
        {
            a.Fun1(1);
            Fun1(5);
        }

    }
    public class B : A
    {
        public override void Fun1(int i)
        {
            base.Fun1(i + 1);
        }

        public static void Main()
        {
            B b = new B();
            A a = new A();

            a.Fun2(b); 
            /*a 调用 class A 中的Fun2,传参b
            即为 Fun2(b){b.Fun1(1); Fun1(5);}   
            b.Fun1() = A.Fun1(i+1) = 2 
            Fun1(5) = A.Fun2(){Fun1(5)} = 5 */
            b.Fun2(a); 
          	/*b 调用基类class A 中的Fun2,传参a
          	即为 Fun2(a){a.Fun1(1);Fun1(5);}
          	a.Fun1() = 1 
          	Fun1(5) = (override)b.Fun1(i+1) = 6 */
        }
    }
```



## 列表

```c#
// 创建列表的2种方式
List<int> scoreList = new List<int>();
var scoreList = new List<int>();
// 插入数据的方式
scoreList.Add(12);
// 读取列表数据
Console.WriteLine(scoreList[0]);
// 读取列表的数据个数
Console.WriteLine(scoreList.Count);
//读取列表的容量大小,容量大小默认为4，不够用时以倍数扩容，8，16，32; 可用 list.Capacity(10)来指定容量大小，扩容按指定容量大小2倍扩容，20，40，80
Console.WriteLine(scoreList.Capacity);
//移除指定位置元素
scoreList.RemoveAt(0);
//取得一个元素在列表中的索引位置，如果位置不存在，返回-1
scoreList.IndexOf(20);
scoreList.LastIndexOf(2); //从后向前搜索
//排序
scoreList.Sort();
```

## 泛型类

关键字 `<T>`，定义时只需要用 T 代表类型，在构造时需要指定 T 的类型

```c#
public class GenericList<T>
{
    public void Add(T input) { }
}
class TestGenericList
{
    private class ExampleClass { }
    static void Main()
    {
        // Declare a list of type int.
        GenericList<int> list1 = new GenericList<int>();
        list1.Add(1);

        // Declare a list of type string.
        GenericList<string> list2 = new GenericList<string>();
        list2.Add("");

        // Declare a list of type ExampleClass.
        GenericList<ExampleClass> list3 = new GenericList<ExampleClass>();
        list3.Add(new ExampleClass());
    }
}
```

## 一些零碎的点

### String

注意 char 和 string 的符号，单引号和双引号

```c#
string s  = "www.helloworld.com";
string newS = s.Replace('.','-'); //char 要用 ' '
string newS = s.Replace(".","---") //string 要用 " "
```

### String和StringBuilder类型

对String对象每个操作都会创建一个新的字符串。

StringBuilder是可变类型，指为对象维护一个缓冲区以容纳字符串的扩展，如果空间可用，会把新数据追加到缓冲区，否则会分配一个新的更大缓冲区。将通常比 String 类提供更好的性能。

使用 String 类型的建议：

- 字符串更改数量很小
- 固定数量的字符串串联操作
- 对字符串执行大量搜索操作（StringBuilder缺少搜索方法）

使用 StringBuilder 类型的建议：

- 对字符串进行未知数量的更改
- 希望对字符串进行大量更改时

## 正则表达式

要在项目中引用`System.Text.RegularExpressions;`命名空间

关键字 `Regex`

```c#
string st = Console.ReadLine(); //接收用户输入的字符串
string pattern = @"^\d*$"; //用正则表达式定义验证规则，此例为"输入只能是数字",用@让 \保持原意，不要转义，此处加@表示 \d 的原意，字符串中的"\"的原意是转义符，如果不用@，会把 \ 和 d 分开看
bool isMatcth =  Regex.IsMatch(st, pattern); //判断是否匹配，输出 bool

Console.WriteLine(isMatcth ? "It's true." : "Just allow number.");
```



```c#
// 检测用户的输入是否合法
using System.Text.RegularExpressions;

while (true)
{
  string st = Console.ReadLine();
  string pattern = @"^\d*$";
  bool isMatcth = Regex.IsMatch(st, pattern);
  if (isMatcth == true)
  {
    Console.WriteLine("is true");
    break;
  }
  else
  {
    Console.WriteLine("is false,please try again");
  }
}
```



```c#
while (true)
{
  string st = Console.ReadLine();
  string pattern = @"^\d*$";
  string patternSearch = @"\d|[a-z]";
  string patternSplit = "[,;.]";
  // 用 match 来找出用户输入字符串里合法字符,使用 Matches 来输入一个匹配 patternSearch 规则的list,类型为 Match
  MatchCollection coll = Regex.Matches(st, patternSearch);
  // 定义一个字符串数组把按 patternSplit 的规则切分好的数据存入
  string[] stSplit = Regex.Split(st, patternSplit); 
  foreach (Match match in coll)
  {
  		Console.Write(match + " "); //把符合条件的字符输出
  } 
  
  foreach(var str in stSplit)
	{
		Console.Write(str + " "); //把切分的字符输出
	}
  
  break;
}
```

## 委托和 Lambda



