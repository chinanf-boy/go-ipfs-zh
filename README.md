# go-ipfs [![explain]][source] [![translate-svg]][translate-list]

[explain]: http://llever.com/explain.svg
[source]: https://github.com/chinanf-boy/go-ipfs-explain
[translate-svg]: http://llever.com/translate.svg
[translate-list]: https://github.com/chinanf-boy/chinese-translate-list

「 ipfs 的 go 语言实现 」

## 更新 ✅

<!-- doc-templite START generated -->
<!-- time = '2018 11.21' -->
<!-- repo = 'ipfs/go-ipfs' -->
<!-- commit = 'b7a48531b7b64fcaa858e2c28e42fb4eeb6fcc0d' -->
翻译的原文 | 与日期 | 最新更新 | 更多
---|---|---|---
[commit] | ⏰ 2018 11.21 | ![last] | [中文翻译][translate-list]

[last]: https://img.shields.io/github/last-commit/ipfs/go-ipfs.svg
[commit]: https://github.com/ipfs/go-ipfs/tree/b7a48531b7b64fcaa858e2c28e42fb4eeb6fcc0d

<!-- doc-templite END generated -->

<details>

- [x] [README.md](./README.md)
- [x] [assets/README.md](./assets/README.zh.md)
- [x] [cmd/ipfs/dist/README.md](./cmd/ipfs/dist/README.zh.md)
- [x] [cmd/ipfswatch/README.md](./cmd/ipfswatch/README.zh.md)
- [x] [docs/README.md](./docs/README.zh.md)
- [x] [docs/command-completion.md](./docs/command-completion.zh.md)
- [x] [docs/config.md](./docs/config.zh.md)
- [x] [docs/datastores.md](./docs/datastores.zh.md)
- [x] [docs/debug-guide.md](./docs/debug-guide.zh.md)
- [x] [docs/experimental-features.md](./docs/experimental-features.zh.md)
- [x] [docs/file-transfer.md](./docs/file-transfer.zh.md)
- [x] [docs/fuse.md](./docs/fuse.zh.md)
- [x] [docs/gateway.md](./docs/gateway.zh.md)
- [x] [docs/github-issue-guide.md](./docs/github-issue-guide.zh.md)
- [x] [docs/implement-api-bindings.md](./docs/implement-api-bindings.zh.md)
- [x] [docs/openbsd.md](./docs/openbsd.zh.md)
- [x] [docs/plugins.md](./docs/plugins.zh.md)
- [x] [docs/releases.md](./docs/releases.zh.md)
- [x] [docs/transports.md](./docs/transports.zh.md)
- [x] [docs/windows.md](./docs/windows.zh.md)
- [x] [misc/launchd/README.md](./misc/launchd/README.zh.md)
- [x] [test/3nodetest/README.md](./test/3nodetest/README.zh.md)
- [x] [test/3nodetest/bootstrap/README.md](./test/3nodetest/bootstrap/README.zh.md)
- [x] [test/3nodetest/server/README.md](./test/3nodetest/server/README.zh.md)
- [x] [test/README.md](./test/README.zh.md)
- [x] [test/dependencies/go-sleep/README.md](./test/dependencies/go-sleep/README.zh.md)
- [x] [test/sharness/README.md](./test/sharness/README.zh.md)
- [x] [thirdparty/README.md](./thirdparty/README.zh.md)

</details>

### 贡献

