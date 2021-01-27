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
# Blender Physics

* TOC
{: toc}
## 流体动画

- 新建一个立方体(球体等)做为液体发射器
  - 在`Physics properties`中添加`Fluid`
  - Type: flow
  - setting: 
    - flow type: liquid
    - Flow Behavior: inflow
    - 勾选 Use Flow
    - 勾选 Initial Velocity
      - Initial X/Y/Z 根据要发射液体的方向设置速度
- 选中立方体, 左上角 `Object - Quick Effect - Quick Liquid` 创建流体运动空间
  - Domian Type : Liquid
  - Resolution Division: 80或以上 (如果渲染没效果就向上增加值, 这是是空间边缘和作用域的距离, 数字越大, 边界和作用域间距越小(渲染时消耗资源越多))
  - 勾选 Diffusion
  - 勾选 Mesh
  - 勾选 Is Resumable
  - Type: Modular(为添加空间中其他碰撞体用)
- 新建一个管道, 或平面
  - 在`Physics properties`中添加`Fluid`
  - Type: Effector
  - Effector Type: Collision
  - 勾选 Is Planar
- 回到运动空间
  - 在setting下点击Bake Data查看效果
    - 如果无效果, 把 resolution Division数字加大
  - Bake Mesh, 如果不Bake, 空间会不透明
- 导出为 `.abc`

