# 参考文档索引

本索引是 paper-writing 技能的文档路由表：先确定"我现在要做什么"，再打开对应的那一份。路径均相对技能根目录。章节指南实际都在 `references/sections/` 下；若某份文档把章节指南写成了不带 `sections/` 的旧扁平路径，按 `references/sections/` 下的同名文件理解。

## 1. 按任务找文档

| 我要做什么 | 读哪一份 | 语言 | 什么时候不用它 |
|---|---|---|---|
| 起一篇新的中文 IEEE 会议论文 | `assets/ieee-cn-template.tex`，骨架见 `references/zh/02-IEEE中文会议论文骨架.md` | 中文 | 目标模板不是 IEEEtran 时，模板不可直接用 |
| 写或改英文 Abstract | `references/sections/abstract.md` | 英文 | 中文摘要改语体 → `references/zh/01-文体规范-成稿零元信息.md`；只想看范句 → `references/examples/abstract-examples.md` |
| 写或改英文 Introduction | `references/sections/introduction.md` | 英文 | 故事没定、贡献没排清时先定故事，别急着套模板 |
| 写 Method | `references/sections/method.md` | 英文 | 只缺模块动机句式 → `references/examples/method-examples.md` |
| 写 Experiments | `references/sections/experiments.md` | 英文 | 数字还没跑出来、需要按基准量级填占位 → `references/zh/03-实验数值与基准对齐.md` |
| 写 Related Work | `references/sections/related-work.md` | 英文 | 文献还没筛完、最强基线没列出时，先列文献再写 |
| 写 Conclusion | `references/sections/conclusion.md` | 英文 | 实验还没成形、局限写不出真话时，先补实验 |
| 投稿前做审稿视角自审 | `references/sections/paper-review.md` | 英文 | 只是单段语言问题 → `references/craft/paragraph-clarity.md` |
| 判断"这段读不通/没有 flow" | `references/craft/paragraph-clarity.md` | 英文原文，概念中英通用 | 真正问题是 claim 缺证据 → `references/craft/claim-evidence.md` |
| 核对 claim 有没有实验撑腰 | `references/craft/claim-evidence.md` | 英文 | 要动章节结构 → 回 `references/sections/` 下对应章节 |
| 写中文期刊/会议论文的文体 | `references/zh/01-文体规范-成稿零元信息.md` | 中文 | 英文投稿；或只需要节序骨架 → `references/zh/02-IEEE中文会议论文骨架.md` |
| 只要中文论文的节序与每节必写要素 | `references/zh/02-IEEE中文会议论文骨架.md` | 中文 | 用非 IEEEtran 模板时不适用其导言区与图表纪律 |
| 按公开基准量级填实验数字（占位值） | `references/zh/03-实验数值与基准对齐.md` | 中文 | 真跑出结果后只需核对；它管的是占位与核实清单，不是实测流程 |
| 搭本地 LaTeX 环境、配 VS Code | `references/zh/04-本地LaTeX工具链.md` | 中文 | 纯 Overleaf 用户可跳过环境一节，直接看排错 |
| 中文论文编译报错、反复排不掉 | `references/zh/05-编译排错手册.md` | 中文 | 报错出在英文模板的字体/文件名时，同样适用 |
| 行文口语化、不像顶刊、摘要写得像流水账 | `references/zh/06-行文与语体-学术书面化.md` | 中文 | 只是段落逻辑不通（不是用词问题）→ `references/craft/paragraph-clarity.md` |
| 编译并做产物验收 | `tools/build_paper.py`，用法与工具链见 `references/zh/04-本地LaTeX工具链.md` | 脚本注释为英文 | 在 Overleaf 上手动编译时用不上该脚本 |
| 找可复用的段落句式与整段范本 | `references/examples/abstract-examples.md`、`references/examples/introduction-examples.md`、`references/examples/method-examples.md` | 英文 | 结构还没定、需要的是写法而不是句式时，先读 `references/sections/` |

## 2. 按轨道划分

三条轨道分层解决不同问题，互不替代：sections 管"这一节怎么组织"，craft 管"句子和论证是否站得住"，zh 管"中文成稿的文体、骨架、数字与编译"。

### `references/sections/` —— 英文 ML/CV/NLP 论文的章节级写法

