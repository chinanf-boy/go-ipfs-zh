# 帮助

go-ipfs是MIT许可的开源软件. 我们欢迎大大小小的贡献! 看看[社区贡献笔记](https://github.com/ipfs/community/blob/master/contributing.zh.md)吧. 

请务必先查看[问题](https://github.com/ipfs/go-ipfs/issues). 在报告内容之前搜索已关闭的内容,并且 (如果可以!) 帮助我们解决 open 中的问题. 

请注意,go-ipfs问题仅适用于 错误报告和可操作功能. 检查[关于报告问题的IPFS社区指南](https://github.com/ipfs/community/blob/master/contributing.zh.md#reporting-issues),如果您的问题不适合作为错误报告或可操作的功能,还有如果您不确定如何在这里提出问题,请查看我们的[关于开放问题的指南](https://github.com/ipfs/go-ipfs/blob/master/docs/github-issue-guide.zh.md)

如果您正在寻求帮助,请前往[船长的日志](https://github.com/ipfs/go-ipfs/issues/2247)并尝试从那里找到一个问题. 

## 行动指南: 

请看,并查看符合我们的要求的[贡献指南](https://github.com/ipfs/community/blob/master/go-code-guidelines.zh.md). 

## 一般准则: 

-   见[dev伪路线图](dev.zh.md). 
-   请遵守描述的协议[主ipfs repo](https://github.com/ipfs/ipfs)和[规范](https://github.com/ipfs/specs) (WIP) . 
-   即使在主存储库上工作,也请创建分支和 pull-request. 
-   提问或谈论事情在[问题](https://github.com/ipfs/go-ipfs/issues)或freenode上的#ipfs. 
-   确保您能够做出贡献 (没有法律问题 - 但我们可能会设置CLA) . 
-   玩的开心!

## 存储库规范指南: 

### 每个提交必须通过测试

PR中的所有提交都必须通过测试. 如果不能通过测试,修复提交 和/或 [压扁他们:多个提交变一个](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History#Squashing-Commits)来通过测试. 我门应该这样做,以便可以轻松使用 git-bisect. 

我们在您推送到分支时运行 CI 测试. 要在本地运行测试,您可以运行以下任何一项: `make build`,`make install`,`make test`,`go test ./...`,取决于你想要做什么. 通常`go test ./...`是你最好的选择. 

### 分支名称

如果您正在使用新功能,请在分支名称前加上前缀`feat/`. 如果你正在解决问题,`fix/`. 如果您只是添加测试,`test/`. 如果要添加文档,`doc/`. 如果您的变更集不属于这些类别之一,请使用您的最佳判断并提出您自己的简短前缀. 

之后,尝试发出此分支正在处理的代码库的哪个部分. 例如,如果要向`DHT`添加新测试,用来测试 `提供程序-providers` 返回的 `nil` ,那么`test/dht/nil-provs`是可以接受的. 如果您的更改不能完全落入单个模块中,则可以使用更通用的描述符,或者保留为稍微更冗长的描述. 

还请尝试将分支名称保持在 <± 20个字符. 它让整体事情变得更加清洁. 还要尽量避免将问题编号放在分支名称中,它会占用空间而不提供有关改变的任何直接相关的信息. 

一些好的分支名称的例子: 

-   `feat/cmds/object-diff`
    -   添加的`ipfs object diff`命令功能请求. 
-   `test/dag/cache-invalid`
    -   用于围绕merkledag的缓存失效代码添加测试. 
-   `doc/unixfs/pkg-desc`
    -   对于在unixfs中添加或改进包描述的分支. 

### 提交消息

提交消息必须以较短的主题行开头,后跟可选的更详细的解释性文本,该文本通过空行与摘要分隔. 我们用[GitCop](https://gitcop.com)检查提交消息是否正确写入. 它会检查以下内容: 

-   提交消息的第一行 (称为主题行) 长度不应超过80个字符. 

-   提交消息应以以下片段结束: 

        License: MIT
        Signed-off-by: User Name <email@address>

    其中"用户名"是作者的真实 (合法) 名称,电子邮件@地址是作者的有效电子邮件地址之一. 

    这些片段意味着作者同意[开发者许可证书](docs/developer-certificate-of-origin)和[MIT许可证](docs/LICENSE)下的工作. 

    为了帮助您自动添加这些片段,您可以运行[setup_commit_msg_hook.sh](https://raw.githubusercontent.com/ipfs/community/master/dev/hooks/setup_commit_msg_hook.sh)脚本将设置一个Git commit-msg 钩子,它将上面的片段添加到你写的所有提交消息中. 

见[有关修改提交的文档](https://github.com/ipfs/community/blob/master/docs/amending-commits.zh.md)有关如何重做提交消息的说明. 

一些示例提交消息: 

    parse_test: improve tests with stdin enabled arg

    Now also check that we get the right arguments from
    the parsing.

    License: MIT
    Signed-off-by: Christian Couder <chriscool@tuxfamily.org>

和

    net/p2p + secio: parallelize crypto handshake

    We had a very nasty problem: handshakes were serial so incoming
    dials would wait for each other to finish handshaking. this was
    particularly problematic when handshakes hung-- nodes would not
    recover quickly. This led to gateways not bootstrapping peers
    fast enough.

    The approach taken here is to do what crypto/tls does:
    defer the handshake until Read/Write[0]. There are a number of
    reasons why this is _the right thing to do_:
    - it delays handshaking until it is known to be necessary (doing io)
    - it "accepts" before the handshake, getting the handshake out of the
      critical path entirely.
    - it defers to the user's parallelization of conn handling. users
      must implement this in some way already so use that, instead of
      picking constants surely to be wrong (how many handshakes to run
      in parallel?)

    [0] http://golang.org/src/crypto/tls/conn.go#L886

    License: MIT
    Signed-off-by: Juan Benet <juan@ipfs.io>
