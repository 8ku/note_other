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
## Themes

### 改变节点连接线的曲度

- Edit -Preferences-Themes-Node Editor-Noodle Curving
- 默认为0(直线), 增加节点即增加曲度

## Animation Node

下载安装插件 [Animation Node](https://animation-nodes.com/)

- **半透明节点表示 输入/输出 为list

### 快捷键

- 调出node input output面板: u

- 自动连接两个node: 选中要连接的node, f

- 右侧菜单: n

- 左侧菜单: t

- 节点打组: ctrl/cmd+g

- 进入/退出组编辑: tab

- debug: 在output添加 `viewer`节点

- 切断连线: ctrl/cmd+right click

- 组织nodes: 添加`frame`节点

- 添加连线中点(把一对多的节点打结): shift+right click

  ![iShot2021-01-15 18.29.57](BlenderNode.assets/iShot2021-01-15%2018.29.57.jpg)

- 

### 技巧

- 节点打组后, 把需要调整的参数连接到`group  input`可以在组外调整

- 记住初始transforms

  - 右侧菜单 - AN - `initial transforms - from current transforms`
  - 在`animation nodes`中添加`object id key`, 选择object, 选择`initial transforms`

- 创建实例并应用modifier

  - `object instancer`
  - 勾选`copy full object`

- 创建矩阵

  - 创建实例 `object instancer`
  - `matrix - distribute matrice`
    - 查看矩阵分布形态, 添加 `3d viewer`
  - 添加`get list length`得到 matrices的数量
  - 把length连接到 `object instancer`上

  ![iShot2021-01-15 23.31.18(1)](BlenderNode.assets/iShot2021-01-15%2023.31.18(1).jpg)
  - 添加`offset vector` 和 `random falloff` 添加random

    ![iShot2021-01-15 23.56.26(1)](BlenderNode.assets/iShot2021-01-15%2023.56.26(1).jpg)

## Shader Node

### fake volumetirc light 假体积光

- 创建一个平面, 命名为 EV
- 创建一个空坐标对象, 命名为 G1_Control, 用于调节灯光照射距离
- 创建另一个空球形对象, 命名为 G2_Control, 用于调研灯光直径
- 在EV中添加节点`emission` `Gradient Texture` `ColorRamp`
- 在`Gradient Texture`上 Ctrl+t  添加 Mapping 和 Texture Coordinate(需要提前安装 Node Wrangler 插件 )
- 把 Texture Coordinate, Mapping, Gradient Texture, ColorRamp打组(cmd+g), 命名为 H_V_Control
  - 进入H_V_Control, 把`Texture Coordinate`和`Mapping`的连接改为使用`Object`, Object 选择G1_control
  - ColorRamp 类型选为 B-Spine
- 复制一个H_V_Control, 重命名为 V_V_Control
  - 进入V_V_Control, Object 选择G2_control
  - Gradient Texture 选择Vector
  - ColorRamp 按辐射的方式调整(中间纯白, 两边纯黑)
- 把H_V_Control和V_V_Control用Mix RGB连接, 命名为 Control Mix RGB
- Control Mix RGB 连接到Emission
- 添加一个Transparent BSDF和一个Mix Shader
- 把Transparent BSDF和Emission连接到Mix Shader
- 把G1_control和G2_control作为FV的子对象
- 添加Noise Texture, ctrl+t添加Mapping和Texture Coordinate
- 添加一个空立方体对象, 命名为Noise Control, 添加到Noise的 Texture Object里, 控制Noise的移动
- 复制一个Mix RGB, 把Noise Texture和Control Mix RGB连上去, 输出连接到Mix Shader的Fac里
- 设置摄像机
- 因为FV是2D的, 光也是2D, 需要让2D的面一直面向摄像机伪装成3D, 在EV的Object Constraint Properties里添加`Locked Track`, Target选择Camera, Track Axis 选择-Z, Locked Axis选择Y
- 设置Noise动画
  - 选择Noise Control, Location Z添加key
  - 20帧, Z移动到30m, 再点击key
  - 切换时间轴到Graph editor: ctrl+tab
  - 选择Z Location, 全选所有帧, 按 t 选择平滑度为线性
  - 添加Modifiers-Cycles, After选择Repeat with Offset

![Snipaste_2021-01-23_23-32-14(1)](BlenderNode.assets/Snipaste_2021-01-23_23-32-14(1).jpg)