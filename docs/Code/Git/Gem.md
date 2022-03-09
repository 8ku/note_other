mac 更新 ruby gems也是一个大坑....系统不允许直接写入更新...太折磨人了..所以Linux还是最好的吧..

## 更新方法-非M1芯片

[参考](https://stackoverflow.com/questions/51126403/you-dont-have-write-permissions-for-the-library-ruby-gems-2-3-0-directory-ma)

```bash
#再安装一个ruby
brew install chruby ruby-install
ruby-install ruby
brew install ruby

#上步完成后会提示更新path, 根据提示更新路径
echo 'export PATH="/usr/local/opt/ruby/bin:/usr/local/lib/ruby/gems/2.7.0/bin:$PATH"' >> ~/.zshrc

#refresh shell
source ~/.zshrc

#check ruby location
which ruby

#check ruby version
ruby -v

#install bundler
gem install bundler

#update bundler
bundler update

#查看gem环境
gem env

#安装 jekyll
sudo gem install -n /usr/local/bin/ jekyll

#本地运行jekyll
jekyll serve --watch

#强制运行jekyll
bundle exec jekyll serve

#运行jekyll缺少bundle
bundle install

#如果提示安装的bundle版本比要求的版本高, 删除根目录下的gemfile.lock, 再次运行
bundle install
```





## 安装Ruby - M1芯片

删除 homebrew

-  `sudo rm -rf /usr/local/Homebrew`

-  `sudo rm -rf /opt/homebrew`

重装 [homebrew](https://brew.sh/)

- `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`

安装 asdf

- `brew install asdf`
- 用 asdf 安装最新的 ruby `asdf install ruby latest`
- 设置为全局 `asdf global ruby x.x.x`
- 重启终端

验证 ruby 版本 `ruby -v`

查看 asdf 中安装的 ruby 的路径 `asdf where ruby`

把 asdf 中 ruby 的路径写入 path `echo 'export PATH="/Users/username/.asdf/installs/ruby/x.x.x/bin:$PATH"' >> ~/.zshrc`

