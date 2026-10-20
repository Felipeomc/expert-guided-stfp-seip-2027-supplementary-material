# Supplementary Material

**Expert-Guided Software Team Formation in Practice: An Optimization Tool, Practitioner Validation, and Lessons Learned**

This repository contains the reproducibility workbooks and the supplementary-material PDF for the paper. It preserves the project-level experimental evidence underlying every reported result (GA calibration, surrogate fidelity, the exact MILP reference, the historical backtest, the algorithmic and direct-LLM baselines, and the blinded practitioner validation) without altering, rounding, or recalculating any experimental value. No sensitive or personally identifiable information is included beyond what was already present, anonymized, in the source organizational data; developer identifiers (e.g. `Dev370`) and project names are preserved as anonymized/pseudonymized source identifiers, not real names.

## 1. Package Structure

```
expert-guided-stfp-seip-2027-supplementary-material/
|-- README.md                                    This file
|-- Supplementary_Material__SEIP_Felipe_.pdf      Supplementary tables S1-S13 covering the dataset,
|                                                  RQ2-RQ5 evidence, V2 algorithmic baselines,
|                                                  runtime provenance, and practitioner validation
|-- 01_GA_Calibration_Adaptive_Racing.xlsx        GA configuration selected by the adaptive-racing
|                                                  procedure (Section IV-C / "Search: A Calibrated GA")
|-- 02_RQ1_Surrogate_Fidelity.xlsx                RQ1: fidelity of the closed-form surrogate to
|                                                  the elicited Bayesian Network
|-- 03_RQ2_MILP_vs_Calibrated_GA.xlsx             RQ2: calibrated GA vs. the exact MILP reference,
|                                                  12 controlled size-four benchmark projects
|-- 04_RQ3_Historical_Backtest_2025.xlsx          RQ3: calibrated GA vs. the organization's real
|                                                  historical teams, 16 held-out 2025 projects
|-- 05_RQ4_Algorithmic_Baselines.xlsx             RQ4: calibrated/refined GA vs. Greedy, Random,
|                                                  and GA_uniform under the refined evaluator
|-- 06_RQ4_Direct_LLM_vs_Calibrated_GA.xlsx       RQ4: calibrated GA vs. the selected direct,
|                                                  leakage-controlled zero-shot LLM response
|-- 07_RQ5_Practitioner_Validation_.xlsx           RQ5: blinded pairwise comparisons (vs. historical
|                                                  and vs. GA_uniform) and isolated team acceptability
|-- 08_RQ5_TeamPlus_Followup.xlsx                 RQ5: formative hands-on TeamPlus follow-up case
|                                                  (one seeded six-person recommendation)
```

Each `.xlsx` file is self-contained: it embeds its own **README**, **Summary**, one or more **raw data** sheets, and a **Source Manifest** sheet. No external file or script is needed to interpret any workbook.

## 2. How to Use This Package

No installation, environment, or code execution is required. Every result reported in the paper is already computed and stored in these workbooks as **evidence**, not as code to be re-run; open any `.xlsx` file directly in Excel, LibreOffice Calc, or Google Sheets.

Each workbook follows the same internal structure:

| Sheet | Purpose |
|---|---|
| `README` | Workbook purpose, research question, scope, worksheet guide, and preservation/confidentiality notes specific to that file. |
| `Summary` | The key comparison table(s) reported in the paper, independently recomputed from the raw sheets (never hand-typed), plus interpretation text and a chart where useful. |
| Raw data sheet(s) | The underlying experimental records, copied verbatim from the organization's original result files, with headers translated to English and original field names documented. |
| `Source Manifest` | Relative source path, file type, size, row/column counts, and SHA-256 checksum for every source file used to build that workbook. |

Formulas in the `Summary`/`Comparison` sheets reference the raw sheets directly (e.g. `06_RQ4_Direct_LLM_vs_Calibrated_GA.xlsx`), so recalculating the workbook in Excel reproduces the same aggregate figures from the same raw rows.

## 3. Workbook-by-Workbook Guide

### 01 — GA Calibration (Adaptive Racing)
The reduced-budget adaptive-racing procedure (F-Race/Iterated-Racing inspired) that selected the GA configuration used throughout the paper, run on the 205 pre-2025 projects (144 training / 31 validation / 30 test, chronologically split). Contains the full staged rankings and all 2,091 individual configuration-evaluation runs.
**Key result:** selected mean fitness 0.6120 vs. baseline 0.5983 on the held-out test set (relative gain 2.29%; 108 wins / 35 losses / 7 ties across 150 paired test runs).

