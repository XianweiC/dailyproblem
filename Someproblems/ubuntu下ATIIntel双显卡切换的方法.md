# ubuntu下ATI/Intel双显卡切换的方法

​                      装了ubuntu 12.04 32bit和win7 64bit双系统后，win7基本不用了，工作全部在win7下做。但是，存在一个问题：运行ubuntu时，笔记本过热。 
   由于笔记本是双显卡（HD5650和Intel I5  480集成显卡），所以怀疑是双显卡切换的问题，于是在ubuntu论坛上找到了相关帖子--《（ATI显卡菜鸟x86闭源帖---A鸟都去学雷锋）总结Ubuntu11.04~12.04的ATI驱动安装（精简很多）》 
​    
​    **步骤如下：
**
   \1. 首先要到AMD官方网站下载linux版的驱动催化剂 
​    
   linux/Pages/radeon_linux.aspx">http://support.amd.com/cn/gpudownload/linux/Pages/radeon_linux.aspx 
​    
   现在版本已经出到12.6了，文件的后缀是。run 
​    
   \2. 在home目录创建一个文件夹，命令如下 
​    
   cd ~/;mkdir catalyst12.6 
​    
   \3. 把下载好的驱动催化剂文件放到创建好的catalyst12.6文件夹中 
​    
   \4. 运行下面的命令 
​    
   chmod +x amd-driver-installer-12-6-x86.x86_64.run 
​    
   \5. 创建。deb的安装包 
​    
   sudo sh ./amd-driver-installer-12-6-x86.x86_64.run --buildpkg Ubuntu/oneiric 
​    
   \6. 安装生成的包 
​    
   sudo dpkg -i fglrx*.deb 
​    
   \7. 生成配置文件 
​    
   sudo aticonfig --initial -f 
​    
   防止配置未生效 
​    
   sudo aticonfig --input=/etc/X11/xorg.conf --tls=1 
​    
   8.重启 【必须！】 
​    
   \9. 检查是否成功 
​    
   fglrxinfo 
  ![img](http://pub.chinaunix.net/uploadfile/2012/1022/20121022030708552.png) 
​    接下来是重头戏了 
​    
   双显卡切换（台式机和thinkpad不一定支持）： 
​    
   aticonfig --pxl # 查看当前正在运行的 显卡模式 
​    
   要切换显卡，输入下面的命令 
​    
   -- sudo aticonfig --px-dgpu # 正在激活运行的是 独显（ discrete）模式 （高性能模式）， 必须重启视频驱动和激活特效（重启电脑就行） 
​    
   -- sudo aticonfig --px-igpu # 正在激活运行的是集成或整合的显卡模式 （节电模式）， 必须重启视频驱动和激活特效（重启电脑就行）                