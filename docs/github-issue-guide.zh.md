
# 如何提交GitHub问题

我们使用GitHub问题来记录我们所有的待办事项和任务. 这是[一个很好的指南](https://guides.github.com/features/issues/),如果你不熟悉的话. 

使用go-ipfs记录问题时,如果您指定了以下信息,将会很有用. 这将有助于我们更快地对问题进行分类. 请用 类型 tag 您的问题. 例如: 

-   "bug: 无法添加文件`ipfs add`"
-   "question: 我如何使用`ipfs block <hash>`?"

将命令放在 反引号 中有助于我们解析自然语言描述,并且建议使用. 

这是一个*鲜活指南*. 如果你看到任何应该在这里的东西,或者没有,或者有改进的想法,请打开一个"meta"问题. 

### 类型

-   "bug": 如果你提交的是一个bug. 
-   "meta": 如果它是关于我们如何运行 go-ipfs,而不是代码相关的东西. 
-   "question": 如果你有问题. 
-   "test failure": 如果测试失败
-   "panic": 如果是一个严重的错误. 
-   "enhancement": 如果你有一个功能,你希望它增强go-ipfs. 

### 平台

对于平台和处理器,只需运行即可`ipfs version --all`并包括该输出. 

你的平台. 

-   "LINUX"
-   "Windows"
-   "苹果电脑"
-   等等. 

### 处理器

你的处理器架构. 

-   "86"
-   "AMD64"
-   "Arm"

### 区块

你的问题涉及什么. 多个项目都可以. 

- "api"
- "bandwidth reduction"
- "bit swap"
- "blockstore"
- "commands"
- "containers + vms"
- "core"
- "daemon + init"
- "dat"
- "discovery"
- "encryption"
- "files"
- "fuse"
- "gateway"
- "gx"
- "interior"
- "pins"
- "libp2p"
- "merkledag"
- "nat"
- "releases"
- "repo"
- "routing"
- "tools"
- "tracking"
- "unix vs dag"

### 优先

- **Critical-严重** - 系统崩溃,应用程序恐慌. 
- **High-高** - 应用程序的主要功能不起作用,API破坏,repo格式破坏等. 
- **Medium-中** - 非必要功能不起作用,性能问题等. 
- **Low-低** - 可选功能不起作用. 
- **Very Low-非常低** - 翻译或文档错误. 一些真正无关紧要的东西,但应该注意未来的版本. 
