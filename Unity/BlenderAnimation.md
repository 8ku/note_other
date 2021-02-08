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
# Blender Node

* TOC
{: toc}
## 工作流程

### Blender 中的k帧流程

- 分屏到 Dope Sheet , 模式选择 Action Editor
- 新建一个动作, 命名, 保存
- 在Pose模式下摆第一帧姿势(使用动画参考图 : 新建一个图像空对象, 载入参考图)
- 摆好姿势后, 全选骨骼, i-Rotation and Location(**最好全程只用IK或FK一种方式k帧, 不然动作会乱**)
- 把时间轴里的Keying-Active Keyting Set 更改为 Rotation and Location(方便观察)
- 全选所有关键帧, cmd+c, 移到13帧(教程参考, 整个行走动画一共13帧), shift+cmd+v 粘贴翻转动作
- 移到第7帧(中间帧), 摆好中间动作, 再 4,10 微调中间动作
- a 全选所有帧(**把光标放到Summary上 a 全部, 记得在两个地方按 a **), cmd+c全选
- 放到最后一帧, shift+cmd+v
- 导出fbx, 勾选 Apply transform, 勾选 Bake Animation
- 导入Unity, 把Model Rig Animation分开导
  - Model: 去掉 Import Cameras Import Lights , apply
  - Rig: animation type 选择 generic , apply
    - 如果要使用Avatar(如果需要在Unity里调整骨骼动画需要使用这个)
      - [安装插件 RigifyToUnity](https://github.com/AlexLemminG/Rigify-To-Unity)
      - 在Blender-中选择`rig`图层, 在 跳舞小人-Rigify to Unity converter , 点击`Prepare rig for Unity`
      - 选择模型和rig, 导出fbx(导出到Unity的Assets中的话Unity会自动读取)
      - Transform - Apply Scallings - FBX Units Scale
      - 勾选  Armature - Only Deform Bones
      - 进入Unity, Rig - Animation Type 选择 Humanoid
      - 即可使用Avatar
    - 在Unity中新建一个Animator Controller, 打开
      - 把动画片段直接拖入Animator窗口
    - 选中导入的对象, 把上一步的Animator Controller拖入 Animator - Controller
  - Animation: 勾选 loop time 和 loop pose, apply
    - 如果有多个动画, 需要一个个勾选 loop time, apply
    - [可以使用这个脚本自动处理](https://www.youtube.com/watch?v=vrN9duEoA6g)
      - 加载后, 菜单栏多一个菜单 Imphenzia , 点击下拉把菜单放到屏幕上
      - 点击导入的物体包, BulkAnimClipSettings菜单会自动寻找动画片段并显示出来
      - 选择所有的Clip Name , Change Animation Settings

### 创建多个动画

- Dope Sheet - 切换到 Action Editor
- 右侧 新建动作
- 全选所有关键帧和Summary里的标签 x 清空
- pose mode 把人物动作复原



## K帧快捷键

- 插入帧: i
- 批量删除帧: 全选帧, 在顶部 summary 行的光标帧, cmd+ left click 会取消选择当前列之前的所有列, 再x
- 缩放关键帧: 全选 s



## 基本动作时长

**动画最后一帧应该和第一帧一样, 所以clip的长度应该为 1~(last - 1)**

| Move Name    | Frames      | Demo       |
| ------------ | ----------- | ---------- |
| Idle         | 30~40       |            |
| Run          | 18 or fewer |            |
| Walk         | 24 or fewer |            |
| Sneak        | 24 or fewer |            |
| React        | 15 or fewer | 发觉       |
| Death        | 15 or fewer |            |
| Knock down   | 12 or fewer | 被打中     |
| Get up       | 30 or fewer | 从地上起来 |
| Attack-Aim   | 10 or fewer | 攻击别人   |
| Attack-Shoot | 14 or fewer |            |
| Attack-Bite  | 14 or fewer |            |
| Attack-Punch | 14 or fewer |            |
| Attack-Kick  | 14 or fewer |            |



## 坑

### 移动Torso不能下蹲

检查两边Foot的 `IK-FK`是不是1, 需要调整到0