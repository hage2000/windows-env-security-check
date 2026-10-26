# 贡献指南 / Contributing Guide

感谢你愿意改进这个项目。这是一个面向普通用户的**隐私可见性工具**，稳定性与"零副作用"承诺高于功能数量。提交前请花两分钟读完本页。

Thanks for helping. This is a **privacy-visibility tool** for non-technical users: stability and the "zero side effects" promise outrank feature count. Please read this page before opening a PR.

> 参与本仓库即表示你已阅读并接受 [LICENSE](LICENSE) 与 [DISCLAIMER.md](DISCLAIMER.md)：本程序永久免费、非商业，仅限个人自有设备使用，禁止用于规避任何单位的安全管控。
>
> By contributing you accept [LICENSE](LICENSE) and [DISCLAIMER.md](DISCLAIMER.md): free forever, non-commercial, personal devices only, never for evading organisational controls.

---

## 一、绝对不能做的事 / Hard rules

1. **不要向 `main` 直接推送。** `main` 已启用分支保护：禁止 force push、禁止删除、禁止直推，所有改动必须走 Pull Request。包括维护者本人。
   *Never push to `main`.* It is protected: no direct pushes, no force pushes, no deletion. Everything goes through a PR — including the maintainer.
2. **不要引入任何联网能力。** 不新增 HTTP / Socket / DNS / 更新检查 / 埋点 / 崩溃上报 / 第三方统计 SDK。这一条没有例外，PR 会因此被直接关闭。
   *No networking of any kind.* No HTTP, sockets, DNS, update checks, telemetry, crash reporting or third-party analytics SDKs. No exceptions; such PRs are closed.
3. **不要引入写入行为。** 不写注册表、不装服务/驱动、不加启动项或计划任务、不写系统目录、不安装证书、不改代理。程序必须保持"只读检测 + 退出即无痕"。
   *No write behaviour.* No registry writes, services, drivers, autoruns, scheduled tasks, system-directory writes, certificate installation or proxy changes. Read-only detection, zero residue after exit.
4. **不要新增运行时依赖或安装器。** 必须保持单文件、免安装、自包含。
   *No new runtime dependencies and no installer.* Single file, portable, self-contained — always.
5. **不要提交二进制文件**（exe / dll / pdb / 压缩包）。二进制通过 Releases 分发，仓库只保留文档、截图与校验值。
   *Do not commit binaries.* They ship via Releases; the repo keeps docs, screenshots and checksums only.
6. **不要引入商业化能力，也不要引入针对组织管控的对抗能力。** 不得加入收费、授权校验、激活、广告、推广、统计或任何形式的盈利入口；不得加入针对单位统一部署的管理端（MDM / DLP / EDR 控制台）的隐藏、反检测或反审计能力。本项目仅面向个人自有设备的隐私自查，这条边界不接受讨论。
   *No commercialisation, no capability aimed at organisational management.* No charging, licensing, activation, ads, promotion, analytics or any monetisation path; and no hiding-from, anti-detection or anti-audit capability aimed at an organisation's management console (MDM / DLP / EDR). The project is scoped to privacy self-checks on personal devices you own — this boundary is not negotiable.

---

## 二、工作流 / Workflow

```bash
# 1. Fork（外部贡献者）或从最新 main 拉分支（维护者）
git clone https://github.com/<your-name>/windows-env-security-check.git
cd windows-env-security-check

# 2. 建分支，命名规则见下
git switch -c feat/bitlocker-status

# 3. 改动 → 自测 → 提交
git add -A
git commit -m "feat(scan): read BitLocker status via WMI"

# 4. 推送并开 PR，目标分支必须是 main
git push -u origin feat/bitlocker-status
```

打开 PR 后，GitHub 会自动请求 [CODEOWNERS](.github/CODEOWNERS)（@hage2000）审核。**至少 1 个 approval + 全部会话已解决 + 无冲突**才会出现绿色合并按钮，且只允许 **Squash merge**（保持 `main` 线性历史）。

After you open a PR, GitHub automatically requests review from [CODEOWNERS](.github/CODEOWNERS). The merge button unlocks only with **1 approval + all conversations resolved + no conflicts**, and only **squash merge** is allowed.

## 三、分支命名 / Branch naming

| 前缀 | 用途 / Purpose | 示例 |
| --- | --- | --- |
| `feat/` | 新功能 / new feature | `feat/recall-detection` |
| `fix/` | 缺陷修复 / bug fix | `fix/tray-icon-restore` |
| `detect/` | 检测规则与特征库 / detection rules | `detect/ip-guard-v5` |
| `docs/` | 文档 / documentation | `docs/en-readme-typo` |
| `perf/` | 性能与资源占用 / performance | `perf/lower-idle-cpu` |

## 四、提交信息 / Commit messages

采用 [Conventional Commits](https://www.conventionalcommits.org/)：

```
<type>(<scope>): <subject>

type:  feat | fix | detect | docs | perf | refactor | chore
scope: scan | ui | tray | report | docs | build
```

示例：`fix(tray): re-register icon on TaskbarCreated broadcast`

## 五、PR 描述必须包含 / A PR must state

1. **动机**：解决什么问题，或补上哪一类漏报/误报。附真实场景或样本。
   *Motivation*: what problem it solves, which false negative/positive it addresses, with a real scenario or sample.
2. **影响面**：是否触及扫描逻辑、界面、托盘、实时监测、报告导出。
   *Impact*: does it touch scanning, UI, tray, live monitoring or report export?
3. **零副作用自检**：确认没有新增网络调用、没有写入行为。列出你用来验证的方法（resmon / Process Monitor / 防火墙出站阻断）。
   *Zero-side-effect check*: confirm no new network calls and no writes; list how you verified (resmon / Process Monitor / outbound block).
4. **资源占用对比**：改动前后的内存、CPU、扫描耗时（有变化时必填）。
   *Footprint delta*: memory, CPU and scan duration before/after, when affected.
5. **截图/GIF**：任何界面改动都请附上。
   *Screenshots/GIF* for any UI change.

## 六、检测规则贡献 / Contributing detection rules

新增一款监控/加密软件特征时，请同时提供：

- 产品正式名称（中文 + 英文）、厂商
- 可识别的证据类型：进程名、服务名、驱动名、安装注册表路径、自启动项、计划任务、根证书 CN、监听端口
- 至少一条**通用兜底规则**思路（避免只认名字，未收录变种也能命中）
- 在你机器上的实测结果：命中项数量与关键证据截图（打码个人信息）

When adding a signature, include the official product name (zh + en), vendor, the evidence types you can match on (process, service, driver, uninstall key, autorun, scheduled task, root CA CN, listening port), at least one **generic fallback rule**, and your measured result with redacted screenshots.

## 七、审查与拒绝 / Review and rejection

维护者会在一周内给出第一次回复。以下情形会被直接拒绝，不进入讨论：

- 引入联网、写入、遥测、自动更新
- 提交二进制、打包安装器、加壳或混淆代码
- 修改 README 中的**隐私与安全声明**使其与真实行为不符
- 移除或削弱分支保护相关配置（`CODEOWNERS`、`.github/` 下的保护性文件）

The maintainer replies within a week. The following are closed without discussion: networking, writes, telemetry or auto-update; committed binaries, installers, packed or obfuscated code; edits that make the privacy statement untrue; removal or weakening of branch-protection configuration.

## 八、安全漏洞 / Security issues

请勿开公开 Issue，按 [SECURITY.md](SECURITY.md) 私下报告。

Do not file a public issue. Follow [SECURITY.md](SECURITY.md).
