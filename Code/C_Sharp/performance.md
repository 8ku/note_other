## Awake & Start

Awake在MonoBehavior创建后就立刻调用，Start将在MonoBehavior创建后在该帧Update之前，在该 Monobehavior.enabled == true 的情况下执行。

我们尽量将其他 Object 的r eference 设置等事情放在 Awake 处理。然后将这些 reference 的 Object 的赋值设置放在 Start() 中来完成。

## 动画播放的性能

- 尽量用 prefab ，尽量少用图片模拟简单动画，例如转向
- 某些只播放一次的动画，例如爆炸或出生特效，放在角色下面成为子物体，调用次数会少













![img](performance.assets/monobehaviour_flowchart.svg)