
# go-ipfs的发布

## 发布时间表

go-ipfs是一个 为期六周 的发布时间表. 发布后,将会有五周的时间来添加任何类型的代码 (功能,错误修正等) . 五周后,一个候选版本被`标记-tag`,只有重要的错误修正将允许发布日提前. 

## 发布候选清单

-   [ ] CHANGELOG.zh.md已更新
    -   使用`./bin/mkreleaselog`生成一个很好的开始列表
-   [ ] 版本字符串在`repo/config/version.go`已经升级
-   [ ] 使用 `vX.Y.Z-rcN` 进行标记提交
-   [ ] 发布gx版本`gx publish`, 按照[gx发布指南](https://github.com/whyrusleeping/gx#publishing-and-releasing)
    -   您必须手动将 gx版本 调整为'rc'

## 预发布清单

-   [ ] 在发布之前,标记'release candidate'供用户进行测试
    -   如果 发现/修复 了错误,请执行另一个候选发布版
-   [ ] 所有测试都通过 (没有例外) 
-   [ ] 运行互操作测试<https://github.com/ipfs/interop#test-with-a-non-yet-released-version-of-go-ipfs>
-   [ ] webui 工作 (对于'works'的大多数定义)  - 测试多个页面并验证没有显示可见错误. 
-   [ ] CHANGELOG.zh.md已更新
    -   使用`./bin/mkreleaselog`生成一个很好的开始列表
-   [ ] 版本字符串`repo/config/version.go`已经升级
-   [ ] 使用 vX.Y.Z 标记提交
-   [ ] 更新发布分支 以 指向发布提交
-   [ ] 发布 dist.ipfs.io
-   [ ] 将下一个版本发布到<https://github.com/ipfs/npm-go-ipfs>
-   [ ] 发布gx版本`gx release`, 按照[gx发布指南](https://github.com/whyrusleeping/gx#publishing-and-releasing)

## 发布后{Post-Release}

-   [ ] 撞 版本字符串`repo/config/version.go`至`vX.Y.Z-dev`
-   通讯
    -   [ ] 创建发布问题
    -   [ ] 公告 (预发布和发布后) 
        -   [ ] 推特
        -   [ ] IRC
        -   [ ] Reddit
    -   [ ] 博客文章 (至少粘贴更改日志. 可选择添加上下文和感谢贡献者. ) 
-   [ ] 更新网站上的HTTP-API文档<https://github.com/ipfs/http-api-docs>
