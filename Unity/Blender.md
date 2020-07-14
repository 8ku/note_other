# Blender

## 三方插件

### 骨骼

- bone layer manager

### 图层管理

- simple_renaming_panel

### 工作流程插件

- [万物有灵](https://shimo.im/docs/tWhW8QJPHhDqKwr9/)
  - 安装好插件后，在`add-on`中导入预设
  - 使用时，点击`import`可应用

### 烘焙

- [Bake Wrangler](https://blenderartists.org/t/bake-wrangler-node-based-baking-tool-set/1187732)
  - [教程](https://www.bilibili.com/s/video/BV14z4y1R789)

## 视图操作

- 放大缩小面板：按住ctrl，按住中键在需要放大缩小的面板上，上下滑动
- 调出/收起属性面板：n

## 选择:

- 随机选择:Select     - Select Random
- 按组选择:Shiift+g
- 灯光方向
  - 主键盘-句号：选择`3D Cursor`，再移动灯光位置

## 物体操作:

- **对物体命名：F2**
- 建立父子关系:     cmd/control+p
- 物体吸附：
  - 吸附到表面，勾选`align rotation to target`可以根据吸附面的方向自动转向
- 沿地面网格移动物体：先按G/R/S，按住ctrl操作
- 选中的物体视图居中并把坐标归零: shift+c
- 切换对齐方式：主键盘-句号
- 选中多个物体时，以每个物体自身中心点缩放：对齐方式选择 `Individual Origins`
- 延局部坐标移动/缩放/旋转：先按快捷键（G/S/R），再按两下方向（X/Y/Z）
- 复制物体:     shift+d
- 对齐物体：ctrl+alt+a
- 向一个轴缩放：编辑模式-shift+ctrl+alt+s
- **复制且让新物体继承原物体(操作原物体时新物体一起被操作): alt+d**
- 延法线挤出:alt+e
- 在物体模式下应用变换(应用后可以让所有数值归零): ctrl+a
- 清除游离点/线/面: mesh-clean up-delete loose
- 翻转物体：alt+f
- 使用正则批量给物体重命名的技巧（有时做镜像复制时会有很多带 .001 的物体）
  - 框选要重命名的物体
  - 使用插件`simple renaming panel`
- 视图:
  - 选中物体最大化：Numpad-句号

## 建模

- 点倒角：ctrl+shift+b
- 添加插件`Extra Objects` 分别勾`Curve` `Mesh`
- 做楼梯
  - 做两个面
  - array
- 做栅栏
  - 平面，ctrl+r 切分
  - ctrl+b 倒角
  - 删除倒角面
  - 挤出
- 做树枝
  - 用点画出主干
  - 添加`skin`
  - 进入编辑模式，a全选，ctrl+a 收缩
  - 选择单独节点 ctrl+a 调整
- 做蔓藤
  - 做要放置蔓藤的平面区域（切分会影响生成方向和密度）
  - 做树叶
  - 在区域中添加粒子生成器
  - `Render`选择`Object`，物体选择树叶
  - `Physics`选择`none`
  - 调整`Rotation`里的参数
- 做冰块
  - 切换到雕刻模式
  - 使用`scrape`
  - `n`打开属性面板，选择`tool`，勾选`Dyntopo`，`Detail size`调小
  - 这样边雕刻，物体会增加细分
  - 最好雕刻完以后，把该物体做为高精模烘到低精上，直接渲染会死机

### array的技巧

- 做螺旋线
  - 创建一个物体，array
  - 建立一个空物体 `Plain Axes`
  - 在array中勾选`Object Offset`，物体选择空物体
  - 使用R旋转，S缩放
  - 勾选`Merge`，`distance`调大
- 沿曲线array不变形
  - 创建平面，array
  - 添加 curve，物体选择曲线
  - 新建一个物体，把该物体做为平面的子物体（ctrl+p）
  - 在`Object properties-instancing`里选择`Face`，去掉`Display Instancer`的勾选

## 人体建模

- 头部

- - 建正方体
  - cmd+2

### 父子关系

- 如果解除父子关系不起作用，试试ctrl+j合并两个物体，再进入编辑模式，L，P解除合并

- 如有一对父子关系物体，想让新物体 C 跟随父物体 B 运动，但不绑定为新的子物体，可在`ObjectConstraint Properties` 中添加 `Copy Location`或其他， `Target` 选择子物体 B（或者在pose mode下，先选B，再选C，shift+ctrl+c)
- 勾选`Offset`可以移动 C ，让 C 和 B 有距离，调整`Influence` 可以调整影响的强度
- 如果`Spece` 选择 `World Space <--> World Space`，两者都使用世界坐标移动；如果选择`Local Space <--> Local Space`，则双方以自己的局部坐标方向移动；

## 骨骼绑定

### 骨骼绑定的要点：

- 建立骨骼前注意把坐标归零 shift+c
- 把骨骼名字显示出来，养成给骨骼命名的习惯
- 确保躯干和腿所有骨骼的Z轴都面向前，手臂骨骼的Z轴向上
- 中心骨骼（root）的坐标必须保持和世界坐标一致，中心骨骼一般位于整个模型的底部中心
  - 先沿Z轴建一根骨骼，命名为root
  - 点击骨骼的tail,shift+s,选择 selection to cursor
  - 沿Y轴移动Tail
  - 或沿Z轴建一根骨骼，再沿X轴旋转-90度
- 使用`Bone Layer Manager`管理骨骼层 [地址](https://gumroad.com/l/STdb)
  - 使用`Bone Layers`右边的圆点可以把选中的骨骼加入该层：先选骨骼，再点圆点
  - ![image-20200628173318326](Blender.assets/image-20200628173318326.png)
  - **root不需要deform，把root单独放到一层中，把其他骨骼全选，shift+w - deform**
- 做好单边骨骼后，复制一份，原骨骼层（DEF）做为导入到其他软件的骨骼结构，复制的骨骼可以放到单独一层，教程用命名为TGT层
- 使用TGT驱动DEF，先选中TGT的单个骨骼，再选中DEF的单个骨骼，shift+ctrl+c-copy transforms，此操作可把DEF层的骨骼互相解绑
- 把TGT层的`deform`取消，之后和人体绑定时不会绑到TGT层和ROOT层
- 把人物的Armature置于细分之上
- 刷权重时，**注意权重影响的是DEF（deform）层，TGT层用于控制人物动作，所以刷权重需要让DEF层显示，TGT层隐藏，不然会找不到所选择的骨节对应的蒙皮区域**
- 使用`Simple rename panel`管理批量命名（此插件可以重命名所有物体，不仅骨骼） [地址](https://gumroad.com/l/simple_renaming_panel)
  - 把需要批量命名的骨骼放到同一层，全选，使用“在选择的物体中替换”



### 骨骼绑定方法1:

使用骨骼绑定控制物体行动的原因是：调整骨骼动画时，变换父级，子级动作也会被记录下来，而直接用物体做动画时，子级动画不会被记录，每个物体的运动是独立的

- 添加骨节:     
  1. e (同时按鼠标中键可保持90度)，之后shift+r，可以往一个方向同比挤出
  2. 右键 `subdivide`
- 添加没有父节点的骨头:shift+a
- 在关节之间加骨骼:f
- 让解除关联/新添加的骨骼关联到物体：shift+w-deform/alt+left click deform(选择多段骨骼时好用)
- 显示骨骼名称：`Object Data Properties-Viewwport Display`，勾选`Name` & `Axes`
- **在编辑模式下调整骨骼朝向**：ctrl+r
- 在骨骼模式下**刷权重**（该模式下可以移动骨骼查看效果）
  - 物体模式下先选中骨骼，再选物体，进入权重刷编辑
  - 按住ctrl，点击左键选择骨节，此时会同时显示此骨节影响的蒙皮
  - **打开`Object propertise-Viewpoint Display`里的 `wireframe`，可以清楚看到权重对面的影响**
  - 使用面选择，按住ctrl选择面，可以把编辑范围限定在选择的面中
  - 推荐使用subtract和mix笔刷，subtract时，使用最后一个preset笔头；mix时，使用1的强度，低一点weight
  - **如果你的角色前臂运动总是影响了胸部和前臂，那是不对的**
- **对齐骨骼**：选择骨骼，再选择被对齐骨骼control+alt+a
- 解除父子关系: 在子节处     右侧骨头 删除父对象(alt+p，alt+p可以选择disconnect bons 或 y，y直接解除父子关系)
- 命名单侧手脚时要加     .L,全选单侧骨骼 (顶上中部的transfomr     pivot point 要换成3d cursor)- 右键:symmetrize
- 重新关联父子关系:     ctrl/cmd + p
- 添加IK: 先选IK, 再选骨骼, pose mode: shift + i
- 先选人体,再选骨架, ctrl+p
- 回归初始状态:     pose mode- alt+r/alt+g/alt+s
- 单独部件(例如眼球)未和身体一起绑定时,可单独选择眼球和骨架:cmd+p,选with empty groups
- 权重刷:object     mode-weight paint
- 权重刷一般用add模式
- 在edit mode里,选中要显示的骨头(带控制器的),m键加入图层,把其余的关闭显示
- 使用pose  mode设置动作时,要选择 Local坐标,不能用Global坐标
- **使用自动分配权重后,进入模型edit mode, 左上菜单Mesh-Weights-Normailze All 来重新计算权重**

 

### 骨骼绑定方法2:

- 插件  rigging:rigify
- 骨骼对齐模型
- 绑定IK: 选Object Data Properties(小人跳舞的图标)-Generate     RIg
- 先全选模型,再选骨骼,ctrl+p—with automation weights

 

### 在绑定骨骼的人物上加衣服

- 添加Cloth     modifier
- 调整Quality     steps(往高调整)
- 调整Tension(往低调)
- 调整Stiffness(僵硬)/Damping(衰减)-bending(往低调)
- 勾选     Collisions-Self Collisions
- Collisions:     distance(调高)
- 给人物身体添加Collision,勾选single Sided

### 骨骼动画

- 大多数骨骼运动是基于局部坐标，而不是世界坐标，所以在最初建立骨骼时，尽量让骨骼的臂部坐标和世界坐标一致 
- 给某个骨骼添加动画：选中要记录动画的骨骼，i

## 动画

- 在需要做动画的坐标上右键，`add driver`

- 打开`drivers`编辑器，调整曲线

- 在对应的属性页面的`custom properties`中(如果要控制骨骼，应在骨骼控制页面中添加)添加新值，起名，保存，右键`copy data path`

- 在`drivers`编辑器中，把刚复制的path粘贴到`path`一栏，`prop`可以选择物体本身

  ![image-20200701165414048](Blender.assets/image-20200701165414048.png)

  ![image-20200701174111695](Blender.assets/image-20200701174111695.png)

  ![image-20200701173935161](Blender.assets/image-20200701173935161.png)

  





## 拓扑: 

- 雕模
- 安装bsurfaces
- 新建一个plane
- 选择画笔
- add     surface
- fn+f9 增加面数
- 加镜像
- 加shrinkwrap     把皮往外offset一点,按住shift可以微量调整
- 打开 吸附至表面(顶上工具栏)
- 两下g 按住alt 散开移动(两下g: 在表面平滑移动)
- 镜像:勾选 clipping, extrude时可以自动合并镜像点
- 安装looptools     右键,再右键添加到收藏, 可使用q 调出收藏快捷菜单
- 选择连续几个点:     cmd+左击
- looptools     - loft: 顶点分散
- looptools     - space: 顶点均匀分布

### 场景建模技巧

- alt+g 物体位置归零
- options，选择“affects origins”，移动原点时吸附表面，让原点落到底部
- 曲线加点:编辑模式下, 选中两个顶点,选择左上角菜单-细分
- 导入其他blender文件:用 link或append
- 在编辑模式下添加细分, 使用smooth工具平滑

##  UV

### UV绘制

- 切换到UV     Editing, press u, select smart UV project, then switch to Texture Paint,     create a new image
- 切换到     Shading, 新建一个checker Texture, 选择上一步保存的image, 连接到roughness, 此时被上了UV的面会全反射环境, 再painting,     能把不需要反射的部分擦除

![img](Blender.assets/clip_image002.jpg)

 

###  物体使用不同UV

- 给整体加texture
- 复制一个材质，在编辑模式下assign需要另赋材质的部分
- 切换到物体模式，把整体材质取消复制标志（这样可以单独调节一个物体两部分的材质）
- ![image-20200708143448208](Blender.assets/image-20200708143448208.png)
- 在UV Editor里单独调整材质

## 烘焙

- 高分烘给低分

  - 使用插件**BAKE WRANGLER**，[教程](https://www.bilibili.com/s/video/BV14z4y1R789)

- ### 法线贴图

  - 复制一个模,做成高精, 雕刻
  - alt+g把两个模对齐
  - 给低精械添加一个材质,添加image texture, color-space:     non-color
  - 渲染模式改为cycles,     在bake中设置bake type为normal
  - 勾选     Selected to active
  - 先选择高精模,再加选低精模,点击bake
  - 如果法线渲染出来有没覆盖好的, 调Ray distance
  - 回到     shader editor, 添加normal map,把image的color连接到normal     map的color, then link normal map’s normal node to     principled BSDF’s normal node
  - 如果要添加表面凹凸, 添加一个Displace modifier, Texture选择到刚才渲染好的贴图



## 材质

### 玻璃材质

- 使用默认材质，把`Transmission`调到最大
- `Render Properties`勾选`Screen Space Reflections`，点开设置，勾选`Reflaction`
- 回到物体材质编辑，`Settings`，勾选`Screen Space REfraction`

### 透明

- 材质面板 `settings-Blend Mode-Alpha Blend`
-  在`Surface-Alpha`拉到0 



## 渲染

- 打开降噪:     compositing

- - use      nodes(左上角)
  - view      layer(右侧)-Passes-Data-Denoising Data
  - node界面: add Denoise

![img](Blender.assets/clip_image004.jpg)

- 加雾效

- - 放一个box,      box显示模式设置为线框, 给box加shader

![img](Blender.assets/clip_image006.jpg)

- 局部渲染:cmd+b(取消局部渲染: ctrl+alt+b)
- 渲染出图: 菜单-render-render image



## 常用快捷键

f: fill / alt+f(beauty fill) 

grid fill : ctrl/cmd + f then grid fill

镜像: mirror

挤出: e or ctrl+right mouse button(再按s,沿法线方向挤出) 

分别挤出(做手指时):alt+e

环切: cmd + r(早期不要用太多环切)

连续先边/点: 首顶点,ctrl 尾顶点

切分: k

松弛

合并顶点: alt + m

衰减编辑开关(调整物体形状): o (shift+o 可以变换模式)

雕刻模式smoothly : shift+左键

在空白处添加新点: ctrl/cmd + 右键

移动模型出现的中心点: shift + 右键(中心点归位: shift+s 中心点回到物体中心:ctrl+shift+alt+c)

add subdivision: cmd + 1/2/3

cmd+2:添加细分

桥接循环边：ctrl+e

分离对象：p(或y)

沿法线方向缩放：alt+s

在物体模式下应用变换(应用后可以让所有数值归零): ctrl+a

把节点一分为二: v

独显物体某部分: shift+h

反选: cmd+i

选择所有连接着的面: l

使用snap把分享的组件合起(例如手臂和身体)

快速顶点对齐:s-z/y/x-0

选中的物体视图居中: shift+c

物体弯曲:先设定弯曲点(shift+右键), 再shift+w

重新计算法线:shift+n

线框模式：shift+z



 

 

delete:x

make face: alt+f

rotate: r

scale: s

move: g

merge: m

change view mode: z

create model: shift+a

exchange edit mode: ctrl+tab or click menu ‘sculpting’

exchange sculpting: shift+space

change brush radius/strenght: f /shift+f

invert brush: ctrl

smooth brush: shift

loop cut: cmd + r

loop line: alt+left click

dulicate : shift + d

select box: b

zoom area: shift + b

zoom : cmd + left mouse

半透明: alt + z

切分: 编辑模式-右键subdivide

fill(封顶): f

单独显示选中物体: /

rotate x: r, x

select all : a 

场景平移: shift + 鼠标中键

调出插件工具条: n

布尔: 安插件 `bool tool` then ctrl+shift+b or ctrl + 小键盘 -，使用时选择`Brush Boolean`，在应用前都可以修改

hide : h / alt+h

把物体中心点归到物体中心: 右键 origin to geometry

**坐标归零: alt+g**

分窗口: 在边缘右键

摄像机视图: 小键盘0(正交摄像机:属性选择Orthographic)

把当前视角设置为摄像机视角: ctrl + alt + numpad0

旋转摄像机视角: 上一步后,点击视角边缘, g移动 r旋转

导入: f12

选择所有相连元素: ctrl+L

擦除: cmd + (三指)

检查面朝向: show overlays - face orientation 

法线方向菜单: 编辑模式下选择所有面, alt + n

查看法线方向: 左上 global - 改为 normal

编辑-点模式-alt+左键: 选择相邻点

切割knife: k

合并点: alt + m

打开snap: shift + tab

添加细分: cmd + 2(需要关闭数字键映射)(反细分: modifier - decimate - unsubdivide/edge-unsubdivide)

挤出: 编辑模式-ctrl+右键（沿法线挤出：alt+e）

倒角: ctrl/cmd + b

两个对象合并: ctrl + j (合并后不能单独处理单个对象, 但可以共享modifier

反细分: modifier - decimate - unsubdivide/edge-unsubdivide

内挤出: i (如果再点击B, 可以让镜像边不挤出)

改变曲线控制柄类型:v

正交视图:Numpad-5

