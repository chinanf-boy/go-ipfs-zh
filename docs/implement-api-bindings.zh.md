
# IPFS API实现文件

这篇简短的文档旨在为任何为IPFS实现实现API绑定的人提供快速指南 - 特别是go-ipfs. 

部分: 

-   IPFS类型
-   API传输
-   API命令
-   实现HTTP API的绑定

## IPFS类型

IPFS使用一组值类型,可用于预先枚举: 

-   `<ipfs-path>`是unix风格的路径,从一开始`/ipfs/<cid>/...`要么`/ipns/<hash>/...`要么`/ipns/<domain>/...`. 
-   `<hash>`是base58编码[multihash](https://github.com/multiformats/multihash)
-   `cid`是一个[Multibase公司](https://github.com/multiformats/multibase)编码[CID](https://github.com/ipld/cid)- 自描述内容寻址标识符

有关流的说明: IPFS是一种流协议. 关于它的一切都可以流式传输. 导入文件时,API请求应旨在流入数据并正确处理背压,以便IPFS节点可以顺序处理它而不会有太大的内存压力.  (如果使用HTTP,通常会通过写入请求主体阻止来处理此问题. ) 

## API传输

与其他所有内容一样,IPFS旨在灵活地处理API传输. 目前,[去-IPF问题](https://github.com/ipfs/go-ipfs)实现支持进程内API和HTTP API. 通过在传输上映射API函数,可以轻松添加更多内容.  (这类似于gRPC也是如此*映射在传输之上*,像HTTP) . 

映射到传输涉及利用传输的功能来表达函数调用. 例如: 

#### CLI API传输

在命令行中,IPFS使用传统的标志和基于arg的映射,其中: 

-   第一个参数选择命令,如在git中 - 例如`ipfs object get`
-   标志指定选项 - 例如`--enc=protobuf -q`
-   其余的是位置论证 - 例如`ipfs object patch <hash1> add-linkfoo <hash2>`
-   文件由filename或stdin指定

 (注意: 当go-ipfs运行守护进程时,CLI API实际上转换为HTTP调用. 否则,它们在同一进程中执行) HTTP API传输

#### 在HTTP中,我们的API分层使用类似REST的映射,其中: 

URL路径选择命令 - 例如

-   URL查询字符串实现选项参数 - 例如`/object/get`
-   URL查询还实现位置参数 - 例如`&enc=protobuf&q=true`
-   请求体流文件数据 - 读取文件或stdin`&arg=<hash1>&arg=add-link&arg=foo&arg=<hash2>`
-   多个流与多部分复用 (todo: 添加tar流支持) 
    -   API命令

## 有一个"标准IPFS API",当前定义为"go-ipfs实现所公开的所有命令". 

有自动生成API文档[. ](https://ipfs.io/docs/api/)你也可以看看[在这里列出](https://git.io/v5KG1),或通过运行获取命令列表`ipfs commands`本地. 

## 实现HTTP API的绑定

如上所述,API命令映射到HTTP\: 

-   URL路径选择命令 - 例如`/object/get`
-   URL查询字符串实现选项参数 - 例如`&enc=protobuf&q=true`
-   URL查询还实现位置参数 - 例如`&arg=<hash1>&arg=add-link&arg=foo&arg=<hash2>`
-   请求体流文件数据 - 读取文件或stdin
    -   多个流与多部分复用 (todo: 添加tar流支持) 

到目前为止,我们有两个不同的HTTP API客户端: 

-   [JS-IPF问题-API](https://github.com/ipfs/js-ipfs-api)- 简单的javascript包装 - 最好看
-   [去-IPF问题/命令/ HTTP](https://git.io/v5KnB)- 基于的广义运输[命令定义](https://git.io/v5KnE)

Go实现很适合回答更难的问题,例如如何处理多部分,或者在边缘条件下应该设置哪些标题. 但是javascript实现非常简洁,易于遵循. 

#### node-ipfs-api的剖析

目前,node-ipfs-api有三个主要文件

-   [SRC / index.js](https://git.io/v5Kn2)定义API模块的客户端将使用的函数. 使用`RequestAPI`,几乎直接将函数调用参数转换为API. 
-   [SRC / GET-文件 -  stream.js](https://git.io/v5Knr)实现最难的部分: 文件流. 这个使用multipart. 
-   [SRC /请求api.js](https://git.io/v5KnP)泛型函数调用来执行实际的HTTP请求

## 关于multipart +检查请求的注意事项

尽管上面已经说过所有的概括,但IPFS API实际上非常简单. 您可以检查所有请求`nc`和`--api`选项 (截至[这个公关](https://github.com/ipfs/go-ipfs/pull/1598), 要么`0.3.8`) : 

    > nc -l 5002 &
    > ipfs --api /ip4/127.0.0.1/tcp/5002 swarm addrs local --enc=json
    POST /api/v0/version?enc=json&stream-channels=true HTTP/1.1
    Host: 127.0.0.1:5002
    User-Agent: /go-ipfs/0.3.8/
    Content-Length: 0
    Content-Type: application/octet-stream
    Accept-Encoding: gzip

唯一困难的部分是让文件流正确.  (现在) 使用multipart将文件流式传输到go-ipfs相当容易. 基本上,我们最终得到这样的HTTP请求: 

    > nc -l 5002 &
    > ipfs --api /ip4/127.0.0.1/tcp/5002 add -r ~/demo/basic/test
    POST /api/v0/add?encoding=json&progress=true&r=true&stream-channels=true HTTP/1.1
    Host: 127.0.0.1:5002
    User-Agent: /go-ipfs/0.3.8/
    Transfer-Encoding: chunked
    Content-Disposition: form-data: name="files"
    Content-Type: multipart/form-data; boundary=2186ef15d8f2c4f100af72d6d345afe36a4d17ef11264ec5b8ec4436447f
    Accept-Encoding: gzip

    1
    -
    e5
    -2186ef15d8f2c4f100af72d6d345afe36a4d17ef11264ec5b8ec4436447f
    Content-Disposition: form-data; name="file"; filename="test"
    Content-Type: multipart/mixed; boundary=acdb172fe12f25e8ffae9981ce6f4580abdefb0cae3ceebe464d802866be


    9c
    --acdb172fe12f25e8ffae9981ce6f4580abdefb0cae3ceebe464d802866be
    Content-Disposition: file; filename="test%2Fbar"
    Content-Type: application/octet-stream


    4
    bar

    dc

    --acdb172fe12f25e8ffae9981ce6f4580abdefb0cae3ceebe464d802866be
    Content-Disposition: file; filename="test%2Fbaz"
    Content-Type: multipart/mixed; boundary=2799ac77a72ef7b8a0281945806b9f9a28f7681145aa8e91b052d599b2dd


    a0
    --2799ac77a72ef7b8a0281945806b9f9a28f7681145aa8e91b052d599b2dd
    Content-Type: application/octet-stream
    Content-Disposition: file; filename="test%2Fbaz%2Fb"


    4
    bar

    a2

    --2799ac77a72ef7b8a0281945806b9f9a28f7681145aa8e91b052d599b2dd
    Content-Disposition: file; filename="test%2Fbaz%2Ff"
    Content-Type: application/octet-stream


    4
    foo

    44

    --2799ac77a72ef7b8a0281945806b9f9a28f7681145aa8e91b052d599b2dd--

    9e

    --acdb172fe12f25e8ffae9981ce6f4580abdefb0cae3ceebe464d802866be
    Content-Disposition: file; filename="test%2Ffoo"
    Content-Type: application/octet-stream


    4
    foo

    44

    --acdb172fe12f25e8ffae9981ce6f4580abdefb0cae3ceebe464d802866be--

    44

    --2186ef15d8f2c4f100af72d6d345afe36a4d17ef11264ec5b8ec4436447f--

    0

哪个产生: <http://gateway.ipfs.io/ipfs/QmNtpA5TBNqHrKf3cLQ1AiUKXiE4JmUodbG5gXrajg8wdv>
