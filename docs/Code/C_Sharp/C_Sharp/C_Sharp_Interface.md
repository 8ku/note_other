# C# Interface



## 快捷键

- 选中所有相同名称: 先选中第一个, alt+shift+分号
- 自动填写方法体: 光标放在关键词上, alt+enter
- 在整个项目里搜索: cmd + 句号







## 杂

接口不能声明实例数据.

使用接口可以在类中包括来自多个源的行为.

用`interface`定义接口, 按命名习惯以大写字母 I 开头 :

```csharp
//声明接口
interface IEquatable<T>
{
  //这个接口包含一个方法,方法字段依次为 返回值,签名,参数
  bool Equals(T obj); 
}
```

- 接口可以包含实例方法, 属性, 事件, 索引器 或这四种成员类型的任意组合
- 接口可以包含静态构造函数、字段、常量或运算符
- 接口**不能**包含实例字段、实例构造函数或终结器
- 默认情况下, 接口成员是公共的
- 实现接口成员, 实现类的对应成员必须是**公共, 非静态**, 并具有与接口成员**相同名称和签名**.

```csharp
//实现接口
public class Car:IEquatable<Car>
{
  public string Make{get;set;}
  public string Model{get;set;}
  public string Year{get;set;}
  
  //实现接口必须使用接口声明中名字一样的方法
  publc bool Equals(Car car)
  {
    //新写法
    return(this.Make, this.Model, this.Year) == (car.Make, car.Model, car.Year);
  }  
}
```

