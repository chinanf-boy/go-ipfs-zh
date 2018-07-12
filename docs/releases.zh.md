
# go-ipfs发布

## 发布时间表

go-ipfs是一个为期六周的发布时间表. 发布后,将会有五周的时间来添加任何类型的代码 (功能,错误修正等) . 五周后,一个候选版本被标记,只有重要的错误修正将被允许到发布日. 

## 发布候选清单

-   [ ] CHANGELOG.zh.md已更新
    -   使用`./bin/mkreleaselog`生成一个很好的入门名单
-   [ ] 版本字符串`repo/config/version.go`已经升级
-   [ ] 使用vX.Y.Z-rcN进行标记提交
-   [ ] 发布gx版本`gx publish`, 按照[gx发布指南](https://github.com/whyrusleeping/gx#publishing-and-releasing)
    -   您必须手动将gx版本调整为'rc'

## 预发布清单

-   [ ] 在发布之前,标记'release candidate'供用户进行测试
    -   如果发现/修复了错误,请执行另一个候选发布版
-   [ ] 所有测试都通过 (没有例外) 
-   [ ] 运行互操作测试<https://github.com/ipfs/interop#test-with-a-non-yet-released-version-of-go-ipfs>
-   [ ] webui工作 (对于'works'的大多数定义)  - 测试多个页面并验证没有显示可见错误. 
-   [ ] CHANGELOG.zh.md已更新
    -   使用`./bin/mkreleaselog`生成一个很好的入门名单
-   [ ] 版本字符串`repo/config/version.go`已经升级
-   [ ] 使用vX.Y.Z标记提交
-   [ ] 更新发布分支以指向发布提交
-   [ ] 发布dist.ipfs.io
-   [ ] 将下一个版本发布到<https://github.com/ipfs/npm-go-ipfs>
-   [ ] 发布gx版本`gx release`, 按照[gx发布指南](https://github.com/whyrusleeping/gx#publishing-and-releasing)

## 释

-   [ ] 凹凸版本字符串`repo/config/version.go`至`vX.Y.Z-dev`
-   通讯
    -   [ ] 创建发布问题
    -   [ ] 公告 (预发布和发布后) 
        -   [ ] 推特
        -   [ ] IRC
        -   [ ] 书签交易
    -   [ ] 博客文章 (至少粘贴更改日志. 可选择添加上下文和感谢贡献者. ) 
-   [ ] 使用更新网站上的HTTP-API文档<https://github.com/ipfs/http-api-docs>