欢迎 👏 勘误/校对/更新贡献 😊 [具体贡献请看](https://github.com/chinanf-boy/chinese-translate-list#贡献)

## 生活

[If help, **buy** me coffee —— 营养跟不上了，给我来瓶营养快线吧! 💰](https://github.com/chinanf-boy/live-need-money)

---

# go-ipfs

![banner](https://ipfs.io/ipfs/QmVk7srrwahXLNmcDYvyUEJptyoxpndnRa57YJ11L4jV26/ipfs.go.png)

[![](https://img.shields.io/badge/made%20by-Protocol%20Labs-blue.svg?style=flat-square)](http://ipn.io)
[![](https://img.shields.io/badge/project-ipfs-blue.svg?style=flat-square)](http://ipfs.io/)
[![](https://img.shields.io/badge/freenode-%23ipfs-blue.svg?style=flat-square)](http://webchat.freenode.net/?channels=%23ipfs)
[![standard-readme compliant](https://img.shields.io/badge/standard--readme-OK-green.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)
[![GoDoc](https://godoc.org/github.com/ipfs/go-ipfs?status.svg)](https://godoc.org/github.com/ipfs/go-ipfs)
[![Build Status](https://travis-ci.org/ipfs/go-ipfs.svg?branch=master)](https://travis-ci.org/ipfs/go-ipfs)

## 项目状态

[![Throughput Graph](https://graphs.waffle.io/ipfs/go-ipfs/throughput.svg)](https://waffle.io/ipfs/go-ipfs/metrics/throughput)

[**`核心开发告示，周报大会`**](https://github.com/ipfs/pm/issues/674)

## 什么是 IPFS?

ipfs 是一个世界性的,版本化的对等文件系统. 它结合了 **Git,BitTorrent,Kademlia,SFS 和 Web** 的好点子. 它就像一个 bittorrent swarm,交换 git 对象. IPFS 提供了一个像 HTTP Web 一样简单的接口,但内置了永久性. 您还可以将世界挂载到 `/ipfs`.

- 有关详情,请参阅: [ipfs/ipfs 协议库](https://github.com/ipfs/ipfs)

- 请将有关 IPFS *设计*的所有问题放到[ipfs repo 问题](https://github.com/ipfs/ipfs/issues)

- 请将有关 GO IPFS *实现*的所有问题在[这个 repo](https://github.com/ipfs/go-ipfs/issues).

## 目录

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [安全问题](#%E5%AE%89%E5%85%A8%E9%97%AE%E9%A2%98)
- [安装](#%E5%AE%89%E8%A3%85)
  - [系统要求](#%E7%B3%BB%E7%BB%9F%E8%A6%81%E6%B1%82)
  - [安装整理好的构建包](#%E5%AE%89%E8%A3%85%E6%95%B4%E7%90%86%E5%A5%BD%E7%9A%84%E6%9E%84%E5%BB%BA%E5%8C%85)
  - [来自 Linux 包管理器](#%E6%9D%A5%E8%87%AA-linux-%E5%8C%85%E7%AE%A1%E7%90%86%E5%99%A8)
    - [Arch Linux](#arch-linux)
    - [nix](#nix)
    - [snap](#snap)
  - [从源代码构建](#%E4%BB%8E%E6%BA%90%E4%BB%A3%E7%A0%81%E6%9E%84%E5%BB%BA)
    - [安装 Go](#%E5%AE%89%E8%A3%85-go)
    - [下载并编译 ipfs](#%E4%B8%8B%E8%BD%BD%E5%B9%B6%E7%BC%96%E8%AF%91-ipfs)
    - [建立在不太常见的系统上](#%E5%BB%BA%E7%AB%8B%E5%9C%A8%E4%B8%8D%E5%A4%AA%E5%B8%B8%E8%A7%81%E7%9A%84%E7%B3%BB%E7%BB%9F%E4%B8%8A)
    - [故障排除](#%E6%95%85%E9%9A%9C%E6%8E%92%E9%99%A4)
  - [更新 go-ipfs](#%E6%9B%B4%E6%96%B0-go-ipfs)
    - [使用 ipfs-update 进行更新](#%E4%BD%BF%E7%94%A8-ipfs-update-%E8%BF%9B%E8%A1%8C%E6%9B%B4%E6%96%B0)
    - [下载 ipfs 的构建,通过 ipfs](#%E4%B8%8B%E8%BD%BD-ipfs-%E7%9A%84%E6%9E%84%E5%BB%BA%E9%80%9A%E8%BF%87-ipfs)
- [命令行总览](#%E5%91%BD%E4%BB%A4%E8%A1%8C%E6%80%BB%E8%A7%88)
- [入门](#%E5%85%A5%E9%97%A8)
  - [有些事情要确定一下](#%E6%9C%89%E4%BA%9B%E4%BA%8B%E6%83%85%E8%A6%81%E7%A1%AE%E5%AE%9A%E4%B8%80%E4%B8%8B)
  - [Docker 用法](#docker-%E7%94%A8%E6%B3%95)
  - [故障排除](#%E6%95%85%E9%9A%9C%E6%8E%92%E9%99%A4-1)
- [Package 们](#package-%E4%BB%AC)
- [开发](#%E5%BC%80%E5%8F%91)
  - [CLI, HTTP-API, 建筑图](#cli-http-api-%E5%BB%BA%E7%AD%91%E5%9B%BE)
  - [测试](#%E6%B5%8B%E8%AF%95)
  - [开发依赖](#%E5%BC%80%E5%8F%91%E4%BE%9D%E8%B5%96)
  - [开发者 笔记](#%E5%BC%80%E5%8F%91%E8%80%85-%E7%AC%94%E8%AE%B0)
- [贡献-帮助](#%E8%B4%A1%E7%8C%AE-%E5%B8%AE%E5%8A%A9)
- [执照](#%E6%89%A7%E7%85%A7)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 安全问题

ipfs 协议及其实现仍处于重大发展阶段. 这意味着我们的协议可能存在问题,或者我们的实现可能存在错误. 而且 - 虽然 ipfs 还没有生产就绪 - 许多人已经在他们的机器上运行节点. 因此,我们非常重视安全漏洞. 如果您发现安全问题,请立即引起我们的注意!

如果您发现可能影响实时部署的漏洞 (例如,暴露远程执行漏洞) ,请将您的报告私下发送至 `security@ipfs.io`. 请不要提交公共问题. security@ipfs.io 的 GPG 密钥 是[4B9665FB 92636D17 7C7A86D3 50AAE8A9 59B13AF3](https://pgp.mit.edu/pks/lookup?op=get&search=0x50AAE8A959B13AF3).

如果问题是无法立即利用的协议弱点 或 尚未部署的问题,请公开讨论.

## 安装

ipfs 的下载说明在: <http://ipfs.io/docs/install/>. 它是 **强烈建议的说明**,如果您对 ipfs 开发不感兴趣,请遵循这些说明.

### 系统要求

ipfs 可以在大多数 Linux,macOS 和 Windows 系统上运行. 我们建议在具有至少 2 GB RAM 的机器上运行它 (只有一个 CPU 内核可以正常运行) ,但只需 1 GB 的内存即可正常运行. 在内存较少的系统上,它可能不完全稳定.

### 安装整理好的构建包

我们在我们的网站上托管预建的二进制文件[发行页面](https://ipfs.io/ipns/dist.ipfs.io#go-ipfs).

从那里:

- 单击页面右侧的蓝色"Download go-ipfs".
- 打开/提取 存档.
- 移动`ipfs`到你的 `Path` 上 (运行`install.sh`能为你做到这一点) .

你也可以从项目的 Github releases 页面下载 go-ipfs ，如果你 被伟大的 GTW 阻止你访问 ipfs.io。

### 来自 Linux 包管理器

- [Arch Linux](#arch-linux)
- [nix](#nix)
- [快照](#snap)

#### Arch Linux

在 Arch Linux 安装 [go-ipfs](https://www.archlinux.org/packages/community/x86_64/go-ipfs/)包.

```
$ sudo pacman -S go-ipfs
```

go-ipfs 的开发版本也在 AUR 下[go-ipfs-git](https://aur.archlinux.org/packages/go-ipfs-git/). 您可以使用自己喜欢的 AUR Helper 安装它,也可以从 AU R 手动安装.

#### nix

对于 Linux 和 MacOSX,您可以使用纯功能包管理器[nix](https://nixos.org/nix/):

```
$ nix-env -i ipfs
```

您也可以使用它的属性名称来安装`ipfs`.

#### snap

随着 snap,在任何一个[支持的 Linux 发行版](https://snapcraft.io/docs/core/install):

```
$ sudo snap install ipfs
```

### 从源代码构建

#### 安装 Go

ipfs 的构建过程需要`Go 1.10`或更高版本. 如果你没有它: [下载 Go 1.10+](https://golang.org/dl/).

您需要将 **Go 的 bin 目录** 添加到您的`$PATH`环境变量,例如,通过将*下面这些代码行*添加到您的`/etc/profile` (用于系统范围的安装) 或`$HOME/.profile`:

    export PATH=$PATH:/usr/local/go/bin
    export PATH=$PATH:$GOPATH/bin

(如果遇到麻烦,请参阅[go 安装说明](https://golang.org/doc/install)) .

#### 下载并编译 ipfs

```
$ go get -u -d github.com/ipfs/go-ipfs

$ cd $GOPATH/src/github.com/ipfs/go-ipfs
$ make install
```

如果你是在 FreeBSD 使用`gmake install` 而不是`make install`.

#### 建立在不太常见的系统上

如果您的操作系统没有得到官方支持,但您仍然想尝试构建 ipfs (在大多数情况下它应该可以正常工作) ,您可以执行以下操作而不是`make install`:

    $ make install_unsupported

注意: 如果,此过程可能会中断[gx](https://github.com/whyrusleeping/gx) (用于依赖关系管理) 或其任何依赖关系`go get`将始终为每个依赖项选择最新的代码,通常会导致 API 不匹配.

#### 故障排除

- 分离[说明可用于在 Windows 上构建](docs/windows.zh.md).
- 也,[OpenBSD 的说明](docs/openbsd.zh.md).
- `git`是必需的,为了`go get`可以获取所有依赖项.
- 包管理器通常包含过时的`golang`包. 确保`go version`至少 1.10. 请参阅上文,了解如何安装 go.
- 如果您对开发感兴趣,请同时安装开发依赖项.
- _警告:_ 旧版本的 OSX FUSE (适用于 Mac OS X) 在安装时可能会导致内核崩溃! - 我们强烈建议您使用[最新版本的 OSX FUSE](http://osxfuse.github.io/). (看到<https://github.com/ipfs/go-ipfs/issues/177>)
- 有关设置 FUSE 的更多详细信息 (以便可以安装文件系统) ,请参阅 [docs](./docs/README.zh.md) 文件夹.
- Shell 命令补充可用于`misc/completion/ipfs-completion.bash`. 读[docs/command-completion.zh.md](docs/command-completion.zh.md)学习如何安装它.
- 见[init 示例](https://github.com/ipfs/website/tree/master/static/docs/examples/init)有关如何将 ipfs 连接到 systemd 或 您运行的任何 init 系统.

### 更新 go-ipfs

#### 使用 ipfs-update 进行更新

ipfs 有一个官方更新工具`ipfs update`. 该工具没有与 ipfs 一起安装,以保持该逻辑独立于主代码库. 要安装`ipfs update`,[在这里下载](https://ipfs.io/ipns/dist.ipfs.io/#ipfs-update).

#### 下载 ipfs 的构建,通过 ipfs

列出 go-ipfs 的可用版本:

```
$ ipfs cat /ipns/dist.ipfs.io/go-ipfs/versions
```

然后,从上一个命令 (\$ VERSION) 查看版本的可用构建:

```
$ ipfs ls /ipns/dist.ipfs.io/go-ipfs/$VERSION
```

要下载版本的给定版本:

```
$ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_darwin-386.tar.gz # darwin 32-bit build
$ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_darwin-amd64.tar.gz # darwin 64-bit build
$ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_freebsd-amd64.tar.gz # freebsd 64-bit build
$ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_linux-386.tar.gz # linux 32-bit build
$ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_linux-amd64.tar.gz # linux 64-bit build
$ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_linux-arm.tar.gz # linux arm build
$ ipfs get /ipns/dist.ipfs.io/go-ipfs/$VERSION/go-ipfs_$VERSION_windows-amd64.zip # windows 64-bit build
```

## 命令行总览

```
    ipfs - 全球(星际)p2p merkle-dag 文件系统.

    ipfs [<flags>] <command> [<arg>] ...

子命令
    基本 COMMANDS
    init          初始化 ipfs 本地配置
    add <path>    将文件添加到 ipfs
    cat <ref>     显示 ipfs 对象数据
    get <ref>     下载 ipfs 对象
    ls <ref>      列出对象的链接
    refs <ref>    列出来自对象的链接哈希值

    数据结构 COMMANDS
    block         与数据存储区中的原始块交互
    object        与原始dag 节点交互
    files         与对象交互,就像它们是 unix文件系统一样

    高级 COMMANDS
    daemon        启动一个长期运行的守护程序进程
    mount         挂载ipfs只读挂载点
    resolve       解决任何类型的名称
    name          发布或解析IPNS名称
    dns           解析DNS链接
    pin           将对象固定到本地存储
    repo          操作ipfs存储库

    网络 COMMANDS
    id            显示有关ipfs peers的信息
    bootstrap     添加或删除引导程序对等项
    swarm         管理与p2p网络的连接
    dht           查询DHT的值或对等体
    ping          测量连接的延迟
    diag          打印诊断

    工具 COMMANDS
    config        管理配置
    version       显示ipfs版本信息
    update        下载并应用go-ipfs更新
    commands      列出所有可用命令

    Use 'ipfs <command> --help' to learn more about each command.

    ipfs使用本地文件系统中的存储库。 默认情况下，可
     在 ~/.ipfs 找到。 要更改位置，请设置 $ipfs_PATH 环境变量：

    export ipfs_PATH=/path/to/ipfsrepo
```

## 入门

也可以看看: <http://ipfs.io/docs/getting-started/>

要开始使用 ipfs ,必须首先在系统上 初始化 ipfs 的配置文件,用`ipfs init`. 看到`ipfs init --help`有关可选参数的信息. 初始化完成后,即可使用`ipfs mount`,`ipfs add`以及任何其他你想试试的命令!

### 有些事情要确定一下

本地'ipfs 正在工作'的基本证明:

    echo "hello world" > hello
    ipfs add hello
    # This should output a hash string that looks something like:
    # QmT78zSuBmuS4z925WZfrqQ1qHaJ56DQaTfyMUF7F8ff5o
    ipfs cat <that hash>

### Docker 用法

ipfs 的 docker 镜像托管在[hub.docker.com/r/ipfs/go-ipfs](https://hub.docker.com/r/ipfs/go-ipfs/). 要使文件在容器内可见,您需要使用 docker 的选项`-v`安装主机目录. 选择要用于 从 ipfs 导入/导出文件 的目录. 您还应该选择一个目录来存储 在重新启动容器时 将保留的 ipfs 文件.

    export ipfs_staging=</absolute/path/to/somewhere/>
    export ipfs_data=</absolute/path/to/somewhere_else/>

启动运行 ipfs 的容器并公开端口 4001,5001 和 8080:

    docker run -d --name ipfs_host -v $ipfs_staging:/export -v $ipfs_data:/data/ipfs -p 4001:4001 -p 127.0.0.1:8080:8080 -p 127.0.0.1:5001:5001 ipfs/go-ipfs:latest

观看 ipfs 日志:

    docker logs -f ipfs_host

等待 ipfs 启动. 当你看到 ipfs 正在运行:

    Gateway (readonly) server
    listening on /ip4/0.0.0.0/tcp/8080

你现在可以停止观看日志了.

运行 ipfs 命令:

    docker exec ipfs_host ipfs <args...>

例如: 连接到同行

    docker exec ipfs_host ipfs swarm peers

添加文件:

    cp -r <something> $ipfs_staging
    docker exec ipfs_host ipfs add -r /export/<something>

停止正在运行的容器:

    docker stop ipfs_host

### 故障排除

如果之前已经安装过 ipfs,并且遇到了使新版本工作的问题,请尝试删除 (或在其他地方备份) ipfs 配置目录 (默认为`〜/.ipfs`) 并重新运行`ipfs init`. 这会将配置文件重新初始化为其默认值,并清除任何错误的本地数据存储区.

请将一般问题和帮助请求发送给我们[论坛](https://discuss.ipfs.io)或我们的 IRC 频道 (freenode #ipfs) .

如果您认为自己发现了错误,请查看[问题清单](https://github.com/ipfs/go-ipfs/issues),如果您没有在那里看到您的问题,请在 IRC (freenode #ipfs) 上与我们联系 或 提交您自己的问题!

## Package 们

> 由 [`package-table`](https://github.com/ipfs-shipyard/package-table)生成此表格 ，运行 `package-table --data=package-list.json`.

IPFS 生态使用的主包的列表。 这里还有三个值得链接的规范:

| 名                                                                           | CI/Travis                                                                                                                                      | CI/Jenkins                                                                                                                                       | Coverage                                                                                                                                                 | 曰                                                  |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| **Files(文件)**                                                                    |
| [`go-unixfs`](//github.com/ipfs/go-unixfs)                                   | [![Travis CI](https://travis-ci.org/ipfs/go-unixfs.svg?branch=master)](https://travis-ci.org/ipfs/go-unixfs)                                   | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-unixfs/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-unixfs)                                   | 核心'文件系统(filesystem)'逻辑                      |
| [`go-mfs`](//github.com/ipfs/go-mfs)                                         | [![Travis CI](https://travis-ci.org/ipfs/go-mfs.svg?branch=master)](https://travis-ci.org/ipfs/go-mfs)                                         | [![jenkins](https://ci.ipfs.team/buildStatus/icon?job=ipfs/go-mfs/master)](https://ci.ipfs.team/job/ipfs/job/go-mfs/job/master/)                 | [![codecov](https://codecov.io/gh/ipfs/go-mfs/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-mfs)                                         | unixfs 的可变文件系统编辑器                         |
| [`go-ipfs-posinfo`](//github.com/ipfs/go-ipfs-posinfo)                       | [![Travis CI](https://travis-ci.org/ipfs/go-ipfs-posinfo.svg?branch=master)](https://travis-ci.org/ipfs/go-ipfs-posinfo)                       | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-ipfs-posinfo/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-ipfs-posinfo)                       | filestore 的辅助数据类型                            |
| [`go-ipfs-chunker`](//github.com/ipfs/go-ipfs-chunker)                       | [![Travis CI](https://travis-ci.org/ipfs/go-ipfs-chunker.svg?branch=master)](https://travis-ci.org/ipfs/go-ipfs-chunker)                       | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-ipfs-chunker/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-ipfs-chunker)                       | 文件分块器                                          |
| **Exchange(信息交换)**                                                                 |
| [`go-ipfs-exchange-interface`](//github.com/ipfs/go-ipfs-exchange-interface) | [![Travis CI](https://travis-ci.org/ipfs/go-ipfs-exchange-interface.svg?branch=master)](https://travis-ci.org/ipfs/go-ipfs-exchange-interface) | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-ipfs-exchange-interface/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-ipfs-exchange-interface) | 交换服务接口                                        |
| [`go-ipfs-exchange-offline`](//github.com/ipfs/go-ipfs-exchange-offline)     | [![Travis CI](https://travis-ci.org/ipfs/go-ipfs-exchange-offline.svg?branch=master)](https://travis-ci.org/ipfs/go-ipfs-exchange-offline)     | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-ipfs-exchange-offline/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-ipfs-exchange-offline)     | （虚拟）交换服务的离线实现                          |
| [`go-bitswap`](//github.com/ipfs/go-bitswap)                                 | [![Travis CI](https://travis-ci.org/ipfs/go-bitswap.svg?branch=master)](https://travis-ci.org/ipfs/go-bitswap)                                 | [![jenkins](https://ci.ipfs.team/buildStatus/icon?job=ipfs/go-bitswap/master)](https://ci.ipfs.team/job/ipfs/job/go-bitswap/job/master/)         | [![codecov](https://codecov.io/gh/ipfs/go-bitswap/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-bitswap)                                 | bitswap 协议实现                                    |
| [`go-blockservice`](//github.com/ipfs/go-blockservice)                       | [![Travis CI](https://travis-ci.org/ipfs/go-blockservice.svg?branch=master)](https://travis-ci.org/ipfs/go-blockservice)                       | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-blockservice/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-blockservice)                       | 将一个块存储和一个交换一起插入的服务                |
| **Datastores(数据存储)n**                                                               |
| [`go-datastore`](//github.com/ipfs/go-datastore)                             | [![Travis CI](https://travis-ci.org/ipfs/go-datastore.svg?branch=master)](https://travis-ci.org/ipfs/go-datastore)                             | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-datastore/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-datastore)                             | 数据存储区接口，适配器和基本实现                    |
| [`go-ipfs-ds-help`](//github.com/ipfs/go-ipfs-ds-help)                       | [![Travis CI](https://travis-ci.org/ipfs/go-ipfs-ds-help.svg?branch=master)](https://travis-ci.org/ipfs/go-ipfs-ds-help)                       | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-ipfs-ds-help/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-ipfs-ds-help)                       | 数据存储区实用程序功能                              |
| [`go-ds-flatfs`](//github.com/ipfs/go-ds-flatfs)                             | [![Travis CI](https://travis-ci.org/ipfs/go-ds-flatfs.svg?branch=master)](https://travis-ci.org/ipfs/go-ds-flatfs)                             | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-ds-flatfs/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-ds-flatfs)                             | 一个基于文件系统的数据存储区                        |
| [`go-ds-measure`](//github.com/ipfs/go-ds-measure)                           | [![Travis CI](https://travis-ci.org/ipfs/go-ds-measure.svg?branch=master)](https://travis-ci.org/ipfs/go-ds-measure)                           | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-ds-measure/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-ds-measure)                           | 一个度量收集数据库适配器                            |
| [`go-ds-leveldb`](//github.com/ipfs/go-ds-leveldb)                           | [![Travis CI](https://travis-ci.org/ipfs/go-ds-leveldb.svg?branch=master)](https://travis-ci.org/ipfs/go-ds-leveldb)                           | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-ds-leveldb/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-ds-leveldb)                           | 一个基于 leveldb 的数据存储区                       |
| [`go-ds-badger`](//github.com/ipfs/go-ds-badger)                             | [![Travis CI](https://travis-ci.org/ipfs/go-ds-badger.svg?branch=master)](https://travis-ci.org/ipfs/go-ds-badger)                             | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-ds-badger/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-ds-badger)                             | 一个基于 badgerdb 的数据存储区                      |
| **Namesys(另命为)**                                                                  |
| [`go-ipns`](//github.com/ipfs/go-ipns)                                       | [![Travis CI](https://travis-ci.org/ipfs/go-ipns.svg?branch=master)](https://travis-ci.org/ipfs/go-ipns)                                       | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-ipns/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-ipns)                                       | IPNS 数据结构和验证逻辑                             |
| **Repo**                                                                     |
| [`go-ipfs-config`](//github.com/ipfs/go-ipfs-config)                         | [![Travis CI](https://travis-ci.org/ipfs/go-ipfs-config.svg?branch=master)](https://travis-ci.org/ipfs/go-ipfs-config)                         | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-ipfs-config/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-ipfs-config)                         | go-ipfs 配置文件 定义                               |
| [`go-fs-lock`](//github.com/ipfs/go-fs-lock)                                 | [![Travis CI](https://travis-ci.org/ipfs/go-fs-lock.svg?branch=master)](https://travis-ci.org/ipfs/go-fs-lock)                                 | [![jenkins](https://ci.ipfs.team/buildStatus/icon?job=ipfs/go-fs-lock/master)](https://ci.ipfs.team/job/ipfs/job/go-fs-lock/job/master/)         | [![codecov](https://codecov.io/gh/ipfs/go-fs-lock/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-fs-lock)                                 | lockfile 管理 函数                                  |
| [`fs-repo-migrations`](//github.com/ipfs/fs-repo-migrations)                 | [![Travis CI](https://travis-ci.org/ipfs/fs-repo-migrations.svg?branch=master)](https://travis-ci.org/ipfs/fs-repo-migrations)                 | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/fs-repo-migrations/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/fs-repo-migrations)                 | repo 迁移                                           |
| **Blocks(块化)**                                                                   |
| [`go-block-format`](//github.com/ipfs/go-block-format)                       | [![Travis CI](https://travis-ci.org/ipfs/go-block-format.svg?branch=master)](https://travis-ci.org/ipfs/go-block-format)                       | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-block-format/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-block-format)                       | block(块) 接口 和 实现                              |
| [`go-ipfs-blockstore`](//github.com/ipfs/go-ipfs-blockstore)                 | [![Travis CI](https://travis-ci.org/ipfs/go-ipfs-blockstore.svg?branch=master)](https://travis-ci.org/ipfs/go-ipfs-blockstore)                 | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-ipfs-blockstore/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-ipfs-blockstore)                 | blockstore 接口 和 实现                             |
| [`go-ipfs-blockstore`](//github.com/ipfs/go-ipfs-blockstore)                 | [![Travis CI](https://travis-ci.org/ipfs/go-ipfs-blockstore.svg?branch=master)](https://travis-ci.org/ipfs/go-ipfs-blockstore)                 | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-ipfs-blockstore/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-ipfs-blockstore)                 | blockstore 接口 和 实现                             |
| **Commands(命令)**                                                                 |
| [`go-ipfs-cmds`](//github.com/ipfs/go-ipfs-cmds)                             | [![Travis CI](https://travis-ci.org/ipfs/go-ipfs-cmds.svg?branch=master)](https://travis-ci.org/ipfs/go-ipfs-cmds)                             | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-ipfs-cmds/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-ipfs-cmds)                             | CLI & HTTP 命令 库                                  |
| [`go-ipfs-cmdkit`](//github.com/ipfs/go-ipfs-cmdkit)                         | [![Travis CI](https://travis-ci.org/ipfs/go-ipfs-cmdkit.svg?branch=master)](https://travis-ci.org/ipfs/go-ipfs-cmdkit)                         | [![jenkins](https://ci.ipfs.team/buildStatus/icon?job=ipfs/go-ipfs-cmdkit/master)](https://ci.ipfs.team/job/ipfs/job/go-ipfs-cmdkit/job/master/) | [![codecov](https://codecov.io/gh/ipfs/go-ipfs-cmdkit/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-ipfs-cmdkit)                         | 命令库的类型帮手                                    |
| [`go-ipfs-blockstore`](//github.com/ipfs/go-ipfs-blockstore)                 | [![Travis CI](https://travis-ci.org/ipfs/go-ipfs-blockstore.svg?branch=master)](https://travis-ci.org/ipfs/go-ipfs-blockstore)                 | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-ipfs-blockstore/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-ipfs-blockstore)                 | blockstore 接口 和 实现                             |
| [`go-ipfs-api`](//github.com/ipfs/go-ipfs-api)                               | [![Travis CI](https://travis-ci.org/ipfs/go-ipfs-api.svg?branch=master)](https://travis-ci.org/ipfs/go-ipfs-api)                               | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-ipfs-api/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-ipfs-api)                               | 一个 IPFS HTTP API 的 shell                         |
| **Metrics & Logging(度量与记录)**                                                        |
| [`go-metrics-interface`](//github.com/ipfs/go-metrics-interface)             | [![Travis CI](https://travis-ci.org/ipfs/go-metrics-interface.svg?branch=master)](https://travis-ci.org/ipfs/go-metrics-interface)             | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-metrics-interface/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-metrics-interface)             | 指标集合 接口                                       |
| [`go-metrics-prometheus`](//github.com/ipfs/go-metrics-prometheus)           | [![Travis CI](https://travis-ci.org/ipfs/go-metrics-prometheus.svg?branch=master)](https://travis-ci.org/ipfs/go-metrics-prometheus)           | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-metrics-prometheus/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-metrics-prometheus)           | prometheus-backed 指标集合                          |
| [`go-log`](//github.com/ipfs/go-log)                                         | [![Travis CI](https://travis-ci.org/ipfs/go-log.svg?branch=master)](https://travis-ci.org/ipfs/go-log)                                         | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-log/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-log)                                         | logging 框架                                        |
| **Generics/Utils(通用/工具)**                                                           |
| [`go-ipfs-routing`](//github.com/ipfs/go-ipfs-routing)                       | [![Travis CI](https://travis-ci.org/ipfs/go-ipfs-routing.svg?branch=master)](https://travis-ci.org/ipfs/go-ipfs-routing)                       | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-ipfs-routing/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-ipfs-routing)                       | routing-路由(content(内容), peer(节点), value) 帮手 |
| [`go-ipfs-util`](//github.com/ipfs/go-ipfs-util)                             | [![Travis CI](https://travis-ci.org/ipfs/go-ipfs-util.svg?branch=master)](https://travis-ci.org/ipfs/go-ipfs-util)                             | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-ipfs-util/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-ipfs-util)                             | the kitchen sink (厨房水槽)                         |
| [`go-ipfs-addr`](//github.com/ipfs/go-ipfs-addr)                             | [![Travis CI](https://travis-ci.org/ipfs/go-ipfs-addr.svg?branch=master)](https://travis-ci.org/ipfs/go-ipfs-addr)                             | N/A                                                                                                                                              | [![codecov](https://codecov.io/gh/ipfs/go-ipfs-addr/branch/master/graph/badge.svg)](https://codecov.io/gh/ipfs/go-ipfs-addr)                             | 工具函数，用于解析 IPFS multiaddrs(多地址)          |

为简洁起见，我们省略了 go-libp2p 和 go-ipld 包。 这些包的表格可以在各自项目的 readme 文件中找到：

- [go-libp2p](https://github.com/libp2p/go-libp2p#packages)
- [go-ipld](https://github.com/ipld/go-ipld#packages)

## 开发

有些地方可以帮助你入门

- Main 文件: [cmd/ipfs/main.go](https://github.com/ipfs/go-ipfs/blob/master/cmd/ipfs/main.go)
- CLI 命令行: [core/commands/](https://github.com/ipfs/go-ipfs/tree/master/core/commands) <br>
- Bitswap ( 数据 往来 引擎) 改造的 bit 协议: [go-bitswap](https://github.com/ipfs/go-bitswap)
- libp2p
  - libp2p: https://github.com/libp2p/go-libp2p
  - DHT: https://github.com/libp2p/go-libp2p-kad-dht
  - PubSub: https://github.com/libp2p/go-libp2p-pubsub

### CLI, HTTP-API, 建筑图

![](https://github.com/ipfs/go-ipfs/docs/cli-http-api-core-diagram.png)

> [源](https://github.com/ipfs/pm/pull/678#discussion_r210410924)

- 虚线(Dotted)意味着“可能会消失”。
- “Legacy”部分是围绕某些命令的薄包装器，用于在新系统和旧系统之间进行转换。
- “守护进程(daemon)”图中的灰色部分用于显示代码是完全相同的，只是我们根据我们是在客户端还是服务器上运行来打开一些部分，和关闭一些部分。

### 测试

```
make test
```

### 开发依赖

如果更改 协议缓冲区,则需要安装[protoc 编译器](https://github.com/google/protobuf).

### 开发者 笔记

请在 [docs](./docs)目录，查看更多开发信息.

## 贡献-帮助

[![](https://cdn.rawgit.com/jbenet/contribute-ipfs-gif/master/img/contribute.gif)](https://github.com/ipfs/community/blob/master/contributing.md)

我们 ❤️ 所有[我们的贡献者](https://github.com/ipfs/go-ipfs/blob/master/docs/AUTHORS);没有你,这个项目不可能成功! 如果您想提供帮助,请参阅[Contribute.zh.md](contribute.zh.md).

该存储库遵守 ipfs[code-行为守则](https://github.com/ipfs/community/blob/master/code-of-conduct.zh.md).

## 执照

[MIT](https://github.com/ipfs/go-ipfs/blob/master/LICENSE)
