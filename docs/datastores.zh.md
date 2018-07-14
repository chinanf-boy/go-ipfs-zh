
# 数据存储配置选项

本文档描述了ipfs配置文件中的`Datastore.Spec`字段不同的值. 

## flatfs

将每个键值对存储 为文件系统上的文件. 

shardFunc-碎片 的前缀是`/repo/flatfs/shard/v1`,然后是分片策略的描述符. 一些示例值是: 

-   `/repo/flatfs/shard/v1/next-to-last/2`
    -   密钥的最后两个字符旁边的碎片
-   `/repo/flatfs/shard/v1/prefix/2`
    -   密钥的两个字符前缀的碎片

```json
{
	"type": "flatfs",
	"path": "<relative path within repo for flatfs root>",
	"shardFunc": "<a descriptor of the sharding scheme>",
	"sync": true|false
}
```

注意: flatfs 仅用作 块存储 (安装在`/blocks`) 作为当前的实现尚未完成. 

## levelds

使用 leveldb 数据库 存储键值对. 

```json
{
	"type": "levelds",
	"path": "<location of db inside repo>",
	"compression": "none" | "snappy",
}
```

## badgerds

使用[badger](https://github.com/dgraph-io/badger)作为一个键值存储. 

```json
{
	"type": "badgerds",
	"path": "<location of badger inside repo",
	"syncWrites": true|false
}
```

## 挂载

允许指定的数据存储区 处理 前缀为给定路径的键. 挂载点 将作为子数据存储 定义中的键添加. 

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

## 测量-measure

此数据存储区是一个包装程序,用来添加 跟踪指标 到任何数据存储区. 

```json
{
	"type": "measure",
	"prefix": "sometag.datastore",
	"child": { datastore being wrapped }
}
```
