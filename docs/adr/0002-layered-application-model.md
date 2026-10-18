# 分层应用模型：声明走 winget，编排走 bootstrap，dotfiles 走仓库目录

覆盖面与应用机制定为三层（对应用户决策 Q3/Q5/Q16）：

1. **声明式层**：软件包与 Windows/开发者系统设置（注册表类）用 winget configuration（DSC）声明，幂等、可审查、有 `winget configure validate/test` 无副作用校验。
2. **编排层**：流程控制类步骤——提权与重启续跑、WSL 侧（Ubuntu 内部）安装、dotfiles 链接、nvm/uv 的具体版本安装——由 bootstrap 脚本负责，不强求塞进 DSC。
3. **dotfiles 层**：Windows 侧与 WSL 侧的个人配置文件作为仓库内独立目录版本化，由 bootstrap 安装（链接/复制）。

关键取舍：不把编排硬塞进 DSC YAML——上游 WindowsDeveloperConfig 正是从 DSC 迁往 PowerShell 引擎（见 docs/research/），其 dev-config.winget 里数百行 YAML 嵌 PowerShell 正是此痛点的证据；但我们也不放弃声明式，只在它擅长的地方用它。拒绝的替代：全 DSC（与 YAML 表达力搏斗）、全 PowerShell（失去声明式与校验，重踩上游弃坑）、配置与 dotfiles 分仓库（迁移多 clone 一次）。
