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

