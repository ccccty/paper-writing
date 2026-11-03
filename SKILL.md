---
name: paper-writing
description: 撰写、重写、润色与投稿前自审学术论文时使用——覆盖英文 ML/CV/NLP 论文与中文科技论文（期刊/会议/学位论文）。提供 Abstract、Introduction、Related Work、Method、Experiments、Conclusion 的章节级写法，段落清晰度与 claim-evidence 对齐，审稿视角对抗式自审，以及中文论文的文体规范、IEEE 中文骨架、LaTeX 工具链与编译排错、按公开基准量级对齐实验数值。也用于把本地 LaTeX 项目跑通渲染出 PDF。输出正文零元信息的成稿，占位数值与待核实项一律剥离到随附的核实清单文件。同样适用于纯英文任务：draft, rewrite, polish and self-review research papers with section-level guidance, paragraph clarity, claim-evidence alignment and adversarial review.
---

# Paper Writing

## 0. 三条铁律（任何语言、任何章节都适用）

1. **成稿零元信息。** 正文禁止出现：【待核实】/【TBD】标记、来源 URL 与来源类型标注、"本文当前版本"、"建议采用"、"此处插入图"等草稿口吻、合规与文件属性声明、形式审查自查表。正文必须是"已经想清楚的成稿"；一切不确定剥离到同目录的 `核实清单.md`。
2. **数据与证据诚信。** 数值只有两种合法来源：用户实测结果，或公开基准论文的官方报告值（仅用于基线对比，须给出处）。论断强度不得超过证据强度——无法被结果支撑的 claim，要么弱化到可辩护强度，要么删除，绝不保留。这条对 Abstract 与 Introduction 是硬约束，因为审稿人先读这两节。做法见 `references/craft/claim-evidence.md`。
3. **可编译是底线（LaTeX 项目）。** 交付的 `.tex` 必须当场编译验证：exit=0、0 缺字、0 错误、无 multiply-defined label。只写不验的论文不算交付。

## 1. 工作流（六拍）

```
定位轨道 → 读稿诊断 → 构建骨架 → 逐段成稿 → 自审收敛 → 交付验证
```

| 拍 | 动作 | 产出 |
|---|---|---|
| 1 定位轨道 | 判断语言与体裁：英文 ML/CV/NLP？中文期刊会议？学位论文？决定后续加载哪条 reference | 轨道判定 |
| 2 读稿诊断 | 通读全文 + 跑诊断清单 + （LaTeX）先编译一次看报错 | 问题列表 |
| 3 构建骨架 | 先写 3-7 条 mini-outline，再动笔；章节骨架见对应 reference | 大纲 |
| 4 逐段成稿 | 一段一个主旨，首句点题；每段标注角色（opening/challenge/method/advantage/evidence/limitation） | 新正文 |
| 5 自审收敛 | 逆向提纲 + claim-evidence 映射 + 五维对抗式自审，逐条消解高风险项 | 修订稿 |
| 6 交付验证 | 编译（如适用）+ 核实清单 + 口头说清占位值 | 成稿 |

## 2. 三条参考轨道（**一次只加载需要的那一份**）

不要一次把全部 reference 读完。按当前任务只加载对应的一份：

### A. `references/sections/` —— 英文论文的章节级写法

| 写什么 | 读哪份 |
|---|---|
| Abstract | `references/sections/abstract.md` |
| Introduction | `references/sections/introduction.md` |
| Related Work | `references/sections/related-work.md` |
| Method | `references/sections/method.md` |
| Experiments | `references/sections/experiments.md` |
| Conclusion | `references/sections/conclusion.md` |
| 投稿前全面自审 | `references/sections/paper-review.md` |

### B. `references/craft/` —— 语言中立的通用手艺

| 问题 | 读哪份 |
|---|---|
| "这段读不通/不顺"、逆向提纲 | `references/craft/paragraph-clarity.md` |
| "这个论断有没有证据"、五维自审、降级措辞 | `references/craft/claim-evidence.md` |

### C. `references/zh/` —— 中文论文轨道

| 问题 | 读哪份 |
|---|---|
| 中文文体规范、零元信息清单、段落闭环 | `references/zh/01-文体规范-成稿零元信息.md` |
| IEEE 中文会议论文骨架 | `references/zh/02-IEEE中文会议论文骨架.md` |
| 按公开基准量级填写/核对实验数值 | `references/zh/03-实验数值与基准对齐.md` |
| 本地 LaTeX 工具链（Tectonic/字体/VS Code） | `references/zh/04-本地LaTeX工具链.md` |
| 编译报错 → 根因 → 修法 | `references/zh/05-编译排错手册.md` |

总路由表见 `references/index.md`；例文库见 `references/examples/index.md`。

## 3. 全局写作原则

1. 段落单主旨，首句点明该段要做什么。
2. 名词自足：新术语先定义再复用；术语全文稳定，改缩写必须全文替换。
3. 句间必须有明确关系：因果、对比、递进、细化、举例——没有关系的句子不要相邻。
4. 每段闭环：问题 → 机理 → 证据 → 收束。实验段的收束必须落到数字（"提升 X 个百分点"），不许"显著提升"了事。
5. 指标带基线论证：每个关键数字给出和谁比、差多少、为什么这个差距合理。
6. 视觉质量是内容不是装饰：干净的 teaser 与 pipeline 图、低墨量可读表格、全文一致的排版。
7. 每图每表必须在正文被引用（"如表 X 所示"）并紧跟一段解读。
8. 结构不得读起来像"对朴素基线的小修小补"：每个模块写清动机、设计、技术优势。
9. 局限写真话、写具体：参数增加、弱配准、适用范围。评审最反感假局限。

