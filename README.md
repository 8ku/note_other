# note_other
### 介绍

书籍以外的各种笔记



### 规则

- 以学科为文件夹名
- 只存储markdown格式笔记
- 可使用working copy pull and push 笔记
- 不要在移动端新增读书笔记，因为要生成gitbook格式

### Tips

- 让 github page 显示数字公式的方法：
  1. 应用系统主题，从[系统主题库](https://pages.github.com/themes/)中拷贝 defalt.html 文件到自己的仓库下，路径为 `/_layouts/default.html`(自己仓库也需要建立同样的 _layouts 路径，不然无法读取)
  
  2. 打开 `defaoult.html`，在 `head` 中添加 `<script type="text/javascript"src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>`
  
  3. 在 `_config.yml` 中添加一行 `markdown: kramdown` ，把默认的markdown渲染方式改为kramdown
  
  4. 更换主题时，需要把 `default.html`文件全部再复制粘贴一次，不然新主题显示会有问题
  
  5. 以上方法失效时，在每个markdown文档头部增加js:
  
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

