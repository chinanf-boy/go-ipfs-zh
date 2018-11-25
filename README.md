
# go-ipfs [![explain]][source] [![translate-svg]][translate-list]

[explain]: http://llever.com/explain.svg
[source]: https://github.com/chinanf-boy/go-ipfs-explain
[translate-svg]: http://llever.com/translate.svg
[translate-list]: https://github.com/chinanf-boy/chinese-translate-list

![banner](https://ipfs.io/ipfs/QmVk7srrwahXLNmcDYvyUEJptyoxpndnRa57YJ11L4jV26/ipfs.go.png)

[![](https://img.shields.io/badge/made%20by-Protocol%20Labs-blue.svg?style=flat-square)](http://ipn.io)
[![](https://img.shields.io/badge/project-ipfs-blue.svg?style=flat-square)](http://ipfs.io/)
[![](https://img.shields.io/badge/freenode-%23ipfs-blue.svg?style=flat-square)](http://webchat.freenode.net/?channels=%23ipfs)
[![standard-readme compliant](https://img.shields.io/badge/standard--readme-OK-green.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)
[![GoDoc](https://godoc.org/github.com/ipfs/go-ipfs?status.svg)](https://godoc.org/github.com/ipfs/go-ipfs)
[![Build Status](https://travis-ci.org/ipfs/go-ipfs.svg?branch=master)](https://travis-ci.org/ipfs/go-ipfs)

[![Throughput Graph](https://graphs.waffle.io/ipfs/go-ipfs/throughput.svg)](https://waffle.io/ipfs/go-ipfs/metrics/throughput)

> ipfs的go语言实现

## 更新 中

<!-- doc-templite START generated -->
<!-- time = '2018 11.21' -->
<!-- repo = 'ipfs/go-ipfs' -->
<!-- commit = 'b7a48531b7b64fcaa858e2c28e42fb4eeb6fcc0d' -->
翻译的原文 | 与日期 | 最新更新 | 更多
---|---|---|---
[commit] | ⏰ 2018 7.9 | ![last] | [中文翻译][translate-list]

[last]: https://img.shields.io/github/last-commit/ipfs/go-ipfs.svg
[commit]: https://github.com/ipfs/go-ipfs/tree/7207b1c1c916a7a78cddad6f94078af408f541c8

<!-- doc-templite END generated -->


<details>

<summary> 细节 ⏰ 2018 7.14 结束</summary>

- [x] [0. dev.zh.md](./dev.zh.md)
- [x] [1. README.md](./README.md)
- [x] [2. contribute.zh.md](./contribute.zh.md)
- [x] [3. docs/command-completion.zh.md](./docs/command-completion.zh.md)
- [x] [4. docs/config.zh.md](./docs/config.zh.md)
- [x] [5. docs/datastores.zh.md](./docs/datastores.zh.md)
- [x] [6. docs/debug-guide.zh.md](./docs/debug-guide.zh.md)
- [x] [7. docs/experimental-features.zh.md](./docs/experimental-features.zh.md)
- [x] [8. docs/file-transfer.zh.md](./docs/file-transfer.zh.md)
- [x] [9. docs/fuse.zh.md](./docs/fuse.zh.md)
- [x] [10. docs/github-issue-guide.zh.md](./docs/github-issue-guide.zh.md)
- [x] [11. docs/implement-api-bindings.zh.md](./docs/implement-api-bindings.zh.md)
- [x] [12. docs/openbsd.zh.md](./docs/openbsd.zh.md)
- [x] [13. docs/plugins.zh.md](./docs/plugins.zh.md)
- [x] [14. docs/README.zh.md](./docs/README.zh.md)
- [x] [15. docs/releases.zh.md](./docs/releases.zh.md)
- [x] [16. docs/transports.zh.md](./docs/transports.zh.md)
- [x] [17. docs/windows.zh.md](./docs/windows.zh.md)

</details>


### 贡献

欢迎 👏 勘误/校对/更新贡献 😊 [具体贡献请看](https://github.com/chinanf-boy/chinese-translate-list#贡献)

## 生活

[help me live , live need money 💰](https://github.com/chinanf-boy/live-need-money)

---

ipfs是一个世界性的,版本化的对等文件系统. 它结合了 **Git,BitTorrent,Kademlia,SFS 和 Web** 的好点子. 它就像一个 bittorrent swarm,交换 git对象. ipfs 提供了一个像 HTTP Web 一样简单的接口,但内置了永久性. 您还可以将世界挂载到 `/ipfs`. 

- 有关详情,请参阅: [https://github.com/ipfs/ipfs](https://github.com/ipfs/ipfs)

- 请将有关 ipfs *设计*的所有问题放到[ipfs repo问题](https://github.com/ipfs/ipfs/issues)

- 请将有关 go-ipfs *实现*的所有问题在[这个repo](https://github.com/ipfs/go-ipfs/issues). 

## 目录

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [安全问题](#%E5%AE%89%E5%85%A8%E9%97%AE%E9%A2%98)
- [安装](#%E5%AE%89%E8%A3%85)
  - [系统要求](#%E7%B3%BB%E7%BB%9F%E8%A6%81%E6%B1%82)
  - [安装整理好的构建包](#%E5%AE%89%E8%A3%85%E6%95%B4%E7%90%86%E5%A5%BD%E7%9A%84%E6%9E%84%E5%BB%BA%E5%8C%85)
  - [来自Linux包管理器](#%E6%9D%A5%E8%87%AAlinux%E5%8C%85%E7%AE%A1%E7%90%86%E5%99%A8)
    - [Arch Linux](#arch-linux)
    - [nix](#nix)
    - [snap](#snap)
  - [从源代码构建](#%E4%BB%8E%E6%BA%90%E4%BB%A3%E7%A0%81%E6%9E%84%E5%BB%BA)
    - [安装Go](#%E5%AE%89%E8%A3%85go)
    - [下载并编译ipfs](#%E4%B8%8B%E8%BD%BD%E5%B9%B6%E7%BC%96%E8%AF%91ipfs)
    - [建立在不太常见的系统上](#%E5%BB%BA%E7%AB%8B%E5%9C%A8%E4%B8%8D%E5%A4%AA%E5%B8%B8%E8%A7%81%E7%9A%84%E7%B3%BB%E7%BB%9F%E4%B8%8A)
    - [故障排除](#%E6%95%85%E9%9A%9C%E6%8E%92%E9%99%A4)
  - [发展依赖](#%E5%8F%91%E5%B1%95%E4%BE%9D%E8%B5%96)
  - [更新](#%E6%9B%B4%E6%96%B0)
    - [使用 ipfs-update 进行更新](#%E4%BD%BF%E7%94%A8-ipfs-update-%E8%BF%9B%E8%A1%8C%E6%9B%B4%E6%96%B0)
    - [下载ipfs的构建,通过ipfs](#%E4%B8%8B%E8%BD%BDipfs%E7%9A%84%E6%9E%84%E5%BB%BA%E9%80%9A%E8%BF%87ipfs)
- [命令行总览](#%E5%91%BD%E4%BB%A4%E8%A1%8C%E6%80%BB%E8%A7%88)
- [入门](#%E5%85%A5%E9%97%A8)
  - [有些事情要确定一下](#%E6%9C%89%E4%BA%9B%E4%BA%8B%E6%83%85%E8%A6%81%E7%A1%AE%E5%AE%9A%E4%B8%80%E4%B8%8B)
  - [Docker用法](#docker%E7%94%A8%E6%B3%95)
  - [故障排除](#%E6%95%85%E9%9A%9C%E6%8E%92%E9%99%A4-1)
- [贡献-帮助](#%E8%B4%A1%E7%8C%AE-%E5%B8%AE%E5%8A%A9)
  - [想加入ipfs?](#%E6%83%B3%E5%8A%A0%E5%85%A5ipfs)
  - [想看看我们的代码？](#%E6%83%B3%E7%9C%8B%E7%9C%8B%E6%88%91%E4%BB%AC%E7%9A%84%E4%BB%A3%E7%A0%81)
- [执照](#%E6%89%A7%E7%85%A7)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 安全问题

ipfs协议及其实现仍处于重大发展阶段. 这意味着我们的协议可能存在问题,或者我们的实现可能存在错误. 而且 - 虽然 ipfs 还没有生产就绪 - 许多人已经在他们的机器上运行节点. 因此,我们非常重视安全漏洞. 如果您发现安全问题,请立即引起我们的注意!

如果您发现可能影响实时部署的漏洞 (例如,暴露远程执行漏洞) ,请将您的报告私下发送至 `security@ipfs.io`. 请不要提交公共问题. security@ipfs.io的 GPG密钥 是[4B9665FB 92636D17 7C7A86D3 50AAE8A9 59B13AF3](https://pgp.mit.edu/pks/lookup?op=get&search=0x50AAE8A959B13AF3). 

如果问题是无法立即利用的协议弱点 或 尚未部署的问题,请公开讨论. 

## 安装

ipfs 的下载说明在: <http://ipfs.io/docs/install/>. 它是 **强烈建议的说明**,如果您对ipfs开发不感兴趣,请遵循这些说明. 

### 系统要求

ipfs 可以在大多数 Linux,macOS和Windows 系统上运行. 我们建议在具有至少2 GB RAM的机器上运行它 (只有一个CPU内核可以正常运行) ,但只需 1 GB的内存即可正常运行. 在内存较少的系统上,它可能不完全稳定. 

### 安装整理好的构建包

我们在我们的网站上托管预建的二进制文件[发行页面](https://ipfs.io/ipns/dist.ipfs.io#go-ipfs). 

从那里: 

-   单击页面右侧的蓝色"Download go-ipfs". 
-   打开/提取 存档. 
-   移动`ipfs`到你的 `Path` 上 (运行`install.sh`能为你做到这一点) . 

### 来自Linux包管理器

-   [Arch Linux](#arch-linux)
-   [nix](#nix)
-   [快照](#snap)

#### Arch Linux

在Arch Linux 安装 [go-ipfs](https://www.archlinux.org/packages/community/x86_64/go-ipfs/)包. 

    $ sudo pacman -S go-ipfs

go-ipfs的开发版本也在AUR下[go-ipfs-git](https://aur.archlinux.org/packages/go-ipfs-git/). 您可以使用自己喜欢的 AUR Helper 安装它,也可以从 AU R手动安装. 

#### nix

对于Linux和MacOSX,您可以使用纯功能包管理器[nix](https://nixos.org/nix/): 

    $ nix-env -i ipfs

您也可以使用它的属性名称来安装`ipfs`. 

#### snap

随着 snap,在任何一个[支持的Linux发行版](https://snapcraft.io/docs/core/install): 

    $ sudo snap install ipfs

### 从源代码构建

#### 安装Go

ipfs的构建过程需要`Go 1.10`或更高版本. 如果你没有它: [下载Go 1.10+](https://golang.org/dl/). 

您需要将 **Go的bin目录** 添加到您的`$PATH`环境变量,例如,通过将*下面这些代码行*添加到您的`/etc/profile` (用于系统范围的安装) 或`$HOME/.profile`: 

    export PATH=$PATH:/usr/local/go/bin
    export PATH=$PATH:$GOPATH/bin

 (如果遇到麻烦,请参阅[go安装说明](https://golang.org/doc/install)) . 

#### 下载并编译ipfs

    $ go get -u -d github.com/ipfs/go-ipfs

    $ cd $GOPATH/src/github.com/ipfs/go-ipfs
    $ make install

如果你是在 FreeBSD使用`gmake install` 而不是`make install`. 

#### 建立在不太常见的系统上

如果您的操作系统没有得到官方支持,但您仍然想尝试构建 ipfs (在大多数情况下它应该可以正常工作) ,您可以执行以下操作而不是`make install`: 

    $ make install_unsupported

注意: 如果,此过程可能会中断[gx](https://github.com/whyrusleeping/gx) (用于依赖关系管理) 或其任何依赖关系`go get`将始终为每个依赖项选择最新的代码,通常会导致API不匹配. 

#### 故障排除

-   分离[说明可用于在Windows上构建](docs/windows.zh.md). 
-   也,[OpenBSD的说明](docs/openbsd.zh.md). 
-   `git`是必需的,为了`go get`可以获取所有依赖项. 
-   包管理器通常包含过时的`golang`包. 确保`go version`至少1.10. 请参阅上文,了解如何安装go. 
-   如果您对开发感兴趣,请同时安装开发依赖项. 
-   *警告: 旧版本的 OSX FUSE (适用于Mac OS X) 在安装时可能会导致内核崩溃!*我们强烈建议您使用[最新版本的OSX FUSE](http://osxfuse.github.io/).  (看到<https://github.com/ipfs/go-ipfs/issues/177>) 
-   有关设置 FUSE 的更多详细信息 (以便可以安装文件系统) ,请参阅 [docs](./docs/README.zh.md) 文件夹. 
-   Shell命令补充可用于`misc/completion/ipfs-completion.bash`. 读[docs/command-completion.zh.md](docs/command-completion.zh.md)学习如何安装它. 
-   见[init示例](https://github.com/ipfs/website/tree/master/static/docs/examples/init)有关如何将 ipfs 连接到 systemd 或 您运行的任何init系统. 

### 发展依赖

如果更改 协议缓冲区,则需要安装[protoc编译器](https://github.com/google/protobuf). 

### 更新

#### 使用 ipfs-update 进行更新

ipfs有一个官方更新工具`ipfs update`. 该工具没有与 ipfs 一起安装,以保持该逻辑独立于主代码库. 要安装`ipfs update`,[在这里下载](https://ipfs.io/ipns/dist.ipfs.io/#ipfs-update). 

#### 下载ipfs的构建,通过ipfs

列出go-ipfs的可用版本: 

    $ ipfs cat /ipns/dist.ipfs.io/go-ipfs/versions

然后,从上一个命令 ($ VERSION) 查看版本的可用构建: 

    $ ipfs ls /ipns/dist.ipfs.io/go-ipfs/$VERSION

要下载版本的给定版本: 

    $ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_darwin-386.tar.gz # darwin 32-bit build
    $ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_darwin-amd64.tar.gz # darwin 64-bit build
    $ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_freebsd-amd64.tar.gz # freebsd 64-bit build
    $ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_linux-386.tar.gz # linux 32-bit build
    $ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_linux-amd64.tar.gz # linux 64-bit build
    $ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_linux-arm.tar.gz # linux arm build
    $ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_windows-amd64.zip # windows 64-bit build

## 命令行总览

      ipfs - Global p2p merkle-dag filesystem.

      ipfs [<flags>] <command> [<arg>] ...

    SUBCOMMANDS
      BASIC COMMANDS
        init          Initialize ipfs local configuration
        add <path>    Add a file to ipfs
        cat <ref>     Show ipfs object data
        get <ref>     Download ipfs objects
        ls <ref>      List links from an object
        refs <ref>    List hashes of links from an object

      DATA STRUCTURE COMMANDS
        block         Interact with raw blocks in the datastore
        object        Interact with raw dag nodes
        files         Interact with objects as if they were a unix filesystem

      ADVANCED COMMANDS
        daemon        Start a long-running daemon process
        mount         Mount an ipfs read-only mountpoint
        resolve       Resolve any type of name
        name          Publish or resolve IPNS names
        dns           Resolve DNS links
        pin           Pin objects to local storage
        repo          Manipulate an ipfs repository

      NETWORK COMMANDS
        id            Show info about ipfs peers
        bootstrap     Add or remove bootstrap peers
        swarm         Manage connections to the p2p network
        dht           Query the DHT for values or peers
        ping          Measure the latency of a connection
        diag          Print diagnostics

      TOOL COMMANDS
        config        Manage configuration
        version       Show ipfs version information
        update        Download and apply go-ipfs updates
        commands      List all available commands

      Use 'ipfs <command> --help' to learn more about each command.

      ipfs uses a repository in the local file system. By default, the repo is located
      at ~/.ipfs. To change the repo location, set the $ipfs_PATH environment variable:

        export ipfs_PATH=/path/to/ipfsrepo

## 入门

也可以看看: <http://ipfs.io/docs/getting-started/>

要开始使用 ipfs ,必须首先在系统上 初始化ipfs 的配置文件,用`ipfs init`. 看到`ipfs init --help`有关可选参数的信息. 初始化完成后,即可使用`ipfs mount`,`ipfs add`以及任何其他你想试试的命令!

### 有些事情要确定一下

本地'ipfs 正在工作'的基本证明: 

    echo "hello world" > hello
    ipfs add hello
    # This should output a hash string that looks something like:
    # QmT78zSuBmuS4z925WZfrqQ1qHaJ56DQaTfyMUF7F8ff5o
    ipfs cat <that hash>

### Docker用法

ipfs 的 docker 镜像托管在[hub.docker.com/r/ipfs/go-ipfs](https://hub.docker.com/r/ipfs/go-ipfs/). 要使文件在容器内可见,您需要使用docker的选项`-v`安装主机目录. 选择要用于 从ipfs导入/导出文件 的目录. 您还应该选择一个目录来存储 在重新启动容器时 将保留的ipfs文件. 

    export ipfs_staging=</absolute/path/to/somewhere/>
    export ipfs_data=</absolute/path/to/somewhere_else/>

启动运行ipfs的容器并公开端口4001,5001和8080: 

    docker run -d --name ipfs_host -v $ipfs_staging:/export -v $ipfs_data:/data/ipfs -p 4001:4001 -p 127.0.0.1:8080:8080 -p 127.0.0.1:5001:5001 ipfs/go-ipfs:latest

观看ipfs日志: 

    docker logs -f ipfs_host

等待ipfs启动. 当你看到ipfs正在运行: 

    Gateway (readonly) server
    listening on /ip4/0.0.0.0/tcp/8080

你现在可以停止观看日志了. 

运行ipfs命令: 

    docker exec ipfs_host ipfs <args...>

例如: 连接到同行

    docker exec ipfs_host ipfs swarm peers

添加文件: 

    cp -r <something> $ipfs_staging
    docker exec ipfs_host ipfs add -r /export/<something>

停止正在运行的容器: 

    docker stop ipfs_host

### 故障排除

如果之前已经安装过ipfs,并且遇到了使新版本工作的问题,请尝试删除 (或在其他地方备份) ipfs配置目录 (默认为`〜/.ipfs`) 并重新运行`ipfs init`. 这会将配置文件重新初始化为其默认值,并清除任何错误的本地数据存储区. 

请将一般问题和帮助请求发送给我们[论坛](https://discuss.ipfs.io)或我们的 IRC频道 (freenode #ipfs) . 

如果您认为自己发现了错误,请查看[问题清单](https://github.com/ipfs/go-ipfs/issues),如果您没有在那里看到您的问题,请在 IRC (freenode #ipfs) 上与我们联系 或 提交您自己的问题!

## 贡献-帮助

我们❤️所有[我们的贡献者](docs/AUTHORS);没有你,这个项目不可能成功! 如果您想提供帮助,请参阅[Contribute.zh.md](contribute.zh.md). 

该存储库遵守ipfs[code-行为守则](https://github.com/ipfs/community/blob/master/code-of-conduct.zh.md). 

### 想加入ipfs?

[![](https://cdn.rawgit.com/jbenet/contribute-ipfs-gif/master/img/contribute.gif)](https://github.com/ipfs/community/blob/master/contributing.zh.md)

### 想看看我们的代码？

有些地方可以帮助你入门。（WIP）

Main 文件: [cmd/ipfs/main.go](https://github.com/ipfs/go-ipfs/blob/master/cmd/ipfs/main.go) <br>
CLI 命令行: [core/commands/](https://github.com/ipfs/go-ipfs/tree/master/core/commands) <br>
Bitswap (the data trading engine) 改造的bit协议: [exchange/bitswap/](https://github.com/ipfs/go-ipfs/tree/master/exchange/bitswap)

DHT: https://github.com/libp2p/go-libp2p-kad-dht <br>
PubSub: https://github.com/libp2p/go-floodsub <br>
libp2p: https://github.com/libp2p/go-libp2p

## 执照

MIT
