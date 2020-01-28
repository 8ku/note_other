Unity中的C#语法

## 基本格式

~~~c#
using System.Collections;
using UnityEngige;
// PlayController :脚本名
public class PlayerController : MonoBehaviour 
{
  //只会执行一次，一般用来初始化
	void Start() 
  {
    
  }
    void Update() 
   {
      
   }
}
~~~

- 不需要带Main方法

- 要访问类中的值，值必须是公开的

  ```c#
  public class someting:MonoBehaviour
  {
    void Start()
    {
      Enemy enemy = new Enemy(); //调用类时需要先实例化
      print(enemy.name); //可访问到 name 字段，不能访问到 hp 字段
      enemy.Move(); //调用方法时直接写，不需要打印，只有字段才用打印
    }
  }
  
  class Enemy
  {
    public string name;
    int hp; //默认是私有的，不显示，也不可从外部调用
    public void Move() //方法如果不 public 外部无法调用
    {
      Debug.Log(name + "move"); // 方法可调用同一个类下的字段，print是 MonoBehavious 中的方法，自定义类不包含 print 方法，不能使用 print
    }
  }
  ```

### 命名空间和类

可自定义命名空间和类，并在代码中引用

```c#
using MyGame; //声明命名空间

public class Player:MonoBehaviour
{
  void Start()
  {
    GameData gd = new GameData(); //实例化自定义命名空间 MyGame 中的自定义类 GameData
    print(gd.name); //输出实例化 GameData 中的字段
    gd.FunctionName(); //输出实例化 GameData 中的方法
  }
}

namespace MyGame //定义命名空间
{
  class GameData //定义类
  {
     public void FunctionName() //定义方法
     {
        Debug.Log("output");
     }
    int hp;
    string name;
  }
}
```



### 代码中消除空行-使用正则

shift + cmd + f ：^\s*\n ，勾选“正则表达式搜索”，点击“替换”

\s ：空白字符

\n：换行符

###  MonoBahaviour

MonoBahaviour 是所有Unity 脚本的基类。



### 使用Debug来显示操作情况

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class BasicController : MonoBehaviour
{
    // Update is called once per frame
    void Update()
    {
        Debug.Log("Horizontal Input = " + Input.GetAxis("Horizontal")); //使用Debug来打印横向坐标
    }
}
```

- 把skybox加到camera下，可以把自定义的skybox材质放进去，在不影响编辑模式的skybox前提下显示自定义skybox

- **Debug 和 Print 的区别**：Debug 是单独的类，Print 是 MonoBehaviour 的一个成员

- Debug的种类：

  - Debug.Log：普通输出
  - Debug.LogWarning：黄色高亮icn
  - Debug.LogError：红色高亮icn

  

## 移动，跳跃，动画

```c#
public RigidBody2D rb;  //定义一个刚体，改名为 rb ，保存后，在图形界面上把 player 的刚体拖到这里绑定
public Animator anime; //把动画控制器绑定角色
publie Collider2D coll; //定义碰撞体
public float speed;  //定义一个类型为speed
public float jumpforce; //定义一个类型设置力的初始大小，在界面上
public LayerMask ground; //定义地面

//FixedUpdate要求用固定的频率调用，除了用来处理物理逻辑之外并不适合处理其他模块的逻辑,有可能 fixedupdate 的频率会高于游戏设定频率，如此 fixedupdate 就会调用太多次
void FixedUpdate() 
{
    Movement(); //引用movement的值
}


