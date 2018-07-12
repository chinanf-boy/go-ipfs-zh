
# 数据存储配置选项

本文档描述了不同的可能值`Datastore.Spec`ipfs配置文件中的字段. 

## flatfs

将每个键值对存储为文件系统上的文件. 

shardFunc的前缀是`/repo/flatfs/shard/v1`然后是分片策略的描述符. 一些示例值是: 

-   `/repo/flatfs/shard/v1/next-to-last/2`
    -   在密钥的最后两个字符旁边的两个碎片上
-   `/repo/flatfs/shard/v1/prefix/2`
    -   基于密钥的两个字符前缀的碎片

```json
{
	"type": "flatfs",
	"path": "<relative path within repo for flatfs root>",
	"shardFunc": "<a descriptor of the sharding scheme>",
	"sync": true|false
}
```

注意: flatfs应仅用作块存储 (安装在`/blocks`) 因为当前的实施尚未完成. 

## levelds

使用leveldb数据库存储键值对. 

```json
{
	"type": "levelds",
	"path": "<location of db inside repo>",
	"compression": "none" | "snappy",
}
```

## badgerds

用途[獾](https://github.com/dgraph-io/badger)作为一个关键的价值商店. 

```json
{
	"type": "badgerds",
	"path": "<location of badger inside repo",
	"syncWrites": true|false
}
```

## 安装

允许指定的数据存储区处理前缀为给定路径的键. 挂载点将作为子数据存储定义中的键添加. 

```json
{
	"type": "mount",
	"mounts": [
		{
			// Insert other datastore definition here, but add the following key:
			"mountpoint": "/path/to/handle"
		},
		{
			// Insert other datastore definition here, but add the following key:
			"mountpoint": "/path/to/handle"
		},
	]
}
```

## 测量

此数据存储区是一个包装程序,可将指标跟踪添加到任何数据存储区. 

```json
{
	"type": "measure",
	"prefix": "sometag.datastore",
	"child": { datastore being wrapped }
}
```
