# 变更记录

本文件记录本仓库的重要变更，格式参考 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/)，
日期为提交日期（YYYY-MM-DD）。

## [Unreleased]

## 2026-11-08 — 小鹤音形 10.26.11 码表核对、文档编号调整

### Changed

- 小鹤音形：按官方 **10.26.11** 码表核对词条规模 —— `build/flypy.table.bin` 内含 **157,636 条**
  （10.26.1 时为 65,350 条）、117,481 个音节；`build/flypy.{table,prism,reverse}.bin`
  更新为官方包内原始文件。
- 文档编号重排为 `01`–`07`：`06-常见问题`、`07-第三方组件与许可`（原 07 / 08），
  各文档与 README、CONTRIBUTING 的交叉链接同步更新。
- `.gitignore` 补充忽略 `__pycache__/` 等临时文件。

## 2026-11-08 — 小鹤音形 10.26.11 升级、可选方案入库

### Changed

- **升级小鹤音形到官方 10.26.11**（挂接包 2026-11-02 版）：主码表 `flypy.table.bin` 1.9 MB → 3.8 MB、
  `prism.bin` 553 KB → 1.1 MB、`reverse.bin` 614 KB → 1.25 MB；`flypy_sys.txt`（8,484 条）、
  `flypy_full全码字.txt`（2,158 条）、`flypydz.dict.yaml`（9,548 条）与官方同步；
  `flypy.schema.yaml` 以官方新版为基线，保留本地 3 处改动（OK 拼字、关闭 4 码自动上屏、繁体用 `s2tw`）；
  key_binder 随之获得 `Caps_Lock`→Esc、`Control+m` 切换方案、`$`/`|` 次选。
- **未启用方案改为「随仓库提供」**：7 个默认未启用的方案（自然码 / 微软 / 紫光 / 拼音加加 / 智能 ABC 双拼、
  纯五笔86、九宫格 t9）与它们专用的 `cn_en_*.txt` 移到 `others/optional/` 并纳入跟踪，附启用说明；
  从 `others/optional/` 复制到根目录的副本由 `.gitignore` 忽略，不会重复跟踪。

### Added

- `others/optional/README.md`：可选方案清单与启用步骤。
- `docs/02` 新增「可选方案」表与「停用 / 启用 / 新增方案」三节；`docs/03` 重写为 10.26.11 版
  （含升级记录、与官方的 3 处差异、升级命令、部署日志说明）。

### Fixed

- `user_dicts/01_custom.dict.yaml`：`Claude claude` 用空格而非 Tab 分隔，部署时触发
  `entry_collector: Encode failure`，已改为 Tab。

### Changed（文档）

- README 补充仓库目标（自用顺手 + 他人开箱即用）与「可选方案」入口。

## 2026-11-08 — 文档开源化重构、跟踪范围精简

### Changed

- **文档重构为开源规范结构**：README 只保留门面（简介、特性、方案表、快速开始、文档索引、许可），
  细节按主题拆入 `docs/`，新增 `docs/README.md` 索引与文档规范、`CHANGELOG.md`、`CONTRIBUTING.md`。
- 文档按主题拆分并加编号前缀（现为 `01`–`07`，含安装部署、方案说明、小鹤音形、英文输入、
  皮肤与自定义词库、常见问题、第三方组件与许可）。
- 原 `docs/flypy配置说明.md` → `docs/03-小鹤音形配置说明.md`；
  原 `docs/各输入方案说明.md` → `docs/02-各输入方案说明.md`（`git mv` 保留历史）。

### Added

- `docs/07-第三方组件与许可.md`：上游项目、许可证归属（GPL-3.0 / LGPL-3.0 / CC BY-SA 4.0 等）与小鹤音形版权说明。
- `docs/06-常见问题.md`：部署、方案、编码、快捷键等高频问题。

### Fixed

- `lua/easy_en.lua`：`wordninja` 模块改用 `pcall` 加载，缺失时降级为「不拆分」，英文方案不再因可选依赖报错。
- `lua/search.lua`：删除 `get_pos` 中数值 `for` 循环内无效的 `i = i + 1`。

### Removed

- 精简仓库跟踪范围（155 → 100 个文件）：`others/` 上游素材与 Go 词库工具、`go.work`、`imgs/`、
  7 个未启用方案及其专用的 `en_dicts/cn_en_*.txt` 移出跟踪（**本地文件保留**）。
- `.gitignore` 增加 `others/flypy/`：小鹤音形官方挂接包原件（zip、搜狗/百度短语）只本地保留，不随仓库分发。

## 2026-08-28

### Changed

- 小鹤音形升级至 **10.26.1**：主码表更新为官方预编译版，`flypy_sys.txt` 符号编码与官网对齐，
  补全官方挂接包缺失的 OK 拼字（`ok_mode`）配置，新增 `flypydz.dict.yaml` / `flypyok.schema.yaml`。
- `rime.lua` 合并新旧日期/时间/计算器函数，兼容 `wubi86_jidian` 等方案。
- 调大候选字体：候选 20 / 序号 16 / 编码提示 17。
- 所有皮肤候选改为横向排列。
- 关闭 4 码全码自动上屏，仅保留分号快符自动上屏（避免连续输入时多出一个空格）。

### Added

- `docs/` 配置说明（小鹤音形详细配置、全部方案说明）。

## 2026-08-27

### Added

- 初始提交：Rime 配置全量（easy_en 英文方案、小鹤双拼、雾凇拼音、五笔等）。
