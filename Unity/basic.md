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

