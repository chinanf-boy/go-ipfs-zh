
# go-ipfs开发

这是对代码库所在位置的简单描述. 

有多个子包: 

-   `bitswap`- 块交换
-   `blocks`- 处理单个块和分片文件
-   `blockservice`- 处理获取和存储块
-   `cmd/ipfs`-  cli-ipfs工具 - 主要 **入口** 
-   `config`- 加载/编辑 配置
-   `core`- 核心节点,加入所有部分
-   `fuse/readonly`- 载入`/ipfs`,限制为只读文件
-   `importer`- 将文件导入ipfs
-   `merkledag`-  merkle dag 数据结构
-   `path`-  merkledag 数据结构 的 路径解析
-   `peer`- 本地和远程对等体的 身份+地址
-   `routing`- 路由系统
-   `routing/dht`-  DHT 默认路由系统实现
-   `swarm`- 连接多路复用,许多对等和许多传输
-   `util`- 各种公共工具🔧

### 做了什么: 

-   merkle dag 数据结构
-   merkle dag的 路径分辨
-   本地存储块
-   基本文件导入/导出 (`ipfs add`,`ipfs cat`) 
-   安装`/ipfs` (尝试`{cat, ls} /ipfs/<path>`) 
-   多路连接 (tcp atm) 
-   同行寻址
-   dht  -  实现基本kademlia路由
-   bitswap  -  实现基本块交换功能
-   加密 - 在网络中的对等体之间建立信任
-   导入时阻止分裂 - 文件分块指纹[Rabin fingerprints]() 等

### 正在进行的工作: 

-   ipns  -  impl`/ipns` 对象发布+路径解析
-   将对象 暴露给 Web`http://ipfs.io/<path>`

### 下一步是什么: 

-   版本控制 -`commit`喜欢数据结构
-   更多...

## 很酷的演示

一系列努力实现的酷炫演示

-   在ipfs 的镜像中 启动VM
-   在ipfs 的文件系统树中 启动VM
-   从ipfs 直接发布静态网站
-   将对象暴露给 Web`http://ipfs.io/<path>`
-   已载入 自动-committing 版本的个人保管箱
-   已载入的加密 个人/群组 保管箱
-   已载入{npm,apt,其他pkg manager}注册机制
-   在ipfs上打开一个视频,然后将其流入
-   观看视频时, 视频来源拓展为 一个种子 - N个节点传输(N ~100)
-   更多尽在[白皮书中](https://github.com/chinanf-boy/ipfs-tour#1-%E7%99%BD%E7%9A%AE%E4%B9%A6) | 或者 
[ipfs/ipfs 的中文翻译](https://github.com/chinanf-boy/ipfs-zh)
