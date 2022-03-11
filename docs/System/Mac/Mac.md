# MAC快捷键



## 基本快捷键


| 功能                                          | 键                                                           |
| --------------------------------------------- | ------------------------------------------------------------ |
| 查看                                          | ls                                                           |
| 打开文件夹                                    | open fileFolderName///                                       |
| 打开当前文件夹                                | open .                                                       |
| 查看隐藏文件                                  | shift+cmd+.(句号)                                            |
| 使用系统preview查看多张图片                   | open *                                                       |
| 查看-隐藏                                     | ls -a                                                        |
| 创建目录                                      | mkdir (make directory)                                       |
| 进入目录                                      | mkdir                                                        |
| 返回上级目录                                  | cd ..                                                        |
| 返回根目录                                    | cd /                                                         |
| 删除目录(空目录)                              | rmdir test (remove directory)                                |
| 删除非空目录(加 -rf直接删除，不出现在回收站） | rm -rf test （remove force)                                  |
| 创建文件                                      | touch 文件名                                                 |
| 拷贝                                          | cp                                                           |
| 查找                                          | find                                                         |
| 用正则查找文件                                | find.-name”*.c”-print                                        |
| 显示当前目录的路径                            | pwd (print working directory)                                |
| 复制文件路径                                  | Option+Command+C                                             |
| 列出当前目录下的所有文件                      | ls                                                           |
| 用默认程序打开文件                            | open                                                         |
| 显示操作系统信息                              | uname -a/uname                                               |
| 清除屏幕或窗口内容                            | clear                                                        |
| 显示当前所有设置过的环境变量                  | env                                                          |
| 列出当前登录过的所有用户                      | who                                                          |
| 显示当前正在操作的用户名                      | whoami                                                       |
| 显示终端或伪终端的名称                        | tty                                                          |
| 查询磁盘使用情况                              | du/du -k subdir                                              |
| 显示文件系统的总空间和可用空间                | df <br />df/tmp                                              |
| 显示当前系统活动的总信息                      | w                                                            |
| 执行.sh文件                                   | ./aa.sh                                                      |
| 刷新DNS                                       | sudo killall -HUP mDNSResponder                              |
| 连续查看图片                                  | 全选所有图片-空格                                            |
| 安装cli命令行应用                             | 输入chmod +x (拖入cli文件)                                   |
| 中断运行                                      | **control+d**                                                |
| 打开表情键盘                                  | alt+cmd+space                                                |
| 显示隐藏文件                                  | cmd+shift+.                                                  |
| 将光标后一个字删除                            | Fn+Delete                                                    |
| 批量修改文件名(方法1)                         | 选择需要修改的文件<br />在其中一个上点右键:<br />根据自己的需要修改 |
| 批量修改文件名(方法2)                         | 安装rename脚本`brew install rename`<br />使用命令`rename ’s/oldname/newname/’ *.png`<br />说明: s是关键词, 前一个参数的引号中为文件名中要替换的部分(替换前/替换后), 后一个参数中代表通配文件名的规则*<br />支持Perl通配符: 把所有文件名结尾添加后缀`rename ’s/$/.txt/’`<br />批量删除文件名 `rename ’s/.txt//’<br />正则匹配部分文件名 `rename 's/text([1-9]).txt/.txt/'` |
| 显示文件简介                                  | cmd+i                                                        |
| 显示资源库                                    | finder--> 单击菜单栏的’前往’ 按下option<br />或终端中输入`chflags nohidden ~/Library/`-显示 `chflags hidden ~/Library/`-隐藏 |
| 剪切式粘贴                                    | cmd+option+v                                                 |
| 强制退出程序                                  | cmd+option+esc                                               |
| 查看程序使用的内存                            | `top -o MEM`                                                 |
| 停止运行命令                                  | ctrl+c                                                       |
| 查看chrome cookie列表                         | `chrome://settings/siteData`                                 |
| 切换桌面                                      | ctrl+1~9                                                     |
| 用命令行查看压缩文件包里的信息                | `zipinfo xxxx.zip`<br />`unzip -l xxx.zip`                   |



## macOS 键符号查找

| 符号 | 键                       |
| :--- | :----------------------- |
| ⌘    | **命令** (**cmd**)       |
| ⌥    | **选项** (**alt**)       |
| ⇧    | **Shift**                |
| ⌃    | **控件** (**ctrl**)      |
| ⇞    | **向上翻页** (**Pg Up**) |
| ⇟    | **向下翻页** (**Pg Dn**) |
| ⌫    | **删除** (**Backspace**) |
| ⌦    | **向前删除**             |
| ⏎    | **Return**               |
| ←→↑↓ | **箭头键**               |
| ↖    | **Home**                 |
| ↘    | **End**                  |
| ␣    | **空格键**               |
| ⇥    | Tab                      |

## 软件安装问题

### 不能打开应用(没有权限打开应用)的解决方法

