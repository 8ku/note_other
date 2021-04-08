## 调用 class

父级 class

```c#
public class Father: MonoBehaviour
{
  protected Animator anime; //protected 表示只有子级可调用
  
  protected virtual void Start() //protected 表示只有子级可调用，子级需要可重新编写 start，所以要加 virtual
  {
    anime = GetComponent<Animator>();
  }
  
  public void Death() //需要公开方法
  {
    Destroy(gameObject);
  }
}

```

子级 class

```c#
public class Son : Father
{
  protected override void Start() //使用主类的标准写法,override 重写
  {
    base.Start(); //使用主类时，需要在此用 base 调用 
        rb = GetComponent<Rigidbody2D>();
        // anime = GetComponent<Animator>();
        coll = GetComponent<Collider2D>();
  }
}
```

引用时

```c#
//引用另一个 class name is Enemy_frog 的脚本文件，引用后可调用此脚本里的所有组件和代码
Father father = collision.gameObject.GetComponent<Father>();
```

