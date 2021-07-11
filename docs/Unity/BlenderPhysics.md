<head>
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$']]
            }
        });
    </script>
      <script src="https://unpkg.com/mermaid@8.0.0/dist/mermaid.min.js"></script>
      <script>mermaid.initialize({startOnLoad:true});</script>
</head>
# Blender Physics



## 流体动画

- 新建一个立方体(球体等)做为液体发射器
  - 在`Physics properties`中添加`Fluid`
  - Type: flow
  - setting: 
    - flow type: liquid
    - Flow Behavior: inflow
    - 勾选 Use Flow
    - 勾选 Initial Velocity
      - Initial X/Y/Z 根据要发射液体的方向设置速度
- 选中立方体, 左上角 `Object - Quick Effect - Quick Liquid` 创建流体运动空间
  - Domian Type : Liquid
  - Resolution Division: 80或以上 (如果渲染没效果就向上增加值, 这是是空间边缘和作用域的距离, 数字越大, 边界和作用域间距越小(渲染时消耗资源越多))
  - 勾选 Diffusion
  - 勾选 Mesh
  - 勾选 Is Resumable
  - Type: Modular(为添加空间中其他碰撞体用)
- 新建一个管道, 或平面
  - 在`Physics properties`中添加`Fluid`
  - Type: Effector
  - Effector Type: Collision
  - 勾选 Is Planar
- 回到运动空间
  - 在setting下点击Bake Data查看效果
    - 如果无效果, 把 resolution Division数字加大
  - Bake Mesh, 如果不Bake, 空间会不透明
- 导出为 `.abc`



## 布娃娃 ragdoll

### 手脚

- 把要脱离的部分和父级解除绑定关系，在本例中为**手部和脚部骨骼**
- 把解除的部分和原父级用IK连接
- 新建`Mesh-single vert`，沿手脚按关节挤出，命名为`ragdoll_line`
  - 全选，沿y轴挤出一点（为了可视，线看不清）
  - 镜像得到右侧手脚
  - 给手脚和手脚尖的顶点建立顶点组`hand.L`, `hand_end.L`, `hand.R`, `hand_end.R` 等
  - 两边肩部建顶点组`pin`
- 给`ragdoll_line`添加布料模拟器
  - `Shape-Pin Group` 选择`pin`组
  - 勾选`Object Collisions`
- 在`Pose mode`下，把`ragdoll_line`绑定为脊柱（`spine`的上一节）的子集：在`Pose Mode`下，选中`spine.001`， `set parent to bone`
  - 点击`play`，移动`spine`看效果
- 给手脚的骨骼建立`bone constraint-Copy Location`  `Damped Track`
  - `Copy Location`
    - `Target` : `regdoll_line`
    - `Vertex Group` : `hand.L`
  -  `Damped Track`
    -  `Target` : `regdoll_line`
    - `Vertex Group` : `hand_end.L`
  - 点击`play`看效果

### 头部

- 新建 `Mesh-single vert`，命名为`ragdoll_head`
  - 添加一个顶点组`head`
  - 添加`Soft Body`模拟器
    - 修改参数`Object-mass` : 0.5kg
- 把顶点绑定为脖子骨骼的子对象：在`Pose Mode`下，选中脖子， `set parent to bone`
- 给头部骨骼添加`bone constraint-Damped Track`
  - `Target` : `ragdoll_head`
  - `Vertex Group` : `head`
- 点击`play`看效果



### 制作碰撞体

- 在大腿、身体、头部位置新建立方体，给立方体添加碰撞体模拟器
- 绑定到对应的骨骼上 `set parent to bone`
- 把碰撞体建组`Collisions`
- `ragdoll`的布料模拟器下`Collisions`
  - 勾选`Object Collisions`
    - `Collision Collection` ：`Collisions`



## 绳摆

### 随绳晃动的小球

- 新建一个mesh的点，拉成直线，细分
- 加skin修改器
- 加cloth修改器
  - Pin Group ： 选择顶点（如果没有组，去给要固定的顶点组建组）
  - 勾选Object Collisions
  - 勾选Self Collisions
- 创建一个悬挂物
  - `copy location` 
  - `copy rotation`

### 摆动的球（类似风铃）

- 新建一个mesh作为控制平面
  - 添加 Rigidbody修改器
    - Type: Passive
    - Settings: Animated
- 新建一个悬挂物
  - 添加 Rigidbody修改器
- 先选择悬挂物，再选择控制平面，`Object-Rigid body-Connect`，生成一个`Constraint`
- 把`Constraint`对齐到控制平面
  - Type: Point (默认的fixed情况下悬挂物不能动)
- 选择`Constraint`，再选择控制平面，cmd+p 连接

