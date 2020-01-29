# note_other
书籍以外的各种笔记

## 目录

- Bolt
  - [bolt](https://8ku.github.io/note_other/bolt/bolt)
  - [Unit_note ](https://8ku.github.io/note_other/bolt/Unit_note)

- Code

  - Python
    - [Python](https://8ku.github.io/note_other/Python/Python)
    - [pandas](https://8ku.github.io/note_other/Python/pandas)
  - C_Sharp
    - [C_Sharp](https://8ku.github.io/note_other/C_Sharp/C_Sharp)
    - [Unity_C_Sharp](https://8ku.github.io/note_other/C_Sharp/Unity_C_Sharp)
  - Unity

    - [Prefab](https://8ku.github.io/note_other/Unity/Prefab)
    - [Animator](https://8ku.github.io/note_other/Unity/Animator)
    - [Shortcuts](https://8ku.github.io/note_other/Unity/Shortcuts)
    - [basic](https://8ku.github.io/note_other/Unity/basic)
    - [Physice](https://8ku.github.io/note_other/Unity/Physics)
    - [GUI](https://8ku.github.io/note_other/Unity/GUI)
    - [Package](https://8ku.github.io/note_other/Unity/Package)

- math

  - [markdown里打数学公式的方法](https://8ku.github.io/note_other/math/markdown里打数学公式的方法 )
  - [贝叶斯推断](https://8ku.github.io/note_other/math/贝叶斯推断)
  - [数学符号表](https://8ku.github.io/note_other/math/数学符号表)
  - [机器学习](https://8ku.github.io/note_other/math/机器学习)
  - [物理学](https://8ku.github.io/note_other/math/物理学)

- RegularExpression

  - [正则表达式](https://8ku.github.io/note_other/RegularExpression/正则表达式 )

- system

  - [Linux](https://8ku.github.io/note_other/system/Linux)
  - [Mac](https://8ku.github.io/note_other/system/Mac)
  - [Windows](https://8ku.github.io/note_other/system/Windows)
  - [markdown_flow](https://8ku.github.io/note_other/system/markdown_flow)

- WomensHistory

  - [女权运动时间轴](https://8ku.github.io/note_other/WomensHistory/feminism_timeline.html)
  - [全球性别差异化报告](https://8ku.github.io/note_other/WomensHistory/GlobalGenderGap)
  
- Mythology

  - [AncientGreece](https://8ku.github.io/note_other/mythology/AncientGreece/ancientgreece)
  - [Nordic](https://8ku.github.io/note_other/mythology/Nordic/nordic)

- GameHistory

### 规则

- 以学科为文件夹名
- 只存储markdown格式笔记
- 可使用working copy pull and push 笔记
- 不要在移动端新增读书笔记，因为要生成gitbook格式

### Tips

- 让github page显示数字公式的方法：
  1. 应用系统主题，从[系统主题库](https://pages.github.com/themes/)中拷贝 defalt.html 文件到自己的仓库下，路径为 `/_layouts/default.html`(自己仓库也需要建立同样的 _layouts 路径，不然无法读取)
  
  2. 打开 `defaoult.html`，在 `head` 中添加 `<script type="text/javascript"src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>`
  
  3. 在 `_config.yml` 中添加一行 `markdown: kramdown` ，把默认的markdown渲染方式改为kramdown
  
  4. 更换主题时，需要把 `default.html`文件全部再复制粘贴一次，不然新主题显示会有问题
  
  5. **以上方法失效时，在每个markdown文档头部增加js:
  
     ```html
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
     </head>
     ```
  
- 在markdown中画流程图的方法
  
  - https://support.typora.io/Draw-Diagrams-With-Markdown/
- 在markdown中画图表的方法
  
  - https://tianqi.name/jekyll-TeXt-theme/docs/en/markdown-enhancements

