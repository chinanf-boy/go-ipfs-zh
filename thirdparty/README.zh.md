第三方由 Golang 包组成,该包不包含 go-ipfs 依赖项,并且可能在稍后成为 ipfs/go-ipfs 供应商(vendored).

此目录下的包*必定不能*导入`ipfs/go-ipfs`的包，也不能在`thirdparty`。
