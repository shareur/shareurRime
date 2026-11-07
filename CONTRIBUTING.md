# 贡献指南

[← 返回 README](README.md) · [文档目录](docs/README.md)

本仓库是个人自用的 Rime 配置公开备份，欢迎通过 Issue 反馈问题、通过 Pull Request 提交改进。
提交前请先阅读本文；常见问题见 [docs/06-常见问题](docs/06-常见问题.md)。

## 一、反馈问题（Issue）

请尽量提供以下信息，便于定位：

1. 平台与前端（macOS 鼠须管 / Windows 小狼毫 / Linux fcitx5-rime、ibus-rime）及版本；
2. `librime` 版本（见 `default.custom.yaml` 的 `customization.rime_version`）；
3. 出问题的**输入方案 ID** 与复现步骤（输入了什么、期望什么、实际什么）；
4. 相关日志或报错：

   | 平台 | 日志位置 |
   | --- | --- |
   | macOS | 控制台.app 搜索 `Squirrel`，或 `~/Library/Logs/` |
   | Windows | `%TEMP%\rime.weasel.*` |
   | Linux | `journalctl -f` 或终端启动 fcitx5 观察输出 |

5. 若怀疑部署问题，附上 `build/` 下对应方案的编译日志/报错信息。

## 二、提交代码（Pull Request）

### 提交范围

- **可以提交**：方案配置（`*.schema.yaml` / `*.custom.yaml`）、词库修正、`lua/` 脚本、文档。
- **不要提交**：`installation.yaml`、`user.yaml`、`sync/`、`*.userdb/`、`*.db.txt`、`rime_yang.zip`、
  `flypy.dict.yaml`、`build/` 下除 `flypy.*.bin` 之外的产物（均为个人数据或运行时产物）。
  `others/flypy/`（官方挂接包原件）同样不提交。
- 从 `others/optional/` 复制到根目录的「启用副本」也不用提交——`.gitignore` 已忽略；
  若改动了副本内容并想长期保留，请把改动同步回 `others/optional/` 里的原件再提交。
- 新增/修改词库前请确认来源与许可，并在 [docs/07-第三方组件与许可](docs/07-第三方组件与许可.md) 中登记。

### 提交信息（Commit message）

与现有历史保持一致：**中文一行主题（不超过 50 字，说明"做了什么"）+ 空行 + 要点 bullet（说明"为什么/影响面"）**。

```
小鹤音形：关闭 4 码全码自动上屏，仅保留分号快符自动上屏

- 连续输入时自动上屏会导致再按空格多出一个空格
- 普通 4 码改为手动空格/选择上屏，快符(;x) 与 OK 拼字不受影响
```

一次提交只做一件事；配置改动与文档改动尽量分开提交。

### 验证

- 改动配置后**必须重新部署并实测**，确认候选、符号、快捷键符合预期；
- 改动 `lua/` 脚本至少跑一次语法检查：`luac -p lua/xxx.lua`；
- 提交前执行 `git status`，确认没有意外的 `??` 未跟踪文件、没有把个人数据带上。

## 三、文档规范

1. **README 只放门面**（简介、特性、方案表、快速开始、文档索引、许可），不放长篇细节。
2. **单一主题单一文件**：具体问题写进 `docs/` 下对应文档；新主题用编号前缀命名（`NN-中文标题.md`）。
3. 新文档需在 [docs/README.md](docs/README.md) 索引中登记，并在头部加「返回索引 / 返回 README」链接。
4. 每篇文档开头一句话说明适用范围；平台差异用表格分列 macOS / Windows / Linux。
5. 文档改动要同步更新 [CHANGELOG.md](CHANGELOG.md)。

## 四、与上游的关系

本仓库与雾凇拼音、Easy Stream English、rime-radical-pinyin、rime-melt 等上游项目**没有从属关系**：

- 通用词库/脚本问题请优先向**上游**反馈（[rime-ice](https://github.com/iDvel/rime-ice) 等）；
- 本仓库只维护个人的方案组合、皮肤、键位与少量脚本改动；
- 从上游同步词库时，请保留各文件头部的来源与作者注释。
