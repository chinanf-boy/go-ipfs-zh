## /ws 和 /wss - websockets

如果您希望浏览器连接到 例如:`/dns4/example.com/tcp/443/wss/ipfs/QmFoo`

- [ ] SSL 证书匹配`/dns4`要么`/dns6`名称
- [ ] go-ipfs 监听`/ip4/127.0.0.1/tcp/8081/ws`
  - 8081 仅仅是一个例子
  - 请注意它`/ws`在这里,不是`/wss`- go-ipfs 目前无法执行 SSL,请参阅下一点
- [ ] nginx
  - 使用 SSL 证书配置
  - 监听 443 端口
  - 转发到 127.0.0.1:8081
