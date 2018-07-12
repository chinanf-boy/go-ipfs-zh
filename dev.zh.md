
# go-ipfs开发

这是对代码库所在位置的简单描述. 

有多个子包: 

-   `bitswap`- 块交换
-   `blocks`- 处理单个块和分片文件的句柄
-   `blockservice`- 处理获取和存储块
-   `cmd/ipfs`-  cli ipfs工具 - 主要**入口点**自动取款机
-   `config`- 加载/编辑配置
-   `core`- 核心节点,加入所有部分
-   `fuse/readonly`- 坐骑`/ipfs`作为只读保险丝fs
-   `importer`- 将文件导入ipfs
-   `merkledag`-  merkle dag数据结构
-   `path`-  merkledag数据结构的路径解析
-   `peer`- 本地和远程对等体的身份+地址
-   `routing`- 路由系统
-   `routing/dht`-  DHT默认路由系统实现
-   `swarm`- 连接多路复用,许多对等和许多传输
-   `util`- 各种公用事业

### 做了什么: 

-   merkle dag数据结构
-   merkle dag的路径分辨率
-   本地存储块
-   基本文件导入/导出 (`ipfs add`,`ipfs cat`) 
-   安装`/ipfs` (尝试`{cat, ls} /ipfs/<path>`) 
-   多路连接 (tcp atm) 
-   同行寻址
-   dht  -  impl基本kademlia路由
-   bitswap  -  impl基本块交换功能
-   加密 - 在网络中的对等体之间建立信任
-   导入时阻止分裂 - 拉宾指纹等

### 正在进行的工作: 

-   ipns  -  impl`/ipns`obj发布+路径解析
-   将对象暴露给Web`http://ipfs.io/<path>`

### 下一步是什么: 

-   版本控制 -`commit`喜欢数据结构
-   更多...

## 很酷的演示

一系列努力实现的酷炫演示

-   从ipfs中的映像启动VM
-   从ipfs中的文件系统树启动VM
-   直接从ipfs发布静态网站
-   将对象暴露给Web`http://ipfs.io/<path>`
-   已安装自动提交版本的个人保管箱
-   已安装的加密个人/群组保管箱
-   挂载{npm,apt,其他pkg manager}注册表
-   在ipfs上打开一个视频,然后将其流入
-   观看拓扑为1种子N leechers (N~100) 的视频
-   更多在3.8节中[纸](https://github.com/ipfs/ipfs/blob/master/papers/ipfs-cap2pfs/ipfs-p2p-file-system.pdf)
