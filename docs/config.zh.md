# go-ipfs 配置文件

go-ipfs 配置文件是一个 json 文档. 它在节点实例化时 读取一次,用于脱机命令或 启动守护程序. 在正在运行的守护程序上执行的命令不会在 **运行时** 读取配置文件.

#### 配置选项

配置文件允许快速调整配置. 配置文件可以应用`--profile`选项到`ipfs init`或者`ipfs config profile apply`命令. 应用配置文件时,将在\$ IPFS_PATH 中创建配置文件的备份

可用配置:

- `server`

  建议用于具有公共 IPv4 地址 (服务器,VPS 等) 的节点,禁用本地网络中的主机和内容暴露.

- `local-discovery`

  设置为默认,受`server`配置影响,在本地网络中启用发现.

- `test`

  减少外部干扰,对于在测试环境中运行 ipfs 非常有用. 请注意,使用这些设置,如果没有手动引导,节点将 无法与网络的其余部分 通信.

- `default-networking`

  恢复默认网络设置. 与`test`配置相反.

- `badgerds`

  用 实验性 badger 数据存储 替换 默认数据存储配置. 如果你运行`ipfs init`之后想应用新的存储,您会需要将数据存储转换为新配置. 你可以这样做[IPF 问题-DS-转换](https://github.com/ipfs/ipfs-ds-convert)

  警告: badger 数据存储区是实验性的. 确保经常备份您的数据.

- `default-datastore`

  恢复默认数据存储配置.

- `lowpower`

  减少系统上的守护进程开销. 可能会影响节点功能,内容发现和数据提取的性能可能会降低.

## 目录

- [`Addresses`](#addresses)
- [`API`](#api)
- [`Bootstrap`](#bootstrap)
- [`Datastore`](#datastore)
- [`Discovery`](#discovery)
- [`Gateway`](#gateway)
- [`Identity`](#identity)
- [`Ipns`](#ipns)
- [`Mounts`](#mounts)
- [`Reprovider`](#reprovider)
- [`Swarm`](#swarm)

## `Addresses`

包含有关此节点要使用的各种侦听器地址的信息.

- `API`

多地址 描述了为本地 HTTP API 提供服务的地址.

默认: `/ip4/127.0.0.1/tcp/5001`

- `Gateway`

Multiaddr 描述为本地网关提供服务的地址.

默认: `/ip4/127.0.0.1/tcp/8080`

- `Swarm`

多地址的数组,描述要 监听 p2p 群连接 的地址.

默认:

```json
["/ip4/0.0.0.0/tcp/4001", "/ip6/::/tcp/4001"]
```

- `Announce`

如果非空,数组指定要向 网络通告的 群地址. 如果为空,守护程序将通知 推测的群集地址.

默认: `[]`

- `NoAnnounce`

群集地址不向网络通告.

默认: `[]`

## `API`

包含 API 网关使用的信息.

- `HTTPHeaders`

要在 API HTTP 服务器的响应中设置的 HTTP 标头的映射.

例:

```json
{
  "Foo": ["bar"]
}
```

默认: `null`

## `Bootstrap`

Bootstrap 是 多个可信节点的数组,用于连接以启动与网络的连接.

默认值: ipfs.io 引导程序节点

## `Datastore`

包含与磁盘存储系统的构造和操作相关的信息.

- `StorageMax`

ipfs 存储库数据存储区大小的软上限. 同`StorageGCWatermark`,用于计算是否触发 gc 运行 (仅当`--enable-gc`标志设置) .

默认: `10GB`

- `StorageGCWatermark`

如果守护程序启用带有 自动 gc 的情况下运行,则会自动触发垃圾收集的`StorageMax`百分比值 (该选项当前默认为 false) .

默认: `90`

- `GCPeriod`

持续时间,指定运行垃圾回收的频率. 仅在启用 自动 gc 时使用.

默认: `1h`

- `HashOnRead`

布尔值. 如果设置为 true,则将对磁盘上的所有块读取 进行散列和验证. 这将导致 CPU 使用率增加.

- `BloomFilterSize`

一个数字,表示 blockstore 的 [bloom 过滤器](https://en.wikipedia.org/wiki/Bloom_filter)的大小 (以字节为单位)。 值为零表示要禁用的功能。

这个网站<https://hur.st/bloomfilter/?n=1e6&p=0.01&m=&k=7> 为各种 bloom 过滤器值生成有用的图样:  
你可以用它来找到最佳的首选值, 这里(进入网站)的 `m` 是 比特单位的`BloomFilterSize`。 记得转换 比特单位 的 `m`, 到 字节量，让它能成为配置文件中的`BloomFilterSize`。
例如, 对于 1,000,000 blocks, 预期的误报率为`1%`, 你最终会得到 9592955 比特单位 的过滤器大小, 所以对于 `BloomFilterSize` 我们就使用到了 1199120 字节.。
在写这文档时, 共有[7 种 hash 函数](https://github.com/ipfs/go-ipfs-blockstore/blob/547442836ade055cc114b562a3cc193d4e57c884/caching.go#L22) 被使用, 所以常量 `k` 为 7 (在公式中)。

默认: `0`

- `Spec`

Spec 定义了 ipfs 数据存储区的结构. 它是一个可组合的结构,其中每个数据存储区由 json 对象 表示. 数据存储可以包装 其他数据存储 以提供额外的功能 (例如,度量-metrics,日志记录-logging 或 缓存-caching) .

这可以手动更改,但是,如果您进行任何需要不同磁盘结构的更改,则需要运行[ipfs-ds-convert 工具](https://github.com/ipfs/ipfs-ds-convert)将数据迁移到新结构中.

有关此配置选项的可能值的更多信息,请参阅 [docs/datastores.zh.md](./datastores.zh.md)

默认:

    {
      "mounts": [
    	{
    	  "child": {
    		"path": "blocks",
    		"shardFunc": "/repo/flatfs/shard/v1/next-to-last/2",
    		"sync": true,
    		"type": "flatfs"
    	  },
    	  "mountpoint": "/blocks",
    	  "prefix": "flatfs.datastore",
    	  "type": "measure"
    	},
    	{
    	  "child": {
    		"compression": "none",
    		"path": "datastore",
    		"type": "levelds"
    	  },
    	  "mountpoint": "/",
    	  "prefix": "leveldb.datastore",
    	  "type": "measure"
    	}
      ],
      "type": "mount"
    }

## `Discovery`

包含用于配置 ipfs 节点发现机制的选项.

- `MDNS` 多播 dns 对等点发现的选项.

- `Enabled`


    mdns是否应处于活动状态的布尔值.

    默认: `true`

    -   `Interval`在发现检查之间等待的秒数.

- `Routing`

内容路由模式. 可以用守护进程覆盖`--routing`选项. 有效模式是:

- `dht` (默认)
  - `dhtclient`
  - `none`

## `Gateway`

HTTP 网关的选项.

- `HTTPHeaders`用于设置网关响应的标头.

默认:

```json
{
  "Access-Control-Allow-Headers": ["X-Requested-With"],
  "Access-Control-Allow-Methods": ["GET"],
  "Access-Control-Allow-Origin": ["*"]
}
```

- `RootRedirect`

用于重定向请求的网址`/`.

默认: `""`

- `Writeable`

一个布尔值,用于配置网关是否可写.

默认: `false`

- `PathPrefixes`
  TODO

默认: `[]`

## `Identity`

- `PeerID`

唯一 PKI 身份标签. 在 init 上设置并且永远不会读取,它仅仅是为了方便起见. Ipfs 将始终在运行时从 其密钥对 生成 peerID.

- `PrivKey`

base64 编码的 protobuf 描述 (和包含) 节点私钥.

## `Ipns`

- `RepublishPeriod`

持续时间,指定重新发布 ipns 记录的频率,以确保它们在网络上保持新鲜. 如果未设置,我们默认为 4 小时.

- `RecordLifetime`

一个持续时间,指定要在 ipns 记录上设置的有效生命周期的值. 如果未设置,我们默认为 24 小时.

- `ResolveCacheSize`

要在已解析的 ipns 条目的 LRU 高速缓存中存储的条目数. 参赛作品将保持缓存状态,直到其生命周期结束.

默认: `128`

## `Mounts`

FUSE 安装位置-Mountpoint 配置选项.

- `IPFS` Mountpoint for`/ipfs/`.

- `IPNS` Mountpoint for`/ipns/`.

- `FuseAllowOther`在挂载点上设置 FUSE 允许其他选项.

## `Reprovider`

- `Interval`设置将 本地内容 重新提交到 路由系统 的轮次之间的时间. 如果未设置,则默认为 12 小时. 如果设置为该值`"0"`它将禁用 内容提取.

注意: 禁用内容重新生成 将 导致网络上的 其他节点无法发现 您拥有自己拥有的对象. 如果您希望 禁用此功能 并让 网络了解您拥有的内容,则必须定期 手动发布您的内容.

- `Strategy`告诉 `reprovider` 应该发布什么. 有效的策略是:
  - "all" (默认) - 发布所有存储的数据
  - "pinned" - 仅发布固定数据
  - "root" - 只发布 直接固定 keys 和递归-recursive 固定的管理员 keys

## `Swarm`

配置群的选项.

- `AddrFilters` 一组地址过滤器 (multiaddr netmasks) ,用于过滤拨号. 看到[这个问题](https://github.com/ipfs/go-ipfs/issues/1226#issuecomment-120494604)了解更多信息.

- `DisableBandwidthMetrics`布尔值,设置为 true 时,将导致 ipfs 无法跟踪 带宽指标. 禁用带宽指标可以显着提高性能,并减少内存使用量.

- `DisableNatPortMap`禁用 NAT 发现.

- `DisableRelay`禁用 p2p 电路 传播传输.

- `EnableRelayHop`为节点启用 HOP 传输. 如果启用此选项,则节点将 充当连接对等体 的 传播电路 中的中间 (Hop Relay) 节点.

### `ConnMgr`

连接管理器 配置.

- `Type`

设置要使用的 连接管理器 的类型,选项包括: `"none"`和`"basic"`.

- `LowWater`

LowWater 是要维护的最小连接数.

- `HighWater`

HighWater 是连接数,当超过时,将触发 连接 GC 操作.

- `GracePeriod`

GracePeriod 是 新连接 不受连接管理器关闭的 持续时间.
