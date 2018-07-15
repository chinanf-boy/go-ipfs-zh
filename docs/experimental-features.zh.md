
# go-ipfs的实验特性

本文档包含 go-ipfs 中的实验性功能列表. 这些功能,命令和API并不成熟,您不应该依赖它们. 一旦它们成熟,就会在 Changelog 和 release 帖子 中提及. 如果它们无法达到成熟,则同样的,会被删除其代码. 

订阅<https://github.com/ipfs/go-ipfs/issues/3397>获得更新. 

当您为 go-ipfs 添加 新的实验性功能或 更改实验性功能时,您必须更新此文档,并在上述问题中链接PR. 

<details>

<summary> 目录 </summary>


<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [ipfs pubsub](#ipfs-pubsub)
  - [状态](#%E7%8A%B6%E6%80%81)
  - [在版本](#%E5%9C%A8%E7%89%88%E6%9C%AC)
  - [如何启用](#%E5%A6%82%E4%BD%95%E5%90%AF%E7%94%A8)
  - [成为真正特性的道路](#%E6%88%90%E4%B8%BA%E7%9C%9F%E6%AD%A3%E7%89%B9%E6%80%A7%E7%9A%84%E9%81%93%E8%B7%AF)
- [客户端模式DHT路由](#%E5%AE%A2%E6%88%B7%E7%AB%AF%E6%A8%A1%E5%BC%8Fdht%E8%B7%AF%E7%94%B1)
  - [状态](#%E7%8A%B6%E6%80%81-1)
  - [在版本](#%E5%9C%A8%E7%89%88%E6%9C%AC-1)
  - [如何启用](#%E5%A6%82%E4%BD%95%E5%90%AF%E7%94%A8-1)
  - [成为真正特性的道路](#%E6%88%90%E4%B8%BA%E7%9C%9F%E6%AD%A3%E7%89%B9%E6%80%A7%E7%9A%84%E9%81%93%E8%B7%AF-1)
- [go-multiplex stream muxer](#go-multiplex-stream-muxer)
  - [状态](#%E7%8A%B6%E6%80%81-2)
  - [在版本](#%E5%9C%A8%E7%89%88%E6%9C%AC-2)
  - [如何启用](#%E5%A6%82%E4%BD%95%E5%90%AF%E7%94%A8-2)
  - [成为真正特性的道路](#%E6%88%90%E4%B8%BA%E7%9C%9F%E6%AD%A3%E7%89%B9%E6%80%A7%E7%9A%84%E9%81%93%E8%B7%AF-2)
- [原始 unix fs 文件](#%E5%8E%9F%E5%A7%8B-unix-fs-%E6%96%87%E4%BB%B6)
  - [状态](#%E7%8A%B6%E6%80%81-3)
  - [在版本](#%E5%9C%A8%E7%89%88%E6%9C%AC-3)
  - [如何启用](#%E5%A6%82%E4%BD%95%E5%90%AF%E7%94%A8-3)
  - [成为真正特性的道路](#%E6%88%90%E4%B8%BA%E7%9C%9F%E6%AD%A3%E7%89%B9%E6%80%A7%E7%9A%84%E9%81%93%E8%B7%AF-3)
- [ipfs文件存储](#ipfs%E6%96%87%E4%BB%B6%E5%AD%98%E5%82%A8)
  - [状态](#%E7%8A%B6%E6%80%81-4)
  - [在版本](#%E5%9C%A8%E7%89%88%E6%9C%AC-4)
  - [如何启用](#%E5%A6%82%E4%BD%95%E5%90%AF%E7%94%A8-4)
  - [成为真正特性的道路](#%E6%88%90%E4%B8%BA%E7%9C%9F%E6%AD%A3%E7%89%B9%E6%80%A7%E7%9A%84%E9%81%93%E8%B7%AF-4)
- [专用网络-Private](#%E4%B8%93%E7%94%A8%E7%BD%91%E7%BB%9C-private)
  - [状态](#%E7%8A%B6%E6%80%81-5)
  - [在版本](#%E5%9C%A8%E7%89%88%E6%9C%AC-5)
  - [如何启用](#%E5%A6%82%E4%BD%95%E5%90%AF%E7%94%A8-5)
  - [成为真正特性的道路](#%E6%88%90%E4%B8%BA%E7%9C%9F%E6%AD%A3%E7%89%B9%E6%80%A7%E7%9A%84%E9%81%93%E8%B7%AF-5)
- [ipfs p2p](#ipfs-p2p)
  - [状态](#%E7%8A%B6%E6%80%81-6)
  - [在版本](#%E5%9C%A8%E7%89%88%E6%9C%AC-6)
  - [如何启用](#%E5%A6%82%E4%BD%95%E5%90%AF%E7%94%A8-6)
  - [如何使用](#%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8)
  - [成为真正特性的道路](#%E6%88%90%E4%B8%BA%E7%9C%9F%E6%AD%A3%E7%89%B9%E6%80%A7%E7%9A%84%E9%81%93%E8%B7%AF-6)
- [线路继电](#%E7%BA%BF%E8%B7%AF%E7%BB%A7%E7%94%B5)
  - [状态](#%E7%8A%B6%E6%80%81-7)
  - [在版本](#%E5%9C%A8%E7%89%88%E6%9C%AC-7)
  - [如何启用](#%E5%A6%82%E4%BD%95%E5%90%AF%E7%94%A8-7)
  - [基本用法:](#%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95)
  - [成为真正特性的道路](#%E6%88%90%E4%B8%BA%E7%9C%9F%E6%AD%A3%E7%89%B9%E6%80%A7%E7%9A%84%E9%81%93%E8%B7%AF-7)
- [插件](#%E6%8F%92%E4%BB%B6)
  - [在版本](#%E5%9C%A8%E7%89%88%E6%9C%AC-8)
  - [状态](#%E7%8A%B6%E6%80%81-8)
  - [基本用法:](#%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95-1)
  - [成为真正特性的道路](#%E6%88%90%E4%B8%BA%E7%9C%9F%E6%AD%A3%E7%89%B9%E6%80%A7%E7%9A%84%E9%81%93%E8%B7%AF-8)
- [Badger数据存储区](#badger%E6%95%B0%E6%8D%AE%E5%AD%98%E5%82%A8%E5%8C%BA)
  - [在版本](#%E5%9C%A8%E7%89%88%E6%9C%AC-9)
  - [基本用法](#%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95)
  - [](#)
  - [成为真正特性的道路](#%E6%88%90%E4%B8%BA%E7%9C%9F%E6%AD%A3%E7%89%B9%E6%80%A7%E7%9A%84%E9%81%93%E8%B7%AF-9)
- [目录分片/ HAMT](#%E7%9B%AE%E5%BD%95%E5%88%86%E7%89%87-hamt)
  - [在版本](#%E5%9C%A8%E7%89%88%E6%9C%AC-10)
  - [状态](#%E7%8A%B6%E6%80%81-9)
  - [基本用法:](#%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95-2)
  - [成为真正特性的道路](#%E6%88%90%E4%B8%BA%E7%9C%9F%E6%AD%A3%E7%89%B9%E6%80%A7%E7%9A%84%E9%81%93%E8%B7%AF-10)
- [IPNS pubsub](#ipns-pubsub)
  - [在版本](#%E5%9C%A8%E7%89%88%E6%9C%AC-11)
  - [状态](#%E7%8A%B6%E6%80%81-10)
  - [如何启用](#%E5%A6%82%E4%BD%95%E5%90%AF%E7%94%A8-8)
  - [成为真正特性的道路](#%E6%88%90%E4%B8%BA%E7%9C%9F%E6%AD%A3%E7%89%B9%E6%80%A7%E7%9A%84%E9%81%93%E8%B7%AF-11)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

</details>

* * *

## ipfs pubsub

### 状态

实验,默认禁用. 

### 在版本

0.4.5

### 如何启用

运行你的守护进程带有`--enable-pubsub-experiment`选项. 然后使用`ipfs pubsub`命令. 

### 成为真正特性的道路

-   [ ] 需要更多人使用并报告其工作情况
-   [ ] 需要实现的身份验证模式
-   [ ] 需要进行性能分析

* * *

## 客户端模式DHT路由

允许dht以不向网络提供请求的模式运行,从而节省带宽. 

### 状态

实验. 

### 在版本

0.4.5

### 如何启用

运行你的守护进程带`--routing=dhtclient`选项. 

### 成为真正特性的道路

-   [ ] 需要更多人使用并报告其工作情况. 
-   [ ] 需要分析它对整个网络的影响. 

* * *

## go-multiplex stream muxer

添加使用 go-multiplex 流复用器 (或代替)yamux和spdy 的支持. 这种多路复用器更简单,并且使用的 内存和带宽 比其他多路复用器少,但缺乏 拥塞控制和抗压逻辑. 它可以试用和试验. 

### 状态

试验

### 在版本

0.4.5

### 如何启用

运行带`--enable-mplex-experiment`

要使其成为默认流复用器,请设置环境变量`LIBP2P_MUX_PREFS`如下: 

    export LIBP2P_MUX_PREFS="/mplex/6.7.0 /yamux/1.0.0 /spdy/3.1.0"

要检查在 任何两个给定对等体之间 使用哪个流复用器,请检查该对应的 json输出`ipfs swarm peers`命令,你会看到这样的事情: 

    $ ipfs swarm peers -v --enc=json | jq .
    {
      "Peers": [
        {
          "Addr": "/ip4/104.131.131.82/tcp/4001",
          "Peer": "QmaCpDMGvV2BGHeYERUEnRQAwe3N8SzbUtfsmvsqQLuvuJ",
          "Latency": "46.032624ms",
          "Muxer": "*peerstream_multiplex.conn",
          "Streams": [
            {
              "Protocol": "/ipfs/bitswap/1.1.0"
            },
            {
              "Protocol": "/ipfs/kad/1.0.0"
            },
            {
              "Protocol": "/ipfs/kad/1.0.0"
            }
          ]
        },
        {
    ...

### 成为真正特性的道路

-   [ ] 各种 重要实际测试和性能指标的工作负载下, 表明它运行良好. 

* * *

## 原始 unix fs 文件

允许在 图形的叶节点 中添加 没有格式化的文件. 

### 状态

实验. 

### 在版本

master,0.4.5

### 如何启用

使用`ipfs add`带`--raw-leaves`. 

### 成为真正特性的道路

-   [ ] 需要更多人使用并报告其工作情况. 

* * *

## ipfs文件存储

允许添加文件 而不重复它们在磁盘上占用的空间. 

### 状态

实验. 

### 在版本

master,0.4.7

### 如何启用

修改你的ipfs配置: 

    ipfs config --json Experimental.FilestoreEnabled true

然后运行`ipfs add`带`--nocopy`

### 成为真正特性的道路

-   [ ] 需要更多人使用并报告其工作情况. 
-   [ ] 需要解决错误状态和故障情况
-   [ ] 需要撰写有关使用,优点和缺点的文档
-   [ ] 需要合并实用程序命令以帮助维护和修复文件存储

* * *

## 专用网络-Private

允许ipfs 仅 连接到具有共享密钥的其他对等方. 

### 状态

试验

### 在版本

master,0.4.7

### 如何启用

使用生成 预共享密钥[ipfs群 密钥 生成 ](https://github.com/Kubuxu/go-ipfs-swarm-key-gen)) : 

    go get github.com/Kubuxu/go-ipfs-swarm-key-gen/ipfs-swarm-key-gen
    ipfs-swarm-key-gen > ~/.ipfs/swarm.key

要加入给定的专用网络,请从网络中的某个人处 获取密钥文件 并 将其保存到`~/.ipfs/swarm.key` (如果您使用的是自定义`$IPFS_PATH`,把它放在那里) . 

使用此功能时,您将无法连接到 **默认** 引导程序节点 (因为我们不属于您的专用网络) ,因此您需要设置自己的引导程序节点. 

首先,要防止您的节点甚至尝试连接到默认的引导程序节点,请运行: 

```bash
ipfs bootstrap rm --all
```

然后添加自己的 bootstrap对等体: 

```bash
ipfs bootstrap add <multiaddr>
```

例如: 

    ipfs bootstrap add /ip4/104.236.76.40/tcp/4001/ipfs/QmSoLV4Bbm51jM9C4gDYZQ9Cy3U6aXMJDAbzgu2fzaDs64

除了它们所服务的功能之外,引导节点 与 网络中的所有其他节点没有区别. 

要格外小心,你也可以设置`LIBP2P_FORCE_PNET`环境变量`1`强制使用私人网络. 如果未配置专用网络,则守护程序将无法启动. 

### 成为真正特性的道路

-   [ ] 需要更多人使用并报告其工作情况
-   [ ] 更多文档

* * *

## ipfs p2p

允许通过 Libp2p流 流动TCP

### 状态

试验

### 在版本

master,0.4.10

### 如何启用

需要在 config 中启用P2P命令

`ipfs config --json Experimental.Libp2pStreamMounting true`

### 如何使用

基本用法: 

-   在一个节点上打开一个侦听器 (节点A) `ipfs p2p listener open p2p-test /ip4/127.0.0.1/tcp/10101`
-   把你希望传递 p2p 连接的应用程序的地址放到`/ip4/127.0.0.1/tcp/10101`
-   在另一个节点上,连接到 节点A 上的侦听器`ipfs p2p stream dial $NODE_A_PEERID p2p-test /ip4/127.0.0.1/tcp/10102`
-   节点B 现在正在 127.0.0.1:10102上 侦听TCP上的连接,将您的应用程序连接到那里以完成连接

### 成为真正特性的道路

-   [ ] 需要更多人使用并报告其工作/适合用例的情况
-   [ ] 更多文档
-   [ ] 支持其他协议

* * *

## 线路继电

当没有直接连接时,允许对等体通过 中间中继节点 连接. 

> 对等体 == 点 == peer

### 状态

试验

### 在版本

master,0.4.11

### 如何启用

默认情况下启用中继传输,允许对等体通过 中继拨号,并侦听传入的中继连接. 可以通过设置`Swarm.DisableRelay = true`禁用传输. 

默认情况下,对等体不充当中间节点 (中继) . 这可以通过设置`Swarm.EnableRelayHop = true`启动. 请注意,需要在 启动在线服务 **之前**设置该选项才能生效;必须重新启动已在线的节点. 

### 基本用法: 

为了通过 **中继节点-QmRelay** 连接 点 <QmA 和 QmB>: 

-   两个点 都应该连接到中继: `ipfs swarm connect /transport/address/ipfs/QmRelay`
-   然后,QmA 可以使用 中继 连接到 QmB: `ipfs swarm connect /ipfs/QmRelay/p2p-circuit/ipfs/QmB`

对等方还可以连接 非特定的中继地址,该地址将尝试拨打已知的中继: `ipfs swarm connect /p2p-circuit/ipfs/QmB`

对等体可以在输出中看到 (非特定的) 中继地址`ipfs swarm addrs listen`

### 成为真正特性的道路

-   [ ] 需要更多人使用它并报告它的工作情况. 
-   [ ] 将中继地址 通告给 DHT,用于 NATed 或其他不可达 的对等体. 
-   [ ] 活跃的中继 发现特定中继地址的*广播*资料. 我们希望 广播了的中继地址 是用于高效响应的特定中继.
-   [ ] 响应中继地址的优先级;可以说,中继地址的优先级应该 低于 直接拨号. 

## 插件

### 在版本

0.4.11

### 状态

试验

插件允许添加功能,而无需重新编译守护程序. 

### 基本用法: 

看到[插件文档](./plugins.zh.md)

### 成为真正特性的道路

-   [ ] 更好地支持 Linux 以外的平台
-   [ ] 更多插件和插件类型
-   [ ] 对稳定性的反馈

## Badger数据存储区

### 在版本

0.4.11

Badger-ds是基于的新数据存储实现<https://github.com/dgraph-io/badger>

### 基本用法

    $ ipfs init --profile=badgerds

要么

    [BACKUP ~/.ipfs]
    $ ipfs config profile apply badgerds
    $ ipfs-ds-convert convert

### 

### 成为真正特性的道路

-   [ ] 需要更多测试
-   [ ] 确保没有未知的主要问题

## 目录分片/ HAMT

### 在版本

0.4.8

### 状态

试验

允许创建具有无限数量条目的目录 - 当前 unixfs目录的大小受 最大块大小 的限制

### 基本用法: 

    ipfs config --json Experimental.ShardingEnabled true

### 成为真正特性的道路

-   [ ] 确保是不需要分片的对象
-   [ ] 通用分片,并在 IPLD和IPFS 之间定义新层

* * *

## IPNS pubsub

### 在版本

0.4.14

### 状态

实验,默认禁用. 

利用 pubsub 实时发布 ipns 记录. 

启用时: 

-   除了发布到 DHT 之外,IPNS发布者还将 记录 推送到 特定名称的 pubsub 主题. 
-   IPNS解析器,在第一次解析时 订阅 特定名称的主题,并通过 pubsub 实时接收随后发布的记录. 这使得后续解决方案是即使的,因为它们通过本地缓存解析. 请注意,初始解析仍然通过DHT,因为 pubsub 中没有消息历史记录. 

发布者 和 解析器节点,都需要启用该功能才能使其有效工作. 

### 如何启用

运行你的守护进程带`--enable-namesys-pubsub`选项;启用 pubsub. 

### 成为真正特性的道路

-   [ ] 需要更多人使用并报告其工作情况
-   [ ] 为订阅,添加 **最后一次记录**分发的机制,这样我们就不必为了初始解析而点击DHT. 或者,我们可以定期重新发布最后一条记录. 
