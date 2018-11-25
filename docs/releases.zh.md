# go-ipfs 的发布

## 发布时间表

go-ipfs 是一个 为期六周 的发布时间表. 发布后,将会有五周的时间来添加任何类型的代码 (功能,错误修正等) . 五周后,一个候选版本被`标记-tag`,只有重要的错误修正将允许发布日提前.

## 发布的候选清单

- [ ] CHANGELOG.zh.md 已更新
  - 使用`./bin/mkreleaselog`生成一个很好的开始列表
- [ ] 在`version.go`的版本字符串已经升级
- [ ] 使用 `vX.Y.Z-rcN` 进行标记提交
- [ ] 发布 gx 版本`gx publish`, 按照[gx 发布指南](https://github.com/whyrusleeping/gx#publishing-and-releasing)
  - 您必须手动将 gx 版本 调整为'rc'

## 预发布清单

- [ ] 在发布之前,标记'release candidate'供用户进行测试
  - 如果 发现/修复 了错误,请执行另一个候选发布版
- [ ] 所有测试都通过 (没有例外)
- [ ] 运行互操作测试<https://github.com/ipfs/interop#test-with-a-non-yet-released-version-of-go-ipfs>
- [ ] webui 工作 (对于'works'的大多数定义) - 测试多个页面并验证没有显示可见错误.
- [ ] CHANGELOG.zh.md 已更新
  - 使用`./bin/mkreleaselog`生成一个很好的开始列表
- [ ] `repo/version.go`的版本字符串已经升级
- [ ] 使用`gx release`发布 gx 版本，根据[gx release 指导](https://github.com/whyrusleeping/gx#publishing-and-releasing)
- [ ] 使用 vX.Y.Z 标记提交
- [ ] 更新发布分支 以 指向发布的提交(`git merge vX.Y.Z`)
- [ ] 发布 dist.ipfs.io
- [ ] 将下一个版本发布到<https://github.com/ipfs/npm-go-ipfs>
- [ ] 发布 gx 版本`gx release`, 按照[gx 发布指南](https://github.com/whyrusleeping/gx#publishing-and-releasing)

## 发布后{Post-Release}

- [ ] 撞 `repo/version.go`中版本字符串到`vX.Y.Z-dev`
- [ ] 上传最终版本到 github releases 页面: https://github.com/ipfs/go-ipfs/releases

- 通讯
  - [ ] 创建发布问题
  - [ ] 公告 (预发布和发布后)
    - [ ] 推特
    - [ ] IRC
    - [ ] Reddit
  - [ ] 博客文章 (至少粘贴更改日志. 可选择添加上下文和感谢贡献者. )
- [ ] 更新网站上的 HTTP-API 文档<https://github.com/ipfs/http-api-docs>
