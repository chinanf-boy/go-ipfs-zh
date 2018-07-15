
# 保险丝-FUSE

`go-ipfs`使 FUSE 挂载操作系统中`/ipfs`和`/ipns`命名空间成为可能,允许任意应用程序访问IPFS. 

## 安装FUSE

在安装IPFS之前,您需要安装和配置保险丝

#### Linux

注意: 虽然本指南适用于大多数发行版,但您可能需要参考您的发行手册以使其工作正常. 

安装`fuse`用您最喜欢的包管理器: 

    sudo apt-get install fuse

将 要运行IPFS守护程序的 用户 添加到`fuse`组: 

```sh
sudo usermod -a -G fuse <username>
```

通过重新启动 ssh连接 或 重新登录系统,重新启动用户会话 (如果处于活动状态) 以应用更改. 

#### Mac OSX  -  OSXFUSE

已发现,`osxfuse`之前`2.7.0`版本会引起内核恐慌. 为了每个人的缘故,请升级 (最新的是`2.7.4`) . 可以在以下位置找到安装程序<https://osxfuse.github.io/>. 还有一个homebrew (`brew install osxfuse`) ,但用户说:从 官方 OSXFUSE 安装程序包是最好的. 

注意`ipfs`自动检查`osxfuse`版本,防止你低于`2.7.0`版本. 

检查osxfuse版本后[比它应该更复杂],运行`ipfs mount`可能要求您安装另一个二进制文件: 

```sh
go get github.com/jbenet/go-fuse-version/fuse-version
```

如果您在安装FUSE 或 安装IPFS 时遇到任何问题,请跳上 IRC 并与我们联系,或者如果您想出新的内容,请添加到此文档中!

## 准备挂载点

默认情况下 ipfs 使用`/ipfs`和`/ipns`安装目录,可以在配置中更改. 你将不得不明确创建`/ipfs`和`/ipns`目录. 请注意,修改root是需要sudo权限. 

```sh
# make the directories
sudo mkdir /ipfs
sudo mkdir /ipns

# chown them so ipfs can use them without root permissions
sudo chown <username> /ipfs
sudo chown <username> /ipns
```

根据您使用的是 OSX还是Linux,请按照前面的说明进行操作. 

## 挂载IPFS

```sh
ipfs daemon --mount
```

如果您希望允许 其他用户 使用挂载点,请编辑`/etc/fuse.conf`启用非root用户,即: 

```sh
# /etc/fuse.conf - Configuration file for Filesystem in Userspace (FUSE)

# Set the maximum number of FUSE mounts allowed to non-root users.
# The default is 1000.
#mount_max = 1000

# Allow non-root users to specify the allow_other or allow_root mount options.
user_allow_other
```

下一组`Mounts.FuseAllowOther`配置为`true`: 

```sh
ipfs config --json Mounts.FuseAllowOther true
ipfs daemon --mount
```

## 故障排除

#### Linux 中的错误`Permission denied`要么`fusermount: user has no write access to mountpoint`

验证用户是否可以读取配置文件: 

```sh
sudo ls -l /etc/fuse.conf
-rw-r----- 1 root fuse 216 Jan  2  2013 /etc/fuse.conf
```

在大多数发行版中,该组命名为`fuse`将在 保险丝-FUSE 安装期间创建. 您可以通过以下方式检查: 

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

如果您设法在 其他系统上 安装 (或者按照上面一个系统的替代路径) ,请为这些文档做出贡献: D
