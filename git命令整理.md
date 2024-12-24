### 初始化和配置
- **初始化仓库**：
  ```bash
  git init
  ```
- **设置全局用户名**：
  ```bash
  git config --global user.name "Your Name"
  ```
- **设置全局邮箱**：
  ```bash
  git config --global user.email "your_email@example.com"
  ```

### 仓库和分支操作
- **克隆远程仓库**：
  ```bash
  git clone [repository-url]
  ```
- **查看远程仓库地址**：
  ```bash
  git remote -v
  ```
- **创建并切换到新分支**：
  ```bash
  git checkout -b [branch-name]
  ```
- **切换到现有分支**：
  ```bash
  git checkout [branch-name]
  ```
- **列出所有分支**：
  ```bash
  git branch
  ```
- **删除本地分支**：
  ```bash
  git branch -d [branch-name]
  ```

### 文件操作
- **添加文件到暂存区**：
  ```bash
  git add [file-name]
  ```
- **添加所有文件到暂存区**：
  ```bash
  git add .
  ```
- **提交更改到仓库**：
  ```bash
  git commit -m "Commit message"
  ```
- **查看仓库状态**：
  ```bash
  git status
  ```

### 查看更改和日志
- **查看文件更改**：
  ```bash
  git diff
  ```
- **查看提交日志**：
  ```bash
  git log
  ```
- **查看更简洁的提交日志**：
  ```bash
  git log --oneline
  ```

### 远程仓库同步
- **拉取最新更改**：
  ```bash
  git pull
  ```
- **推送到远程仓库**：
  ```bash
  git push
  ```
- **强制推送到远程仓库**：
  ```bash
  git push -f
  ```
- **拉取指定分支**：
  ```bash
  git pull origin [branch-name]
  ```
- **推送到指定分支**：
  ```bash
  git push origin [branch-name]
  ```

### 撤销和回退
- **撤销暂存的文件**：
  ```bash
  git reset HEAD [file-name]
  ```
- **回退到上一个提交**：
  ```bash
  git reset --hard HEAD~1
  ```
- **回退到指定提交**：
  ```bash
  git reset --hard [commit-hash]
  ```
- **撤销对文件的更改**：
  ```bash
  git checkout -- [file-name]
  ```
