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
# Blender 2 Unity

* TOC
  {: toc}
  
  ## 物理动画到Untiy

无法把高级材质(如透明等)带过来

- 在blender中录制动画
- 保存文件为 .abc
- 在Unity中装载插件 `Alembic`
- 把`.abc`文件拖入Assets, 调整Scale Factor - Apply
- 把包文件(不是单个物体文件)放到场景中, 新建Timeline
- 把包文件拖入时间轴, 选择 `Add Clip With Alembic Track`

## 普通模型到Unity

- 保存文件为`.fbx`
  - **如果有材质, 要把 `Path Mode` 改为 Copy**, 不然材质导不出来
- 在Unity中直接导入
- 导入时在模型的`Materials`中更改`Location-Use External Materials`, 这样在Unity中也可编辑模型材质



## Blender - Mixamo - Unity

- save model as **xxx.FBX**

- Import to Mixamo

- Download model as **FBX for Unity(.Fbx)**, e.g *player.fbx*

- Select a pose, Download as **FBX for Unity(.Fbx)**, **Without Skin**

- Drag model(Download from Mixamo, e.g *player.fbx*) into Unity
  
  - Import Settings
    
    - Animation Type: **Humanoid**
    
    - Avatar Definition: **Create From This Model**

- Drag model with animation(e.g *running.fbx*) into Unity
  
  - Import Settings
    
    - Animation Type: **Humanoid**
    
    - Avatar Definition: **Copy From Other Avatar**
