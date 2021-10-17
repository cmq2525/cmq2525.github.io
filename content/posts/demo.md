---
title: "Demo"
date: 2021-10-17T12:38:50+08:00
draft: false
tags: ["NFS"]
categories: ["Install", "documentation"]
---
参考：
1.[Ubuntu 16.04系统上NFS的安装与使用](https://blog.csdn.net/CSDN_duomaomao/article/details/77822883)

2.[nfs的使用](https://www.huweihuang.com/linux-notes/tools/nfs-usage.html)

#### 1.安装
**执行以下命令安装NFS服务器，apt会自动安装nfs-common、rpcbind等13个软件包**

`sudo apt install nfs-kernel-server`



#### 2.配置
创建目录
`mkdir -p /mnt/data/cmq/data/nfs-storage`

修改配置文件

`vim /etc/exports`

添加以下信息

`/mnt/data/cmq/data/nfs-storage *(rw,insecure,sync,no_subtree_check,no_root_squash)`



(如果已经开启了nfs服务，则需要执行`sudo exportfs -a`让配置生效）

#### 3.启动服务
```
sudo service rpcbind start
sudo service nfs-kernel-server restart
```

确认是否生效（应该出现之前指定的目录）：

`showmount -e`

4.访问
需要安装nfs客户端：

`sudo apt-get install nfs-common`

创建目录并挂载：
```
mkdir -p  /home/chenmengqi/cmq-test
mount -t nfs -o nolock 10.122.101.6:/mnt/data/cmq/data/nfs-storage /home/chenmengqi/cmq-test
```
