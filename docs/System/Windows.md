## 命令



| 功能                           | 键                                                           |
| ------------------------------ | ------------------------------------------------------------ |
| 在当前目录下新建文件           | `copy nul emptyfile.txt`<br />`type nul > emptyfile.txt`     |
| 刷新DNS                        | cmd   ipconfig /flushdns                                     |
| 强制关闭程序                   | - 任务管理器-详细信息：找到程序的PID<br />- cmd - `tskill PID` |
| 查看本机ip                     | `curl ipinfo.io` <br />`ipconfig/all`<br />或者使用在线网站  |
| 查看特殊字符表                 | `charmap`                                                    |
| 在当前文件夹下打开git bash     | shift+F10                                                    |
| 查看端口占用情况（以1080为例） | netstat -ano\|findstr “1080”<br />最后一个数字是软件PID      |
| 用PID查看程度名称              | tasklist\|findstr "9088"                                     |
| chrome截长图                   | F12-->Ctrl+Shift+P --> full -->回车                          |
| firefox截长图                  | 地址栏右侧 “。。。” 下拉菜单中选择截图                       |



### 文件操作

| 功能                          | 键                                                           |
| ----------------------------- | ------------------------------------------------------------ |
| 打开命令行界面                | win+r                                                        |
| 在当前目录下递归查找文件      | dir /S filename<br />Dir: 查看文件<br />/S: 显示指定目录和所有子目录的文件 |
| 切换盘符                      | cd /d d:                                                     |
| 模糊匹配                      | dir /S filename*                                             |
| 查看当前位置的文件/文件夹列表 | dir /b<br />dir *                                            |
| 打开文件                      | start filename                                               |
| 打开文件夹                    | start foldername                                             |
| 打开当前路径                  | start .                                                      |
| 运行 exe 文件                 | xxx.exe                                                      |







### 经常失去意识的程序PID

- outllook：4144



### CMD使用代理

把代理设置到系统环境中

1. 打开 `此电脑 - 属性 - 高级系统设置 - 环境变量 - 系统变量`
2. 新增两个系统变量
   1. `http_proxy` : `socks5://127.0.0.1:xxxx`
   2. `https_proxy` : `socks5://127.0.0.1:xxxx`
3. 在cmd中使用 `curl www.google.com` 测试，如果结果有内容，说明OK



## 生成目录树结构文件

`tree /f > list.txt`

## 图片批量压缩工具

https://pngquant.org/



