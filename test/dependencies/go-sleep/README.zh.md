# 睡觉睡一段时间

这个 UNIX 工具是一层薄薄的`time.Sleep()`包装器。 它的目的是提供一种不需要很多秒便携式睡眠方式。

看<https://godoc.org/time#ParseDuration>如何指定持续时间.

### 安装

```sh
go install github.com/chriscool/go-sleep
```

### 用途:

```
> go-sleep
Usage: go-sleep <duration>
Valid time units are "ns", "us" (or "µs"), "ms", "s", "m", "h".
See https://godoc.org/time#ParseDuration for more.
> time go-sleep 100ms

real    0m0.104s
user    0m0.000s
sys     0m0.007s
```

### 许可证

MIT
