mac 更新 ruby gems也是一个大坑....系统不允许直接写入更新...太折磨人了..所以Linux还是最好的吧..

## 更新方法

[参考](https://stackoverflow.com/questions/51126403/you-dont-have-write-permissions-for-the-library-ruby-gems-2-3-0-directory-ma)

```yaml
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
```

