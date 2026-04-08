# Metabolomics Workflow — Workshop Notebook

This repository contains a Jupyter notebook for end-to-end analysis of untargeted metabolomics data. It was developed for use in the BIO513 Systems Biology course at the University of Gothenburg and covers the full analytical pipeline from raw feature table to statistical results and visualisations.

---

## Overview

The notebook walks through a standard metabolomics analysis workflow in a single, configurable pipeline:

| Step | Description |
|---|---|
| Data loading | Reads a CSV feature table with sample metadata and metabolite abundances |
| Preprocessing | Missing value imputation, normalisation, log transformation, and scaling |
| Univariate analysis | t-test and/or Mann-Whitney U test with Benjamini-Hochberg FDR correction |
| Volcano plot | Visual summary of fold change vs. statistical significance |
| PCA | Principal component analysis with scores plot and biplot |
| OPLS-DA | Supervised multivariate classification with permutation testing, VIP scores, and S-plot |
| Visualisations | Boxplots for top metabolites, metabolite and sample correlation heatmaps, abundance heatmap |
| PDF report | Automated summary report of all results |

---

## Dataset

The example dataset used in this notebook is `children_infection_control_primary_53_64_125.csv`, a primary metabolomics dataset comparing children with infection vs. healthy controls.

> The data file is not tracked in this repository. Place it in the same directory as the notebook before running.

---

## Requirements

Install the required packages with:

```bash
pip install pandas numpy matplotlib scipy scikit-learn
```

---

## How to Use

1. Clone this repository:

```bash
git clone <repo-url>
cd <repo-folder>
```

2. Place your data file in the repository folder.

3. Open the notebook:

```bash
jupyter notebook metabolomics_workflow_notebook.ipynb
```

4. Update the **Configuration** cell at the top of the notebook to match your data:

```python
input_file        = "your_data.csv"   # path to your CSV file
sample_col        = None              # column name for sample IDs (None = auto-detect first column)
group_col         = None              # column name for group labels (None = auto-detect second column)
normalization     = "pqn"             # none | total_sum | pqn
log_transform     = "log2"            # none | log2 | log10 | ln
scaling           = "pareto"          # none | uv | pareto
univariate_method = "both"            # t_test | mannwhitney | both
```

5. Run all cells from top to bottom (**Cell → Run All**).

---

## Input Data Format

The CSV file must follow this structure:

| sample_id | group | metabolite_1 | metabolite_2 | ... |
|---|---|---|---|---|
| S01 | control | 1234.5 | 567.8 | ... |
| S02 | infection | 2345.6 | 432.1 | ... |

- **Column 1:** Sample identifiers
- **Column 2:** Group labels (exactly two groups for OPLS-DA)
- **Columns 3+:** Numeric metabolite abundances (missing values allowed)

---

## Outputs

All results are saved to the `results/` folder (created automatically):

| File | Description |
|---|---|
| `processed_data.csv` | Normalised and scaled abundance matrix |
| `transformed_unscaled_data.csv` | Log-transformed but unscaled matrix |
| `univariate_results.csv` | Full univariate statistics table |
| `volcano_plot_data.csv` | Data underlying the volcano plot |
| `pca_scores.csv` | PCA scores per sample |
| `oplsda_splot_data.csv` | S-plot correlation and covariance values |
| `metabolite_correlation_matrix_clustered.csv` | Clustered metabolite correlation matrix |
| `sample_correlation_matrix_clustered.csv` | Clustered sample correlation matrix |
| `metabolomics_report.pdf` | Automated PDF report with all figures |
| `run_metadata.json` | Record of all parameters used in the run |
| `boxplots/` | Individual boxplots for top significant metabolites |

---

## Analysis Parameters

| Parameter | Default | Options | Description |
|---|---|---|---|
| `normalization` | `pqn` | `none`, `total_sum`, `pqn` | Sample normalisation method |
| `log_transform` | `log2` | `none`, `log2`, `log10`, `ln` | Log transformation |
| `scaling` | `pareto` | `none`, `uv`, `pareto` | Feature scaling |
| `univariate_method` | `both` | `t_test`, `mannwhitney`, `both` | Statistical test |
| `pca_components` | `5` | integer ≥ 2 | Number of PCA components |
| `opls_components` | `1` | integer ≥ 1 | Number of OPLS-DA components |
| `cv_folds` | `5` | integer ≥ 2 | Cross-validation folds |
| `outer_cv_folds` | `0` | integer; 0 = skip | Outer folds for nested CV |
| `permutations` | `200` | integer | Permutations for OPLS-DA validation |
| `p_threshold` | `0.05` | float | Significance threshold for volcano plot |
| `fc_threshold` | `1.0` | float | Fold change threshold (log2 scale) |
| `corr_method` | `pearson` | `pearson`, `spearman` | Correlation method for heatmaps |
