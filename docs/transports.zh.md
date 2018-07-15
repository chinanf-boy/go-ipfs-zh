
## /ws 和 /wss  -  websockets

如果您希望浏览器连接到 例如:`/dns4/example.com/tcp/443/wss/ipfs/QmFoo`

-   [ ] SSL证书匹配`/dns4`要么`/dns6`名称
-   [ ] go-ipfs监听`/ip4/127.0.0.1/tcp/8081/ws`
    -   8081仅仅是一个例子
    -   请注意它`/ws`在这里,不是`/wss`-  go-ipfs 目前无法执行SSL,请参阅下一点
-   [ ] nginx
    -   使用SSL证书配置
    -   监听443端口
    -   转发到127.0.0.1:8081