- `references/sections/abstract.md`：三套摘要逻辑模板（挑战→贡献、挑战→洞见→贡献、多贡献并列）与改写检查，解决"摘要只会复述方法"。
- `references/sections/introduction.md`：Introduction 的逻辑图与多套模板（任务/应用、技术挑战、pipeline 叙事），解决"引言讲不清为什么难、贡献为什么成立"。
- `references/sections/related-work.md`：按技术主题而非年份分组，每个主题收束到"还缺什么、本文补什么"，解决"相关工作像文献罗列"。
- `references/sections/method.md`：写前问题清单、pipeline 草图、模块三要素（设计/动机/技术优势）与逐段写法，解决"方法节写成流水账"。
- `references/sections/experiments.md`：有效性、因果性、实用价值三个核心问题与对应实验配置，解决"只有主表、没有支撑"。
- `references/sections/conclusion.md`：问题与思路复述、最强证据、影响与局限段落的结构，解决"结论空泛或回避局限"。
- `references/sections/paper-review.md`：贡献、写作清晰度、实验强度、评估完备性、方法设计五维对抗式自审清单，解决"投稿前不知道审稿人会打哪里"。

### `references/craft/` —— 语言中立的通用手艺

- `references/craft/paragraph-clarity.md`：单段单主旨、首句立论、句间关系与反向大纲，解决"读者跟丢、段落内部没有推进"。
- `references/craft/claim-evidence.md`：claim 分类与逐类证据门槛（事实/测量/比较/因果/泛化）、证据不足时的降级动作与对抗式自审，解决"结论比数据走得远"。

### `references/zh/` —— 中文论文的文体、骨架、数值与工具链

- `references/zh/01-文体规范-成稿零元信息.md`：中文论文的文体依据与"成稿零元信息"三条铁律（正文不残留待核实标记、占位说明、写作指令），不确定性一律剥离到核实清单，解决"成稿像工作笔记"。
- `references/zh/02-IEEE中文会议论文骨架.md`：节序即论证链、每节必写要素、中文 IEEEtran 导言区、图表与数字单位纪律，解决"中文稿结构散、格式不齐"。
- `references/zh/03-实验数值与基准对齐.md`：从公开基准论文取锚点、设增量合理的占位值、写进核实清单，解决"用户只给一句'指标按差不多的填'"。
- `references/zh/04-本地LaTeX工具链.md`：本机 Tectonic、字体、VS Code、LaTeX Workshop 与 TeX shim 的实测布局和命令，解决"环境从零搭不起来"。
- `references/zh/05-编译排错手册.md`：报错→根因→修法的对照表（字体缺失、文件名无扩展名、biber 不可用、PowerShell 传参），解决"同一个报错反复试错"。
- `references/zh/06-行文与语体-学术书面化.md`：顶刊语体三条判据、禁用词与句式清单（口语/网感/AI 套话）、句式改写规则、摘要五段结构、数字与量词硬约束、五组真实改写标尺、交付前五步语体自查，解决"内容对了但读起来像技术博客"。

## 3. 例文库

`references/examples/` 存整段英文范例与可复用句式，不是教程。用法：先由对应 sections 文件定好结构与段落角色，再到这里找"这一段长什么样"；只借句子的逻辑与推进方式，不抄原句。

什么时候不该来：故事、贡献、实验证据还没落定时，例文只会诱导你套空模板；中文论文的语体问题属于 `references/zh/`。

三份例文索引及实测覆盖数量：

- `references/examples/abstract-examples.md`：3 篇（`references/examples/abstract/` 下 template-a/b/c，分别对应三套摘要模板）。
- `references/examples/introduction-examples.md`：13 篇（`references/examples/introduction/`，含任务/应用 4 篇、技术挑战 4 篇、pipeline 5 篇）。
- `references/examples/method-examples.md`：9 篇（`references/examples/method/`，含写作前问题 1 篇、模块范例 4 篇、章节模板 3 篇、常见问题 1 篇）。

`references/examples/` 一概从这三份分册索引进入；不要再从目录结构自行猜测分组。

## 4. 加载纪律

一次只加载当前任务需要的那一份，不要一次把 `references/sections/` 全读完。

1. 上下文成本：sections 七份合计约 37 KB，整包读进来会挤掉稿件正文与用户的具体要求，而真正相关的往往只有其中一两节。
2. 互相干扰：章节指南各带一套模板和术语（Introduction 的"技术挑战"叙事、Method 的"模块三要素"、Abstract 的三版本），同时在场容易串模板，把摘要的写法带进方法节，造成术语漂移。
3. 操作顺序：先定当前任务 → 只读第 1 节表格对应的那一行 → 需要例文时再只读对应索引里的一小节 → 换任务时换文件，不要在旧文件上叠读。
4. 允许的例外：收尾自审时 `references/sections/paper-review.md` 可与正在改的章节文件同读；排错时 `references/zh/04-本地LaTeX工具链.md` 与 `references/zh/05-编译排错手册.md` 可同读。