### 02 — RQ1: Surrogate Fidelity
Fidelity of the closed-form surrogate to the elicited Bayesian Network, over the enumerated input space (26,250 scenarios), on 1,200 real team configurations, and against the six prior expert-workshop scenarios.
**Key result:** Brier = 0.0156, MAE = 0.0385 on 5,320 held-out input scenarios; Brier = 0.0328, MAE = 0.0496 on real team configurations.

### 03 — RQ2: MILP Reference vs. Calibrated GA
The GA vs. an exact Mixed-Integer Linear Programming (MILP, Gurobi) reference solving the identical surrogate objective, on 12 controlled size-four (k=4) benchmark projects, 30 GA runs each.
**Key result:** the GA reached the certified optimum in 8 of 12 projects; the mean best-of-30 gap was 0.50% (max 2.26%); 73/360 individual runs hit the exact optimum; median per-project speedup 13.95x.

### 04 — RQ3: Historical Backtest (2025)
Calibrated GA vs. the organization's real historical teams on the 16 temporally held-out 2025 projects, 30 GA runs per project.
**Key result:** the GA's best-of-30 recommendation outscored the historical team in all 16 projects; mean relative gain 35.15% (median 34.27%); mean AE gain 0.1466.

### 05 — RQ4: Algorithmic Baselines
The calibrated/refined GA is compared with Greedy, Random, and GA_uniform on the same 16 held-out 2025 projects. GA_uniform uses an equal-weight simple-mean search objective. Its representative team is selected by maximum `fitness_uniform` across 30 seeds per project, with the lowest seed breaking exact ties, and is then evaluated with the final refined evaluator. Random-Search is excluded from this post-refinement comparison because its refined execution was incomplete; the earlier experiment remains separate.
**Key result:** under the common refined evaluator, the calibrated/refined GA achieved a mean AE of 0.5905 versus 0.5675 for GA_uniform, with 14 wins, 2 ties, and 0 losses. It also outscored Random and Greedy on all 16 projects.

### 06 — RQ4: Direct LLM vs. Calibrated GA
Calibrated GA vs. the selected response from a leakage-controlled, zero-shot direct-LLM baseline using ChatGPT's web interface (recorded interface model label `GPT-5.6 Sol`; reasoning mode set to `High`), on the same 16 held-out 2025 projects.
**Key result:** the GA best-of-30 outscored the selected LLM response on all 16 projects; mean AE gap 0.1241 (95% CI [0.0802, 0.1680]); mean relative gain 25.03%.

### 07 — RQ5: Blinded Practitioner Validation
The staffing authority's blinded pairwise comparisons (calibrated GA vs. historical team, and vs. GA_uniform where compositions differed) and isolated acceptability judgements for the 16 calibrated-GA teams. Includes the decoded condition cross-reference for every anonymized team code and the within-participant consistency checks. Nineteen comparison rows involving a since-confirmed-contaminated direct-LLM condition were excluded from this workbook; only the 33 retained historical/GA_uniform comparisons are included, matching the paper's design exactly.
**Key result:** vs. historical, calibrated GA selected in 3/16 (18.8%), equivalent in 1/16 (6.3%), historical in 12/16 (75.0%); vs. GA_uniform, calibrated GA in 2/12 (16.7%), equivalent in 5/12 (41.7%), GA_uniform in 5/12 (41.7%); acceptability 12/16 (75.0%) staffable as-is or with minor changes.

### 08 — RQ5: TeamPlus Formative Follow-Up
The single hands-on TeamPlus session that followed the blinded RQ5 workbook: one new six-person project case, one fixed-seed GA execution, 20 ranked candidate teams.
**Key result:** the participant accepted the rank-1 recommendation (AE = 0.8411) without any roster change; this is descriptive, formative evidence from one seeded run and is not part of the RQ5 acceptability count.

## 4. Reproducibility Notes

* No experimental value was corrected, rounded, reordered, filtered, or recomputed in any raw data sheet. Only column headers, sheet names, and added documentation/interpretation text were translated to English; original source field names are documented in every raw sheet and in each workbook's Source Manifest.
* Every `Summary` figure quoted above was independently recomputed from the corresponding workbook's raw sheets during preparation of this package and matches the paper's reported values exactly.
* Every workbook's `Source Manifest` sheet lists the exact source files (path, type, size, row/column counts, SHA-256) used to build it, so any project-level figure can be traced back to its origin.
* Project names and developer identifiers throughout this package are the organization's own anonymized/pseudonymized identifiers (e.g. `Dev370`, `P439`), not real names. Each workbook's `README` sheet carries a confidentiality note specific to its content.

## 5. Contact

For questions about this material, please contact the corresponding author.
