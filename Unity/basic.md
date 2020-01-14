# 基本概念

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



