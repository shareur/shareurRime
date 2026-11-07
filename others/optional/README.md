# 可选方案（默认未启用）

本目录收录**未在仓库默认配置里启用**的输入方案，方便需要时一键启用。
它们不参与开箱即用的 `schema_list`，因此不影响默认使用；但文件本身**已纳入仓库跟踪**，换机器不用重新找。

## 一、方案清单

| 文件 | 方案 ID | 说明 | 还需要一并复制 |
| --- | --- | --- | --- |
| `double_pinyin.schema.yaml` | `double_pinyin` | 自然码双拼（挂雾凇词库 `rime_ice`） | `en_dicts/cn_en_double_pinyin.txt` |
| `double_pinyin_abc.schema.yaml` | `double_pinyin_abc` | 智能 ABC 双拼 | `en_dicts/cn_en_abc.txt` |
| `double_pinyin_mspy.schema.yaml` | `double_pinyin_mspy` | 微软双拼 | `en_dicts/cn_en_mspy.txt` |
| `double_pinyin_ziguang.schema.yaml` | `double_pinyin_ziguang` | 紫光双拼 | `en_dicts/cn_en_ziguang.txt` |
| `double_pinyin_jiajia.schema.yaml` | `double_pinyin_jiajia` | 拼音加加双拼 | `en_dicts/cn_en_jiajia.txt` |
| `t9.schema.yaml` | `t9` | 九宫格（仓输入法 / Hamster，`__include: rime_ice.schema.yaml:/`） | 无（用到 `lua/t9_preedit.lua`，已在仓库内） |
| `wubi86.schema.yaml` | `wubi86` | 纯五笔 86（词库 `wubi86.dict.yaml` 已在仓库根目录） | 无 |

> 双拼方案都用雾凇词库 `rime_ice.dict.yaml`，并带中英混输词库 `en_dicts/cn_en_*.txt`；
> 这些 `cn_en_*.txt` 只被对应的双拼方案引用，所以随方案一起放在本目录。

## 二、启用方法

以「微软双拼」为例（其他方案把文件名换掉即可）：

```bash
cd ~/.local/share/fcitx5/rime          # macOS 为 ~/Library/Rime，Windows 为 %APPDATA%\Rime

# 1. 复制方案文件到 Rime 用户目录根
cp others/optional/double_pinyin_mspy.schema.yaml .

# 2. 复制该方案专用的中英混输词库（纯五笔86 / t9 跳过此步）
cp others/optional/en_dicts/cn_en_mspy.txt en_dicts/
```

3. 编辑 `default.custom.yaml`，把方案加进 `schema_list`：

```yaml
patch:
  schema_list:
    - {schema: double_pinyin_flypy}
    - {schema: double_pinyin_mspy}     # ← 新增这一行
    ...
```

4. 在输入法菜单里**重新部署**，然后按 `` Ctrl+` ``（或 `F4`）就能选到新方案。

## 三、注意事项

- **复制出来的文件不会进 git**：仓库 `.gitignore` 已经把根目录的同名方案文件与 `en_dicts/cn_en_*.txt` 列为忽略，
  所以「启用」这个动作不会让 `git status` 变脏，也不会造成同一文件被跟踪两份。
- 想**停用**：把根目录那份 `*.schema.yaml` 删掉（或从 `schema_list` 里去掉）再重新部署即可；
  `others/optional/` 里的原件始终保留。
- 如果改动过根目录那份方案，且希望长期保留，请把改动同步回 `others/optional/` 里的原件并提交。
- `t9` 是给**手机端**（仓输入法 Hamster / iRime）用的九宫格方案，桌面端启用体验一般；
  参考 `others/Hamster/`、`others/iRime/` 下的移动端配置示例（这两个目录不随仓库跟踪）。
- 许可证与来源：这些方案改编自 [雾凇拼音](https://github.com/iDvel/rime-ice) 等上游，见
  [docs/07-第三方组件与许可](../../docs/07-第三方组件与许可.md)。
