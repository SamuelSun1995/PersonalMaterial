# Ubuntu 16.04升级内核到20.04

# 一、首先需要从16.04 → 18.04

sudo mv /etc/apt/sources.list ~/

sudo mv /etc/apt/sources.list.d/*.list ~/

1. # 改变源（粘贴下面这一段到终端并运行）

cat <<EOF | sudo tee /etc/apt/sources.list

deb http://archive.ubuntu.com/ubuntu/ xenial-backports main universe multiverse restricted

deb http://archive.ubuntu.com/ubuntu/ xenial main universe multiverse restricted

deb http://archive.ubuntu.com/ubuntu/ xenial-updates main universe multiverse restricted

deb http://security.ubuntu.com/ubuntu/ xenial-security main universe multiverse restricted

EOF

1. # 依次执行以下语句

sudo add-apt-repository "deb http://archive.ubuntu.com/ubuntu/ xenial-backports main universe multiverse restricted"

sudo add-apt-repository "deb http://archive.ubuntu.com/ubuntu/ xenial main universe multiverse restricted"

sudo add-apt-repository "deb http://archive.ubuntu.com/ubuntu/ xenial-updates main universe multiverse restricted"

sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu/ xenial-security main universe multiverse restricted"

1. # 执行升级

sudo apt-get update

sudo apt-get upgrade

sudo apt-get purge ubuntu-advantage-tools --autoremove

sudo rm /etc/apt/sources.list.d/ubuntu-esm-infra.list

sudo do-release-upgrade



# 二、18.04 → 20.04

基本一样的步骤,但是必须要先升级到18.04：

sudo mv /etc/apt/sources.list ~/

sudo mv /etc/apt/sources.list.d/*.list ~/

1. # 改变源（粘贴下面这一段到终端并运行）

cat <<EOF | sudo tee /etc/apt/sources.list

deb http://archive.ubuntu.com/ubuntu/ bionic-backports main universe multiverse restricted

deb http://archive.ubuntu.com/ubuntu/ bionic main universe multiverse restricted

deb http://archive.ubuntu.com/ubuntu/ bionic-updates main universe multiverse restricted

deb http://security.ubuntu.com/ubuntu/ bionic-security main universe multiverse restricted

EOF

1. # 依次执行以下语句

sudo add-apt-repository "deb http://archive.ubuntu.com/ubuntu/ bionic-backports main universe multiverse restricted"

sudo add-apt-repository "deb http://archive.ubuntu.com/ubuntu/ bionic main universe multiverse restricted"

sudo add-apt-repository "deb http://archive.ubuntu.com/ubuntu/ bionic-updates main universe multiverse restricted"

sudo add-apt-repository "deb http://security.ubuntu.com/ubuntu/ bionic-security main universe multiverse restricted"

1. # 执行升级

sudo apt-get update

sudo apt-get upgrade

sudo apt-get purge ubuntu-advantage-tools --autoremove

sudo rm /etc/apt/sources.list.d/ubuntu-esm-infra.list

sudo do-release-upgrade



# Q&A

1. sudo apt-get update 报错

> E: 无法下载 http://security.ubuntu.com/ubuntu/dists/xenial-security/universe/dep11/Components-amd64.yml 无法打开文件 /var/lib/apt/lists/partial/security.ubuntu.com_ubuntu_dists_xenial-security_universe_dep11_Components-amd64.yml.xz - open (13: 权限不够) [IP: 185.125.190.39 80]

>  E: 部分索引文件下载失败。如果忽略它们，那将转而使用旧的索引文件。

解决：到这个目录下删掉这个就行；（我是备份了一下，以防有用）



1. ModuleNotFoundError: No module named 'softwareproperties'

解决：依次执行以下操作：

-  sudo vi /usr/bin/add-apt-repository
- \#!/usr/bin/python3修改为#!/usr/bin/python3.5即可。



1. ModuleNotFoundError: No module named 'lsb_release'

解决：依次执行以下操作：

- sudo vi /usr/bin/lsb_release

 更改：#!/usr/bin/python3.5m -Es



1. ModuleNotFoundError: No module named 'DistUpgrade'

解决：依次执行以下命令：

- head -n1 /usr/bin/do-release-upgrade  #找到指向的python
- sudo rm -rf /usr/bin/python3 # 上面找到的python链接
- ln -s /usr/bin/python3.5 /usr/bin/python3 # 用原始链接替换



1. ModuleNotFoundError: No module named 'shlex'

解决：shlex是本地一个基础库，这边的解决方式就是更改默认的Python如下：

- （第一种方式）将脚本的头的  #!/usr/bin/env python 改成 #!/usr/bin/env python3
- （第二种方式）改变系统的Python版本，可以REF：https://blog.csdn.net/White_Idiot/article/details/78240298



> 目前遇到的问题就这些，欢迎补充~