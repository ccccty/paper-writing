# Claim–Evidence Mapping and Adversarial Self-Review

Scope: this file asks whether each claim is *backed* and whether the paper survives a hostile reader; `references/craft/paragraph-clarity.md` asks whether the prose is *readable*. A fluent paragraph that asserts an unsupported superlative passes that file and fails this one. Fix evidence first, then flow; rewriting a sentence cannot create the missing ablation.

Rule of the document: every declarative sentence that a reviewer could dispute is a claim, and every claim must own one row in a mapping table with a locatable evidence cell. Prose that cannot be mapped is either decoration or a rejection risk.

## 1. Claim taxonomy

Classify before you judge. The evidence bar differs by class, and most overclaims are a claim silently promoted one class (a measured number promoted to a comparative, a comparative promoted to a causal).

| Type | What must exist for `supported` | Typical failure | Downgrade move when it fails |
| --- | --- | --- | --- |
| **Fact** | A primary citation, or a pointer into the paper's own artifact (dataset table, instrument spec, standard definition) | Attributing a limitation to a cited work that does not state it; a "well-known" premise with no source | Keep the sentence, attach the citation; if no source exists, restate as an assumption of this paper and say so |
| **Measured** | One table/figure cell **plus** the full setting: dataset, split, metric definition, budget, seeds | A number in the abstract with no matching cell; a value whose protocol lives only in the appendix | Report the setting inline, or move the number down to where the setting is defined |
| **Comparative** | Both arms under the same protocol, in the same table, margin in the metric's own unit | Baseline copied from another paper under a different backbone; "better" asserted across tables | Name the cell and the protocol match: "by X on metric M over the strongest baseline in Table N, same backbone and budget" |
| **Causal** | An intervention isolating the cause (leave-one-out ablation, control, matched-parameter variant) **plus** a mechanism argument, with the obvious alternative explanations excluded | Gain attributed to module M while M also adds parameters, data, or compute | Demote to association ("co-occurs with"), or add the isolating row with parameters matched |
| **Generalization** | Two or more independent settings outside the tuning setting, and an explicit statement of tested scope | One dataset, one backbone, one language, then "in general" / "any" | Enumerate the tested scope in the sentence itself; untested axes become stated limitations |

Downgrade by **narrowing**, not by hedging. Adding "may", "potentially", or "to some extent" to an unsupported claim produces a vaguer unsupported claim; a reviewer reads hedges as an admission that the evidence is thin. The only honest downgrades are: narrow the population (which datasets), narrow the setting (which protocol, which scale), narrow the claim type (causal → comparative → measured → observation), or delete.

Strength ladder, strongest to weakest — a claim may move down freely, never up without new evidence:

`universal claim > scoped generalization > comparative on fixed protocol > measured value > observation / hypothesis`

## 2. Mapping table template

One row per claim, claims quoted verbatim with location so a stale row is detectable after revision. Keep the table outside the paper; if it must live in the LaTeX source, use a three-line `booktabs` table so it does not read as a results table.

| ID | Claim (verbatim) + location | Type | Evidence (Table / Fig / citation) | Status | Action |
| --- | --- | --- | --- | --- | --- |
| A1 | | | | | |
| A2 | | | | | |
| A3 | | | | | |

```latex
\begin{table}[t]\centering\small
\begin{tabular}{@{}p{0.4cm}p{5.4cm}p{1.6cm}p{3.4cm}p{1.9cm}p{2.1cm}@{}}
\toprule
ID & Claim (verbatim, \S) & Type & Evidence & Status & Action \\
\midrule
A1 & & & & & \\
A2 & & & & & \\
A3 & & & & & \\
\bottomrule
\end{tabular}
\end{table}
```