## 4. 诊断清单（机械执行，逐条扫）

1. **占位符扫描**：`--`、待填、待补、建议、模板、blankfigure、空表、TODO。
2. **label 冲突**：`\label{...}` 全文不得重复（复制粘贴图表代码块是重灾区）。
3. **图题与文件名一致**：图文件改用途后题注必须同步。
4. **引用完整性**：每条参考文献至少被 `\cite` 一次；正文每个 `\cite` 有对应条目。
5. **数字一致性**：摘要、正文、表格、结论中的同一指标处处相等；提升量 = 两表之差，当场心算复核。
6. **命名一致性**：模块名、方法名全文统一。
7. **贡献对齐**：Introduction 的贡献条目与 Experiments 小节一一对应，缺一条就是扣分项。
8. **作者/单位/邮箱**：无法代填，保留占位并写入核实清单置顶。

## 5. 自审收敛（三件必做的事）

1. **逆向提纲**：写下全文主论点 → 每段主题句 → 每段证据点，检查映射。映射不上的段落删或改。做法见 `references/craft/paragraph-clarity.md`。
2. **claim-evidence 映射**：给 Abstract 与 Introduction 的每条主要论断建立 `Claim | 类型 | 证据来源 | 状态 | 处理动作`。状态为 needs-evidence/unsupported 的，当场降级或删除。做法与降级措辞表见 `references/craft/claim-evidence.md`。
3. **五维对抗式自审**：contribution / writing clarity / experimental strength / evaluation completeness / method design soundness，以挑剔审稿人的视角逐项提问并回答，直到主要拒稿风险被显式解决。清单见 `references/sections/paper-review.md`。

## 6. 中文论文轨道要点

1. 中文正文走 §0 的铁律，尤其"零元信息"：不确定性一律进 `核实清单.md`。
2. 骨架默认值（IEEE 中文会议稿）：引言 / 相关工作 / 数据集与问题定义 / 方法 / 实验与结果分析 / 讨论 / 结论。细节见 `references/zh/02-IEEE中文会议论文骨架.md`。
3. 实验数值按基准对齐法填写（用户授权填占位值时）：找到公开基准 → 抽取官方表格数字 → 基线行用官方真值 → 本方法按"最强基线 + 合理增量"设定 → 全篇一致性扫描 → **所有占位值逐表逐行写入核实清单**。见 `references/zh/03-实验数值与基准对齐.md`。
4. 带占位数值投稿属学术不端，交付时必须口头提醒用户替换为真实实验结果——这条提醒不可省略。
5. 新建中文论文项目时，以 `assets/ieee-cn-template.tex` 为骨架起点。

## 7. LaTeX 编译与验证

```powershell
Set-Location <论文目录>            # 先 cd，之后全部用相对路径
$env:TECTONIC_CACHE_DIR="D:\devtools\tectonic\cache"
& D:\devtools\tectonic\tectonic.exe -X compile --synctex --keep-logs main.tex
```

验证脚本（在论文目录内用 `.` 传参；从 DSH pwsh 给 python 传中文绝对路径会被 GBK 重编码损坏，一律相对路径）：

```
python tools\build_paper.py .
```

工具链布局、字体安装、VS Code 侧配置见 `references/zh/04-本地LaTeX工具链.md`；报错对照表见 `references/zh/05-编译排错手册.md`。

验收标准：`exit code = 0`、`Missing character = 0`、`LaTeX Warning = 0`（cite 类首遍提示最终必须归零）、`multiply defined = 0`、PDF 页数符合预期、抽取文本无乱码替代符。

## 8. 交付格式

- LaTeX 论文：编译验证过的 `main.pdf` + `核实清单.md`，用 present 工具一并交付。
- 纯文稿：修订后的正文 + 自审清单 + claim-evidence 映射表。
- 口头汇报：做了什么、哪些数字是官方值哪些是占位值、用户必须处理什么。

## 9. 输出契约（被要求改写或撰写章节时）

1. 紧凑的章节大纲（3-7 条）。
2. 修订后的段落，并标注每段角色（opening/challenge/method/advantage/evidence/limitation）。
3. 简短自审清单：清晰度、流畅度、术语一致性、无支撑论断、缺失证据。
4. 主要论断的 claim-evidence 映射：`Claim: ... | Evidence: ... | Status: supported/needs evidence`。

## 10. 边界

- 军工/国重研发**项目申报书**（建议书/立项论证/任务书）→ 用 `proposal-generator-cn`，本技能只管**学术论文**。
- 中国发明专利文件 → 用 `patent-china`。
- 输出 Word/PPT/Excel 交付物时叠加对应 `office-*` 技能。
- 图表绘制本身（draw.io 等）→ 用对应绘图技能，本技能只管图表在论文中的呈现纪律。