# Credits and Citations

This repository is a **merge and reorganization**. Most of the writing methodology here is not original work by this repository. This file records exactly where each part comes from, so the chain of attribution stays intact when material is reused.

---

## 1. Writing methodology, paragraph craft, and the example bank

**Prof. Peng Sida (彭思达)** — public study notes on research writing.

- Notes: https://pengsida.notion.site/c1a22465a0fa4b15a12985223916048e
- Repository: https://github.com/pengsida/learning_research

The following parts of this skill derive from Prof. Peng's openly shared notes:

| In this repo | Derived from |
|---|---|
| `references/sections/*` (Introduction, Abstract, Related Work, Method, Experiments, Conclusion) | Section-level writing patterns described in his notes |
| `references/craft/paragraph-clarity.md` | "Does my writing flow" reverse-outlining method |
| `references/examples/**` (abstract / introduction / method example bank) | Worked examples drawn from his notes, based on his own published papers |

Sincere thanks to Prof. Peng for making these notes publicly available.

---

## 2. Skill packaging (upstream of this repo)

**Master-cai** — packaged the above methodology into an agent skill.

- Repository: https://github.com/Master-cai/Research-Paper-Writing-Skills
- License: MIT (© 2026 Master-cai)

This repository builds directly on that work: it inherits the license, retains the original copyright notice in `LICENSE`, and keeps the same section/craft/example organization, reorganized into a unified router.

---

## 3. Papers used for the worked examples

The method-writing examples under `references/examples/` are worked from these two papers. Please cite the originals if you reuse the example text.

**Neural Body** — used for the module triad, overview, and figure-text examples.

> Sida Peng, Yuanqing Zhang, Yinghao Xu, Qianqian Wang, Qing Shuai, Hujun Bao, Xiaowei Zhou.
> *Neural Body: Implicit Neural Representations with Structured Latent Codes for Novel View Synthesis of Dynamic Humans.*
> CVPR 2021. arXiv:2012.15838. DOI: 10.1109/CVPR46437.2021.00894

**Instant-NGP** — used for the module design example.

> Thomas Müller, Alex Evans, Christoph Schied, Alexander Keller.
> *Instant Neural Graphics Primitives with a Multiresolution Hash Encoding.*
> ACM Transactions on Graphics 41(4), 2022. DOI: 10.1145/3528223.3530127

---

## 4. Original to this repository

The following parts were assembled for this repository and are original (still under the repository's MIT license):

- `SKILL.md` — the unified router, six-beat workflow, three iron rules, and the diagnostic checklist
- `references/craft/claim-evidence.md` — claim grading, mapping template, adversarial five-dimension review
- `references/zh/**` — the Chinese track: style specification ("zero meta-information" delivery), IEEE Chinese conference skeleton, benchmark-aligned numeric workflow, local LaTeX toolchain notes, compile troubleshooting manual
- `references/index.md` — the task → document routing table
- `assets/ieee-cn-template.tex` — IEEEtran + xeCJK Chinese paper skeleton
- `tools/build_paper.py` — Tectonic compile + acceptance gate
- `README.md`, `README_zh.md`, `CREDITS.md`

---

## 5. Reuse

If you fork, repackage, or redistribute this skill, please keep:

1. the `LICENSE` file with the original copyright notice (© 2026 Master-cai, MIT);
2. this attribution chain back to Prof. Peng Sida's notes and Master-cai's skill repository;
3. the citations for Neural Body and Instant-NGP if you keep the worked examples.

Attribution is cheap and makes the whole ecosystem better. Thank you.