# Gitbook

## 使用行内HTML CSS样式

### 上下横线

```html
<div style="border-style:solid;border-width:2px 0px;border-color:powderblue:padding:10px;margin-bottom:10px;">
your text
</div>
```

[可直接使用名称的颜色参考](https://www.w3schools.com/colors/colors_names.asp)

### 有序/无序/缩进列表

```html
有序列表
<ol>
  <li></li>
</ol>
无序列表
<ul>
  <li></li>
</ul>
缩进列表
<dl>
  <dt></dt>
  <dd></dd>
</dl>
```



### div position

```html
页面滚动时悬浮在最顶部
<style>
div.sticky {
  position: -webkit-sticky;
  position: sticky;
  top: 0;
  padding: 5px;
  background-color: #cae8ca;
  border: 2px solid #4CAF50;
</style>
```



### 段落高亮-设置在文字上

```html
<p style="background-color:red;">
  your text
</p>
```



### 行内高亮

```html
your <span style="background-color:red;">text</span>
```



### Markdown字体颜色大小设置

```markdown
<font color=red size=5>your text</font>
```



