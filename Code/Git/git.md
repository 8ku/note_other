# Git

## 修改git推送方式

[参考](https://git-scm.com/book/zh/v2/%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%8A%E7%9A%84-Git-%E7%94%9F%E6%88%90-SSH-%E5%85%AC%E9%92%A5)

[git官方说明](https://help.github.com/cn/github/authenticating-to-github/connecting-to-github-with-ssh)

1. 检查现有的推送方式

   ```
   git remote -v
   ```

2. 从http改为ssh

   ```
   git remote set-url origin git@github.com:username/xx.git
   ```

3. 从ssh改为http

   ```
   git remote set-url origin https://github.com/username/xx.git
   ```

4. 查看现在的ssh

   ```
   cd ~/.ssh
   ls
   ```

5. 生成ssh密钥并显示(加 -o 可以比默认格式更能抗暴力破解)

   ```
   ssh-keygen -o
   cat ~/.ssh/id_rsa.pub
   ```

6. 复制并在github上粘贴.