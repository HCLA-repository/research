# HCLA: Experimental Source Code and Results

This repository contains selected Jupyter notebooks and experimental output files associated with **“HCLA: A Human-Centered LLM-Agent Architecture for Contextualizing Digital Asset Anomaly Detection.”** The files are organized by research question (RQ1–RQ5), with separate directories for experimental code, recorded outputs, and shared analysis resources.

**Scope:** This is a curated research artifact package. The included result files can be inspected and compared with the manuscript, but the presence of a notebook alongside a CSV does not, by itself, establish which exact execution or code revision generated that CSV. No experiments were rerun when this package was assembled.

## Repository Structure

```text
01_RQ1_Detector_Generalization/
  01_source/
    HCLA_Qwen_Llama_OpenRouter_Checkpoint_Resume.ipynb
  02_results/
    rq1_all_runs.csv
    rq1_mean.csv
    rq1_sd.csv
    rq1_paper_mean_sd.csv

02_RQ2_Narrative_Grounding/
  01_source/
    HCLA_RQ2_LIGHT_LGBM_50plus10x10.ipynb
  02_results_main50/
    rq2_main50_narratives.csv
    rq2_main50_claims.csv
    rq2_main50_metrics_by_case.csv
    rq2_main50_paper_summary.csv
  03_results_stability10x10/
    rq2_stability10x10_narratives.csv
    rq2_stability10x10_claims.csv
    rq2_stability10x10_metrics.csv
    rq2_stability10x10_paper_summary.csv

03_RQ3_Explanation_Comparison/
  01_source/
    HCLA_RQ3_4Methods_50Cases.ipynb
  02_results/
    rq3_explanations.csv
    rq3_judgments.csv
    rq3_summary.csv
    rq3_friedman_test.csv
    rq3_posthoc_wilcoxon_holm.csv
    rq3_ceiling_diagnostics.csv

04_RQ4_Component_Ablation/
  01_source/
    RQ4_ONLY_HCLA_Component_Ablation.ipynb
  02_results/
    rq4_ablation_full.csv
    rq4_ablation_summary.csv
    rq4_case_level_aggregated.csv
    rq4_caselevel_friedman_wilcoxon_holm.csv

05_RQ5_Robustness/
  01_source/
    RQ5_Standalone_NoJSON.ipynb
  02_results/
    rq5_robustness_full.csv
    rq5_robustness_summary.csv
    rq5_case_level_aggregated.csv
    rq5_caselevel_friedman_wilcoxon_holm.csv

06_Shared_Inputs_and_Statistics/
  01_input/
    evidence_packages.pkl
  02_source/
    HCLA_RQ3_RQ4_RQ5_PostHoc_Statistics.ipynb
```

## RQ1 — Detector Generalization

**Source:** `01_RQ1_Detector_Generalization/01_source/HCLA_Qwen_Llama_OpenRouter_Checkpoint_Resume.ipynb`

The integrated notebook includes detector preprocessing, random and temporal data partitioning, address-feature inclusion/removal, evaluation metrics, checkpointing, and additional HCLA experimentation. Its RQ1 section evaluates four protocols (E1–E4) across multiple classifiers, including LightGBM, Logistic Regression, Random Forest, and XGBoost.

**Recorded files:**
- `rq1_all_runs.csv` — 48 detector/protocol/seed runs.
- `rq1_mean.csv` and `rq1_sd.csv` — aggregated detector performance.
- `rq1_paper_mean_sd.csv` — paper-oriented summary of mean and standard deviation.

**Manuscript mapping:** Table 3 and supplementary Tables 9–11.

## RQ2 — Narrative Evidence Grounding

**Source:** `02_RQ2_Narrative_Grounding/01_source/HCLA_RQ2_LIGHT_LGBM_50plus10x10.ipynb`

This notebook prepares LightGBM-based evidence packages, generates Baseline and HCLA narratives using Qwen, and assesses claim-level support using a Llama judge. The main experiment uses **50 matched cases × 2 conditions**, and the stability experiment uses **10 cases × 2 conditions × 10 repetitions**.

