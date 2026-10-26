# 安全策略 / Security Policy

## 支持范围 / Supported versions

只有最新 Release 版本接受安全修复。旧版本请先升级再报告。

Only the latest release receives security fixes. Please upgrade before reporting.

| 版本 | 支持 |
| --- | --- |
| 1.5.x | ✅ |
| < 1.5 | ❌ |

## 报告安全问题 / Reporting a vulnerability

**请不要开公开 Issue。** 请通过以下任一渠道私下联系维护者：

- GitHub 私密漏洞报告：仓库 **Security** 标签页 → *Report a vulnerability*
- 邮件：见维护者 GitHub 主页公开邮箱 / See the public email on the maintainer's GitHub profile

Please **do not open a public issue**. Use GitHub's *Report a vulnerability* (repository **Security** tab) or the maintainer's public email.

报告中请包含：受影响版本、复现步骤、期望行为与实际行为、可能的影响、你的验证环境（Windows 版本 / 权限）。

Include: affected version, reproduction steps, expected vs. actual behaviour, potential impact, and your environment (Windows build / privilege level).

## 我们的响应 / Our response

| 阶段 | 目标时间 |
| --- | --- |
| 确认收到 | 72 小时内 / within 72 hours |
| 初步评估 | 7 天内 / within 7 days |
| 修复发布 | 视严重程度，通常 30 天内 / typically within 30 days |

修复发布后会在 Release Notes 中致谢（如果你希望匿名请注明）。

We credit reporters in the release notes unless you ask to stay anonymous.

## 本项目特别关注的漏洞类型 / What we care about most

1. **任何形式的网络行为**：程序发起 DNS 查询、TCP/UDP 连接、加载远程资源——这是对本项目根本承诺的违背，按最高严重级别处理。
   *Any network behaviour at all* — DNS lookups, TCP/UDP connections, remote resource loading. This contradicts the project's core promise and is treated as critical.
2. **任何形式的写入或持久化**：写注册表、装服务/驱动/证书、改代理、写系统目录、留存文件。
   *Any write or persistence*: registry, services, drivers, certificates, proxy changes, system-directory writes, leftover files.
3. **检测结果被篡改或伪造**：例如某个软件能让本程序漏报自己、或伪造绿色结论。
   *Tampering with or faking results*: a product able to hide itself from the scanner, or to forge a green verdict.
4. **提权与代码执行**：报告的导出路径、路径拼接、注册表/服务读取中的解析缺陷导致任意代码执行。
   *Privilege escalation / code execution* via report export paths, path handling, or parsing of registry/service data.
5. **隐私泄露**：导出的报告包含用户未预期的敏感信息（用户名、完整路径、主机名等）。
   *Privacy leakage*: exported reports containing unexpected sensitive data (usernames, full paths, hostnames).

## 不在范围内 / Out of scope

- 程序未做代码签名导致的 SmartScreen 提示（已知设计）
- 需要物理接触或已在管理员权限下才能利用的通用 Windows 行为
- 第三方安全软件把本程序误判为风险（请向该厂商提交误报，同时欢迎在本仓库开 Issue 讨论）

- SmartScreen warnings caused by the unsigned binary (known by design)
- Generic Windows behaviour requiring physical access or pre-existing admin rights
- Third-party AV flagging this tool (report to that vendor; feel free to discuss it in an issue here)
