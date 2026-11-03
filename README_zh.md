# paper-writing

中文 | [English](./README.md)

一个 agent 技能，管**学术论文的撰写、重写与投稿前自审**——同时覆盖英文 ML/CV/NLP 论文和中文期刊/会议论文。

它由原先两个独立技能合并而来：英文论文的章节级写作方法论，加上中文论文的文体规范与一套能跑通的本地 LaTeX 工具链。

## 它能做什么

| 轨道 | 目录 | 用途 |
|---|---|---|
| 章节写作（英文） | `references/sections/` | Abstract、Introduction、Related Work、Method、Experiments、Conclusion 的章节级写法，以及投稿前审稿清单 |
| 通用手艺（语言中立） | `references/craft/` | 段落清晰度与逆向提纲；claim-evidence 映射、证据分级、对抗式自审 |
| 中文论文 | `references/zh/` | 中文文体规范（成稿零元信息）、IEEE 中文会议论文骨架、基准对齐的数值填写、本地 LaTeX 工具链、编译排错 |
| 例文库 | `references/examples/` | 从已发表论文中拆解的 example bank（摘要 / 引言 / 方法） |

三条铁律贯穿所有轨道：**正文零元信息**（一切不确定剥离到同目录 `核实清单.md`）、**claim 必须有证据**（扣不住就降级或删除）、**LaTeX 项目没编译干净不算交付**。

## 仓库结构

```
paper-writing/
├── SKILL.md                     # 路由 + 统一工作流 + 三条铁律
├── CREDITS.md                   # 完整致谢与引用记录
├── agents/openai.yaml           # agent 接口元信息
├── references/
│   ├── index.md                 # 「我要做什么 → 该读哪一份」路由表
│   ├── sections/                # 英文论文章节指南
│   ├── craft/                   # 段落清晰度、claim-evidence
│   ├── zh/                      # 中文轨道（01-05）
│   └── examples/                # 例文库
├── assets/ieee-cn-template.tex  # IEEEtran + xeCJK 中文骨架
└── tools/build_paper.py         # Tectonic 编译 + 验收闸门
```

## 安装

把本目录复制或链接到你的 agent 技能目录，保证安装目录根下就是 `SKILL.md`。

```bash
# Codex
mkdir -p "$CODEX_HOME/skills" && cp -R paper-writing "$CODEX_HOME/skills/"

# Claude Code（全局）
mkdir -p "$HOME/.claude/skills" && cp -R paper-writing "$HOME/.claude/skills/"

# Claude Code（项目级）
mkdir -p .claude/skills && cp -R paper-writing .claude/skills/

# Gemini
mkdir -p "$HOME/.gemini/skills" && cp -R paper-writing "$HOME/.gemini/skills/"
```

Windows 下如果想让真实目录留在别的盘，可以建目录联接（junction）而不必复制：

```powershell
New-Item -ItemType Junction -Path "$HOME\.dsh\skills\paper-writing" -Target "D:\path\to\paper-writing"
```

## 用法

```text
用 paper-writing 重写我的 Introduction，并检查 claim-evidence 是否对齐。
用 paper-writing 把我的中文论文改成可直接投稿的成稿，数值按基准对齐填写。
用 paper-writing 帮我把 main.tex 编译跑通并做投稿前自审。
```

`references/index.md` 会把具体任务（比如「这段读不通」）映射到**唯一**该加载的那份文档——一次只读一份，不要一次把整个库读进来。

## 编译闸门

```bash
cd <论文目录>
python <技能目录>/tools/build_paper.py . --tex main.tex
```

按 `--tectonic` → `$TECTONIC_BIN` → `PATH` → Windows 默认路径的顺序找 Tectonic；编译失败、缺字、引用未定义、label 重复都会判失败。

## 致谢与引用

**本仓库是一次合并与重新组织，大部分写作方法论并非本仓库原创。** 完整来源记录见 [CREDITS.md](./CREDITS.md)。简要说明：

- **彭思达老师** —— 章节写作方法论、段落流畅度检查、例文库，均源自他公开分享的学习笔记（[笔记](https://pengsida.notion.site/c1a22465a0fa4b15a12985223916048e)、[仓库](https://github.com/pengsida/learning_research)）。衷心感谢他把这些经验公开出来。
- **Master-cai** —— 把上述笔记封装成 agent 技能（[Research-Paper-Writing-Skills](https://github.com/Master-cai/Research-Paper-Writing-Skills)，MIT），本仓库直接在其基础上继续做，并继承其 MIT 许可。
- **Neural Body**（彭思达 等，CVPR 2021）与 **Instant-NGP**（Müller 等，ACM TOG 2022）—— `references/examples/` 里的方法写作示例是从这两篇论文拆解而来。
- 中文轨道（`references/zh/`、`assets/ieee-cn-template.tex`、`tools/build_paper.py`）是为本仓库编写的原创内容。

如果你从这里取用材料，请把这条署名链一并保留。

## 许可证

MIT，见 [LICENSE](./LICENSE)。按许可要求保留原始版权声明（© 2026 Master-cai）。