# 使用 ipfs 传输文件

本文档是帮助解决使用 ipfs 在两台计算机之间传输文件的问题的指南.

## 文件传输

首先,确保 ipfs 在两台计算机上运行. 要验证,请运行`ipfs id`在每台机器上检查是否`Addresses`字段中有内容. 如果它说`null`,那么您的节点不在线,您将需要运行`ipfs daemon`.

现在,用例是: 您要传输节点"A"的文件和 要将文件传输到节点"B"的节点. 在节点 A 上,使用以下命令`ipfs add`将文件添加到 ipfs. 这将打印出您添加的内容的多个哈希. 现在,在节点 B 上,您可以使用获取内容`ipfs get <hash>`.

> 如果是文件夹,文件夹的哈希和文件夹内文件的哈希是不同的

    # On A
    > ipfs add myfile.txt
    added QmZJ1xT1T9KYkHhgRhbv8D7mYrbemaXwYUkg7CeHdrk1Ye myfile.txt

    # On B
    > ipfs get QmZJ1xT1T9KYkHhgRhbv8D7mYrbemaXwYUkg7CeHdrk1Ye
    Saving file(s) to QmZJ1xT1T9KYkHhgRhbv8D7mYrbemaXwYUkg7CeHdrk1Ye
     13 B / 13 B [=====================================================] 100.00% 1s

如果有效,并下载了文件,那么恭喜! 您刚刚使用 ipfs 在互联网上移动文件!但是,如果那样的话`ipfs get`命令停滞的,没有输出,那么继续往下看.

## 故障排除

所以你的 ipfs 文件传输似乎无法正常工作. 发生这种情况的主要原因是 节点 B 无法弄清楚如何连接到 节点 A,或者 节点 B 甚至不知道它必须连接到 节点 A.

### 检查现有连接

首先要做的是仔细检查两个节点实际上是在运行 还是 在线运行. 为此,请运行`ipfs id`在每台机器上. 如果两个节点都显示某些地址 (如下例所示) ,那么您的节点就在线了.

```json
{
  "ID": "QmTNwsFkLAed15kQEC1ZJWPfoNbBQnMFojfJKQ9sZj1dk8",
  "PublicKey": "CAASpgIwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQDZb6znj3LQZKP1+X81exf+vbnqNCMtHjZ5RKTCm7Fytnfe+AI1fhs9YbZdkgFkM1HLxmIOLQj2bMXPIGxUM+EnewN8tWurx4B3+lR/LWNwNYcCFL+jF2ltc6SE6BC8kMLEZd4zidOLPZ8lIRpd0x3qmsjhGefuRwrKeKlR4tQ3C76ziOms47uLdiVVkl5LyJ5+mn4rXOjNKt/oy2O4m1St7X7/yNt8qQgYsPfe/hCOywxCEIHEkqmil+vn7bu4RpAtsUzCcBDoLUIWuU3i6qfytD05hP8Clo+at+l//ctjMxylf3IQ5qyP+yfvazk+WHcsB0tWueEmiU5P2nfUUIR3AgMBAAE=",
  "Addresses": [
    "/ip4/127.0.0.1/tcp/4001/ipfs/QmTNwsFkLAed15kQEC1ZJWPfoNbBQnMFojfJKQ9sZj1dk8",
    "/ip4/192.168.2.131/tcp/4001/ipfs/QmTNwsFkLAed15kQEC1ZJWPfoNbBQnMFojfJKQ9sZj1dk8"
  ],
  "AgentVersion": "go-ipfs/0.4.11-dev/",
  "ProtocolVersion": "ipfs/0.1.0"
}
```

接下来,检查节点是否彼此连接. 你可以通过运行`ipfs swarm peers`在一个节点上来做到这一点,并检查输出中的其他对等节点 ID. 如果是两个节点*是*连接,和`ipfs get`命令仍然悬挂,然后出现意外情况,我建议提交一个问题. 如果它们没有连接,那么让我们尝试调试原因. (注意: 如果您只是想要工作,可以通过'手动将节点 A 连接到节点 B'. 完成调试过程,并报告 IRC 上 ipfs 团队 情况有助于我们理解人们常遇的常见陷阱)

### 检查供应商

在 ipfs 上请求内容时,节点会在 DHT 中搜索"提供者记录{provider records}",以查看谁拥有哪些内容. 让我们在 节点 B 上 手动执行此操作,以确保节点 B 能够确定节点 A 具有数据. 运行`ipfs dht findprovs <hash>`. 我们希望看到 节点 A 的 对等 ID 打印出来. 如果此命令 不返回任何内容 (或返回不是 节点 A 的 ID) ,则网络上不存在具有该数据 A 的记录. 如果在节点 A 没有运行守护程序的情况下 添加数据,则会发生这种情况. 如果发生这种情况,您可以在节点 A 上, 运行`ipfs dht provide <hash>` 向网络 **手动提供** 通知您 有该哈希值. 然后,如果你重新启动`ipfs get`命令,节点 B 现在应该能够告诉你 节点 A 具有的内容. 如果节点 A 的对等 ID 出现在初次使用`findprovs`时或 **手动提供**哈希 **没有解决**问题,那么节点 B 很可能 无法连接到节点 A.

### 检查地址

在 节点 B 不能简单地形成到节点 A 的连接的情况下,尽管知道它需要,但可能的罪魁祸首是 坏了的 NAT. 当节点 B 获知它需要连接到 节点 A 时,它检查 DHT 以查找节点 A 的地址,然后开始尝试连接它们. 我们可以通过运行`ipfs dht findpeer <node A peerID>`在节点 B 上检查这些地址. 此命令应返回 节点 A 的地址列表. 如果它没有返回任何地址,那么您应该尝试运行前面步骤中的 **手动提供** 命令. 地址输出示例可能如下所示:

    /ip4/127.0.0.1/tcp/4001
    /ip4/192.168.2.133/tcp/4001
    /ip4/88.157.217.196/tcp/63674

在这种情况下,我们可以看到 localhost (127.0.0.1) 地址,一个 LAN 地址 (192.168._._ ) 和另一个地址. 如果 此第三个地址与您的外部 IP 匹配,则 网络知道 您的节点 的有效外部地址. 此时,可以安全地假设您的节点难以遍历 NAT 情况. 如果是这种情况,您可以尝试在节点 A 的路由器上启用 `UPnP或NAT-PMP`,然后重试该过程. 否则,您可以尝试手动将节点 A 连接到节点 B.

### 手动将节点 A 连接到 B

在节点 B 上运行`ipfs id`,并获取其中一个 包含其公共 IP 地址的 multiaddrs,然后 在节点 A 上运行`ipfs swarm connect <multiaddr>`,您还可以尝试使用中继连接,以获取更多信息[阅读本文档](./experimental-features.zh.md#circuit-relay). 仍然\*不起作用,那么你应该加入 IRC 并在那里寻求帮助,或者在 github 上提出问题.

如果这个手动步骤*没有*工作,或者你可能有 NAT 遍历 的问题,ipfs 无法弄清楚如何联通. 请向我们报告此类情况,以便我们可以修复它们.
