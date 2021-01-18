# git中常见的命令

```bash
# 列出所有本地分支
git branch

# 列出所有远程分支
git branch -r

# 新建一个分支，但依然停留在当前分支
git branch [branch-name]

#切换分支
git checkout [branch-name]

# 新建一个分支，并切换到该分支
git checkout -b [branch]

# 合并指定分支到当前分支$ 
git merge [branch]

# 删除分支$ 
git branch -d [branch-name]

# 删除远程分支$ 
git push origin --delete [branch-name]$ git branch -dr [remote/branch]
```