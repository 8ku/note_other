| 功能                           | 键                                                           |
| ------------------------------ | ------------------------------------------------------------ |
| 在当前目录下新建文件           | cd .>a.文件类型                                              |
| 刷新DNS                        | cmd   ipconfig /flushdns                                     |
| 强制关闭程序                   | - 任务管理器-详细信息：找到程序的PID<br />- cmd - `tskill PID` |
| 查看本机ip                     | `curl ipinfo.io` <br />`ipconfig/all`<br />或者使用在线网站  |
| 查看特殊字符表                 | `charmap`                                                    |
| 在当前文件夹下打开git bash     | shift+F10                                                    |
| 查看端口占用情况（以1080为例） | netstat -ano\|findstr “1080”<br />最后一个数字是软件PID      |
| 用PID查看程度名称              | tasklist\|findstr "9088"                                     |
| chrome截长图                   | F12-->Ctrl+Shift+P --> full -->回车                          |
| firefox截长图                  | 地址栏右侧 “。。。” 下拉菜单中选择截图                       |

### 经常失去意识的程序PID

- outllook：4144



## 生成目录树结构文件

`tree /f > list.txt`

## 图片批量压缩工具

https://pngquant.org/