# gcc编译，找不到conio.h解决方法        

## 如题

ubuntu下编译遇到 conio.h找不到文件的问题， conio.h非标准库，在windows平台可以，在linux平台用curses.h 
 ubuntu下运行命令：

```bash
    sudo apt-get install libncurses5-dev
```

即可。