Status vocabulary, fixed: `supported` (evidence exists and matches the claim's class), `needs-evidence` (a cell probably exists but is not cited, or the protocol match is unverified), `unsupported` (no cell can support it as written), `weakened` (text edited to a defensible form), `removed`.

Action vocabulary, fixed: `cite cell` / `add ablation` / `rerun baseline` / `narrow scope` / `downgrade class` / `delete sentence`.

### Illustrative rows (numbers are schematic — the column shape is what transfers)

| ID | Claim (verbatim) + location | Type | Evidence | Status | Action |
| --- | --- | --- | --- | --- | --- |
| A1 | "Our method reaches 41.2 mIoU on D2, 3.8 points above the strongest baseline." (Abstract, line 3) | Measured + Comparative | Table 2, row 6 vs row 2; same backbone, same 100-epoch budget, 3 seeds | supported | cite cell inline — currently the abstract gives no table pointer |
| A2 | "significantly outperforms all prior methods" (Abstract, line 4) | Comparative (universal) | Table 2 compares 3 baselines; the margin over the second is 0.4, inside the ±0.6 seed spread; the strongest published method is absent | unsupported | downgrade class → "improves over the re-run baselines in Table 2 by 3.8 points on D2"; either add the missing baseline or delete "all prior" |
| A3 | "The gain comes from the gating module." (Conclusion, line 2) | Causal | Table 4 removes gating but also removes 1.9M parameters and reports one dataset only | needs-evidence | add a parameter-matched variant row; until then rewrite as "removing the gating module lowers D2 mIoU by 3.8 (Table 4)" |

Read the three rows as a pattern: A1 is defensible because the cell, the protocol match, and the unit are all named; A2 fails because "all prior" is a universal claim with a three-baseline table behind it; A3 fails because the intervention is not isolating — the causal sentence survives only if the confound (parameters) is closed.

## 3. Audit procedure

Three passes, in this order. The order matters: claims concentrate in three cheap sections, and every one of them is proved or refuted in a fourth section that is expensive to read.

**Pass 1 — harvest (20 min).** Read only Abstract, the contribution list in the Introduction, and the Conclusion. Every declarative sentence becomes a row. Do not judge yet, do not open the experiments. These three sections hold nearly all unbacked claims and cost the least to scan.

**Pass 2 — trace.** For each row, jump to the evidence and fill the cell. Sort the table by status. Work the `unsupported` rows first — each is either a text edit or a missing experiment, and both answers change the paper's shape.

**Pass 3 — reverse sweep.** Read Experiments and Method, and ask which tables, figures, and ablations are cited by **no** claim. Orphan evidence is one of two things: a contribution nobody sold, or dead weight a reviewer will read as padding. Both are fixes to the text.

### High-risk patterns by section

| Section | High-risk pattern | What to check |
| --- | --- | --- |
| Abstract | `best` / `SOTA` / `first` / `outperforms all` with no comparison cell and no scope | Is the named competitor in the table? Is "first" backed by a related-work sweep, or only by the authors' reading? |
| Abstract | A number with no setting, or a setting that differs from the table's | Same value, same unit, same split as the cell it points to |
| Introduction | Contribution bullet *k* has no matching Method subsection, or no row in Experiments | Enumerate: one bullet, one subsection, one experiment. Unmatched bullets are the most common reject trigger |
| Introduction | The claimed failure of prior work asserted without citation or reproducibility | Does the paper show the failure, or only assert it? "Unlike [3], we ..." requires [3] in the comparison table |
| Related Work | A limitation attributed to a cited method that its own paper never states | The reviewer may be that author; attribute only what the source claims |
| Method | Mechanism sentences ("this module captures long-range dependency") written as fact | Is it a hypothesis stated as a design rationale, or a verified effect? Rewrite as intent, verify in ablation |
| Method | Complexity / efficiency claim with no derivation or measured wall-clock | Asymptotic claim at the scale actually used in experiments |
| Experiments | "Significant" without seeds, confidence interval, or a test | Report the spread; if the spread exceeds the margin, the claim is not comparative |
| Experiments | Best-in-bold per column while training budget, augmentation, or resolution differ by row | Budget-matched table, or a footnote per row stating the difference |
| Experiments | Baseline numbers copied from another paper | Mark each row `reported` vs `re-run`; a copied number inherits the other paper's protocol |
| Discussion / Limitations | A limitation that contradicts an abstract claim | Contradiction must be resolved in the abstract, not in a footnote |
| Conclusion | Causal sentence with no tested intervention; future work phrased as a result | Every "stems from" / "thanks to" needs the isolating row from Pass 2 |

Cross-reference the section-writing rules while harvesting: `references/sections/abstract.md` (experiment-summary sentence must match a table), `references/sections/introduction.md` (contribution list is the paper's promise, Experiments is the payment), `references/sections/paper-review.md` (the rejection dimensions this audit pre-empts).

## 4. Five-dimension self-review questions

Answer each with a location, not a judgement. "Yes" without a table or section number is not an answer. A question that cannot be answered in one sentence is itself a finding.

**Contribution**
1. If Section 3.2 were deleted, which abstract claim loses its support? If none, 3.2 is not a contribution and the bullet list is inflated.
2. Which single sentence would a reviewer quote as the novelty, and which table row proves it?
3. Is the gain attributable to the idea, or to extra parameters, data, or compute? Point to the matched-budget row.
4. Which named prior method already does part of this, and why is it absent from the comparison table?
5. Does the paper state what it does **not** claim? An unbounded scope is read as an overclaim regardless of the evidence.

**Writing clarity**
1. For each module, is there a sentence of the form "because X fails at Y, we do Z", and is Y measured in a table or figure?
2. Can one reported number be recomputed from the described protocol alone — dataset, split, epochs, metric implementation?
3. Is every symbol in every equation defined before first use, and does the notation match the appendix?
4. Does each caption state what to look at and what the takeaway is, so the figure stands alone?
5. Are the same quantities named identically in text, axis labels, and table headers?

**Experimental strength**
1. Is the margin larger than the run-to-run spread you report? Give both numbers side by side.
2. For the strongest baseline, is the number the one *it* reports or your re-run, and is that stated per row?
3. Does the advantage survive the budget-matched comparison — same parameters, FLOPs, training data?
4. On how many of the N datasets/settings is the method better, and does the paper say so where it is worse?
5. Is the absolute value competitive with the best published number, independently of your relative gain?

**Evaluation completeness**
1. Does every design choice named in Method appear as exactly one ablation row, with all other factors frozen?
2. Is there an ablation that isolates the interaction between two modules, not only leave-one-out?
3. Are the metrics the ones the cited baselines were selected on; if a new metric is introduced, is its correlation with the target task shown?
4. Is at least one dataset included on which the central claim could fail? A benchmark where the method cannot lose validates nothing.
5. Are the protocol, thresholds/prompts/hyperparameters, and seed policy documented well enough for a re-run?

**Method design soundness**
1. Which assumption would break the method if violated, and is there an experiment that violates it?
2. Does the efficiency claim hold at the scale used in the experiments, not only asymptotically?
3. How many new hyperparameters does the method add, and is the tuning protocol identical to the baselines'?
4. After the module is added, is accuracy-per-unit-cost better or worse than the baseline?
5. Can a reviewer construct an input where the method is worse, and does the paper show that case?

## 5. Downgrade wording table

Left column is the sentence as commonly drafted; middle column is the specific reason it fails; right column is a form that survives review. Prefer a number plus a scope over any adverb. Delete `very`, `significantly`, `substantially`, `remarkably`, `dramatically` unless a test or a table cell stands behind the word.

| Overclaim | Why it fails | Defensible rewrite |
| --- | --- | --- |
| "significantly outperforms prior methods" | "Significantly" implies a test that was not run; "prior methods" implies a complete baseline set | "improves by 3.8 mIoU over the strongest re-run baseline on D2 (Table 2), under identical backbone and training budget" |
| "achieves state-of-the-art performance" | SOTA is time-indexed and set-dependent; the leaderboard may have moved | "the best reported D2 test value among methods trained on the public split, as of the comparison date in Table 2" |
| "is the first to study X" | "First" requires a literature sweep the paper usually did not run | "to our knowledge, prior work has not addressed X under setting Y; Table 1 lists the closest methods and how their settings differ" |
| "generalizes to unseen domains" | One transfer experiment does not establish generality | "transfers to D3 and D4 without retuning, dropping 2.1 points relative to in-domain" |
| "the improvement stems from the gating module" | The ablation confounds the module with parameter count | "removing the gating module lowers D2 mIoU by 3.8 at matched parameter count (Table 4)" |
| "is robust to noise" | Robustness is a curve, not a property | "degrades by 1.2 points at σ = 0.1, against 4.6 points for the baseline (Fig. 5)" |
| "is efficient" | Efficiency needs a denominator | "uses 38% fewer FLOPs and 11 ms less latency per frame at equal accuracy (Table 5)" |
| "can be applied to any backbone" | "Any" is untested by construction | "we verify on three backbones (ResNet-50, ViT-B, Swin-T); other backbones are out of scope" |
| "our novel module" | "Novel" without a named delta is an assertion of taste | "unlike [7], the module needs no per-scene tuning, at the cost of one extra hyperparameter" |
| "results demonstrate the effectiveness of X" | Demonstrates what, by how much, against whom | "X raises mIoU from 37.4 to 41.2 on D2 (Table 2), and the gain persists on D3 and D4" |
| "widely used in practice" | Frequency claim with no source | cite a survey or an adoption statistic, or delete the sentence |

Two mechanical rules that catch most of the table automatically: (i) no comparative adjective without a cell reference in the same sentence or the previous one; (ii) no universal quantifier (`all`, `any`, `every`, `always`) anywhere in Abstract or Conclusion unless the tested scope literally covers it.

## 6. Completion criteria

The claim–evidence review passes when all of the following hold, checked against the file, not against memory:

1. Every declarative sentence in Abstract, the Introduction contribution list, and the Conclusion has a row in the mapping table.
2. No row carries status `needs-evidence` or `unsupported`; every `weakened` or `removed` action is applied in the actual text, verified by searching the source for the old wording.
3. Every comparative claim names a table cell and a protocol match (backbone, budget, data).
4. Every causal claim has an isolating ablation row — one factor changed, the confounds closed.
5. Every generalization claim states its tested scope in the sentence, and that scope equals the scope in Experiments.
6. Every number in the Abstract appears in a table or figure with the same value, unit, and split.
7. No superlative (`best`, `SOTA`, `first`, `only`, `novel`) appears without a scope qualifier or an explicit comparison set.
8. The reverse sweep is empty: every table, figure, and ablation is cited by at least one claim, or its presence is justified.
9. A reader holding the paper plus this file can locate the evidence for any claim in under thirty seconds.

Fail condition, sufficient on its own: one abstract claim whose evidence row is empty. Fix that before touching style, structure, or figure quality — everything downstream of an unsupported headline claim is wasted revision.