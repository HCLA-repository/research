# HCLA: Experimental Source Code and Results

## Overview

This repository provides the experimental source code, Jupyter notebooks, and selected result files associated with the study:

**HCLA: A Human-Centered LLM-Agent Architecture for Contextualizing Digital Asset Anomaly Detection**

The study extends the previously introduced HCLA framework by systematically evaluating detector generalization, evidence grounding, explanation quality, architectural components, and robustness.

The repository is organized around five research questions (RQ1–RQ5) to support transparency, result verification, and reproducibility.

## Research Questions

### RQ1 — Detector Generalization

**Research Question:** To what extent does the Evidence Scoring module generalize beyond recurring address-level associations?

RQ1 investigates the generalization performance of machine-learning anomaly detectors under four evaluation protocols:

- **E1:** Address-included reference evaluation.
- **E2:** Address features removed.
- **E3:** Temporal evaluation with address features removed.
- **E4:** Temporal and address-disjoint evaluation.

The experiments compare LightGBM, Logistic Regression, Random Forest, and XGBoost.

Under the E4 protocol, LightGBM achieves:

- PR-AUC: **0.8232**
- Anomaly F1-score: **0.7269**

**Manuscript correspondence:** Table 3 and supplementary Tables 9–11.

### RQ2 — Narrative Evidence Grounding

**Research Question:** To what extent are HCLA narratives supported by the evidence explicitly supplied to the Justification component?

RQ2 compares baseline explanations with evidence-constrained HCLA narratives.

The evaluation consists of:

- Main experiment: 50 matched cases × 2 conditions.
- Stability experiment: 10 cases × 2 conditions × 10 repetitions.
- Evaluation metrics: Evidence Support Rate (ESR), Unsupported Claim Rate (UCR), Contradiction Rate (CR), and Evidence Consistency (EC).

**Main findings:**

| Metric | Baseline | HCLA |
|---|---:|---:|
| ESR ↑ | 0.8998 | 0.9672 |
| UCR ↓ | 0.0968 | 0.0261 |
| CR ↓ | 0.0033 | 0.0067 |
| EC ↑ | 0.9360 | 0.9800 |

The results indicate that HCLA improves evidence support and reduces unsupported claims relative to the baseline, although not every grounding metric improves.

**Manuscript correspondence:** Table 4.

### RQ3 — Explanation Format Comparison

**Research Question:** How does HCLA compare with numerical, feature-attribution, and template-based explanations in clarity, evidence integration, and calibrated usefulness?

RQ3 evaluates four explanation formats using 50 matched cases:

1. **Numerical:** Prediction label and anomaly probability.
2. **Feature Attribution:** Prediction information with SHAP-based feature contributions.
3. **Template:** Deterministic explanation based on supplied evidence.
4. **HCLA:** LLM-generated contextual explanation using the evidence package.

A total of 200 explanations are evaluated using three metrics:

- Clarity
- Evidence Integration
- Calibrated Usefulness

**Reported HCLA results:**

| Metric | Mean | Standard Deviation |
|---|---:|---:|
| Clarity | 4.94 | 0.24 |
| Evidence Integration | 4.10 | 0.30 |
| Calibrated Usefulness | 4.78 | 0.42 |

Statistical analyses use Friedman tests and paired Wilcoxon comparisons with Holm correction.

All reported HCLA-versus-baseline comparisons remain statistically significant after correction.

These scores reflect automated evaluation and should not be interpreted as direct measurements of human decision performance.

**Manuscript correspondence:** Tables 5 and 6.

### RQ4 — Component Ablation

**Research Question:** What is the contribution of role separation, evidence constraints, and interactive refinement to narrative grounding and explanation quality?

RQ4 evaluates four configurations:

- Full HCLA
- HCLA without Role Separation
- HCLA without Evidence Constraint
- HCLA without Interactive Refinement

The experiment uses:

- 50 cases
- 4 conditions
- 3 repetitions
- **600 total observations**

Evaluation metrics include ESR, UCR, CR, Clarity, Trust Support, and Actionability.

The results show that evidence constraints contribute most strongly to narrative grounding.

For example, removing evidence constraints decreases ESR from **0.752 to 0.637** and increases UCR from **0.246 to 0.361**.

However, removing constraints can increase automated explanation-quality scores, indicating a trade-off between factual grounding and presentation quality.

Statistical analyses aggregate repeated observations at the case level before applying Friedman and Wilcoxon-Holm tests.

**Manuscript correspondence:** Tables 7 and 12.

### RQ5 — Robustness and Repeated Generation

**Research Question:** How stable and robust is HCLA under repeated generation, ambiguous queries, and adversarial instructions?

RQ5 evaluates three conditions:

- Standard
- Ambiguous
- Adversarial

The experiment includes 50 cases, 10 repetitions per condition, and **1,500 generated explanations**.

The evaluation considers:

- Evidence Support Rate
- Unsupported Claim Rate
- Contradiction Rate
- Constraint Adherence
- Semantic Consistency

The reported results demonstrate high evidence support under standard and ambiguous queries.

Adversarial instructions reduce constraint adherence from **0.9760 to 0.4960**, highlighting limitations of prompt-level evidence constraints.

**Manuscript correspondence:** Table 8.

## Models and Experimental Environment

The experiments use the following components:

| Component | Model or Method |
|---|---|
| Primary anomaly detector | LightGBM |
| Additional detectors | Logistic Regression, Random Forest, XGBoost |
| Explanation generation | Qwen3 235B A22B Instruct 2507 |
| Automated explanation evaluation | Llama 3.3 70B Instruct |
| Feature attribution | SHAP |
| LLM API access | OpenRouter |
| Statistical analysis | Friedman test, Wilcoxon signed-rank test, Holm correction |
| Implementation environment | Python / Jupyter Notebook |

Explanation generation and evaluation are conducted using separate language models.

The reported generation temperature is 0.2, while automated evaluation uses temperature 0.0.

## Reproducibility and Result Verification

The repository contains selected source files and experimental artifacts corresponding to the manuscript's reported results.

Available results have been organized by research question and checked against the reported experimental designs and numerical summaries.

These checks support **result-level consistency** but do not constitute independent end-to-end reproduction of every experiment.

Some notebooks retain outputs from preliminary or pilot executions. Such saved outputs should not be confused with the final experimental results recorded in the corresponding CSV files.

For repeated-measures analyses, observations are aggregated at the appropriate case level before statistical testing.

Reproducing experiments involving external language models requires valid API access, compatible model versions, the necessary input data, and the original experimental configuration.

## Data Availability

The experiments use a provider-labelled Bitcoin transaction dataset containing **387,419 transactions** collected between 2020 and 2024.

The dataset contains 318,388 normal and 69,031 anomalous transaction records.

The underlying dataset was supplied for academic research and is not included in this repository.

Derived experimental artifacts may also be subject to data-sharing restrictions.

## Limitations

The reported findings should be interpreted within the experimental protocols used in the manuscript.

Automated explanation-quality ratings do not establish improvements in human trust or real-world investigative performance.

The experiments also do not establish complete freedom from data leakage, formal causal faithfulness, or guaranteed resistance to adversarial instructions.

The proposed Evidence-Constrained Verification (ECV) algorithm is a methodological extension and was not empirically validated as part of the reported RQ1–RQ5 results.

## Citation

If you use this repository, please cite the associated HCLA study:

**HCLA: A Human-Centered LLM-Agent Architecture for Contextualizing Digital Asset Anomaly Detection.**

Please refer to the final published version for complete bibliographic information.

## Research Repository

https://github.com/HCLA-repository/research
