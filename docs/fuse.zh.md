
# 保险丝

`go-ipfs`可以安装`/ipfs`和`/ipns`操作系统中的命名空间,允许任意应用程序访问IPFS. 

## 安装FUSE

在安装IPFS之前,您需要安装和配置保险丝

#### Linux的

注意: 虽然本指南适用于大多数发行版,但您可能需要参考您的发行手册以使其工作正常. 

安装`fuse`与您最喜欢的包管理器: 

    sudo apt-get install fuse

将要运行IPFS守护程序的用户添加到`fuse`组: 

```sh
sudo usermod -a -G fuse <username>
```

通过重新启动ssh连接或重新登录系统,重新启动用户会话 (如果处于活动状态) 以应用更改. 

#### Mac OSX  -  OSXFUSE

它已被发现的版本`osxfuse`之前`2.7.0`会引起内核恐慌. 为了每个人的缘故,请升级 (最新的写作时间是`2.7.4`) . 可以在以下位置找到安装程序<https://osxfuse.github.io/>. 还有一个自制的公式 (`brew install osxfuse`) 但用户报告从官方OSXFUSE安装程序包安装的最佳结果. 

注意`ipfs`尝试自动版本检查`osxfuse`如果你有前任,可以防止你在脚下射击`2.7.0`. 自检查OSXFUSE版本[比它应该更复杂],跑步`ipfs mount`可能要求您安装另一个二进制文件: 

```sh
go get github.com/jbenet/go-fuse-version/fuse-version
```

如果您在安装FUSE或安装IPFS时遇到任何问题,请跳上IRC并与我们联系,或者如果您想出新的内容,请添加到此文档中!

## 准备挂载点

默认情况下ipfs使用`/ipfs`和`/ipns`安装目录,可以在配置中更改. 你将不得不创建`/ipfs`和`/ipns`目录明确. 请注意,修改root需要sudo权限. 

```sh
# make the directories
sudo mkdir /ipfs
sudo mkdir /ipns

# chown them so ipfs can use them without root permissions
sudo chown <username> /ipfs
sudo chown <username> /ipns
```

根据您使用的是OSX还是Linux,请按照前面的说明进行操作. 

## 挂载IPFS

```sh
ipfs daemon --mount
```

如果您希望允许其他用户使用挂载点,请进行编辑`/etc/fuse.conf`启用非root用户,即: 

```sh
# /etc/fuse.conf - Configuration file for Filesystem in Userspace (FUSE)

# Set the maximum number of FUSE mounts allowed to non-root users.
# The default is 1000.
#mount_max = 1000

# Allow non-root users to specify the allow_other or allow_root mount options.
user_allow_other
```

下一组`Mounts.FuseAllowOther`配置选项`true`: 

```sh
ipfs config --json Mounts.FuseAllowOther true
ipfs daemon --mount
```

## 故障排除

#### `Permission denied`要么`fusermount: user has no write access to mountpoint`Linux中的错误

验证用户是否可以读取配置文件: 

```sh
sudo ls -l /etc/fuse.conf
-rw-r----- 1 root fuse 216 Jan  2  2013 /etc/fuse.conf
```

在大多数发行版中,该组命名为`fuse`将在保险丝安装期间创建. 您可以通过以下方式检查: 

```sh
sudo grep -q fuse /etc/group && echo fuse_group_present || echo fuse_group_missing
```

如果该组存在,只需将您的常规用户添加到`fuse`组: 

```sh
sudo usermod -G fuse -a <username>
```

如果该组不存在,请创建`fuse`组 (将常规用户添加到其中) 并设置必要的权限,例如: 

```sh
sudo chgrp fuse /etc/fuse.conf
sudo chmod g+r  /etc/fuse.conf
```

<!--
TODO: udev rules for /dev/fuse?
-->

注意使用`fuse`group是可选的,可能取决于您的操作系统. 只要为用户运行设置了适当的权限,就可以使用其他组`ipfs mount`命令. 

#### 挂载命令崩溃和挂载点卡住

    sudo umount /ipfs
    sudo umount /ipns

如果您设法在其他系统上安装 (或者按照上面一个系统的替代路径) ,请为这些文档做出贡献: D
