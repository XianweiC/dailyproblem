# Colab的一些操作

## 前言

由于目前缺少服务器资源，综合下来，Colab是最优选择，现将各种使用方法进行总结。

## 操作

- 修改tensorflow版本

  1. 首先，重启colab（否则会切换失败）

  ```python
  import os
  os.kill(os.getpid(), 9)
  ```

  2. 切换版本

  ```
  %tensorflow_version 1.x
  ```


- 挂载Google Drive

  ```python
  from google.colab import drive
  drive.mount('/content/drive', force_remount=True)
  ```

- 切换当前目录

  ```python
  import os
  os.chdir(your_path)
  #os.getcwd()
  ```

- 切换文件

  ```python
  path = '/content/data.qian.zip'
  
  import zipfile
  
  '''
  基本格式：zipfile.ZipFile(filename[,mode[,compression[,allowZip64]]])
  mode：可选 r,w,a 代表不同的打开文件的方式；r 只读；w 重写；a 添加
  compression：指出这个 zipfile 用什么压缩方法，默认是 ZIP_STORED，另一种选择是 ZIP_DEFLATED；
  allowZip64：bool型变量，当设置为True时可以创建大于 2G 的 zip 文件，默认值 True；
  '''
  
  zip_file = zipfile.ZipFile(path)
  zip_list = zip_file.namelist() # 得到压缩包里所有文件
  
  for f in zip_list:
      zip_file.extract(f, '/content/drive/MyDrive/tacotronv2_wavernn/data.qian') # 循环解压文件到指定目录
   
  zip_file.close() # 关闭文件，必须有，释放内存
  ```

- 查看GPU

  ```terminal
  !/opt/bin/nvidia-smi
  ```

- 在tensorflow2.x 中使用tensorflow1.x

  ```python
  import tensorflow.compat.v1 as tf
  tf.disable_eager_execution()
  ```

  