
# go-ipfs的实验特性

本文档包含go-ipfs中的实验性功能列表. 这些功能,命令和API并不成熟,您不应该依赖它们. 一旦它们成熟,就会在更改日志和发布帖子中提及. 如果它们未达到成熟度,则同样适用,并删除其代码. 

订阅<https://github.com/ipfs/go-ipfs/issues/3397>获得更新. 

当您为go-ipfs添加新的实验性功能或更改实验性功能时,您必须更新此文档,并在上述问题中链接PR. 

-   [ipfs pubsub](#ipfs-pubsub)
-   [客户端模式DHT路由](#client-mode-dht-routing)
-   [go-multiplex stream muxer](#go-multiplex-stream-muxer)
-   [unixfs文件的原始叶子](#raw-leaves-for-unixfs-files)
-   [ipfs文件存储](#ipfs-filestore)
-   [BadgerDB数据存储区](#badger-datastore)
-   [专用网络](#private-networks)
-   [ipfs p2p](#ipfs-p2p)
-   [电路继电器](#circuit-relay)
-   [插件](#plugins)
-   [目录分片/ HAMT](#directory-sharding-hamt)
-   [IPNS PubSub](#ipns-pubsub)

* * *

## ipfs pubsub

### 州

实验,默认禁用. 

### 在版本中

0.4.5

### 如何启用

用你的守护进程运行你的守护进程`--enable-pubsub-experiment`旗. 然后使用`ipfs pubsub`命令. 

### 成为真正特色的道路

-   [ ] 需要更多人使用并报告其工作情况
-   [ ] 需要实现的身份验证模式
-   [ ] 需要进行性能分析

* * *

## 客户端模式DHT路由

允许dht以不向网络提供请求的模式运行,从而节省带宽. 

### 州

实验. 

### 在版本中

0.4.5

### 如何启用

用你的守护进程运行你的守护进程`--routing=dhtclient`旗. 

### 成为真正特色的道路

-   [ ] 需要更多人使用并报告其工作情况. 
-   [ ] 需要分析它对整个网络的影响. 

* * *

## go-multiplex stream muxer

添加了对与yamux和spdy一起使用go-multiplex流复用器 (或代替) 的支持. 这种多路复用器更简单,并且使用的内存和带宽比其他多路复用器少,但缺乏拥塞控制和背压逻辑. 它可以试用和试验. 

### 州

试验

### 在版本中

0.4.5

### 如何启用

用你的守护进程运行`--enable-mplex-experiment`

要使其成为默认流复用器,请设置环境变量`LIBP2P_MUX_PREFS`如下: 

    export LIBP2P_MUX_PREFS="/mplex/6.7.0 /yamux/1.0.0 /spdy/3.1.0"

要检查在任何两个给定对等体之间使用哪个流复用器,请检查该对应的json输出`ipfs swarm peers`命令,你会看到这样的事情: 

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

### 成为真正特色的道路

-   [ ] 各种工作负载的重要实际测试和性能指标表明它运行良好. 

* * *

## 原始叶子为unixfs文件

允许在图形的叶节点中添加没有格式化的文件. 

### 州

实验. 

### 在版本中

大师,0.4.5

### 如何启用

使用`--raw-leaves`打电话时的标志`ipfs add`. 

### 成为真正特色的道路

-   [ ] 需要更多人使用并报告其工作情况. 

* * *

## ipfs文件存储

允许添加文件而不重复它们在磁盘上占用的空间. 

### 州

实验. 

### 在版本中

大师,0.4.7

### 如何启用

修改你的ipfs配置: 

    ipfs config --json Experimental.FilestoreEnabled true

然后通过`--nocopy`运行时标记`ipfs add`

### 成为真正特色的道路

-   [ ] 需要更多人使用并报告其工作情况. 
-   [ ] 需要解决错误状态和故障情况
-   [ ] 需要撰写有关使用,优点和缺点的文档
-   [ ] 需要合并实用程序命令以帮助维护和修复文件存储

* * *

## 专用网络

允许ipfs仅连接到具有共享密钥的其他对等方. 

### 州

试验

### 在版本中

大师,0.4.7

### 如何启用

使用生成预共享密钥[IPF问题-群密钥根](https://github.com/Kubuxu/go-ipfs-swarm-key-gen)) : 

    go get github.com/Kubuxu/go-ipfs-swarm-key-gen/ipfs-swarm-key-gen
    ipfs-swarm-key-gen > ~/.ipfs/swarm.key

要加入给定的专用网络,请从网络中的某个人处获取密钥文件并将其保存到`~/.ipfs/swarm.key` (如果您使用的是自定义`$IPFS_PATH`,把它放在那里) . 

使用此功能时,您将无法连接到默认引导程序节点 (因为我们不属于您的专用网络) ,因此您需要设置自己的引导程序节点. 

首先,要防止您的节点甚至尝试连接到默认的引导程序节点,请运行: 

```bash
ipfs bootstrap rm --all
```

然后添加自己的bootstrap对等体: 

```bash
ipfs bootstrap add <multiaddr>
```

例如: 

    ipfs bootstrap add /ip4/104.236.76.40/tcp/4001/ipfs/QmSoLV4Bbm51jM9C4gDYZQ9Cy3U6aXMJDAbzgu2fzaDs64

除了它们所服务的功能之外,引导节点与网络中的所有其他节点没有区别. 

要格外小心,你也可以设置`LIBP2P_FORCE_PNET`环境变量`1`强制使用私人网络. 如果未配置专用网络,则守护程序将无法启动. 

### 成为真正特色的道路

-   [ ] 需要更多人使用并报告其工作情况
-   [ ] 更多文档

* * *

## ipfs p2p

允许通过Libp2p流隧道TCP连接

### 州

试验

### 在版本中

大师,0.4.10

### 如何启用

需要在config中启用P2P命令

`ipfs config --json Experimental.Libp2pStreamMounting true`

### 如何使用

基本用法: 

-   在一个节点上打开一个侦听器 (节点A) `ipfs p2p listener open p2p-test /ip4/127.0.0.1/tcp/10101`
-   哪里`/ip4/127.0.0.1/tcp/10101`把你希望传递p2p连接的应用程序的地址放到
-   在另一个节点上,连接到节点A上的侦听器`ipfs p2p stream dial $NODE_A_PEERID p2p-test /ip4/127.0.0.1/tcp/10102`
-   节点B现在正在127.0.0.1:10102上侦听TCP上的连接,将您的应用程序连接到那里以完成连接

### 成为真正特色的道路

-   [ ] 需要更多人使用并报告其工作/适合用例的情况
-   [ ] 更多文档
-   [ ] 支持其他协议

* * *

## 电路继电器

当没有直接连接时,允许对等体通过中间中继节点连接. 

### 州

试验

### 在版本中

大师,0.4.11

### 如何启用

默认情况下启用中继传输,允许对等体通过中继拨号并侦听传入的中继连接. 可以通过设置禁用传输`Swarm.DisableRelay = true`在配置中. 

默认情况下,对等体不充当中间节点 (中继) . 这可以通过设置启用`Swarm.EnableRelayHop = true`在配置中. 请注意,需要在启动在线服务之前设置该选项才能生效;必须重新启动已在线的节点. 

### 基本用法: 

为了通过中继节点QmRelay连接对等体QmA和QmB: 

-   两个对等体都应该连接到中继: `ipfs swarm connect /transport/address/ipfs/QmRelay`
-   然后,Peer QmA可以使用继电器连接到对等QmB: `ipfs swarm connect /ipfs/QmRelay/p2p-circuit/ipfs/QmB`

对等方还可以连接非特定的中继地址,该地址将尝试拨打已知的中继: `ipfs swarm connect /p2p-circuit/ipfs/QmB`

对等方可以在输出中看到 (非特定的) 中继地址`ipfs swarm addrs listen`

### 成为真正特色的道路

-   [ ] 需要更多人使用它并报告它的工作情况. 
-   [ ] 将中继地址通告给DHT,用于NAT或其他不可达的对等体. 
-   [ ] 特定中继地址通告的活动中继发现. 我们希望广告中继地址指定用于高效拨号的特定中继. 
-   [ ] 拨打中继地址的优先级;可以说,中继地址的优先级应该低于直接拨号. 

## 插件

### 在版本中

0.4.11

### 州

试验

插件允许添加功能而无需重新编译守护程序. 

### 基本用法: 

看到[插件文档](./plugins.zh.md)

### 成为真正特色的道路

-   [ ] 更好地支持Linux以外的平台
-   [ ] 更多插件和插件类型
-   [ ] 对稳定性的反馈

    ## Badger数据存储区

    ### 在版本中

    0.4.11

    Badger-ds是基于的新数据存储实现<https://github.com/dgraph-io/badger>

    ### 基本用法

        $ ipfs init --profile=badgerds

    要么

        [BACKUP ~/.ipfs]
        $ ipfs config profile apply badgerds
        $ ipfs-ds-convert convert

### 

### 成为真正特色的道路

-   [ ] 需要更多测试
-   [ ] 确保没有未知的主要问题

## 目录分片/ HAMT

### 在版本中

0.4.8

### 州

试验

允许创建具有无限数量条目的目录 - 当前unixfs目录的大小受最大块大小的限制

### 基本用法: 

    ipfs config --json Experimental.ShardingEnabled true

### 成为真正特色的道路

-   [ ] 确保不需要分片的对象不是
-   [ ] 通用分片并在IPLD和IPFS之间定义新层

* * *

## IPNS pubsub

### 在版本中

0.4.14

### 州

实验,默认禁用. 

利用pubsub实时发布ipns记录. 

启用时: 

-   除了发布到DHT之外,IPNS发布者还将记录推送到特定于名称的pubsub主题. 
-   IPNS解析器在第一个分辨率上订阅特定于名称的主题,并通过pubsub实时接收随后发布的记录. 这使得后续解决方案即时,因为它们通过本地缓存解析. 请注意,初始分辨率仍然通过DHT,因为pubsub中没有消息历史记录. 

发布者和解析器节点都需要启用该功能才能使其有效工作. 

### 如何启用

用你的守护进程运行你的守护进程`--enable-namesys-pubsub`旗;启用pubsub. 

### 成为真正特色的道路

-   [ ] 需要更多人使用并报告其工作情况
-   [ ] 为订阅添加最后一次记录分发的机制,这样我们就不必为了初始解析而点击DHT. 或者,我们可以定期重新发布最后一条记录. 
