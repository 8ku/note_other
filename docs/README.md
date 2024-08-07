# Notes Other

因为原主题全文搜索不好用, 更换为docsify.

[插件地址](https://docsify.js.org/#/awesome?id=plugins)

## 一些额外的语法

### 强调内容 `!> content`

!> important contents

### 普通提示 `?> normal content`

?> normal content



## 代码高亮指定语言支持

[添加对应的语法js到index.html](https://cdn.jsdelivr.net/npm/prismjs@1/components/)

## 安装方法

[官方文档](https://docsify.js.org/#/zh-cn/quickstart) 

全局安装

```bash
npm i docsify-cli -g
```

初始化

```bash
docsify init ./docs
```

本地预览

```bash
docsify serve docs
```



### 主题

[参考](https://angry-swanson-b4e47b.netlify.app/themes)

```html
<link rel="stylesheet" href="//unpkg.com/docsify/themes/vue.css">
<link rel="stylesheet" href="//unpkg.com/docsify/themes/buble.css">
<link rel="stylesheet" href="//unpkg.com/docsify/themes/dark.css">
<link rel="stylesheet" href="//unpkg.com/docsify/themes/pure.css">
```

### 添加自己的css

```html
<!-- index head 里添加 -->
<!-- Custom theme stylesheet -->
<link rel="stylesheet" href="theme-custom.css">
```

新建`theme-custom.css`

```css
:root {
  --base-font-size: 14px;
  /*--theme-color   : purple;*/
}


.highlight {
    box-shadow:inset 0 -10px 0 #ffff006e, 0 2px 0 #ffff006e;
    font-weight:bold;
}

.wavy {
    text-decoration: underline wavy red;
}
```



### mac安装时的权限问题

[参考](https://stackoverflow.com/questions/48910876/error-eacces-permission-denied-access-usr-local-lib-node-modules)

查看所有者

```bash
ls -la /usr/local/lib/node_modules
```

查看当前用户名称

```bash
whoami
```

把目录owner改为当前用户

```bash
sudo chown -R [owner]:[owner] /usr/local/lib/node_modules
```

or

```bash
sudo chown -R ownerName: /usr/local/lib/node_modules
```

