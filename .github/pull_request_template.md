## 这个 PR 做了什么 / What does this PR do

<!-- 一句话说明 / one sentence -->

## 动机 / Motivation

<!-- 解决什么问题？补哪一类漏报或误报？请附真实场景或样本。 -->
<!-- What problem does it solve? Which false negative / positive? Real scenario or sample here. -->

## 影响面 / Impact

- [ ] 扫描逻辑 / scanning logic
- [ ] 界面 / UI
- [ ] 托盘与实时监测 / tray & live monitoring
- [ ] 报告导出 / report export
- [ ] 仅文档 / docs only
- [ ] 其他 / other:

## 零副作用自检 / Zero-side-effect self-check

- [ ] 没有新增任何网络调用（HTTP / Socket / DNS / 更新检查 / 埋点）
      No new network calls of any kind
- [ ] 没有新增任何写入或持久化（注册表 / 服务 / 启动项 / 计划任务 / 证书 / 代理 / 系统目录）
      No new writes or persistence
- [ ] 没有新增运行时依赖或安装器，仍是单文件免安装
      Still single-file, portable, no new runtime dependency
- [ ] 没有提交二进制文件
      No binaries committed

验证方法 / How verified：

<!-- 例如 resmon 网络页为 0；防火墙阻断出站后结果一致；Process Monitor 无 TCP/UDP Send -->
<!-- e.g. resmon network tab shows zero; identical results with outbound blocked; no TCP/UDP Send in Procmon -->

## 资源占用对比 / Footprint delta

| 指标 | 改动前 | 改动后 |
| --- | --- | --- |
| 空闲内存 / idle memory |  |  |
| 扫描后内存 / post-scan memory |  |  |
| 空闲 CPU / idle CPU |  |  |
| 扫描耗时 / scan duration |  |  |

## 界面改动截图 / Screenshots (UI changes)

<!-- 拖入图片 / drag images here -->

## 关联 Issue / Related issue

Closes #
