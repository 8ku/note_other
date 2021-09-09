# Gitbook

## 坑

### 安装插件报错

**问题**：用`gitbook build`的时候报错插件没安装

**解决方法**：用 `npm` 命令单独安装插件

```bash
Error: Couldn't locate plugins "search-plus-pro", Run 'gitbook install' to install plugins from registry.

npm install gitbook-plugin-search-pro

npm install gitbook-plugin-intopic-toc
```

### 用gitbook-cli安装gitbook报错

- 安装gitbook-cli `npm install -g gitbook-cli`
- 安装gitbook `gitbook -V`，会自动安装
  - 报错`if (cb) cb.apply(this, arguments)`
- 打开出错的文件，注释掉一下62-64三行

```js
52 fs.lchmod = chmodFix(fs. Lchmod)
53
54 fs. chownsync 二 chownFixSync( fs. chownsync)
55 fs. fchownsync 二 chownFixSync(fs. fchownsync)
56 fs. 1chownSync = chownFixSync(fs. 1chownsync)
57
58 fs. chmodsync = chmodFixSync( fs. chmodsync)
59 fs. fchmodsync 二 chmodFixsync(fs. fchmodsync)
60 fs. Lchmodsync = chmodFixSync(fs. Lchmodsync)
61
62 //fs.stat = statFix(fs. stat)
63 //fs. fstat = statFix(fs. fstat)
64 //fs.lstat = statFix(fs.lstat)
65
```

- 再次`gitbook -V` 安装 gitbook





## 自定义css

- 更改`book.json`文件，把css指向自定义css文件，注意`styles`段

```json
{
  "styles":{
      "website":"./websiteStyle.css"
  },
  "plugins": [
   "-fontsettings",
   "-lunr", "-search", "search-pro",	
    "intopic-toc"
  ],
  "pluginsConfig": {
    "intopic-toc": {
      "selector": ".markdown-section h2,.markdown-section h3",
      "visible": true,
      "label": {
        "en": "In this article"
      }
    }
  }
}
```

- 在根目录下创建`websiteStyle.css`



### 导出不同版本

```bash
gitbook pdf
gitbook epub
gitbook mobi
```



## 自动生成summary

### [安装](https://github.com/julianxhokaxhiu/gitbook-plugin-summary)

- `book.json`里加入

- ```json
  {
    "plugins": [
      "summary"
    ]
  }
  ```

- `npm install gitbook-plugin-summary`

- 在根目录建文件夹，每个层级添加一个`readme.md`文件，md文件以文件夹名字为一级标题

- `gitbook serve` 看效果

### 优劣势

- 优势
  - 生成epub时自带层级目录
- 劣势
  - 有bug，经常无法生成层级，都是平层
  - 每级文件夹都要加readme文件，很冗余
  - readme文件的一级标题必须和文件夹名一致，不然无法生成层级目录，对操作要求高



## 离线html可点击

在生成的`_book - gitbook - theme.js`中搜索` if(m)for(n.handler&&`，把 `if(m)`改为 `if(false)`



## 使用行内HTML CSS样式

### 上下横线

```html
<div style="border-style:solid;border-width:2px 0px;border-color:powderblue:padding:10px;margin-bottom:10px;">
your text
</div>
```

<span style="border-style:solid;border-width:2px 0px;border-color:powderblue:padding:10px;margin-bottom:10px;">
效果
</span>



[可直接使用名称的颜色参考](https://www.w3schools.com/colors/colors_names.asp)

### div 半透明背景色

```html
<div style=
    "background:rgba(0,0,0,0.05);
     padding:10px;
     color:red;">
  ddd
</div>
```

<span style=
    "background:rgba(0,0,0,0.05);
     padding:10px;
     color:red;">
  效果
</span>



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



### 高亮另一种效果

```html
<span style="box-shadow:inset 0 -10px 0 yellow, 0 2px 0 yellow;font-weight:bold;"></span>
```

<span style="box-shadow:inset 0 -10px 0 yellow, 0 2px 0 yellow;font-weight:bold;">效果</span>



### 涂黑效果

```html
<a style="color:black;background-color:black"
   onMouseOver="this.style.color='#fff';this.style.backgroundColor='#000'"
   onMouseOut="this.style.color='#000';this.style.backgroundColor='#000'" >Text</a>
```

<a style="color:black;background-color:black"
   onMouseOver="this.style.color='#fff';this.style.backgroundColor='#000'"
   onMouseOut="this.style.color='#000';this.style.backgroundColor='#000'" >效果</a>

### Markdown字体颜色大小设置

```markdown
<font color=red size=5>your text</font>
```