**Recorded files:**
- `02_results_main50/rq2_main50_narratives.csv` — 100 generated explanations.
- `02_results_main50/rq2_main50_claims.csv` — 613 evaluated claim rows.
- `02_results_main50/rq2_main50_metrics_by_case.csv` — 100 case-condition metric rows (ESR, UCR, CR, EC).
- `02_results_main50/rq2_main50_paper_summary.csv` — Baseline and HCLA summary metrics.
- `03_results_stability10x10/rq2_stability10x10_narratives.csv` — 200 repeated explanations.
- `03_results_stability10x10/rq2_stability10x10_claims.csv` — 1,190 evaluated claim rows.
- `03_results_stability10x10/rq2_stability10x10_metrics.csv` — 200 case-condition-repetition metric rows.
- `03_results_stability10x10/rq2_stability10x10_paper_summary.csv` — stability summary metrics.

**Manuscript mapping:** Section 4.3 and Table 4.

## RQ3 — Explanation Format Comparison

**Source:** `03_RQ3_Explanation_Comparison/01_source/HCLA_RQ3_4Methods_50Cases.ipynb`

This notebook compares four explanation formats for matched cases: **Numerical**, **Feature Attribution**, **Template**, and **HCLA**. Each is evaluated on **Clarity**, **Evidence Integration**, and **Calibrated Usefulness** using a Llama-based rubric. The code configures a 50-case full evaluation (`RQ3_PILOT = False`, `RQ3_FULL_N = 50`), although a separate pilot mode is also defined.

**Recorded files:**
- `rq3_explanations.csv` — 200 explanations (50 cases × 4 formats).
- `rq3_judgments.csv` — 200 explanation-level automated judgments.
- `rq3_summary.csv` — per-format metric summaries.
- `rq3_friedman_test.csv` — Friedman tests for the three quality metrics.
- `rq3_posthoc_wilcoxon_holm.csv` — pairwise Wilcoxon results with Holm correction.
- `rq3_ceiling_diagnostics.csv` — score concentration and ceiling-effect diagnostics.

**Manuscript mapping:** Sections 4.4 and 5.3; Tables 5–6.

## RQ4 — Component Ablation

**Source:** `04_RQ4_Component_Ablation/01_source/RQ4_ONLY_HCLA_Component_Ablation.ipynb`

This notebook compares **Full HCLA**, **Without Role Separation**, **Without Evidence Constraint**, and **Without Interactive Refinement**. The experimental design uses **50 cases × 4 conditions × 3 repetitions** and records both claim-grounding metrics (ESR, UCR, CR) and automated quality ratings (Clarity, Trust Support, Actionability).

**Recorded files:**
- `rq4_ablation_full.csv` — 600 case-condition-repetition records.
- `rq4_ablation_summary.csv` — descriptive metric summaries.
- `rq4_case_level_aggregated.csv` — 200 case-condition averages after averaging repetitions.
- `rq4_caselevel_friedman_wilcoxon_holm.csv` — case-level Friedman and Holm-adjusted Wilcoxon analyses.

### RQ4: Data Generation and Final Statistical Analysis

The RQ4 results are associated with **two separate notebooks**:

1. **Experiment generation:** `04_RQ4_Component_Ablation/01_source/RQ4_ONLY_HCLA_Component_Ablation.ipynb` defines the four ablation conditions and the three-repeat experiment. Its archived output, `rq4_ablation_full.csv`, contains **600 observations** (50 cases × 4 conditions × 3 repetitions), with descriptive results corresponding to manuscript **Table 7**.
2. **Final case-level inference:** `06_Shared_Inputs_and_Statistics/02_source/HCLA_RQ3_RQ4_RQ5_PostHoc_Statistics.ipynb` aggregates the three repetitions within each `case_id` and `condition`, yielding **200 case–condition means**. Friedman tests use **50 matched cases**, followed by paired Wilcoxon signed-rank tests with Holm correction across six condition pairs. The archived `rq4_caselevel_friedman_wilcoxon_holm.csv` corresponds to manuscript **Table 12**.

