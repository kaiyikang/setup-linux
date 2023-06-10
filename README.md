# setup-linux

This is a Repo to record how to introduce the setup process of Linux.

## Usage

```bash
sudo apt update;
sudo apt upgrade;
sudo apt install git;
sudo apt install neovim;
git clone git@github.com:kaiyikang/setup-linux.git;
```


## Close Wlan

```bash
sudo apt install net-tools;
man ip;
ip addr;
sudo ip link set wlan0 down;
```


## 如何安装

reference: [教程地址](https://github.com/seamusdemora/PiFormulae/blob/master/FileShare.md#3a-edit-the-samba-configuration-file)

本文目的，将外置硬盘挂载到树莓派，并使用samba作为shared Folder提供给macbook。

首先是挂载，将硬盘插入树莓派，并使用下面的命令查看：
```bash
sudo fdisk --list
(or)
sudo lsldk --fs
```
这个指令可以查看和硬盘相关的信息，例如：label信息（ssd），硬盘类型（exFat）等等。


我想使用自动挂载，但没有成功，但依旧尝试了下面的步骤：
```bash
sudo vim /etc/fstab
# add the following contetns)
LABEL=SSD /home/kangyikai/mntSSD exfat defaults,uid=1000,gid=1000 0 0
```

然后使用这个指令挂载，它会执行在fstab中记录的内容：
```bash
sudo mount -av
```

自动挂载没有解决，似乎是因为权限问题。当然，这不会影响接下来的内容。

安装samba
```bash
sudo apt-get install samba samba-common-bin 
```

备份samba的配置文件
```bash
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.bkup
```

添加下面的内容到文件的末尾
```samba
[sandisk16gb]
Comment = Shared Folder
Path = /home/pi/mntThumbDrv
Browseable = yes
Writeable = yes
only guest = no
create mask = 0700
directory mask = 0700
force user = pi
```

将用户添加到samba的数据库中
```bash
sudo smbpassed -a kang
```

重新启动samba，加载配置文件
```bash
sudo /etc/init.d/smbd restart
```


