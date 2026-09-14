# Credit Risk Scoring

> An end-to-end credit risk modelling project for estimating the probability of default (PD), comparing interpretable scorecards with machine-learning models, and evaluating calibration and decision-usefulness.

## Overview

This project develops a credit scoring workflow from raw data preparation through model comparison and calibration. It examines two complementary approaches:

- A **logistic-regression scorecard**, emphasizing transparency and explainability.
- An **XGBoost model**, used as a non-linear machine-learning benchmark.

The aim is to estimate default risk consistently and to assess the trade-offs among predictive power, calibration, interpretability, stability, and practical decision use.

> This is a portfolio and analytical project. It is not presented as a production lending system, an automated credit-decision engine, or a model used with live customer data.

## Business objective

For each applicant or account, the model estimates:

\[
PD = P(\text{default} = 1 \mid X)
\]

where \(X\) represents available borrower, credit, and behavioural characteristics. A PD estimate can support risk-based segmentation, manual-review prioritization, credit-policy analysis, or pricing decisions, subject to lending policy, fairness, regulatory, and governance controls.

A model output must not be treated as the sole basis for an adverse action or credit decision.

## Analytical workflow

```text
Raw credit data
      |
      v
Data preparation and target definition
      |
      v
EDA, data quality, missingness, and class distribution checks
      |
      +--> Logistic-regression scorecard
      |
      +--> XGBoost benchmark
                    |
                    v
Performance comparison and probability calibration
                    |
                    v
Threshold / risk-band analysis and model interpretation
                    |
                    v
Decision support with human and policy governance
```

## Repository structure

```text
credit-risk-scoring/
├── notebooks/  # Data preparation, EDA, modelling, comparison, calibration
├── outputs/    # Generated analytical outputs and artifacts
├── src/        # Reusable Python code
├── README.md
├── pyproject.toml
└── uv.lock
```

## Notebooks

| Notebook | Purpose |
|---|---|
| `01_data_preparation.ipynb` | Prepares modelling data, defines the target, and establishes a reproducible analytical dataset. |
| `02_eda.ipynb` | Explores distributions, missingness, feature relationships, class balance, and data-quality issues. |
| `03_scorecard_logistique.ipynb` | Develops an interpretable logistic-regression scorecard for default-risk estimation. |
| `04_xgboost.ipynb` | Develops an XGBoost model as a machine-learning benchmark. |
| `05_model_comparison_and_calibration.ipynb` | Compares candidates and assesses calibration of predicted default probabilities. |

## Model approaches

### Logistic-regression scorecard

The scorecard is a transparent baseline for modelling PD. Its strengths include clear feature effects, easier explanation to business stakeholders, and a natural path toward risk bands or points-based scorecards. It is especially useful when interpretability, documentation, and model governance are primary constraints.

### XGBoost benchmark

XGBoost captures non-linear relationships and interactions that may not be represented in a linear scorecard. It is evaluated as a benchmark, not presumed to be superior by default. Any performance improvement must be weighed against explainability, stability, calibration, fairness, and operational complexity.

### Calibration

A ranking model can separate higher- and lower-risk cases while still producing poorly calibrated probabilities. Since PD is often used quantitatively, calibration is assessed separately from discrimination. A well-calibrated prediction should correspond, over appropriate groups and horizons, to observed default rates.

## Evaluation framework

The project evaluates models through complementary dimensions rather than a single score:

| Dimension | Why it matters |
|---|---|
| Discrimination | Measures how well the model ranks higher-risk and lower-risk cases. Typical measures can include ROC-AUC, Gini, KS, or PR-AUC where appropriate. |
| Calibration | Assesses whether predicted PD values align with observed default rates. |
| Threshold / risk-band behaviour | Tests the operational impact of cut-offs or segmentation rules. |
| Stability | Examines whether results remain consistent across time periods or relevant population segments. |
| Interpretability | Ensures risk drivers can be explained and challenged. |
| Governance readiness | Considers reproducibility, documentation, data lineage, limitations, and monitoring needs. |

## Decision-use considerations

The project treats scoring as decision support. A practical lending workflow can be:

```text
Applicant / account data
          |
          v
Validated features -> PD model -> calibrated PD
          |
          v
Risk band, policy rules, and affordability checks
          |
          v
Approve / refer / decline decision process
          |
          v
Human review and adverse-action / audit requirements where applicable
```

Thresholds must be set using business objectives and policy constraints, not selected only to maximize a technical metric. Relevant considerations include expected loss, approval rate, customer outcomes, portfolio concentration, review capacity, and false-positive/false-negative cost.

## Responsible modelling and governance

- Use model outputs as a controlled input to credit decisions, not as an unchallenged automated determination.
- Preserve feature definitions, target horizon, observation window, sample splits, and transformation logic.
- Evaluate performance, calibration, and stability before and after deployment.
- Test for prohibited variables, proxy effects, disparate outcomes, and applicable fairness or regulatory requirements.
- Keep sensitive borrower data out of source control; use synthetic, anonymized, or properly governed data in public demonstrations.
- Record model version, feature schema, calibration method, score, policy outcome, and reviewer action where relevant.

## Running the project

The project uses Python and is configured with `pyproject.toml` and `uv.lock`.

```bash
uv sync
uv run jupyter notebook
```

Run the notebooks in numerical order. Verify expected data paths and data-governance requirements before execution.

## Current status

**Current phase: completed analytical workflow and portfolio documentation.** The repository includes data preparation, EDA, logistic scorecard modelling, XGBoost benchmarking, and model comparison/calibration. The next increment would be a formal validation report covering target definition, data lineage, discrimination, calibration, stability, explainability, fairness checks, and monitoring recommendations.
