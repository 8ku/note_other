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
# Unity Shader

* TOC
{: toc}
在Unity中使用node创建和编辑着色器.

## 安装配置

- 安装`Shadergraph` 和 `Universal RP` 包
- `Edit > Render Pipeline > Universal Render Pipeline > Upgrade ...` 更新原来的Unity自带Shader(如果切换后材质变红)
- 创建设置SRP : 菜单栏`Assets > Create > Rendering>Universal Pipeline Asset`，会创建出来一个文件，这是渲染管线的配置文件。
- 在菜单栏 `Edit > Project Settings > Graphics` 中设置刚才的SRP文件
- 创建ShaderGraph文件: `Create > Shader > PBR / Sub / Unlit Graph`
  - *PBR Graph* PBR图
  - *Sub Graph* 子图，用于创建一些可复用的节点
  - *Unlit Graph* 不受光照的图
- 双击打开Shader Graph 窗口

## 使用摄像机特效

### 建立依赖

- 在 Hierarchy 新建一个 Volume --> Global Volume, 置于最顶层

  - 新建一个Profile
  - 模式选择Global的话会针对所有物体有效

- 在MainCamera - Renderer 

  - 勾选 Post Processing

- <p style="background-color:red;">
     Global Volume的 Layer 必须包含在 Main Camera - Environment - Volume Mask 层中, 不然无法生效
  </p>



### 相机景深

- 在Global Volume中添加 Depth Of Field
- Mode: Gaussian(快, 资源消耗少) / Bokeh(慢, 真实, 资源消耗多)



### 相机暗角

添加 Vigentte

### 颗粒感

添加 Film Grain ( 杂色是动态的, 效果不是很好)



## 设置调整

### 阴影清晰度优化

- 打开UniversalRenderPipelineAsset
- 找到`Shadows`, 调整`Cascades`为更高
- `Lightning - Shadow Resolution` 调整为更高
- 调整`Shadows` 的 `Deptch Bias` 和 `Normal Bias`



## 特效渲染节点

### 玻璃

![Glass_shade_node](UnityShader.assets/Glass_shade_node.jpg)

其中的`Custom Function`

```
Input
Normal Vector3
ViewDir Vector3
IndewofRef Vector1

Outputs
Out Vector3

Type: String
Name: Refraction
Body:
Out = refract(ViewDir, Normal, IndexofRef);
```

[教程](https://www.codinblack.com/glass-shader-using-shader-graph-in-unity3d/)



### 卡通配色

- 新建一个Unlit Shader

- 新建一个文件夹 Includes, 新建`Lighting.hlsl`文件, (mac)下用sublime打开(添加 `HLSL Syntax`插件)

  ```hlsl 
  #ifndef CUSTOM_LIGHTING_INCLUDED
  #define CUSTOM_LIGHTING_INCLUDED
  
  // CalculateMainLight是方法名 float是告诉Unity用的是什么类型的值
  void CalculateMainLight_float(float3 WorldPos, out float3 Direction, out float3 Color){
  #if SHADERGRAPH_PREVIEW
  	Direction = float3(0.5, 0.5, 0);
  	Color = 1;
  #else
  	Light mainLight = getMainLight(0);
  	Direction = mainLight.direction;
  	Color = mainLight.color;
  #endif
  
  }
  #endif
  ```

- 在 Unilit Shaer 中新建一个`Custom Function`, 按上一步定义的值添加 input out value

  - Input : WorldPos - Vector3
  - output: Direction - Vector3
  - output: Color - Vector3
  - type: File
  - Name: CalculateMainLight
  - Source: Lighting.hlsl

- 添加一个`Position`(Absolute World) - `Custom Function`

- add `Normal Vector`(法线方向)  `dot product`

  <div class = "mermaid">
  graph LR
  CustomFunction & NormalVector --> dotproduct       
  </div>

  ```mermaid
  graph LR
  CustomFunction & NormalVector --> dotproduct    
  ```

  



## 贴图

### 漫贴反射图要点

- 如果不需要贴图的反射, 在贴图的Inspector中
  - Filter Mode: Point(no filter)
  - Compression: None
- 在材质Inspector中
  - Smoothness: 0
- 在导入的带rig的模型包中, 选择非rig以外所有模型子对象**(不要选rig)**, 拖入材质到 Element 0

