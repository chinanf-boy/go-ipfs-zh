
# go-ipfs配置文件

go-ipfs配置文件是一个json文档. 它在节点实例化时读取一次,用于脱机命令或启动守护程序. 在正在运行的守护程序上执行的命令不会在运行时读取配置文件. 

#### 简介

配置文件允许快速调整配置. 配置文件可以应用`--profile`国旗`ipfs init`或者`ipfs config profile apply`命令. 应用配置文件时,将在$ IPFS_PATH中创建配置文件的备份

可用资料: 

-   `server`

    建议用于具有公共IPv4地址 (服务器,VPS等) 的节点,禁用本地网络中的主机和内容发现. 

-   `local-discovery`

    将默认值设置为受影响的字段`server`配置文件,在本地网络中启用发现. 

-   `test`

    减少外部干扰,对于在测试环境中运行ipfs非常有用. 请注意,使用这些设置,如果没有手动引导,节点将无法与网络的其余部分通信. 

-   `default-networking`

    恢复默认网络设置. 逆的轮廓`test`个人资料. 

-   `badgerds`

    用实验性badger数据存储替换默认数据存储配置. 如果您之后应用此配置文件`ipfs init`,您需要将数据存储转换为新配置. 你可以这样做[IPF问题-DS-转换](https://github.com/ipfs/ipfs-ds-convert)

    警告: badger数据存储区是实验性的. 确保经常备份您的数据. 

-   `default-datastore`

    恢复默认数据存储配置. 

-   `lowpower`

    减少系统上的守护进程开销. 可能会影响节点功能,内容发现和数据提取的性能可能会降低. 

## 目录

-   [`Addresses`](#addresses)
-   [`API`](#api)
-   [`Bootstrap`](#bootstrap)
-   [`Datastore`](#datastore)
-   [`Discovery`](#discovery)
-   [`Gateway`](#gateway)
-   [`Identity`](#identity)
-   [`Ipns`](#ipns)
-   [`Mounts`](#mounts)
-   [`Reprovider`](#reprovider)
-   [`Swarm`](#swarm)

## `Addresses`

包含有关此节点要使用的各种侦听器地址的信息. 

-   `API`Multiaddr描述了为本地HTTP API提供服务的地址. 

默认: `/ip4/127.0.0.1/tcp/5001`

-   `Gateway`Multiaddr描述为本地网关提供服务的地址. 

默认: `/ip4/127.0.0.1/tcp/8080`

-   `Swarm`多个数据符的数组,描述要监听p2p群连接的地址. 

默认: 

```json
[
  "/ip4/0.0.0.0/tcp/4001",
  "/ip6/::/tcp/4001"
]
```

-   `Announce`如果非空,则此阵列指定要向网络通告的群地址. 如果为空,守护程序将通知推断的群集地址. 

默认: `[]`

-   `NoAnnounce`群集地址不向网络通告. 

默认: `[]`

## `API`

包含API网关使用的信息. 

-   `HTTPHeaders`要在API HTTP服务器的响应中设置的HTTP标头的映射. 

例: 

```json
{
	"Foo": ["bar"]
}
```

默认: `null`

## `Bootstrap`

Bootstrap是一组可信节点的多个数组,用于连接以启动与网络的连接. 

默认值: ipfs.io引导程序节点

## `Datastore`

包含与磁盘存储系统的构造和操作相关的信息. 

-   `StorageMax`ipfs存储库数据存储区大小的软上限. 同`StorageGCWatermark`,用于计算是否触发gc运行 (仅当`--enable-gc`标志设置) . 

默认: `10GB`

-   `StorageGCWatermark`百分比`StorageMax`如果守护程序在启用自动gc的情况下运行,则会自动触发垃圾收集的值 (该选项当前默认为false) . 

默认: `90`

-   `GCPeriod`持续时间,指定运行垃圾回收的频率. 仅在启用自动gc时使用. 

默认: `1h`

-   `HashOnRead`布尔值. 如果设置为true,则将对磁盘上的所有块读取进行散列和验证. 这将导致CPU利用率增加. 

-   `BloomFilterSize`一个数字,表示blockstore的bloom过滤器的大小 (以字节为单位) . 值为零表示要禁用的功能. 

默认: `0`

-   `Spec`Spec定义了ipfs数据存储区的结构. 它是一个可组合的结构,其中每个数据存储区由json对象表示. 数据存储可以包装其他数据存储以提供额外的功能 (例如,度量,日志记录或缓存) . 

这可以手动更改,但是,如果您进行任何需要不同磁盘结构的更改,则需要运行[ipfs-ds-convert工具](https://github.com/ipfs/ipfs-ds-convert)将数据迁移到新结构中. 

有关此配置选项的可能值的更多信息,请参阅docs / datastores.zh.md

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

包含用于配置ipfs节点发现机制的选项. 

-   `MDNS`多播dns对等点发现的选项. 

    -   `Enabled`mdns是否应处于活动状态的布尔值. 

默认: `true`

-   `Interval`在发现检查之间等待的秒数. 

-   `Routing`内容路由模式. 可以用守护进程覆盖`--routing`旗. 有效模式是: 
    -   `dht` (默认) 
    -   `dhtclient`
    -   `none`

## `Gateway`

HTTP网关的选项. 

-   `HTTPHeaders`用于设置网关响应的标头. 

默认: 

```json
{
	"Access-Control-Allow-Headers": [
		"X-Requested-With"
	],
	"Access-Control-Allow-Methods": [
		"GET"
	],
	"Access-Control-Allow-Origin": [
		"*"
	]
}
```

-   `RootRedirect`用于重定向请求的网址`/`至. 

默认: `""`

-   `Writeable`一个布尔值,用于配置网关是否可写. 

默认: `false`

-   `PathPrefixes`去做

默认: `[]`

## `Identity`

-   `PeerID`这个config同伴的唯一PKI身份标签. 在init上设置并且永远不会读取,它仅仅是为了方便起见. Ipfs将始终在运行时从其密钥对生成peerID. 

-   `PrivKey`base64编码的protobuf描述 (和包含) 节点私钥. 

## `Ipns`

-   `RepublishPeriod`持续时间,指定重新发布ipns记录的频率,以确保它们在网络上保持新鲜. 如果未设置,我们默认为4小时. 

-   `RecordLifetime`一个持续时间,指定要在ipns记录上设置的有效生命周期的值. 如果未设置,我们默认为24小时. 

-   `ResolveCacheSize`要在已解析的ipns条目的LRU高速缓存中存储的条目数. 参赛作品将保持缓存状态,直到其生命周期结束. 

默认: `128`

## `Mounts`

FUSE安装点配置选项. 

-   `IPFS`Mountpoint for`/ipfs/`. 

-   `IPNS`Mountpoint for`/ipns/`. 

-   `FuseAllowOther`在挂载点上设置FUSE allow other选项. 

## `Reprovider`

-   `Interval`设置将本地内容重新提交到路由系统的轮次之间的时间. 如果未设置,则默认为12小时. 如果设置为该值`"0"`它将禁用内容提取. 

注意: 禁用内容重新生成将导致网络上的其他节点无法发现您拥有自己拥有的对象. 如果您希望禁用此功能并让网络了解您拥有的内容,则必须定期手动宣布您的内容. 

-   `Strategy`告诉reprovider应该宣布什么. 有效的策略是: 
    -   "all" (默认)  - 宣布所有存储的数据
    -   "固定" - 仅发布固定数据
    -   "root" - 只宣布递归引脚的直接固定键和根键

## `Swarm`

配置群的选项. 

-   `AddrFilters`一组地址过滤器 (multiaddr netmasks) ,用于过滤拨号. 看到[这个问题](https://github.com/ipfs/go-ipfs/issues/1226#issuecomment-120494604)了解更多信息. 

-   `DisableBandwidthMetrics`布尔值,设置为true时,将导致ipfs无法跟踪带宽指标. 禁用带宽指标可以显着提高性能,并减少内存使用量. 

-   `DisableNatPortMap`禁用NAT发现. 

-   `DisableRelay`禁用p2p电路中继传输. 

-   `EnableRelayHop`为节点启用HOP中继. 如果启用此选项,则节点将充当连接对等体的中继电路中的中间 (Hop Relay) 节点. 

### `ConnMgr`

连接管理器配置. 

-   `Type`设置要使用的连接管理器的类型,选项包括: `"none"`和`"basic"`. 

-   `LowWater`LowWater是要维护的最小连接数. 

-   `HighWater`HighWater是连接数,当超过时,将触发连接GC操作. 
-   `GracePeriod`GracePeriod是新连接不受连接管理器关闭的持续时间. 
