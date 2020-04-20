# Git

## 修改git推送方式

[参考](https://git-scm.com/book/zh/v2/%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%8A%E7%9A%84-Git-%E7%94%9F%E6%88%90-SSH-%E5%85%AC%E9%92%A5)

[git官方说明](https://help.github.com/cn/github/authenticating-to-github/connecting-to-github-with-ssh)

1. 检查现有的推送方式

   ```yaml
   git remote -v
   ```

2. 从http改为ssh

   ```yaml
   git remote set-url origin git@github.com:username/xx.git
   ```

3. 从ssh改为http

   ```yaml
   git remote set-url origin https://github.com/username/xx.git
   ```

4. 查看现在的ssh

   ```yaml
   cd ~/.ssh
   ls
   ```

5. 生成ssh密钥并显示(加 -o 可以比默认格式更能抗暴力破解)

   ```yaml
   ssh-keygen -o
   cat ~/.ssh/id_rsa.pub
   ```

6. 复制并在github上粘贴.

## 切换 git 本地账号

1. 查看配置

```yaml
git config --global --list
git config --list
```

2. 切换账号

```yaml
git config --global user.name "name"
git config --global user.email "email"
```

## 多账户

[参考](https://juejin.im/post/5dfcb9ebf265da33e82bc5b0)

1. 把git换成要用的用户名和邮箱

```yml
git config --global user.name "name"
git config --global user.email "email"
```

2. 生成SSH Key，指定文件名，避免覆盖原有文件，注意下列代码中的`id_rsa.another`

```yaml
ssh-keygen -t rsa -f ~/.ssh/id_rsa_another -C <Git注册邮箱>
# -t 用来指定加密算法为 rsa；
# -C 后面是个注释信息，并不一定要和你 Git 账户的邮箱或者 Git 账户名保持一致，只是常常是和你账户邮箱保持一致，这样设置，就能知道这个公钥被绑定在哪个 Git 账户上了。
```

3. 配置config文件，如果存在，直接打开

```yaml
touch ~/.ssh/config
```

4. 修改config文件相关信息，注意Host 和Hostname要写主机名

```yaml
Host github.com
	HostName github.com
    IdentityFile ~/.ssh/id_rsa
    User 8ku

Host github8ku
	HostName github.com
    IdentityFile ~/.ssh/id_rsa_another
    User another
```

5. 测试

```yaml
ssh -T git@github.com
Hi xxx! You've successfully authenticated, but GitHub does not provide shell access.

ssh -T github8ku
```

6. 各种报错的解决方法

```yaml
# 用别名测试ssh被denied(publickey)
ssh-add -K ~/.ssh/id_rsa_another
# 提示 Could not open a connection to your authentication agent.
eval 'ssh-agent'
ssh-agent bash
#提示 The agent has no identities. 清除代理
ssh-add -D
# 清除后再添加不同的ssh
ssh-add ~/.ssh/id_rsa
ssh-add ~/.ssh/id_rsa_another
# clone remote 的时候用别名
git clone git@github8ku:bakumatata.github.io.git
git remote add . git@github8ku:bakumatata.github.io.git
```

