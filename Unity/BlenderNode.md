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
## Animation Node

下载安装插件 [Animation Node](https://animation-nodes.com/)

- **半透明节点表示 输入/输出 为list

### 快捷键

- 调出node input output面板: u

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