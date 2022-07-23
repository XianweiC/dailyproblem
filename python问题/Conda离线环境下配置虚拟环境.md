# Conda离线环境下配置虚拟环境

1.   准备工作

     一台联网机器，用于安装所需库文件

     ```bash
     # 安装打包工具
     conda install -c conda-forge conda-pack
     
     # envname为需要导出的环境名称，conda_envname为打包文件名称
     conda pack -n envsname -o conda_envsname.tar.gz
     ```

2.   将打包文件通过ftp上传

     ```bash
     # envname即为迁移过来的环境名称
     mkdir -p ~/anaconda3/envs/envsname
     
     #将压缩包解压至环境目录下
     tar -zxvf conda_envsname.tar.gz -C ~/anaconda3/envs/envsname
     ```

3.   检查是否转移成功

     ```bash
     conda activate envsname
      
     pip list
     conda list
     ```

     