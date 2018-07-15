
# IPFS API实现文档

这篇简短的文档旨在为任何想知道 api-绑定的实现,特别是go-ipfs{ipfs的主要实现软件}的人们. 

章节:

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [IPFS API实现文档](#ipfs-api%E5%AE%9E%E7%8E%B0%E6%96%87%E6%A1%A3)
  - [IPFS类型](#ipfs%E7%B1%BB%E5%9E%8B)
  - [API传输](#api%E4%BC%A0%E8%BE%93)
      - [API传输的CLI](#api%E4%BC%A0%E8%BE%93%E7%9A%84cli)
      - [HTTP API传输](#http-api%E4%BC%A0%E8%BE%93)
  - [API命令](#api%E5%91%BD%E4%BB%A4)
  - [实现 HTTP API的绑定](#%E5%AE%9E%E7%8E%B0-http-api%E7%9A%84%E7%BB%91%E5%AE%9A)
      - [node-ipfs-api的剖析](#node-ipfs-api%E7%9A%84%E5%89%96%E6%9E%90)
  - [关于 multipart + 检查 请求 的注意事项](#%E5%85%B3%E4%BA%8E-multipart--%E6%A3%80%E6%9F%A5-%E8%AF%B7%E6%B1%82-%E7%9A%84%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## IPFS类型

IPFS使用一组 `set`值类型,可用于预先枚举: 

-   `<ipfs-path>`是 unix风格 的路径,从一开始`/ipfs/<cid>/...`要么`/ipns/<hash>/...`要么`/ipns/<domain>/...`. 
-   `<hash>`是 base58 编码[multihash](https://github.com/multiformats/multihash)
-   `cid`是一个[Multibase](https://github.com/multiformats/multibase)编码[CID](https://github.com/ipld/cid)- 自描述内容寻址标识符

有关流的说明: IPFS是一种流协议. 关于它的一切都可以流式传输. 导入文件时,API请求,应旨在流入数据,并正确处理`背压-back-pressure`,以便 IPFS节点可以顺序处理它而不会有太大的内存压力.  (如果使用HTTP,通常会,通过写入请求主体堵塞来处理此问题. ) 

## API传输

与其他所有内容一样,IPFS 旨在灵活地处理API传输. 目前,[go-ipfs](https://github.com/ipfs/go-ipfs)实现支持 进程内API 和 HTTP API. 通过在传输上 映射API函数,可以轻松添加更多内容.  (这类似于 gRPC 也是如此*映射在传输之上*,像 HTTP) . 

映射到传输涉及利用 传输的功能 来表达函数调用. 例如: 

#### API传输的CLI

在命令行中,IPFS使用 传统的flag 和 基于arg 的映射,其中: 

-   第一个参数选择命令,如在 git 中 - 例如`ipfs object get`
-   flag指定选项 - 例如`--enc=protobuf -q`
-   其余的是位置参数 - 例如`ipfs object patch <hash1> add-linkfoo <hash2>`
-   文件由 filename 或 stdin 指定

 (注意: 当 go-ipfs 运行守护进程时,CLI API实际上转换为 HTTP调用. 否则,它们在同一进程中执行) 

#### HTTP API传输

在HTTP中,我们的 API分层 使用类似 REST的映射,其中: 

-   URL路径选择命令 - 例如:`/object/get`
-   URL查询字符串 实现 选项参数 - 例如:`&enc=protobuf&q=true`
-   URL查询 还实现 位置参数 - 例如:`&arg=<hash1>&arg=add-link&arg=foo&arg=<hash2>`
-   请求主体流文件数据 - 读取文件 或 stdin
    -   多个流与多部分复用 (todo: 添加 tar流 支持) 
    

## API命令

这是"标准IPFS API",当前定义为"go-ipfs实现所公开的所有命令". 
有自动生成[API 文档](https://ipfs.io/docs/api/),你也可以看看[在这里列出](https://git.io/v5KG1),或通过运行`ipfs commands`获取命令列表. 

## 实现 HTTP API的绑定

如上所述,API命令映射到HTTP: 

-   URL路径 选择 命令 - 例如`/object/get`
-   URL查询字符串 实现 选项参数 - 例如`&enc=protobuf&q=true`
-   URL查询 还实现 位置参数 - 例如`&arg=<hash1>&arg=add-link&arg=foo&arg=<hash2>`
-   请求主体流文件数据 - 读取文件 或 stdin
    -   多个流与多部分复用 (todo: 添加tar流支持) 

到目前为止,我们有两个不同的 HTTP API客户端: 

-   [js-ipfs-API](https://github.com/ipfs/js-ipfs-api)- 简单的javascript包装 - 最好看
-   [go-ipfs/commands/http](https://git.io/v5KnB)- 基于[命令定义](https://git.io/v5KnE)的常见传输

Go实现很适合回答更难的问题,例如如何处理 **多部分**,或者在边缘条件下应该设置哪些标题. 但是 javascript实现也非常简洁,易于遵循. 

#### node-ipfs-api的剖析

目前,node-ipfs-api有三个主要文件

- [src/index.js](https://git.io/v5Kn2)定义API模块的客户端将使用的函数. 使用`RequestAPI`,几乎直接将 函数调用参数 转换为API. 
- [src/get-files-stream.js](https://git.io/v5Knr)实现最难的部分: 文件流. 这个使用 multipart. 
- [src/request-api.js](https://git.io/v5KnP)泛型函数调用 来执行实际的 HTTP请求

## 关于 multipart + 检查 请求 的注意事项

尽管上面已经说过所有的概括,但 IPFS API 实际上非常简单. 您可以检查所有请求带`nc`和`--api`选项 (截至[这个PR](https://github.com/ipfs/go-ipfs/pull/1598), 要么`0.3.8`) : 

    > nc -l 5002 &
    > ipfs --api /ip4/127.0.0.1/tcp/5002 swarm addrs local --enc=json
    POST /api/v0/version?enc=json&stream-channels=true HTTP/1.1
    Host: 127.0.0.1:5002
    User-Agent: /go-ipfs/0.3.8/
    Content-Length: 0
    Content-Type: application/octet-stream
    Accept-Encoding: gzip

唯一困难的部分是让文件流正确.  (现在) 使用 multipart 将文件流式传输到go-ipfs 相当容易. 基本上,我们最终得到这样的HTTP请求: 

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

是在这里产生的: <http://gateway.ipfs.io/ipfs/QmNtpA5TBNqHrKf3cLQ1AiUKXiE4JmUodbG5gXrajg8wdv>
