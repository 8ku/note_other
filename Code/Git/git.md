# Git

## 修改git推送方式

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

   