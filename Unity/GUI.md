# GUI

## FairyGUI 和 UGUI 的区别

- FairyGUI 把 GUI 编辑分离出来，用发布的方式更新界面设计，在团队合作里提高效率
- UGUI 内置于 Unity 中

## UI 界面按钮注册

把 GameManager 拖入对应的按钮中（例如 “继续游戏”） On Click 中，选择相应方法

## UI 设置技巧

### 获取 UI 宽高最安全的方式

使用 Inspector 面板右侧的 Debug 模式可以看到更多属性

```c#
//此方法不用考虑锚点有位置变化，都可正确获得 UI 宽高
RectTransform rect = transform.GetComponent<RectTransform>();
rect.rect.width;
```

###  Canvas 的三种渲染模式

- Screen Space - Overlay：在当前屏幕置顶
- Screen Space - camera：在当前屏幕摄像机前，可调整 UI 和相机的距离来实现 UI 和场景中物体在相机中的前后顺序
- World Space：变成一个可以移动的 3D 图层

### UI 单位和像素的关系

默认是100 px = 1unit = 1m，可以调整图片和 unit 的比例达到放大场景中对象的效果

### UI适配屏幕比例

在 Canvas 上添加脚本

```c#
void Start()
    {
        float wSale = Screen.width / 1920.0f; //要用浮点型，1920为设计时所用的屏幕宽度
        float hScale = Screen.height / 1080.0f;

        GetComponent<CanvasScaler>().scaleFactor = wSale;
    }
```

### GraphicRaycaster 图片的点击检测

Canvas 下的 GraphicRaycaster 组件

- Blocking Objects ：检测的是物体身上挂的 collider 的类型，不是根据游戏物体的类型

### Canvas group

在 Canvas / Canvas 下的元素中 添加，可以对 Canvas 下的素材进行集体操作