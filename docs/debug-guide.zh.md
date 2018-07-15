
# 常用性能调试指南

这是一个帮助调试 go-ipfs的文档. 如果可以,请 添加 它!

### 目录

<!-- START doctoc -->
<!-- END doctoc -->

### 开始

当你看到 ipfs 发生了(使用大量的CPU,内存或其他很奇怪的东西)事情时,你要做的第一件事就是收集所有相关的分析信息. 

-   goroutine 转储
    -   `curl localhost:5001/debug/pprof/goroutine\?debug=2 > ipfs.stacks`
-   30秒的CPU配置文件
    -   `curl localhost:5001/debug/pprof/profile > ipfs.cpuprof`
-   堆跟踪转储
    -   `curl localhost:5001/debug/pprof/heap > ipfs.heap`
-   系统信息
    -   `ipfs diag sys > ipfs.sysinfo`

捆绑所有这些,并包含您正在运行的 ipfs 二进制文件的副本 (具有完全相同的二进制文件很重要,它包含调试信息) . 

如果你感到无畏,你可以调查自己: 

### 分析堆栈转储

首先要寻找的是悬挂的 goroutines  - 任何已经停留超过一分钟的 goroutine 都应该引起注意. 它看起来像: 

    goroutine 2306090 [semacquire, 458 minutes]:
    sync.runtime_Semacquire(0xc8222fd3e4)
      /home/whyrusleeping/go/src/runtime/sema.go:47 +0x26
    sync.(*Mutex).Lock(0xc8222fd3e0)
      /home/whyrusleeping/go/src/sync/mutex.go:83 +0x1c4
    gx/ipfs/QmedFDs1WHcv3bcknfo64dw4mT1112yptW1H65Y2Wc7KTV/yamux.(*Session).Close(0xc8222fd340, 0x0, 0x0)
      /home/whyrusleeping/gopkg/src/gx/ipfs/QmedFDs1WHcv3bcknfo64dw4mT1112yptW1H65Y2Wc7KTV/yamux/session.go:205 +0x55
    gx/ipfs/QmWSJzRkCMJFHYUQZxKwPX8WA7XipaPtfiwMPARP51ymfn/go-stream-muxer/yamux.(*conn).Close(0xc8222fd340, 0x0, 0x0)
      /home/whyrusleeping/gopkg/src/gx/ipfs/QmWSJzRkCMJFHYUQZxKwPX8WA7XipaPtfiwMPARP51ymfn/go-stream-muxer/yamux/yamux.go:39 +0x2d
    gx/ipfs/QmZK81vcgMhpb2t7GNbozk7qzt6Rj4zFqitpvsWT9mduW8/go-peerstream.(*Conn).Close(0xc8257a2000, 0x0, 0x0)
      /home/whyrusleeping/gopkg/src/gx/ipfs/QmZK81vcgMhpb2t7GNbozk7qzt6Rj4zFqitpvsWT9mduW8/go-peerstream/conn.go:156 +0x1f2
    created by gx/ipfs/QmZK81vcgMhpb2t7GNbozk7qzt6Rj4zFqitpvsWT9mduW8/go-peerstream.(*Conn).GoClose
      /home/whyrusleeping/gopkg/src/gx/ipfs/QmZK81vcgMhpb2t7GNbozk7qzt6Rj4zFqitpvsWT9mduW8/go-peerstream/conn.go:131 +0xab

在顶部,您可以看到此goroutine (编号2306090) 已等待获取信号量`458`分钟. 那似乎很糟糕. 查看其余的跟踪,我们看到它正在等待的确切行是 **runtime/sema.go** 的第47行. 这不是特别有用,所以我们继续前进. 接下来,我们看到该调用是由 **yamux/session.go** 的205行进行`yamux.Session`中的`Close`的方法. 这似乎是一个问题. 

鉴于这些信息,请查找另一个可能在 堆栈转储的其余部分 中持有有问题的信号量的 goroutine.  (如果您需要帮助,请执行ping操作,我们会将其删除. ) 

goroutines会被悬挂 有几个不同的原因: 

-   `semacquire`意味着我们正在等待锁定或信号量. 
-   `select`意味着 goroutine 挂在一个select语句中,并且没有一个案例产生任何东西. 
-   `chan receive`和`chan send`分别等待接收或发送频道. 
-   `IO wait`通常意味着我们正在等待套接字读取或写入数据,尽管它*大概*意味着我们正在等待一个非常慢的文件系统. 

如果你看到任何这些标签*没有*一个`,
X minutes`后缀,通常意味着没有问题 - 你只是在短暂的等待中找到了goroutine. 如果等待时间超过几分钟,这或者意味着 goroutine 没有做太多,或者有些事情是非常错误的. 

### 分析CPU配置文件

go团队写了一篇文章[关于性能分析的优秀文章](http://blog.golang.org/profiling-go-programs). 如果您已经收集了上述信息,可以跳到他们开始讨论的地方`go tool pprof`. 我的分析方法是运行`web`命令,生成 SVG点图 并在浏览器中打开它. 这是轻松指出代码中热点位置的最快捷方式. 

### 其他

如果您有任何疑问,或者希望我们分析一些奇怪的 go-ipfs 行为,请告诉我们,并确保包含顶部提到的所有分析信息. 
