# github将本地仓库连接至远程仓库

```
cw@DESKTOP-UBUTA83 MINGW64 /d/WorkSpace/Typora (master)
$ git remote add origin https://github.com/Monster-c/dailyproblem.git

cw@DESKTOP-UBUTA83 MINGW64 /d/WorkSpace/Typora (master)
$ git push -u origin master
Logon failed, use ctrl+c to cancel basic credential prompt.
Enumerating objects: 12, done.
Counting objects: 100% (12/12), done.
Delta compression using up to 8 threads
Compressing objects: 100% (12/12), done.
Writing objects: 100% (12/12), 6.39 KiB | 2.13 MiB/s, done.
Total 12 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/Monster-c/dailyproblem.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```



```bash
git强制将本地仓库覆盖到远程仓库
git push -f --set-upstream origin master:master
```

