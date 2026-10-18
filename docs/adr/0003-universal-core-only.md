# 通用核心配置：仓库只声明每台开发机都需要的

用户拥有多台开发机（模式相近：Windows + WSL，Python/TS/Go），本仓库将应用到全部机器。判据：只有「每台开发机都需要」的内容才进核心声明（编辑器、终端、shell、语言管理器、git、CLI 工具、系统偏好）；机器个性化的工具（本机的 JetBrains 套件、Typora、GitHub Desktop）不进仓库，由各机手动安装维护，且受「移除清单之外不碰」原则保护。同一判据的推论：**git 身份因机而异，属机器数据**——仓库中的 gitconfig 模板不含 [user] 段，通过 `include.path = ~/.gitidentity` 引用每台机器本地的身份文件（bootstrap 首次生成占位，不入仓库）。拒绝的替代：按机器拆 profile（目前各机差异仅个性工具，不值得）；仓库内置可选模块/override 机制（为假想的共享需求做设计，YAGNI，真出现再引入）。
