## Awake & Start

Awake在MonoBehavior创建后就立刻调用，Start将在MonoBehavior创建后在该帧Update之前，在该 Monobehavior.enabled == true 的情况下执行。

我们尽量将其他 Object 的r eference 设置等事情放在 Awake 处理。然后将这些 reference 的 Object 的赋值设置放在 Start() 中来完成。

## 动画播放的性能

- 尽量用 prefab ，尽量少用图片模拟简单动画，例如转向
- 某些只播放一次的动画，例如爆炸或出生特效，放在角色下面成为子物体，调用次数会少

## FindObject的性能

- GameObject.Find()
  - 通过名称, 如果物品active是false的话,找不到
  - 使用递归方法,非常耗性能,尽量少用,不要在Update里用
- Transform.Find()
  - 先用GameObject.Find找到父对象, 再用transform.Find找子对象
  - 可以查找隐藏对象, 必须保证顶级父对象active是true
  - 找孙对象 `father.transform.Find(“son/grandson”).gameObject;`
- GameObject.FindObjectOfType
  - 按物体身上挂载的组件找, 同样用递归, 效率不高

## 类的性能

先判断是需要挂在物体上的组件,还是普通类.

如果是和组件无关,不要继承 MonoBehaviour ,保持纯粹性, 减少性能消耗

如果属于组件,必须继承MonoBehaviour

## Update FixedUpdate LateUpdate

- 处理Rigidbody时需要用FixedUpdate代替Update,因为机器性能不同,会影响帧处理速度,用于FixedUpdate强制固定帧速率,保证动画速度一致
- FixedUpdate的时间间隔可以在 Edit > ProjectSetting > time > Fixedtimestep 中修改
- LateUpdate晚于Update调用,可用于控制同一物体身上的不同脚本,挂载LateUpdate的脚本晚于Update脚本执行,如果两个脚本中都有动画,在其中一个脚本使用LateUpdate可以防止动画在同一时间执行导致的抖动











![img](performance.assets/monobehaviour_flowchart.svg)