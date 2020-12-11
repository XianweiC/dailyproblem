# git将本地仓库clone至github

## create a new repository on the command line

```shell
echo "# test" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/Monster-c/test.git
git push -u origin master
```

## or push an existing repository from the command line

```shell
git remote add origin https://github.com/Monster-c/test.git
git push -u origin master
```

