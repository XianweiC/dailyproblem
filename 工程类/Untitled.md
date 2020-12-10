# git push提示Username for 'https://github.com' 解决办法

因为一些不当remote操作，根据github提示，最后git push提示Username for 'https://github.com'  

注意这里的账号是没问题，可以password并不是账号密码的这个密码，而是github里面 develop setting 里面的acess key;

```
$ git add .

$ git commit -m 'first commit'

[master (root-commit) 3f1b963] first commit

 1 files changed, 59 insertions(+)

 create mode 100644 readme.md

$ git remote add origin https://github.com/XXXX/project.git

$ git push -u origin master

Username for 'https://github.com':
```

网上搜索了一堆方案，最后实施繁杂而有各种因环境不同产生的问题；最终找到一个最直接有效的方法：

不用 HTTP 而是用 SSH 

change

```
https://github.com/XXXX/project.git 
```

to

```
git@github.com:XXXX/project.git
```

对应项目下运行

open -e .git/config

修改config里面的对应值即可。