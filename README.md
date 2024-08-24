# Learning-record

学习记录

## Git学习相关


### 参考教程

> [基于 VScode 的 git 详细使用指南【保姆级！建议收藏！】](https://blog.csdn.net/weixin_48024605/article/details/136037857)
> [最全的git命令（详细）和对常见git操作流程讲解](https://segmentfault.com/a/1190000042347483)


### git 实例

```
# 为了简化示例，我将假设你正在处理两个分支：main（或你项目的默认分支）和feature（一个功能分支）。

# 假设你已经在你的Git仓库中，并且已经做了一些更改  和 初始配置
  
# 1. 将更改添加到暂存区  
git add <file1> <file2> # 假设你更改了file1和file2  
  
# 2. 提交更改到本地仓库  
git commit -m "Add new features to file1 and file2"  
  
# 3. 切换到feature分支（假设它已存在）  
git switch feature # 或者在旧版Git中使用 git checkout feature  
  
# 在feature分支上做一些额外的更改...  
  
# 4. 再次将更改添加到暂存区并提交  
git add <file3>  
git commit -m "Implement additional feature in file3"  
  
# 5. 现在，假设你想将feature分支的更改合并到main分支  
# 首先，确保你在main分支上  
git switch main  
  
# 执行合并操作  
git merge feature  
  
# 解决可能出现的任何合并冲突（如果有的话）  
# ...（解决冲突后，使用 git add 来标记冲突已解决）  
# git add <conflicted-file>  
# git commit # 如果有必要，Git可能会要求你提交一个合并提交  
  
# 6. 推送main分支的更改到远程仓库  
git push origin main  
  
# 7. 现在，如果你想要获取远程仓库的最新更改（例如，其他人可能已经推送了更改）  
git pull origin main  
  
# 假设你意识到最近的几个提交有误，你想要重置它们  
# 注意：下面的操作会丢弃最近的提交，请谨慎使用  
# 首先，查看提交历史来确定你想要重置到的提交  
git log  
  
# 假设你想要重置到某个特定的提交（使用其哈希值的前几位作为引用）  
git reset --hard <commit-hash-prefix>  
  
# 8. 添加或更新远程仓库信息  
# 如果需要添加一个新的远程仓库  
git remote add new-remote <url>  
  
# 如果需要更新远程仓库的URL  
git remote set-url origin <new-url>  
  
# 9. 从远程仓库获取最新数据但不合并  
git fetch origin  
  
# 现在，你的本地仓库已经更新为包含远程仓库的最新信息，  
# 但你还没有将这些更改合并到你的工作分支中。
```



### 常见git命令汇总

```python


# 1. 初始化Git仓库  
git init  
# 初始化一个新的Git仓库  
  
# 2. 添加文件到暂存区  
git add <file>  
# 将文件添加到暂存区  
  
# 3. 提交更改  
git commit -m "Commit message"  
# 将暂存区的更改提交到仓库中，并附带一条消息  
  
# 4. 切换到分支  
git switch <branch>  # Git 2.23+  
# 切换到指定的分支（Git 2.23及更高版本使用git switch）  
# 或者（旧版Git）  
git checkout <branch>  
  
# 5. 创建新分支  
git branch <branch-name>  
# 创建一个新的分支  
  
# 6. 删除分支  
git branch -d <branch-name>  
# 删除一个已合并的分支  
# 强制删除（未合并）  
git branch -D <branch-name>  
  
# 7. 推送更改到远程仓库  
git push <remote> <branch>  
# 将本地分支的更改推送到远程仓库  
  
# 8. 从远程仓库拉取更改  
git pull <remote> <branch>  
# 从远程仓库获取最新更改并合并到当前分支  
  
# 9. 合并分支  
git merge <branch>  
# 将指定分支的更改合并到当前分支  
  
# 10. 重置当前分支到指定提交  
git reset --hard <commit>  
# 将当前分支重置到指定的提交，丢弃之后的所有更改  
  
# 11. 添加远程仓库  
git remote add <name> <url>  
# 添加一个新的远程仓库  
  
# 12. 删除远程仓库  
git remote remove <name>  
# 删除远程仓库  
  
# 13. 查看远程仓库信息  
git remote -v  
# 查看远程仓库的详细信息  
  
# 14. 显示当前状态  
git status  
# 显示当前工作目录和暂存区的状态  
  
# 15. 查看提交历史  
git log  
# 查看提交历史  
  
# 16. 从远程仓库获取更改但不合并  
git fetch <remote>  
# 从远程仓库获取最新更改但不合并  
  
# 17. 暂存更改  
git stash  
# 暂存当前工作区的更改，以便稍后恢复  
  
# 18. 恢复暂存的更改  
git stash pop  
# 恢复最近一次暂存的更改并删除stash中的记录  
  
# 19. 变基  
git rebase <branch>  
# 将一系列提交合并到另一个分支上，保持一个线性的提交历史  
  
# 20. 标记提交  
git tag <tag-name>  
# 给当前分支的最新提交打标签  
  
# 21. 检出文件到工作目录（旧版Git）  
git checkout -- <file>  
# 恢复工作树中的文件到最近一次提交时的状态  
  
# 22. 撤销工作目录的更改（不暂存）  
git restore <file>  # Git 2.23+  
# 撤销工作目录中文件的更改（不暂存）  
  
# 23. 撤销暂存区的更改  
git restore --staged <file>  # Git 2.23+  
# 将文件从暂存区撤回到工作目录  
  
# 24. 查看差异  
git diff  
# 查看工作目录与暂存区之间的差异  
# 或者  
git diff <commit>  
# 查看当前工作目录与指定提交之间的差异  
  
# 25. 撤销最近的提交（不改变工作目录）  
git revert <commit>  
# 创建一个新的提交来“撤销”指定提交的更改  
  
# 26. 清理未跟踪的文件  
git clean -f  
# 清理工作目录中未跟踪的文件  
  
# 27. 列出所有分支  
git branch -a  
# 列出所有本地和远程分支  
  
# 28. 强制推送更改到远程仓库  
git push <remote> <branch> --force  
# 强制将本地分支的更改推送到远程仓库（慎用）  
  
# 29. 检出特定版本的文件  
git checkout <commit>^ -- <file>  
# 检出指定提交中文件的版本到工作目录（旧版Git）  
# 或者（Git 2.23+）  
git restore --source=<commit> --staged --worktree --


```
