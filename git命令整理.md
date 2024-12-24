## git配置

### 1. 初始化和配置

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
- **设置全局 diff 工具**：
  ```bash
  git config --global diff.tool mydifftool
  ```
- **设置全局合并工具**：
  ```bash
  git config --global merge.tool mymergetool
  ```

### 2. 仓库和分支操作

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
- **列出所有本地和远程分支**：
  ```bash
  git branch -a
  ```
- **删除本地分支**：
  ```bash
  git branch -d [branch-name]
  ```
- **删除远程分支**：
  ```bash
  git push origin --delete [branch-name]
  ```
- **重命名分支**：
  ```bash
  git branch -m [old-name] [new-name]
  ```

### 3. 文件操作

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

### 4. 查看更改和日志

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

### 5. 远程仓库同步

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

### 6. 撤销和回退

- **撤销暂存的文件**：
  ```bash
  git reset HEAD [file-name]
  ```
- **回退到上一个提交**：
  ```bash
  git reset --hard HEAD~1
  git push -f origin [current-branch]
  ```
- **回退到指定提交**：
  ```bash
  git reset --hard [commit-hash]
  ```
- **撤销对文件的更改**：
  ```bash
  git checkout -- [file-name]
  ```
- **撤销工作目录中的所有未提交更改**：
  ```bash
  git reset --hard
  git clean -fdx
  ```

### 7. 合并与冲突

- **合并特定分支到当前分支**：
  ```bash
  git merge [branch-name]
  ```
- **解决冲突后标记为已解决**：
  ```bash
  git add [resolved-files]
  git commit
  ```
- **撤销最近的合并**：
  ```bash
  git merge --abort
  ```

### 8. 标签管理

- **创建标签**：
  ```bash
  git tag [tag-name]
  ```
- **列出所有标签**：
  ```bash
  git tag
  ```
- **推送标签到远程仓库**：
  ```bash
  git push origin [tag-name]
  ```
- **删除本地标签**：
  ```bash
  git tag -d [tag-name]
  ```

### 9. 子模块管理

- **添加子模块**：
  ```bash
  git submodule add [repository-url] [path]
  ```
- **更新子模块**：
  ```bash
  git submodule update --init --recursive
  ```

### 10. 远程仓库操作

- **添加远程仓库**：
  ```bash
  git remote add [remote-name] [repository-url]
  ```
- **重命名远程仓库**：
  ```bash
  git remote rename [old-name] [new-name]
  ```
- **查看远程仓库的引用和URL**：
  ```bash
  git remote show [remote-name]
  ```

### 11. 高级搜索

- **搜索提交信息**：
  ```bash
  git log -S[search-term]
  ```

- **搜索代码**：
  ```bash
  git grep --heading -e "search-term"
  ```

### 12. 高级查看更改

- **查看两个分支之间的差异**：
  ```bash
  git diff [branch1]...[branch2]
  ```
- **查看某个特定提交的详细差异**：
  ```bash
  git show [commit-hash]
  ```
- **查看某个文件的版本历史**：
  ```bash
  git log -p [file-name]
  ```

这个整理包含了所有您之前提供的信息，并去除了重复的命令。希望这个清单对您有所帮助，如果您有任何疑问或需要进一步的解释，请随时告诉我。



## 具体操作

如果您已经有了一个包含文件的文件夹，并希望将它初始化为 Git 仓库并推送到远程仓库，您可以按照以下步骤操作：

### 1. 初始化本地 Git 仓库
在您的文件夹中打开命令行（终端），并执行以下命令来初始化 Git 仓库：

```bash
cd /path/to/your/folder
git init
```

### 2. 添加文件到仓库
将所有文件添加到 Git 的暂存区：

```bash
git add .
```

或者，如果您只想添加特定的文件，可以指定文件名：

```bash
git add <file1> <file2> ...
```

### 3. 提交更改
提交您的更改到本地仓库：

```bash
git commit -m "Initial commit"
```

### 4. 创建远程仓库
在远程 Git 服务（如 GitHub、GitLab 或 Bitbucket）上创建一个新的仓库。记下仓库的 URL。

### 5. 添加远程仓库地址
将您的本地仓库与远程仓库关联起来：

```bash
git remote set-url origin
```

```bash
git remote add origin [remote-repository-url]
```
将 `[remote-repository-url]` 替换为您远程仓库的实际 URL。

### 6. 推送到远程仓库
推送您的本地提交到远程仓库：

```bash
git push -u origin main
```
如果您的默认分支名不是 `main`（例如，在 GitHub 上创建的新仓库默认分支名为 `main`，而在 GitLab 和 Bitbucket 上是 `master`），请将 `main` 替换为相应的分支名。

### 7. 后续提交
之后，每当您需要推送新的提交到远程仓库时，只需执行：

```bash
git push
```

这些步骤将帮助您将一个已有的文件夹初始化为 Git 仓库，并推送到远程仓库。如果在操作过程中遇到任何问题，欢迎随时提问。

### 报错处理

```
git pull origin master --allow-unrelated-histories
```

