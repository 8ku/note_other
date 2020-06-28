# Blender

## 选择:

- 随机选择:Select     - Select Random
- 按组选择:Shiift+g

 

## 物体操作:

- 建立父子关系:     cmd+p
- 复制物体:     shift+d
- 复制且让新物体继承原物体(操作原物体时新物体一起被操作): alt+d
- 延法线挤出:alt+e
- 清除游离点/线/面: mesh-clean up-delete loose
- 视图:
  - Numpad: .
- 做楼梯
  - 用array

## 人体建模

- 头部

- - 建正方体
  - cmd+2

### 骨骼绑定1:

- 添加骨节:     shift + e (同时按鼠标中键可保持90度)
- 添加没有父节点的骨头:shift+a
- 在关节之间加骨骼:f
- 解除父子关系: 在子节处     右侧骨头 删除父对象(alt+p 或 y)
- 命名单侧手脚时要加     .L,全选单侧骨骼 (顶上中部的transfomr     pivot point 要换成3d cursor)- 右键:symmetrize
- 重新关联父子关系:     ctrl/cmd + p
- 添加IK: 先选IK, 再选骨骼, pose mode: shift + i
- 先选人体,再选骨架, ctrl+p
- 回归初始状态:     pose mode- alt+r
- 单独部件(例如眼球)未和身体一起绑定时,可单独选择眼球和骨架:cmd+p,选with empty groups
- 权重刷:object     mode-weight paint
- 权重刷一般用add模式
- 在edit mode里,选中要显示的骨头(带控制器的),m键加入图层,把其余的关闭显示
- 使用pose     mode设置动作时,要选择 Local坐标,不能用Global坐标
- **使用自动分配权重后,进入模型edit mode, 左上菜单Mesh-Weights-Normailze All 来重新计算权重

 

### 骨骼绑定2:

- 插件     rigging:rigify
- 骨骼对齐模型
- 绑定IK: 选Object Data Properties(小人跳舞的图标)-Generate     RIg
- 先全选模型,再选骨骼,ctrl+p—with automation weights

 

### 在绑定骨骼的人物是加衣服

- 添加Cloth     modifier
- 调整Quality     steps(往高调整)
- 调整Tension(往低调)
- 调整Stiffness(僵硬)/Damping(衰减)-bending(往低调)
- 勾选     Collisions-Self Collisions
- Collisions:     distance(调高)
- 给人物身体添加Collision,勾选single Sided

 

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

 

### UV绘制

- 切换到UV     Editing, press u, select smart UV project, then switch to Texture Paint,     create a new image
- 切换到     Shading, 新建一个checker Texture, 选择上一步保存的image, 连接到roughness, 此时被上了UV的面会全反射环境, 再painting,     能把不需要反射的部分擦除

![img](Blender.assets/clip_image002.jpg)

 

### 法线贴图

- 复制一个模,做成高精, 雕刻
- alt+g把两个模对齐
- 给低精械添加一个材质,添加image texture, color-space:     non-color
- 渲染模式改为cycles,     在bake中设置bake type为normal
- 勾选     Selected to active
- 先选择高精模,再加选低精模,点击bake
- 如果法线渲染出来有没覆盖好的, 调Ray distance
- 回到     shader editor, 添加normal map,把image的color连接到normal     map的color, then link normal map’s normal node to     principled BSDF’s normal node
- 如果要添加表面凹凸, 添加一个Displace modifier, Texture选择到刚才渲染好的贴图

 

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

点倒角：ctrl+shift+b

 

 

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

布尔: 安插件 then ctrl+shift+b or ctrl + 小键盘 -

hide : h / alt+h

把物体中心点归到物体中心: 右键 origin to geometry

坐标归零: alt+g

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

