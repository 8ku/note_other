# Physics

## 2D

### [Rigidbody 2D](https://docs.unity3d.com/Manual/class-Rigidbody2D.html)

- 同一个物体上的多个对撞机 collider 不会互相碰撞，所以一个物体可以加多个对撞机。
- **将刚体 Constrants 里的 z 勾选，让它不会飞起来**
- rigidbody 如果没有 collider 不能互相碰撞
- Body Type，根据运动方式和碰撞交互形式来选择：
  -  Dynamic 动态的
    - 适用于所有类型的刚体
  - Kinematic 动力学上的
  - Static 静态的

### Conllider

- isTrigger ：means is the collier a trigger? if yes, it doesn’s hit a collision. 

## 光照贴图

- 烘焙
  - static 灯光
  - 把灯光改为 baked
  - lighting settings 中，生成灯光

## 导航系统（寻路系统）

### 添加可行走区域

window - AI - Navigation -Bake

如果需要让某些物体可穿过，点击物体，Inspector ，取消 Navigation Static

取消物体某些部分的行走区域，先选择物体的 mech Renderers 部分，在 Navigation - Object 中，把 Navigation Area 设置为 Not Walkable

### 给角色添加寻路控制器

add componet - Nav Mesh Agent

### 添加目的地

把代码加到 player 下

```c#
using UnityEngine;
using UnityEngine.AI; //引用 AI 模块

public class Player : MonoBehaviour
{
    public NavMeshAgent meshAgent; //定义一个对象装载 Nav Mesh Agent


    // Update is called once per frame
    void Update()
    {
        if (Input.GetMouseButtonDown(0)) //如果鼠标按下
        {
           // Returns a ray going from camera through a screen point.
            Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);
            RaycastHit hit; //接收射线返回的坐标
            if (Physics.Raycast(ray, out hit)) //如果 ray 得到值，传出给 hit
            {
                meshAgent.SetDestination(hit.point); //把 hit 的坐标传给 mechAgent 的 Destination
            }
        }
    }
}
```