**Important implementation distinction:** The experimental notebook and an earlier section of the shared statistical notebook also contain a case–repetition (`index=["case_id", "rep"]`) analysis. That approach treats up to 150 case–repetition combinations as separate blocks and is **not** the reference implementation for the final manuscript's case-level inference. Use the `groupby(["case_id", "condition"])` aggregation and subsequent `index="case_id"` pivot in the shared post-hoc notebook when checking Table 12. Having both variants in the archive does not prove which revision was executed originally.

**Manuscript mapping:** Sections 4.5 and 5.4; Tables 7 and 12.

## RQ5 — Robustness and Repeated Generation

**Source:** `05_RQ5_Robustness/01_source/RQ5_Standalone_NoJSON.ipynb`

This standalone notebook generates and evaluates responses under **Standard**, **Ambiguous**, and **Adversarial** instructions. It includes checkpointing, claim-based evaluation, and semantic-consistency estimation.

**Recorded files:**
- `rq5_robustness_full.csv` — 1,500 observations (50 cases × 3 conditions × 10 repetitions).
- `rq5_robustness_summary.csv` — summary statistics by condition.
- `rq5_case_level_aggregated.csv` — 150 case-condition averages.
- `rq5_caselevel_friedman_wilcoxon_holm.csv` — case-level statistical comparisons.

### RQ5: Why the Code Says 100 but the Reported Experiment Uses 50

`RQ5_N_CASES = 100` sets a **maximum**, not a mandatory number of cases. The notebook then caps the selected sample to the available evidence packages:

```python
RQ5_N_CASES = min(RQ5_N_CASES, len(evidence_packages))
selected_cases = list(evidence_packages[:RQ5_N_CASES])
```

In the archived ZIP, `06_Shared_Inputs_and_Statistics/01_input/evidence_packages.pkl` contains **50 distinct cases**. The `rq5_robustness_full.csv` file contains **1,500 rows** across the same **50 case IDs**, three conditions (Standard, Ambiguous, Adversarial), and ten repetitions per case–condition combination. The set of case IDs in the PKL and CSV matches exactly.

Thus, under the archived input, the effective sample size is **min(100, 50) = 50 cases**, consistent with the design reported in manuscript **Table 8**. This verifies the archived sample-selection logic and output structure; it does not constitute an independent rerun of the LLM experiment.

**Manuscript mapping:** Sections 4.6 and 5.5; Table 8.

## Shared Input and Statistical Analysis

- `06_Shared_Inputs_and_Statistics/01_input/evidence_packages.pkl` — a serialized collection of selected transaction-level evidence packages, including detector outputs and feature attribution inputs used in explanation experiments.
- `06_Shared_Inputs_and_Statistics/02_source/HCLA_RQ3_RQ4_RQ5_PostHoc_Statistics.ipynb` — post-hoc analyses for RQ3–RQ5, including case-level aggregation, Friedman tests, paired Wilcoxon tests, and Holm correction.

**Data-sharing caution:** The PKL file may contain information derived from a restricted, provider-supplied research dataset. Confirm redistribution permission before placing it in a public repository.

## Reproducibility and Security Notes

- Notebook outputs and execution counts were cleared in the GitHub-oriented package. Missing saved outputs do not imply that an archived CSV was not generated in an earlier execution.
- Korean comments, documentation, and user-facing messages were translated to English for readability. Experimental datasets, CSV/PKL artifacts, and core experiment configuration were retained.
- API credentials must be supplied through **environment variables or an approved secret manager**. Do not commit API keys, credential-bearing notebook outputs, or local configuration files containing secrets.
- The raw provider-supplied Bitcoin dataset is **not included**. Re-executing detector training or SHAP extraction requires authorized access to the original data and the appropriate environment.
- Experimental outputs involving hosted LLMs may depend on API availability, model version, sampling parameters, and provider behavior.
- The archive permits checking RQ4 case-level statistical analysis and RQ5 sample selection against the retained outputs. The exact source revision used in the historical API executions is not independently established.
- Files are organized by their correspondence to the manuscript, **not** by independently verified commit-level provenance or complete end-to-end reproduction.

## Reference

**HCLA: A Human-Centered LLM-Agent Architecture for Contextualizing Digital Asset Anomaly Detection**

Repository: https://github.com/HCLA-repository/research

Please use the final published article for complete citation metadata once available.
