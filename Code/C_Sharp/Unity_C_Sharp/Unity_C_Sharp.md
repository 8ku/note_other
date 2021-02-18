# Unity中的C#语法

* TOC
{:toc}

## 基本格式

- 方法用大驼峰；
- 变量用小驼峰；

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
      Invoke("Move", 2.0f); // 直接调用方法，在2秒之后调用
      InvokeRepeating("Move",4.0f,2.0f); // 4秒之后调用，每2秒调用一次
    }
    
    void Update()
      {
          // Cancel all Invoke calls
          if (Input.GetButton("Fire1"))
              CancelInvoke(); //可以在开始时调用方法，在 Update 中监听按键，取消调用所有方法 Cancels all Invoke calls
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



### 结构体 struct

结构体和类（class）不同，结构体中的值不能单独修改，要整体赋值。例如

```c#
transform.position = new Vector3(3, 3, 3);
transform.position.x = 10; //报错，不能直接修改值

Vector3 pos = transform.position; //新建一个值来储存结构体信息
pos.x = 10; //修改值
transform.position = pos; //把值整体更新到结构体中
```



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

### 3d移动目标

Vector3.Distance(目标位置,起始位置)

## 镜头跟踪

1. 2D

```c#
public Transform player; // 取得跟随对象的位置

void Update()
{
    transform.position = new Vector3(player.position.x, player.position.y, -10f);
}
```

2. 3D

脚本挂在相机上

```c#
public Transform player; // 取得跟随对象的位置
[SerializeField] //显示私有变量，能在Inspector中编辑
private Vector3 offset; // 设置初始距离

void Start()
{
  offset = transform.position - player.position; //初始化时得到相机和跟随对象的距离
}
void Update()
{
    transform.position = offset + hero.position; // 移动时相机的位置 = 跟随对象的位置 + 两者的距离
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
          break;//可以用 break 来打断或中断循环
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
  someone.GetComponent<ClssFileName>().method; //获取物体脚本中的方法
  someone.GetComponentInParent<ClssFileName>.method; //视角：子物体身上的脚本，获得父物体身上的脚本方法
  someone.GetComponentInChildren<ClassFileName>.method; //父物体获得子物体身上的脚本方法
}
```

2. 获取组件及脚本 

   查询 Unity 核心模块：文档 `UnityEngine.CoreModule`

```c#
public class somethin; //找脚本就直接定义脚本，找组件就定义组件，组件必须存在 
private Transform something; //transform 是 Unity 的核心模块，可以直接定义

void Start()
{
  something.子类(); //获取脚本中的东西
  something = GameObject.Find("gameObject_name").transform;
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
FindObjectOfType<PlayerController>().CherryCount(); //根据 object 的名称查找
foreach(GameObject i in go){print(i);} //可以用 foreach 来查看找到的项
```

5. 通过单例化调用脚本，不太喜欢，static 感觉有限制，后期学ECS

```c#
public class something: MonoBehavious
{
  //把该脚本单例化，就可以从别的角色直接调用该脚本下的方法和值,单例化必须保证一个类只有一个实例,并提供一个全局访问点
  public static something instance; 
  
  private void Awake()
    {
        instance = this;// 在启动时调用一下，不写会调用不了。
    }
}
```

**单例模式的注意点**

```c#
//定义一个静态变量来保存类的实例,此例的类名为 Singleton
private static Singleton instance;

//定义私有构造函数,外界不能创建该类实例
private Singleton(){}

//定义一个标识来标记线程开关
private static readonly object locker = new object();

//定义仅有方法提供一个全局访问点,也可以定义公有属性提供全局访问点
public static Singleton GetInstance()
{
  //使用 lock 方法
  //lock 语句获取给定对象的互斥 lock，执行语句块，然后释放 lock。 持有 lock 时，持有 lock 的线程可以再次获取并释放 lock。 阻止任何其他线程获取 lock 并等待释放 lock。
  // 当第一个线程运行到这里时，此时会对locker对象 "加锁"，
  // 当第二个线程运行该方法时，首先检测到locker对象为"加锁"状态，该线程就会挂起等待第一个线程解锁
  // lock语句运行完之后（即线程运行完之后）会对该对象"解锁"
  lock (locker)
  {
  	if (instance == null)
  	{    
      //如果类的实例不存在则创建,否则直接返回
    	instance = new Singleton();
    }    
  }
  return instance;
}
```





```c#
//调用的脚本
something.instance.function();
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

void Update()
{
  newBullet(); //调用实例
}


void newBullet()
{
  bu = GameObject.Instantiate( bullet, transform.position, transform.rotation); // instantiate:实例化，第一个值：实例化的原对象，第二：位置，第三：角度
}
```



## Singleton 实例化

从游戏开始到关闭都会一直存在, 不会被销毁, 一般用于Game Setting, 管理场景 关卡 音乐切换

singleton会隐藏脚本依赖, 如果脚本里的方法有依赖, 会使问题变得不易发现.



## normalized 归一化

把当前值转化为（0，1）内的值。为了简化运算，优化性能。

Current vector is unchanged .

```c#
Vector2 direction = new Vector2(x,y).normalized;
Move(direction);
```





## Input

```c#
Input.GetMouseButtonDown(0); //0:鼠标左键，1：鼠标右键，2：鼠标中键
```



```c#
// 用按键给物体的运动加速
cube.Translate(Vector3.right * Time.deltaTime * Input.GetAxis("Horizontal"));
```



## 位置及跟随运动

- 设置一个物体和另一个物体有一段距离时停止运动

- Vector的方向：

  - 假设 a > b （a(3,4,5),b(2,2,1)）
  - a - b ：b 向 a 运动
  - b - a：a 向 b 运动

  ```c#
  private Transform b;
  
  void Start()
  {
    b = GameObject.Find("target").transform;
  }
  
  a = b.position; // 先取得 b 的位置
  a.y -= 1.5f; // a 的 y (或 x ) - a和 b 的距离
  
  transform.position = Vector3.MoveTowards(transform.position, a, speed * Time.deltaTime); //使用 MoveTowards 方法
  ```

- 跟随运动

  ```c#
  transform.parent = b; //指定物体为父级
  ```



## 碰撞

```c#
private void OnCollisionEnter(Collider2D collision)
{
  print(collision.collider.name); //获取碰撞物体的名字
}
```



## 触发区域

```c#
private void OnTriggerEnter(Collider other) //此方法不需要更改方法，只编辑返回值就可以
    {
        print("opps! " + other.name); //获取碰到的触发物体的名字
    }
```

## Random 随机数

- ` Random.Range(min,max);  `
  - int : Return a random integer number between `min` [inclusive] and `max` [exclusive]
  - float：Return a random float number between  ` min `  [inclusive] and ` max ` [inclusive]

```c#
public class ExampleClass : MonoBehaviour
{
    public GameObject prefab;
    // Instantiate the Prefab somewhere between -10.0 and 10.0 on the x-z plane
    void Start()
    {
        Vector3 position = new Vector3(Random.Range(-10.0f, 10.0f), 0, Random.Range(-10.0f, 10.0f));
        Instantiate(prefab, position, Quaternion.identity); //Quaternion.identity:不旋转
    }
}
```

- ` Random.InitState(int seed);  `

```c#
private float[] noiseValues;
    void Start()
    {
        Random.InitState(10); //10 seed, if don't set ,Unity will random as it own rule.
      	// Random.InitState((int)System.DateTime.Now.Ticks); // get the system time and force change frome long to int, not necessary
        noiseValues = new float[5]; //5 line
        for (int i = 0; i < noiseValues.Length; i++)
        {
            noiseValues[i] = Random.value; //Random.value is return a random number between 0.0[inclusive] and 1.0[inclusive]
            Debug.Log(noiseValues[i]);
        }
    }
```

- ` Random.insideUnitCircle ` 在一个半径为1的圆的范围内随机生成

  ```c#
  transform.position = Random.insideUnitCircle * 5;
  ```

- ` Random.insideUnitSphere ` 在一个半径为1的球体内随机生成



## 显示分数

```c#
using UnityEngine.UI; // 要用 text 组件显示分数 ，text 在 UI Module 下

public Text scoreText; // 定义一个变量放 text 组件
private int scores; // 定义一个变量接收分数计数
void Update()
{
   if (Input.GetMouseButtonDown(0)) // 每按一次鼠标
   {
     scores++; // 分数+1
     scoreText.text = scores.ToString(); //把 scores 中存的值显示在 scoreText 上。
   }
  
}
```

## 重载/切换场景

```c#
using UnityEngine.SceneManagement; //需要调用场景管理 Module

void Update()
{
  SceneManager.LoadScene(SceneManager.GetActiveScene().buildIndex);
}
```

- 显示场景加载进度 ` SceneManager.LoadSceneAsync `

```c#
using UnityEngine.SceneManagement;
public class Example : MonoBehaviour
{
    void Update()
    {
        // Press the space key to start coroutine
        if (Input.GetKeyDown(KeyCode.Space))
        {
            // Use a coroutine to load the Scene in the background
            StartCoroutine(LoadYourAsyncScene());
        }
    }

    IEnumerator LoadYourAsyncScene()
    {
        // The Application loads the Scene in the background as the current Scene runs.
        // This is particularly good for creating loading screens.
        // You could also load the Scene by using sceneBuildIndex. In this case Scene2 has
        // a sceneBuildIndex of 1 as shown in Build Settings.

        AsyncOperation asyncLoad = SceneManager.LoadSceneAsync("Scene2");

        // Wait until the asynchronous scene fully loads
        while (!asyncLoad.isDone)
        {
            yield return null;
        }
    }
}
```



## 时间

### Time

- ` Time.timeScale` 控制动作的快慢，0为暂停，1为匀速，>1为加速 , <1 为减速，不可<0

- 默认单位为1米，一帧调用一次 Update，则1帧运动1米，一秒60帧则1秒运动60米，使用 ` *Time.deltaTime` 是 * 每帧使用的秒数，根据电脑性能，如果 FPS 为60 ，则 Time.deltaTime 为 0.0167

- ` Time.realtimeSinceStartup` ：用于测试性能耗费时间。

  ```c#
  float time1 = Time.realtimeSinceStartup;
  for (int i = 0; i< 10; i++)
  {
    Method1();
  }
  float time2 = Time.realtimeSinceStartup;
  Debug.Log(time2 - time1);
  ```

## 发送消息

1.  ` GameObject.BroadcastMessage` ：给一个对象及其所有子对象发送消息（脚本挂在父物体上）

```c#
// 发消息的对象
public GameObject Receiver; //需要先指定一个接收者

void Start()
{
  Receiver.BroadcastMessage("ApplyDamage");
}
```



```c#
// 接收消息的对象

void ApplyDamage() // 直接引用方法
{
  print("received!");
}
```

2. `GameObject.SendMessage` ：只给当前接收者发送消息，不会同时给子物体发送。

```c#
//发送消息方，通过 sendmessage 来触发方法
collision.SendMessage("Die");
```



```c#
//接收消息方,有一个方法就可以
public void Die()
{
  sr.sprite = BrokenSprite;
}
```



3. ` GameObject.SendMessageUpwards` ：给当前物体及其父物体发送信息，直到根级

## 协程 Coroutine

- 在执行其他方法时同时执行其他方法的方法。
- 协程方法可以暂停。
- **[必须]**使用 ` yield return ` 来停止并返回参数。
- IEnumerator：迭代器

```c#
public class time : MonoBehaviour
{
    public GameObject cube; //指定一个游戏物体
  
    void Update() //在 Update 方法中调用
    {
        if (Input.GetKeyDown(KeyCode.Space)) //当按下空格键时，开启协程
        {
            StartCoroutine("Fade"); // 调用方法,使用方法名，开启和关闭必须使用同样的规则，例如都用方法名
        }
      	if (Input.GetKeyDown(KeyCode.D))
        {
          StopCoroutine("Fade"); //按下 D 停止调用协程，使用方法名，停止协程不能直接使用方法
        }
      
    }
    IEnumerator Fade()  //定义方法
    {
        for (; ; ) //死循环
        {
            Color c = cube.GetComponent<Renderer>().material.color;
            Color newColor = Color.Lerp(c, Color.red, 0.02f); //使用插值 lerp
            cube.GetComponent<Renderer>().material.color = newColor;
            yield return new WaitForSeconds(0.1f); //暂停0.1秒后执行下一句
            if (Mathf.Abs(Color.red.g - newColor.g) <= 0.01f) //如果颜色已经变为目标颜色红色
            {
                break; //则退出循环
            }
        }
    }
}
```

## Math的应用

- Clamp：范围值，如果当前值大于范围最小值，取最小，当前值大于范围最大值，取最大。

  ```c#
  private int hp = 100;
  void TakeDamage()
  {
    hp = Mathf.Clamp(hp, 0, 100); //当 hp 小于0，返回0；hp 大于100，返回100
  }
  ```

- Ceil：向上取整
- Floor：向下取整
- Pow（f, p）：取 f 的 p 次方
- Sqrt ：返回 x 的平方根
- PingPong/Repeat（t , length）：值 t 在 0 ~ length 范围内循环，如果需要从 x ~ length 之间运动，` x + Mathf.PingPong(t, length-x);
- Lerp（a, b , t ）：a 开始值，b 结束值（b>a），t 插值（t = 0，返回 a；t=1，返回b） 先快后慢。
- MoveTowards（current，target，maxdelta）：匀速接近或远离目标，maxdelta 步值

## Quaternion 四元数

用于改变旋转的角度。

```c#
public Transform cube;
// 设置物体的角度方法1:直接使用欧拉角
cube.eulerAngles = new Vector3(45, 45, 45);
// 设置物体的角度方法2：把欧拉角转为四元数
cube.rotation = Quaternion.Euler(new Vector3(45, 45, 45)); 
cube.rotaiton = Quaternion.Euler(transform.eulerAngles+bullectEulerAngles);
```

- LookRotation：让控制角色面向目标

```c#
public Transform Player;
public Transform Enemy;

void  Update()
{
  Vector3 direction = Enemy.position - Player.position; //从 Player 朝向 Enemy 的向量
  direction.y = 0; //如果需要锁定某个轴的旋转
  Player.rotation = Quaternion.LookRotation(dircetion);
  
}
```

- Slerp：球面插值，在插值中加入曲率，更平缓

```c#
private void Update()
    {
        Vector3 direction = Player.position - Enemy.position; //注意方向
        Quaternion target = Quaternion.LookRotation(direction);
        Player.rotation = Quaternion.Slerp(Player.rotation, target, Time.deltaTime);
    }
```

## Rigidbody

### Move and rotation

- 用 rigidbody 控制物体的移动和旋转要比 Transform 更快，如果物体有刚体时

```c#
public Rigidbody Player; //定义 rigidbody
Rigidbody Player; //也可以不 public rigidbody
Vector3 v3;

void Start()
{
  Player.position = new Vector3(2,2,3); //直接设置 rigidbody 的位置
  v3 = new Vector3(0,100,0);
  Player = GetComponent<Rigidbody>(); //如果不public 获取，则需要在内部指定
  
}

void Update()
{
  player.MovePosition(player.transform.position + Vector3.forward * Time.deltaTime); // 持续移动物体推荐使用 MovePosition ，MovePosition 会给移动增加插值，使移动更平滑，如果需要直接移动，使用 position 
  Quaternion deltaRotation = Quaternion.Euler(v3 * Time.deltaTime); // Rigidbody 的 rotation 是一个 Quaternion
  player.MoveRotation(player.rotation * deltaRotation);//持续旋转物体使用 MoveRotation,此处为 让物体围绕世界坐标的 y 轴旋转
  
  
}
```

### AddForce( Vector3 , ForceMode ) ;

给运动添加力，力符合力学定律。

```c#
public int/float force;
public Rigidbody Player;

void Update()
{
  Player.AddForce(Vector3(0,20,0) * force,ForceMode.Force); //或者把 force 使用在某个轴上
}
```

| [Force](ForceMode.Force.html)                   | Add a continuous force to the rigidbody, using its mass.     |
| ----------------------------------------------- | ------------------------------------------------------------ |
| [Acceleration](ForceMode.Acceleration.html)     | Add a continuous acceleration to the rigidbody, ignoring its mass. |
| [Impulse](ForceMode.Impulse.html)               | Add an instant force impulse to the rigidbody, using its mass. |
| [VelocityChange](ForceMode.VelocityChange.html) | Add an instant velocity change to the rigidbody, ignoring its mass. |

## Camera

- 获得鼠标点击的位置，并返回物体的名字

```c#
    private Camera mainCamera;

    void Start()
    {       
        mainCamera = Camera.main;
    }

    private void Update()
    {
        Ray ray = mainCamera.ScreenPointToRay(Input.mousePosition); //创建射线
      	Ray ray = new Ray(transform.position, transform.forward); //创建射线的另一个方法    
        RaycastHit hit; //定义一个变量放 out 的参数
        bool isCollider = Physics.Raycast(ray, out hit); //raycast 可以指定射线长度
        if (isCollider)
        {
            Debug.Log(hit.collider.name); //返回鼠标触碰的物体的名字
          	Debug.DrawRay(ray.origin, ray.direction * 10, Color.yellow); //画出射线
        }
    }
```



### 从物体发出射线

```c#
//从IK脚部发出射线
RaycastHit hit;
Ray ray = new Ray(animator.GetIKPosition(AvatarIKGoal.LeftFoot) + Vector3.up, Vector3.down);
Debug.DrawyRay(animator.GetIKPosition(AvatarIKGoal.LeftFoot), Vector3.down, Color.red);

//从碰撞物体表面发出normal射线
Debug.DrawRay(hit.nomal, hit.normal, Color.green);
```







## 监听GUI 事件

```c#
using UnityEngine.UI;
using System;
using TMPro; //如果使用有 texmeshpro 的组件，需要引用命名空间

public GameObject btn;
public GameObject slider;
public GameObject dropdown;
public GameObject toggle;


void Start()
{
  btn.GetComponent<Button>().onClick.AddListener(this.btnOnClick); // 在 button 组件上添加监听方法
  slider.GetComponent<Slider>().onClick.AddListener(this.silderChange); // 在 slider 上添加监听方法
  dropdown.GetComponent<Dropdown>().onClick.AddListener(this.dropdownChange); // 在普通 dropdown 上添加监听方法
  dropdown.GetComponent<TMP_Dropdown>().onClick.AddListener(this.dropdownChange); //在 TMP dropdown 上添加监听方法
	dropdown.GetComponent<Toggle>().onClick.AddListener(this.toggleIsTrue); 
} 

void btnOnClick()
{
  
}

void sliderChange(float value)
{
  
}

void dropdownChange(Int32 value)
{
   Debug.Log("What you want!" + value);
}

void toggleIsTrue(bool value)
{
   Debug.Log("cancel that check! " + value);
}
```

### 跟鼠标相关的事件接口

文档：Manual / Scripting / Event System / Supported System

方法不可修改参数，只能修改触发后的事件。

挂在哪个物体上就只能控制当前物体。

```c#
using UnityEngine UI;
using UnityEngine.EventSystems; //要引用 event systems 才能使用里面的事件方法

public class time : MonoBehaviour, IPointerDownHandler // Called when a pointer is pressed on the object
{
    public void OnPointerDown(PointerEventData eventData)
    {
        Debug.Log("hey you!");
    }
}
```

## CharacterController

不经过 rigidbody 控制物体的运动。

```c#
// 脚本名字不可以重名，有一个组件为 CharacterController，脚本不可命名为CharacterController。
public float Speed = 3;
private CharacterController cc;

private void Start()
{
    cc = GetComponent<CharacterController>();
}

private void Update()
{
    float h = Input.GetAxis("Horizontal");
    float v = Input.GetAxis("Vertical");

    cc.SimpleMove(new Vector3(h, 0, v) * Speed); 
  	cc.Move(new Vector3(h, 0, v) * Speed * Time.deltaTime); // move 需要给一个时间间隔，没有重力影响
}
```

## Mesh

把一个物体的 mech 修改成另一个物体的。

```c#
public Mesh mesh;

void Start()
{
  GetComponent<MeshFilter>().mesh = mesh; //复制一个实例再赋值
  GetComponent<MeshFilter>().shareMesh = mesh; //直接share,性能更快
}
```

## Material

```c#
//用  MeshRenderer 里的 material 改变物体颜色
private Material mat;

private void Start()
{
   mat = GetComponent<MeshRenderer>().material;
}

private void Update()
{
   mat.color = Color.Lerp(mat.color, Color.red, Time.deltaTime);
}
```



```c#
// 把物体颜色变为自定义颜色，因为 Color 是 struct 结构体，不可以单独对结构体内部元素赋值，需要先转换。color 和 vector4 可以互相转换。

    private Material mat;

    private void Start()
    {
        mat = GetComponent<MeshRenderer>().material;
    }

    private void Update()
    {
        Vector4 v4 = new Color(0.3f, 0.4f, 0.6f); //先设置一个目标颜色
        mat.color = Color.Lerp(mat.color, v4, Time.deltaTime);
    }
```

## 数组

```c#
public Sprite[] tankSprite; //创建一个公开的 sprite 数组，即可把动画图片拖到数组中

private void Awake()
    {
        sr = GetComponent<SpriteRenderer>();
    }

private void Update()
{
  sr.sprite = tankSprite[1];
}
```

切换怪物出现次序

```c#
public GameObject[] Monsters; //创建一个游戏物体组，把游戏物体拖入
public GameObject activeMonster = null; //创建一个位置放置被随机到的游戏物体

private void ActivateMonster()
{
  int i = Random.Range(0, Monster.Length); //随机循环一组长度为 Monsters 的长度的数组
  activeMonster = Monsters[i];
  activeMonster.SetActive(true);
}

```





## 冻结/解冻游戏

```c#
// 暂停游戏，冻结时间
Time.timeScale = 0f;
Curor.visible = true; // 隐藏鼠标
// 回到游戏，解冻时间
Time.timeScale = 1f;
Curor.visible = false; // 显示鼠标，可以点击
```

