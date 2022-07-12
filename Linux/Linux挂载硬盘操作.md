# Linux挂载硬盘操作

## 查看文件系统

```shell
df -HT
---
文件系统       类型     容量  已用  可用 已用% 挂载点
tmpfs          tmpfs    1.7G  2.3M  1.7G    1% /run
/dev/nvme0n1p2 ext4     125G   51G   69G   43% /
tmpfs          tmpfs    8.4G  7.7M  8.4G    1% /dev/shm
tmpfs          tmpfs    5.3M  4.1k  5.3M    1% /run/lock
/dev/nvme0n1p1 vfat     536M  5.5M  531M    2% /boot/efi
/dev/sda2      fuseblk  323G  117G  206G   37% /media/xianwei/D
/dev/sda4      fuseblk  356G  181G  176G   51% /media/xianwei/F
/dev/sda3      fuseblk  323G   63G  261G   20% /media/xianwei/E
tmpfs          tmpfs    1.7G  2.6M  1.7G    1% /run/user/1000
```

## 挂载

```
# 如果是ntfs类型,其中最后的文件夹爱名称即为自定义挂载盘符的名称
sudo mount ntfslabel /dev/sda2 /media/xianwei/D

#如果是ext2或ext3
sudo mount e2label /dev/sda2 /media/xianwei/F
```

## 卸载

```shell
sudo umount /dev/sda2
```

---

有时重启需要手动重新挂载，较为繁琐，这里给出自动挂载方法

## 查看磁盘分区的UUID，确定要挂载的磁盘的UUID:

```shell
sudo blkid
---
/dev/sda4: LABEL="F" BLOCK_SIZE="512" UUID="88BE8D09BE8CF14C" TYPE="ntfs" PARTLABEL="Basic data partition" PARTUUID="5776fdd7-1bcc-42cd-804b-61b9d757239d"
/dev/sda2: LABEL="D" BLOCK_SIZE="512" UUID="28D6F269D6F236A2" TYPE="ntfs" PARTLABEL="Basic data partition" PARTUUID="2673db28-bf3f-4e6f-9ed9-995c6900fd32"
/dev/sda3: LABEL="E" BLOCK_SIZE="512" UUID="C8A4865EA4864EBE" TYPE="ntfs" PARTLABEL="Basic data partition" PARTUUID="6d316e05-769e-466b-922d-ebd81aef6d1c"
```

## 配置开机自动挂载

将分区信息写入`/etc/fstab`文件启动自动挂载

```shell
sudo vim /etc/fstab
---
# 在文件末尾添加
UUID=28D6F269D6F236A2 /media/xianwei/D ntfs defaults 0 0
```

添加的内容说明

```shell
<fs spec> <fs file> <fs vfstype> <fs mntops> <fs freq> <fs passno>
---
<fs spec>: 分区定位，可以是UUID或者LABEL
<fs file>:具体挂载点位置，例如/media/xianwei/D
<fs vfstype>:挂载磁盘类型，Linux一般为ext4,Windows一般为ntfs
<fs mntops>：挂载参数，一般为defaults
<fs freq>：磁盘备份，默认为0不备份
<fs passno>：磁盘检查，默认为0不检查
```

## 重启系统

修改完`/etc/fstab`文件后，运行

```shell
sudo mount -a
```

验证配置是否正确，配置不正确可能会导致系统无法正常启动
