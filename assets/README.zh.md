# IPFS 加载的资产

## 生成文档

不再直接编辑`.go`文件.

而是编辑源文件,并从资产目录中使用`go generate`:

```
go get -u github.com/jteeuwen/go-bindata/...
go generate
```
