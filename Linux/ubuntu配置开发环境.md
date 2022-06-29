# `ubuntu`配置开发环境

## 更换镜像源

```bash
# 备份默认镜像源
sudo cp /etc/apt/source.list /etc/apt/source_backup.list
#更换源为清华大学
sudo nano /etc/apt/source.list
#ctrl + shift + 6进入选择模式
# ↓ 全选 ctrl + k删除
#将清华源粘贴
# -------------------
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# -------------------
# ctrl + x退出 Y保存
#更新源
sudo apt update
```



## 必备工具

```bash
sudo apt isntall git vim openssh-server net-tools curl
```



---

## install zsh

```bash
sudo apt install -y zsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
# 如果报错
# curl: (7) Failed to connect to raw.githubusercontent.com port 443: Connection refused
sudo修改/etc/hosts, 在末尾加入
199.232.68.133 raw.github.com
199.232.28.133 raw.githubusercontent.com
```

