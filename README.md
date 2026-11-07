# shareurRime

个人在用的 Rime（中州韵输入法引擎）配置，同时也希望成为一份**开箱即用**的参考配置。

两个目标：

1. **自己用着顺手** —— 日常主力是**小鹤双拼**和**小鹤音形**：主码表来自小鹤官方挂接包，
   配上雾凇拼音词库、英文整句补全、五笔兜底、符号/快符编码，键位不折腾。
2. **别人拿来即用** —— 方案、词库、皮肤、快捷键、Lua 扩展都已配好，clone 下来「重新部署」就能打字，
   不必逐个方案拼装；不需要的方案在 `default.custom.yaml` 里删一行即可。

技术上以 [雾凇拼音](https://github.com/iDvel/rime-ice) 为底座，集成 [Easy Stream English](https://github.com/stevenspage/easy_stream_english) 英文整句补全，
并挂接官方**小鹤音形 10.26.11**。适用于 [Rime](https://rime.im/) 各前端：macOS 鼠须管（Squirrel）、
Windows 小狼毫（Weasel）、Linux ibus-rime / fcitx5-rime。纯文本配置、跨平台通用，在 librime 1.13 / Weasel 0.17.4 环境验证。

## 特性

- **主力方案：小鹤双拼 / 小鹤音形**：小鹤音形官方 10.26.11 挂接，含符号编码、OK 拼字、熟手/常规/初学三种模式、万能键反查
- **开箱即用**：16 个方案已启用、皮肤已配好、快捷键已统一；不想要的方案删一行即可
- **中英文输入**：全拼 / 小鹤双拼 / 小鹤音形 / 五笔 86 / 极点五笔 + 英文自动补全（25 万词 + 2.7 万人名）
- **英文整句拆分**：连写英文自动拆词（wordninja 为可选依赖，缺失时自动降级，不影响输入）
- **候选体验**：长词优先、置顶词、短英文降权、部件拆字辅码、以词定字
- **外观**：亮暗双主题跟随系统、候选横向排列、字体回退列表
- **个人词库**：`user_dicts/`、`custom_phrase.txt` 可直接扩充

## 输入方案

| 方案 ID | 名称 | 类型 |
| --- | --- | --- |
| `flypy` | 小鹤音形 10.26.11 | 双拼 + 形码 |
| `double_pinyin_flypy` | 小鹤双拼 | 双拼 |
| `rime_ice` | 雾凇拼音 | 全拼 |
| `pinyin_simp` | 简体拼音 | 全拼 |
| `wubi86_jidian` / `_pinyin` / `_trad` / `_trad_pinyin` | 极点五笔 86 系列 | 形码 / 混输 / 繁体 |
| `wubi_pinyin` / `wubi_trad` | 五笔 86 混输 / 简入繁出 | 形码 |
| `easy_en` | Easy Stream English | 英文补全 |
| `melt_eng` | Easy English Nano | 英文轻量 |
| `radical_pinyin` | 部件拆字 | 反查 |
| `xhup_express` / `xhup_fluency` | 小鶴音形·連打 / 語句流 | 双拼 + 形码 |
| `numbers` | 大写数字 | 数字 |
| `flypyok` / `flypydz` | 小鹤 OK 拼字 / 反查单字 | 依赖方案，不单独使用 |

> 实际启用列表以 `default.custom.yaml` 的 `schema_list` 为准。
> 另外还有 7 个**默认未启用但已随仓库提供**的方案（自然码 / 微软 / 紫光 / 拼音加加 / 智能 ABC 双拼、纯五笔86、九宫格 t9），
> 放在 [`others/optional/`](others/optional/README.md)，复制回根目录 + 加一行 `schema_list` 即可启用。

## 快速开始

1. **放到 Rime 用户目录**（先备份原有内容）

   | 平台 / 前端 | 目录 |
   | --- | --- |
   | macOS 鼠须管 | `~/Library/Rime` |
   | Windows 小狼毫 | `%APPDATA%\Rime` |
   | Linux fcitx5-rime | `~/.local/share/fcitx5/rime` |
   | Linux ibus-rime | `~/.config/ibus/rime` |

   ```bash
   git clone https://github.com/shareur/shareurRime.git ~/Library/Rime   # 以 macOS 为例
   ```

2. **重新部署**：输入法菜单 → 重新部署（Deploy）。首次部署需编译全量词库，几分钟属正常。
3. **切换方案**：按 `` Ctrl+` ``（或 `F4`）呼出方案菜单。

> 仓库不含 `build/`（**小鹤音形主码表三个 `.bin` 例外，必须保留**）、个人词频库 `*.userdb/`、同步备份 `sync/`，
> 这些是运行时产物或个人数据，部署后自动生成。详见 [docs/01-安装与部署](docs/01-安装与部署.md)。

## 文档

完整文档见 **[docs/](docs/README.md)**：

| 文档 | 内容 |
| --- | --- |
| [01-安装与部署](docs/01-安装与部署.md) | 前端与目录、git/ZIP 安装、部署、目录结构、更新与卸载 |
| [02-各输入方案说明](docs/02-各输入方案说明.md) | 16 个方案的用途、依赖与增删方法 |
| [03-小鹤音形配置说明](docs/03-小鹤音形配置说明.md) | 码表组成、模式切换、符号编码、OK 拼字、反查 |
| [04-英文输入说明](docs/04-英文输入说明.md) | 英文词库、整句拆分、Lua 增强组件 |
| [05-皮肤字体与自定义词库](docs/05-皮肤字体与自定义词库.md) | 主题、字体回退、自定义短语与个人词库 |
| [06-常见问题](docs/06-常见问题.md) | 部署、方案、编码、快捷键排查 |
| [07-第三方组件与许可](docs/07-第三方组件与许可.md) | 上游项目与许可归属、小鹤音形版权说明 |

变更记录见 [CHANGELOG.md](CHANGELOG.md)，提交与文档规范见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## 许可与致谢

- 本仓库的个人配置与文档以 **GPL-3.0** 发布，见 [LICENSE](LICENSE)。
- 仓库包含多个上游项目的词库与脚本（雾凇拼音 GPL-3.0、Easy Stream English LGPL-3.0、rime-radical-pinyin、
  rime-melt、小鹤音形等），**各自的许可与权利仍归原作者**，清单见 [docs/07-第三方组件与许可](docs/07-第三方组件与许可.md)。
- 小鹤音形方案与码表版权属何海峰（[flypy.cc](https://flypy.cc/)）；本仓库只收录官方挂接包提供的预编译码表，
  **不提供主码表源码**，商业使用或二次分发请联系原作者。

感谢 [Dvel](https://github.com/iDvel)、[Mirtle](https://github.com/mirtlecn)、[tumuyan](https://github.com/tumuyan)、
[stevenspage](https://github.com/stevenspage) 以及 Rime 社区各位皮肤、脚本作者的无私分享。