void Movement()
{
    float horizontalmove = Input.GetAxis("Horizontal");  // 读取键盘横向移动的坐标axis,横向移动只有三个值，-1 为向左移动，1 为向右移动 ，0 为不动，Horizontal要区分大小写，要拼写正确，和系统默认的名称保持一致
    float facedirection = Input.GetAxisRaw("Horizontal"); //get axis raw 表示只取 0，1，-1 三个值
  
  	// 角色移动
    if (horizontalmove != 0) //如果横向移动的值不为0，说明 player 在移动，则设置刚体的速率为 x = 当前坐标 * 速度 ，y = 刚体的 y 速率
    {
        rb.velocity = new Vector2(horizontalmove * speed * Time.delta.Time, rb.velocity.y); //delta time 表示距上一次调用Update或FixedUpdate所用的时间，使动作更平滑，而不是使用一个常量的值 
      // 借用 facediction 的值设置动画变换的值为1或0，为0时为 idle，为1时为 run 
      anime.SetFloat("running",Mathf.Abs(facediction));
    }
  
   if (facedirection != 0)
   {
     transform.localScale = new Vector3(facedirection,1,1); // 因为 transform 的属性有 x,y,z 三个值，所以要用 vector3
   }
  
  // 角色跳跃
  if (Input.GetButtonDown("Jump"))
  {
    // 设置跳跃的高度，x 保持不变，y 变化
    rb.velocity = new Vector2(rb.velocity.x, jumpforce * Time.deltaTime);
    //设置动画切换为跳跃
    anime.SetBool("jumping",true); 
  }
}
void SwitchAnime()
{
  // 设定 idle 的初始状态
  anime.SetBool("idle",false); 
  
  if (anime.GetBool("jumping"))
  {
    if (rb.velocity.y < 0)
    {
      anime.SetBool("jumping",false);
      anime.SetBool("falling",true);
    }
    else if (coll.IsTouchingLayers(ground))
    {
      anime.SetBool("falling",false);
      anime.SetBool("idle",true);
    }
  }
}
```



## 镜头跟踪

```c#
public Transform player;
void Update()
{
    transform.position = new Vector3(player.position.x, player.position.y, -10f);
}
```



## for/while 循环销毁子物体

```c#
void Start()
{
	// Transform 是 Unity 的一种内置类型，获得这个主体下的所有子级
  Transform[] children = transform.GetComponentsInChildren<Transform>();

  for(int i = 0; i< children.Length; i++) // 遍历子级的长度
      {
        if (children[i] != transform) //如果子级中不包含本体，如果不写这一句，会把父级一起销毁
        {
          GameObject.Destroy(children[i].gameObject); //销毁子级
        }
      }
}
```

while 语句：

```c#
void Start()
{
  Transform[] children = transform.GetComponentsInChildren<Transform>();
  
  int i = 0;
  while(i < children.Length)
  {
    if (children[i] != transform) 
        {
          GameObject.Destroy(children[i].gameObject); //销毁子级
        }
    		i++;
  }
}
```

### foreach 循环

也称为只读循环，相比 for 循环更简洁，只能遍历，不能修改值。

```c#
public class HeroType : MonoBehaviour
{
    void Start()
    {
        Transform[] children = transform.GetComponentsInChildren<Transform>();

        foreach(Transform i in children)
        {
            if (i != transform)
            {
                Destroy(i.gameObject);
            }
        }
    }
}
```



## 访问组件，启用/禁用组件

### 获取本物体/子物体中的组件

通过 transform 组件获取物体，因为所有物体都有 transform 组件，所以可以用 transform 代表物体本身

```c#
 Transform t = GetComponent<Transform>(); //Transform:组件类型,transform 是内置组件，可以不用用 get 来访问

Transform t = GetComponentInChildren<Transform>(); //获取子物件组件
```

获取子物体

```c#
transform.Find("子级/孙级");
```





### 获取其他物体及组件

1. 获取物体 game object

```c#
public GameObject someone;  //先定义一个参数，把要获取的物体拖拽进来

void Start()
{
  someone.GetComponent<Rigidbody2D>(); //获取物体组件
}
```

2. 获取组件及脚本

```c#
public class somethin; //找脚本就直接定义脚本，找组件就定义组件，组件必须存在 

void Start()
{
  somethin.子类(); //获取脚本中的东西
}
```

3. 通过 gameObject 的 Find 方法查找物体，如果有多个同名物品，只会返回第一个，效率很低，不推荐使用

```c#
GameObject go = GameObject.Find("Main Camera");
```

4. 通过标签查找物体

```c#
GameObject go = GameObject.FindWithTag("Player"); //根据 tag 名称返回active 的第一个结果
GameObject go = GameObject.FindGameObjectsWithTag("Player"); //返回这个 Tag 的列表，顺序随机
foreach(GameObject i in go){print(i);} //可以用 foreach 来查看找到的项
```



### 启用/禁用组件

只有视图面板上可以勾选的组件可以被启/禁用

```c#
void Start()
{
  BoxCollider2D coll = GetComponent<BoxCollider2D>(); //获取物体组件
  coll.enabled =  false; //禁用组件
}
```



## 实例化

```c#
public GameObject bullet; //建一个游戏物体，把要实例化的物体拖拽进来

GameObject.Instantiate( bullet, transform.position, transform.rotation); // instantiate:实例化，第一个值：实例化的原对象
```



## Input

```c#
Input.GetMouseButtonDown(0); //0:鼠标左键，1：鼠标右键，2：鼠标中键
```

