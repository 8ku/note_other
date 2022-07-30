# Terminal

## 终端vpn

- 打开bash_profile `open ~/.bash_profile`，如果没有，创建`touch ~/.bash_profile`

```bash
function proxy_on(){
    export http_proxy=http://127.0.0.1:1087
    export https_proxy=http://127.0.0.1:1087
    echo -e "已开启代理"
}
function proxy_off(){
    unset http_proxy
    unset https_proxy
    echo -e "已关闭代理"
}
```

- 让配置生效 `source ~/.bash_profile`
- 测试 `curl ip.gs`
- 开启 `proxy_on`，关闭 `proxy_off`

## 安装Homebrew

`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`

### 安装node

`brew install node`

卸载node

```bash
brew uninstall node
brew cleanup
rm -f /usr/local/bin/npm /usr/local/lib/dtrace/node.d
rm -rf ~/.npm
```

测试node版本 `node -v npm -v` 

## 在 Terminal 中配置打开文件的应用

### Sublime

- 确认 Sublime 的路径： `open -a /Applications/Sublime\ Text.app`，如果可以打开应用，说明路径没问题
- 把路径设置到 bash_profile 中
  - `nano ~/.bash_profile`
  - `alias subl=“open -a /Applications/Sublime\ Text.app”`
  - 保存后 refresh bash `source ~/.bash_profile`
- 可以用 `subl`来打开文件

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



## ffmpeg

### 基本用法

- 下载安装 

- 转换视频格式
  
  - `ffmpeg -i input.mov output.mp4`
