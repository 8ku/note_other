Unity中的C#语法

基本格式：

~~~c#
using System.Collections;
using UnityEngige;
// PlayController :脚本名
public class PlayerController : MonoBehaviour 
{
	void Start() {
        
    }
    void Update() {
        
    }
}
~~~

- 不需要带Main方法

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

## 移动，跳跃，动画

```c#
public RigidBody2D rb;  //定义一个刚体，改名为 rb ，保存后，在图形界面上把 player 的刚体拖到这里绑定
public Animator anime; //把动画控制器绑定角色
public float speed;  //定义一个类型为speed
public float jumpforce; //定义一个类型设置力的初始大小，在界面上

void FixedUpdate() //FixedUpdate要求用固定的频率调用，除了用来处理物理逻辑之外并不适合处理其他模块的逻辑,有可能 fixedupdate 的频率会高于游戏设定频率，如此 fixedupdate 就会调用太多次
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
    rb.velocity = new Vector2(rb.velocity.x, jumpforce * Time.deltaTime);
  }
}
```

## 动画效果