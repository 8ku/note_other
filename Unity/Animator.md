# 动画控制

## 创建人物动画

- 在人物角色下创建 Animator 组件
  - 或者 直接创建一个 Animation ，拖到角色下，会自动生成一个 Animator 
- 在 Assets 下创建 Animation - Player 文件夹，在文件夹中创建 Animator Controller 
- 把新建的 Controller 拖到人物角色下的 Controller 下绑定
- window - Animation ( cmd + 6 ) 调出动画窗口，创建新动画
- 把分割好的动画图片一次性拖到时间轴上，点击最左和最右两个 keyframe 拖拽可以平均拉长（先把图片的Pixel Per Unit 调整到16 ）
- 在 window - Animator 中把 idle 和 run 做连接
  - 点击箭头，从 idle 到 run：先在animator 视窗里增加一个变量（例如 running ），再在 inspector - Conditions 中调用 running ，“当 running greater than 0.1, then change state”
  - **animator里的变量命名规范最好统一**
  - 如果需要状态马上变化，把 Has Exit Time 去勾，Transition Duration 设置为 0 
  - 另一个设置为 when running is less than 0.1, then change state.
  - 在角色的控制脚本中声明 animator，绑定控制器

## 动作

- **IDLE：待命状态**
  - defalt 状态，静止状态，可以做呼吸动画
- **walk**
- **run**

## 骨骼绑定

- 方式
  - 使用assets的模型改造
  - 从3D建模软件中导入，支持`.fbx` 文件，因为模型导入可能被重构，最好的方法是在3D软件中制作好部件，导入U3D中拼接
  - Animation Rigging 技术
  - 注意比例：Unity3D中默认 1单位距离 = 1米。
- **导入模型的技术要求：**
  - 法线要正确：Unity3D中不可以修改多边形法线方向，所以如果错了就必须返回Maya进行修改再重新导入；
  - 比例要正确：如果按照Maya默认1单位=1厘米，那么1米高的物体在Maya中就应该高100个单位，同时导入时`Scale Factor`设置为0.01；
  - Pivot Point要提前设置好；
  - 位移归零位置要在坐标原点（但初始位置不一定要在原点）；
  - 不能有构造历史（导出FBX的时候会自动统一清空构造历史，所以不要有任何依赖于构造历史的修改变化）；
  - UV都放在(0,1)象限内，且保持UV正向（Maya中显示为蓝色为正向）；
  - 单一mesh的UV不要有重叠；
  - 只使用smooth bind进行绑定；
  - 动画必须全部由动画曲线关键帧控制；
  - 骨骼命名最好提前做好。
  - 关键词：3d 动画绑定 unity   [参考](https://www.jianshu.com/p/e2aa4d898fb7)
- 插件
  - 2D
    - `2D Animation  `  `2D PSD Importer`  安装后可导入<u>PSB</u>文件
    - 第3方插件 `puppet 2D`
  - 3D
    - 第3方插件 `puppet 3D`

## 绘制2D 地图

-  新建 2D Project - Tilemap
- Windows - 2D - Tile Patette
- 把地图元素用 Sprite Editor 切好
- 在 Tile Patette 中新建 palette ，把切好的元素拖入，点击保存

## 创建动画的快捷方法

在素材中直接把切好的图拖入 Hierarchy