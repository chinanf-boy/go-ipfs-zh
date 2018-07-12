
# 命令完成

Shell命令完成由脚本提供[/misc/completion/ipfs-completion.bash](../misc/completion/ipfs-completion.bash). 

## 安装

看到它工作的最简单方法是运行`source misc/completion/ipfs-completion.bash`直接从你的壳. 这只是暂时的,要完全启用它,您必须执行以下步骤之一. 

### Bash on Linux

对于bash,可以通过几种方式启用完成. 一种是将完成脚本复制到目录`~/.ipfs/`然后在文件中`~/.bash_completion`加

```bash
source ~/.ipfs/ipfs-completion.bash
```

它会在下次加载bash时自动加载. 要在系统上全局启用ipfs命令,您还可以将完成脚本复制到`/etc/bash_completion.d/`. 

## 其他参考文献

-   <https://www.debian-administration.org/article/316/An_introduction_to_bash_completion_part_1>
