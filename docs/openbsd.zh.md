
# 在OpenBSD上构建

## 准备你的系统

确保你有`git`,`go`和`gmake`安装在您的系统上. 

    $ doas pkg_add -v git go gmake

## 准备去环境

确保您的gopath已设置: 

    $ export GOPATH=~/go
    $ echo "$GOPATH"
    $ export PATH="$PATH:$GOPATH/bin"

## 建立

该`install_unsupported`target适用于openbsd. 这将安装`gx`,`gx-go`并运行`go install -tags nofuse ./cmd/ipfs`. 

    $ go get -v -u -d github.com/ipfs/go-ipfs

    $ cd $GOPATH/src/github.com/ipfs/go-ipfs
    $ gmake install_unsupported

如果一切顺利,你的ipfs二进制文件应该准备好了`$GOPATH/bin/ipfs`. 

    $ ipfs version
