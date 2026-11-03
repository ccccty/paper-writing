# paper-writing

[中文](./README_zh.md) | English

A single agent skill for **writing, rewriting and self-reviewing research papers** — covering both English ML/CV/NLP papers and Chinese journal/conference papers.

It merges two previously separate skills into one routed skill: section-level writing craft for English papers, and Chinese-language style rules + a working LaTeX toolchain.

## What it does

| Track | Directory | Purpose |
|---|---|---|
| Section writing (EN) | `references/sections/` | Section-level guidance for Abstract, Introduction, Related Work, Method, Experiments, Conclusion, plus a pre-submission review checklist |
| Writing craft (language-neutral) | `references/craft/` | Paragraph clarity & reverse outlining; claim–evidence mapping, evidence grading and adversarial self-review |
| Chinese papers | `references/zh/` | Chinese style spec ("zero meta-information" delivery), IEEE Chinese conference skeleton, benchmark-aligned numeric tables, local LaTeX toolchain, compile troubleshooting |
| Examples | `references/examples/` | A worked example bank (abstract / introduction / method) drawn from published papers |

Three iron rules apply to every track: **no meta-information in the manuscript body** (all uncertainty goes to a separate `核实清单.md`), **no claim without evidence** (weaken or delete), and **a LaTeX project is not delivered until it compiles clean**.

## Repository layout

```
paper-writing/
├── SKILL.md                     # router + unified workflow + iron rules
├── CREDITS.md                   # full attribution and citations
├── agents/openai.yaml           # agent interface metadata
├── references/
│   ├── index.md                 # task → document routing table
│   ├── sections/                # English section guides
│   ├── craft/                   # paragraph clarity, claim-evidence
│   ├── zh/                      # Chinese track (01-05)
│   └── examples/                # example bank
├── assets/ieee-cn-template.tex  # IEEEtran + xeCJK Chinese skeleton
└── tools/build_paper.py         # Tectonic compile + acceptance gate
```

## Install

Copy or symlink this directory into your agent's skills folder, keeping `SKILL.md` at the root of the installed directory.

```bash
# Codex
mkdir -p "$CODEX_HOME/skills" && cp -R paper-writing "$CODEX_HOME/skills/"

# Claude Code (global)
mkdir -p "$HOME/.claude/skills" && cp -R paper-writing "$HOME/.claude/skills/"

# Claude Code (project-level)
mkdir -p .claude/skills && cp -R paper-writing .claude/skills/

# Gemini
mkdir -p "$HOME/.gemini/skills" && cp -R paper-writing "$HOME/.gemini/skills/"
```

On Windows you can keep the real directory on another drive and create a directory junction instead of copying:

```powershell
New-Item -ItemType Junction -Path "$HOME\.dsh\skills\paper-writing" -Target "D:\path\to\paper-writing"
```

## Usage

```text
Use paper-writing to rewrite my Introduction and check claim-evidence alignment.
用 paper-writing 把我的中文论文改成可直接投稿的成稿，数值走基准对齐。
用 paper-writing 帮我把 main.tex 编译跑通并做投稿前自审。
```

`references/index.md` maps a concrete task ("this paragraph doesn't flow") to the single document to load — load one at a time rather than reading the whole library.

## Compile gate

```bash
cd <paper dir>
python <skill>/tools/build_paper.py . --tex main.tex
```

Finds Tectonic via `--tectonic`, `$TECTONIC_BIN`, `PATH`, or the Windows default; fails the build on compile errors, missing glyphs, undefined citations or duplicated labels.

## Credits and attribution

This repository is a merge and reorganization, and most of the writing methodology is **not original to it**. See [CREDITS.md](./CREDITS.md) for the full record. In short:

- **Prof. Peng Sida (彭思达)** — the section-writing methodology, the paragraph-flow check, and the worked example bank originate from his publicly shared study notes ([notes](https://pengsida.notion.site/c1a22465a0fa4b15a12985223916048e), [repo](https://github.com/pengsida/learning_research)). Thank you for sharing these openly.
- **Master-cai** — packaged those notes into an agent skill ([Research-Paper-Writing-Skills](https://github.com/Master-cai/Research-Paper-Writing-Skills), MIT), which this repo builds on directly and inherits the MIT license from.
- **Neural Body** (Peng Sida et al., CVPR 2021) and **Instant-NGP** (Müller et al., ACM TOG 2022) — the method examples in `references/examples/` are worked from these two papers.
- The Chinese track (`references/zh/`, `assets/ieee-cn-template.tex`, `tools/build_paper.py`) is original work assembled for this repository.

If you reuse material from here, please keep the attribution chain intact.

## License

MIT. See [LICENSE](./LICENSE). The original copyright notice (© 2026 Master-cai) is retained as required by the license.