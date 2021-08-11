# Notes Other

因为原主题全文搜索不好用, 更换为docsify.

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

