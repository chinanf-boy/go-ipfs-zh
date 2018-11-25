# 命令行补充

Shell 命令行补充由脚本[/misc/completion/ipfs-completion.bash](https://github.com/ipfs/go-ipfs/blob/master/misc/completion/ipfs-completion.bash)提供。

## 安装

看到它工作的最简单方法，是直接在你的 Shell 运行`source misc/completion/ipfs-completion.bash`. 这只是暂时的,要完全启用它,您必须执行以下步骤之一.

### Bash on Linux

对于 bash,可以通过几种方式启用该脚本. 一种是将脚本复制到`~/.ipfs/`目录,然后在`~/.bash_completion`中加上:

```bash
source ~/.ipfs/ipfs-completion.bash
```

它会在下次加载 bash 时,自动加载。 要在系统上全局启用 ipfs 命令,您还可以将补充脚本复制到`/etc/bash_completion.d/`.

## 其他参考文献

- <https://www.debian-administration.org/article/316/An_introduction_to_bash_completion_part_1>
