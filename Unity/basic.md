# 基本概念

## HUD Head-Up Display

抬头显示，指在屏幕上显示游戏相关信息

## 2d tile技巧

- 设置图片 Pixels per unit 为16，sprite mode 为 mulitple ，用 sprite editor 切割好图片
- 设置图层：Sorting Layer 可设置多个图层，越下面排在越前面
  - Order in Layer 是相同图层内的排序 ，数字越大越前面
- 创建Player：新建一个sprite，把贴图拖到 Sprite 中
- Player 要碰撞要添加刚体 rigidbody 和 碰撞体 Collider，地面也要添加碰撞体 tilemap collider
- Player 在空中翻转：Rigidbody 2D - Constraints - Freeze Rotation z ：打勾，冻结z轴旋转

## 移动

```c#
public RigidBody2D rb;  //定义一个刚体，改名为 rb ，保存后，在图形界面上把 player 的刚体拖到这里绑定
public float speed;  //定义一个类型为speed

void Update()
{
    Movement(); //引用movement的值
}


void Movement()
{
    float horizontalmove;  //定义一个字段为 横向移动
    horizontalmove = Input.GetAxis("Horizontal");  // 读取键盘横向移动的坐标axis,横向移动只有三个值，-1 为向左移动，1 为向右移动 ，0 为不动，Horizontal要区分大小写，要拼写正确，和系统默认的名称保持一致
    
    if (horizontalmove != 0) //如果横向移动的值不为0，说明 player 在移动，则设置刚体的速率为 x = 当前坐标 * 速度 ，y = 刚体的 y 速率
    {
        rb.velocity = new Vector2(horizontalmove * speed, rb.velocity.y);
    }
}
```

**将刚体 Constrants 里的 z 勾选，让它不会飞起来**