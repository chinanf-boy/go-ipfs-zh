# 网关

IPFS 网关是传统 Web 浏览器和 IPFS 之间的桥梁.通过网关，用户可以浏览存储在 IPFS 中的文件和网站，就好像它们存储在传统 Web 服务器中一样。

默认情况下，go-ipfs 节点在`http://127.0.0.1:8080/`运行网关。

我们还提供了一个公共网关`https://ipfs.io`。 如果你曾经见过表格(form)中的`https://ipfs.io/ipfs/Qm...`链接，这就是来自*我们的*网关。

## 配置

网关的配置选项(简要地)描述在[config](https://github.com/chinanf-boy/go-ipfs-zh/blob/master/docs/config.zh.md#网关)文档.

## 目录

为了方便起见，网关(大多数)在服务目录的行为，就像普通 Web 服务器:

- 1.  如果目录包含`index.html`文件:

  - 1.  如果路径不以`/`结尾，附加一个`/`重定向。这有助于避免来自不同路径，却重复的内容.<sup>&dagger;</sup>
  - 2. 否则，提供`index.html`文件.

- 2. 动态构建和提供此目录内容的列表.

<sub><sup>&dagger;</sup>如果查询字符串包含一个`go-get=1`参数 ，则重定向会被跳过。见[PR#3964](https://github.com/ipfs/go-ipfs/pull/3963)详情</sub>

## 文件名

在下载文件时，浏览器通常通过查看路径的最后一个字段，来猜测文件的文件名。不幸的是,当一个文件(不含目录)的*直接*链接，最后的字段只是一个 CID(`Qm...`)，而这对用户并不友好。

为了解决这个问题，可以添加一个`filename=some_filename`参数到查询字符串，以显式指定文件名.例如:

> <https://ipfs.io/ipfs/QmfM2r8seH2GiRaC4esTjeraXEachRt8ZsSeGaWTPLyMoG?filename=hello_world.txt>

## MIME 类型

托多

## 只读 API

为了方便起见,网关暴露了只读(read-only) API。此只读 API 暴露了一个普通 API 的只读"安全"的子集.

例如,您使用此来下载块:

```
> curl https://ipfs.io/api/v0/block/get/zb2rhi36Gc9GJWijLEL6zW45MBux5FcFv5gJmjXA7VAMozEXY
```
