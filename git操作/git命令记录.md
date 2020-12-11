## 一些git命令记录

```bash
$git update-git-for-windows
#git版本升级，需要挂梯子

git log
#查看日志，也就是提交变标号，方便进行回滚

git status
#显示工作区状态，善用status能够及时了解git状态

git add filename
#将文件添加到暂存区
git add .
#添加所有变化的文件

git commit -m "infor"
#将暂存区文件提交到branch，-m是添加此次提交的说明

git push -u origin master/main
#远程push到github,master or main取决于你的branch master的name，个人认为master似乎更加顺耳

git pull
#拉取远程仓库的新文件
```

