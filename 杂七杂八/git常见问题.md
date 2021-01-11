# git常见问题

```
You are not currently on a branch.
```

问题：pull的时候又出现冲突 ，出现：

```bash
$ git pull    You are not currently on a branch, so I cannot use any
'branch.<branchname>.merge' in your configuration file.
Please specify which remote branch you want to use on the command
line and try again (e.g. 'git pull <repository> <refspec>').
See git-pull(1) for details.
```


解决方法：

首先git checkout -b temp

其次git checkout master

即可恢复到master repository的状态，然后就可以pull了