- 应用程序 - 右键：显示包内容 - Contents - MacOS 
- 终端：`chmod +x ‘拖入1’ ` 回车执行

### 提示已损坏/软件有危险无法打开

`sudo xattr -d com.apple.quarantine /Applications/xxxx.app`

### 闪退

`codesign --force --deep --sign - /Applications/name.app`

## 删除 office 的历史记录

清空下列两个文件中的内容

```
~/Library/Containers/com.microsoft.Word/Data/Library/Preferences/com.microsoft.Word.securebookmarks.plist
~/Library/Containers/com.microsoft.Word/Data/Library/Preferences/com.microsoft.Word.plist
```

### Excel

- 编辑单元格: ctrl + u 

## office更新速度很慢问题

- dns 保留 114.114.114.114
- 挂vpn, 在自定义规则中添加 `akamaized.net` `azurewebsites.net`
- 清理dns缓存 `sudo killall -HUP mDNSResponder `

## 使用tree查看文件夹结构

- 安装 `brew install tree`
- 查看所有文件 `tree -a`
- 只显示文件夹 `tree -d`
- 显示项目层级，n表示层级 `tree -l n`
- 过滤不想显示的文件或文件夹 `tree -I "node_modules"`
- 将项目结构输出到文件 `tree >tree.md`
- 查看更多命令 `tree --help`

## LaunchPad 图标重排

```
defaults write com.apple.dock ResetLaunchPad -bool true; killall Dock
```



## 批量压缩图片

[参考](https://juejin.im/entry/5b18a1985188257d960ec9ac)

```xaml
<!--安装-->
brew install imagemagick
<!--查看该目录下所有图片数据-->
identify *
<!--把所有图片压缩60%, 质量为70-->
mogrify -resize 60% -quality 70 *
```

## 命令行自动补全

- 终端- nano .inputrc

- 粘贴以下文字

  ```xml
  set completion-ignore-case on
  set show-all-if-ambiguous on
  TAB: menu-complete
  ```

- ctrl+o 回车

- 重启终端

## FD搜索工具

### 安装

`brew install fd`

### 按指定类型`-t`

- 文件(f): `fd -tf keyword`
- 目录(d): `fd -td keyword`
- 符号链接(l): `fd -tl keyword`
- 可执行文件(x):  `fd -tx keyword`

### 搜索指定目录

fd keyword /目录名

### 通过正则表达式搜索

举例: 包含字母且文件名后缀为png的文件 `fd ‘[a-z]\.png$’`

### 搜索隐藏文件

fd -H keyword

### 按扩展名搜索

fd -e md

搜索文件名包含readme且扩展名是md的文件 `fd -e md readme`

### 排除特定目录或文件

搜索除lib目录外所有包含关键字是readme的文件或目录

fd -E lib readme

搜索指定目录下除文件名后缀为js的所有文件

fd -E ‘*.js’ -tf . source/lib/fatclick

## Dash离线文档下载方式

- 断网, 点击要下载的包,把弹出提示框中的地址复制后在浏览器打开
- 选择一个地址用下载软件下载
- 下载后放到某个文件夹下
- 打开Dash添加本地文档



## 卸载包

- 安装brew: https://brew.sh/
- 安装包: `brew install wget`
- 查询包: `brew search /wge*/
- 列出已安装软件: `brew list`
- 更新brew: `brew update`
- 卸载包: `brew uninstall wget`



## Mac M1芯片下安装

- 安装brew: `arch -arm64 brew install xxx`



## 用ffmpeg转换格式

### 安装

- 非 M1 芯片：`brew install ffmpeg`
- M1 芯片：`arch -arm64 brew install ffmpeg`



### 转换

- webm -> gif : `ffmpeg - input.webm -pix_fmt rgb24 output.gif



## gif压缩 gifsicle

### 安装

- 非 M1 芯片：`brew install gifsicle`
- M1 芯片：`arch -arm64 brew install gifsicle`

### 压缩

- `gifsicle -i input.gif --colors 24 -o output.gif`
- `gifsicle -O3 --colors 256 --lossy=30 -o output.gif input.gif`





## 下载整站内容

### 安装 wget

- 非 M1 芯片：`brew install wget`
- M1 芯片：`arch -arm64 brew install wget`

### 扒站

`wget -c -r -np -k -L https://www.xxxx.com`

深入3层链接 `wget -c -r -np -k -l 3 -L -p xxx.com`

参数解释：

- -c, -continue 接着下载没有下载完的文件
- -r, -recursive 递归下载
- -np, -no-parent 不要追溯到父目录
- -k, -convert-links 转换非相对链接为相对链接
- -L, -relative 仅仅跟踪相对链接
- -p, -page-requistes 下载显示HTML文件的所有图片





## Alfred

### 插件

- [Menu-Bar-Search](https://github.com/BenziAhamed/Menu-Bar-Search)
- [New-Terminal-Window](https://github.com/miromannino/alfred-new-terminal-window)
- [Quick Search-Eudic](https://github.com/huhesper/Quick-Search)
