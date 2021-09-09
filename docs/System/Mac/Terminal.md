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

