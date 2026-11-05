# HCLA Research: Evidence-Grounded Explanations for Digital Asset Anomaly Detection

This repository contains Jupyter notebooks supporting experiments on **Human-Centered LLM-Agent (HCLA)** explanations for digital asset anomaly detection. The study investigates detector generalization under different feature and split settings, the grounding of LLM-generated explanations in available evidence, explanation format, architectural component contributions, and robustness.

The experiments build upon the previously introduced HCLA framework, while examining its behavior under additional evaluation settings. The notebooks are research artifacts rather than a production deployment.

## Research questions

| Research question | Focus | Relevant directory |
| --- | --- | --- |
| **RQ1** | Detector performance and generalization across address-feature and data-splitting conditions | `notebooks/00_integrated/` |
| **RQ2** | Evidence support and unsupported claims in generated explanations | `notebooks/RQ2_evidence_validation/` |
| **RQ3** | Comparison of alternative explanation formats | `notebooks/RQ3_explanation_comparison/` |
| **RQ4** | Ablation of HCLA architectural components | `notebooks/RQ4_component_ablation/` |
| **RQ5** | Robustness to repeated generation, ambiguity, and adversarial instructions | `notebooks/RQ5_robustness/` |

Additional post-hoc statistical analysis for RQ3–RQ5 is provided under `notebooks/statistical_analysis/`.

## Repository structure

```text
research/
├── README.md
└── notebooks/
    ├── 00_integrated/
    │   └── HCLA_Qwen_Llama_OpenRouter_Checkpoint_Resume.ipynb
    ├── RQ2_evidence_validation/
    │   ├── HCLA_RQ2_LIGHT_LGBM_50plus10x10.ipynb
    │   ├── HCLA_RQ2_FAST_FULL_5workers.ipynb
    │   ├── HCLA_RQ2_TRUE_ONECLICK_NO_PREV_VARS.ipynb
    │   ├── HCLA_RQ2_LIGHT_LGBM_100rows_5workers.ipynb
    │   └── HCLA_RQ2_ONECLICK_From_RQ1_PKL.ipynb
    ├── RQ3_explanation_comparison/
    │   ├── HCLA_RQ3_4Methods_RevisedMetrics.ipynb
    │   └── HCLA_RQ3_4Methods_50Cases.ipynb
    ├── RQ4_component_ablation/
    │   └── RQ4_ONLY_HCLA_Component_Ablation.ipynb
    ├── RQ5_robustness/
    │   └── RQ5_Standalone_NoJSON.ipynb
    └── statistical_analysis/
        └── HCLA_RQ3_RQ4_RQ5_PostHoc_Statistics.ipynb
```

### Integrated notebook and RQ1

`00_integrated/HCLA_Qwen_Llama_OpenRouter_Checkpoint_Resume.ipynb` is **not exclusively an RQ1 notebook**: it includes the detector experiments and parts of the downstream LLM evaluation workflow. The RQ1 experiment compares four conditions:

| Condition | Address features | Evaluation split |
| --- | --- | --- |
| E1 | Included | Random |
| E2 | Removed | Random |
| E3 | Removed | Temporal |
| E4 | Removed | Temporal + address-disjoint |

These conditions help examine how apparent detector performance changes when potentially identifying features are removed and generalization is assessed under more restrictive splits.

### RQ2: Evidence validation

The RQ2 notebooks investigate whether explanations are supported by the detector outputs and accompanying evidence. They include different execution variants, including limited-sample runs, parallel processing, and workflows that use saved artifacts from earlier detector experiments. The available notebooks are alternatives or related experiments; they should not all be assumed to be consecutive steps of a single pipeline.

### RQ3: Explanation comparison

The RQ3 notebooks compare numerical, tabular, two-stage, and full HCLA explanation configurations. They provide alternative evaluation scripts and metric variants.

### RQ4: Component ablation

The RQ4 notebook examines the effect of removing selected components, including role separation, evidence constraints, and refinement, relative to the full configuration.

### RQ5: Robustness

The RQ5 notebook contains robustness-oriented tests covering repeated generation, ambiguous inputs, and adversarial prompting.

## Environment and dependencies

The notebooks use **Python 3** and Jupyter/Google Colab-style workflows. Dependencies differ between notebooks. Imported packages include:

- `numpy`, `pandas`, `scipy`, `matplotlib`
- `scikit-learn`, `lightgbm`, `xgboost`, `shap`
- `torch`
- `openai` (client used for compatible API calls)

A typical starting environment can be prepared using:

```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
python -m pip install jupyter numpy pandas scipy matplotlib scikit-learn lightgbm xgboost shap torch openai
jupyter lab
```

This is a **starting dependency list**, not a version-locked or fully validated environment specification. Some notebooks contain Google Colab-specific imports or paths and may require adjustments for local execution.

## Running the experiments

1. Clone the repository:

   ```bash
   git clone https://github.com/HCLA-repository/research.git
   cd research
   ```

2. Open the relevant notebook in Jupyter or Google Colab.
3. Obtain the corresponding research dataset through its authorized source and configure the notebook's input paths (for example, `DATA_PATH`). The dataset is not assumed to be bundled with this repository.
4. For notebooks using hosted LLMs, configure your own `OPENROUTER_API_KEY` securely. API access, model availability, usage limits, and costs may apply. **Do not commit API keys or credentials.**
5. Check notebook-specific configuration cells, saved-model/artifact paths, and upstream output requirements before running.
6. Execute the appropriate notebook and inspect the generated metrics and output artifacts.

**Suggested order:** Start with the integrated notebook to understand the detector and evidence-generation workflow. Then select the dedicated RQ2–RQ5 notebooks needed for the relevant analysis. Run the statistical-analysis notebook after generating its required input results.

> **Reproducibility note:** The notebooks have not been verified here as a clean, end-to-end run on a fresh machine. Exact numerical reproduction can depend on the dataset version, sampling, random seeds, package versions, external model versions, API behavior, and availability of upstream artifacts. A notebook filename such as `ONECLICK` does not eliminate these prerequisites.

## Methodological notes

- **Generalization:** RQ1 separates random-split evaluation from more restrictive temporal and address-disjoint settings.
- **Evidence grounding:** LLM-generated narratives should be evaluated against available evidence rather than treated as verified facts.
- **Ablation and robustness:** Component-level and stress-test results are intended to help characterize behavior and limitations, not to guarantee reliability on unseen applications.
- **External services:** Some experiments rely on third-party hosted language models; their outputs can vary over time.

## Data, privacy, and licensing

Raw data access and redistribution are subject to the original data provider's terms. Do not upload restricted transaction records, personal information, or credentials to this repository. Review data-handling requirements before sending any records to external model APIs.

No software license is asserted by this README. If reuse or redistribution is intended, add an appropriate `LICENSE` file. Without one, normal copyright restrictions apply.

## Citation

If you use this repository in academic work, please cite the associated HCLA publication(s). Full publication metadata and an authoritative BibTeX entry should be added once finalized. Distinguish the original framework paper from the subsequent evaluation/extension study when citing their respective contributions.

## Limitations

This repository contains experimental notebooks. Some scripts are alternative implementations or exploratory variants, and not all notebooks are guaranteed to run independently. Please check each notebook's input assumptions and configuration before use. Results should be interpreted within the study's data, model, and evaluation scope.
