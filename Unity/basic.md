# 基本概念

## Unity官方文档离线版打开方式

- [从官网下载离线版文档](https://docs.unity3d.com/Manual/UnityManual.html)，左侧 Unity User Manual - Offline documentation
- 把本地保存路径复制，在浏览器打开，在最后补上 index.html

## HUD Head-Up Display

抬头显示，指在屏幕上显示游戏相关信息

## 2d tile技巧

- 设置图片 Pixels per unit 为16，sprite mode 为 mulitple ，用 sprite editor 切割好图片（如果是素材的话）
  - 在 Hierarchy 中新建 Tilemap ,点击 Tilemap，打开 window - 2d - Tile Palette ，拖入切割好的图片总体
  - 可以在 Tilemap 模式下画前景和背景
  - 给 Tilemap 加对撞机，添加 Tilemap Collider 2D，这样角色就不会漏出画面
- 设置图层：Sorting Layer 可设置多个图层，越下面排在越前面
  - Order in Layer 是相同图层内的排序 ，数字越大越前面
- 创建Player：新建一个Sprite，把贴图拖到 Sprite 中
- Player 要碰撞要添加刚体 rigidbody 和 碰撞体 Collider，地面也要添加碰撞体 tilemap collider
- Player 在空中翻转：Rigidbody 2D - Constraints - Freeze Rotation z ：打勾，冻结z轴旋转

## 镜头跟踪

使用插件 Cinemachine - Create 2D Camera - CM vcam1

- 设置 follow - player
- Dead Zone：设置镜头不会移动的区域
- Screen X/Y：设置角色偏移屏幕多远
- 处理镜头跟随出背景边界问题：
  - 在 Extensions 下选择 Cinemachine Confiner
  - 给 background 添加一个 Polygon Collider 2D 多边形对撞机
    - 勾选 Is Trigger：表示?
  - 在 CM vcam1 - Cinemachine Confiner -Bounding Shape 2D 中选择 background

## 设置游戏按键

- Edit -  Project Settings - Input - 右键复制一组按键设定

## 光效

- 2D 光效包：Lightweight RP
- 光源是3D 的，如果看不到光效，看下 Z 轴的位置

## 音效

- Audio Listener：声音接收器
- Audio Source：音源
- Audio Clips：音频片段

## transform及其他

transform 经常用于代表物体本身，脚本中直接用 transform.position 代表物体本身的位置信息

## FPS Frames Per Second

每秒传输的帧数。

处理能力 = 分辨率 * 刷新率

影响帧数的因素：

- 电脑显卡
- 显示器刷新率

游戏中一般人能接受的最低 FPS 约为 30Hz，基本流畅等级需要大于 60Hz。

游戏设计中，如果使用电脑默认的 FPS ，假设设计电脑为30Hz ( 1秒30帧 ) ，玩家电脑为60Hz ( 1秒60帧 )，则在玩家电脑上看画面会有卡顿（1秒只播放30张图片）。

为了解决这个问题，Unity 为移动速度时添加一个方法 `Time.deltaTime`，意思为下一秒的开始时间只依赖于上秒的完成时间，是一个动态值，这给动画增加了顺滑的效果。

### FixUpdate

固定帧，Unity 中的 FixUpdate 默认固定帧为 50 FPS ，即 Time.fixeddeltaTime 固定为0.02。如果游戏（玩家）电脑更新频率为 25Hz，游戏每刷新1帧要调用2次 FixUpdate ，如果玩家电脑为 100Hz ，游戏每刷新 2 帧调用 1 次 FixUpdate。

## GameManager

- 脚本名直接叫 GameManager 时，脚本的图标会变化，一个场景只能有一个 GameManager