# Computational Metabolomics (Computer Lab Module in BIO513)

## The Lab

The aim of this lab is to gain practical insight into metabolomics by reading the article:

> Mickiewicz B. *et al.* (2012). *NMR-based metabolic profiling provides diagnostic and prognostic information in critically ill children with suspected infection.* **Critical Care** 16:R172. https://doi.org/10.1186/cc11us

and analysing the corresponding dataset `children_infection.csv` using Python.

The lab has three steps:

1. **Read** the relevant parts of the article and try to understand what analyses were performed and what the main findings were.
2. **Apply** the uni- and multivariate methods you have learnt on the same data using Python. A notebook (`metabolomics_workflow_notebook.ipynb`) is provided as a starting point or source of inspiration — use of it is optional. Additional guidance on how the workflow operates and how to run it outside of a Jupyter Notebook is available in `Guide_to_Metabolomics_Workflow.docx`.
3. **Compare** your results with the article and discuss similarities, differences, and possible reasons for them.

You are free to perform any relevant analyses. However, since PCA and OPLS-DA are standard methods in metabolomics, you are encouraged to include them. Univariate analysis should also be performed.

> **Note on software:** R is more commonly used in metabolomics research due to the availability of specialised packages. Here we use Python, which gives you more flexibility in how you structure the analysis.

---

## The Dataset

The dataset contains ¹H NMR urine metabolite profiles from children admitted to a paediatric intensive care unit (PICU), across three groups: **Infection**, **SIRS** (systemic inflammatory response without confirmed infection), and **Control** (healthy children).

> ⚠️ **Data preparation:** The workflow notebook requires exactly **two groups**. Before running, filter `children_infection.csv` to the two groups you want to compare (e.g. Infection vs. Control) — either in Excel or by modifying the `KEEP_GROUPS` variable in the notebook configuration cell.

---

## Repository Contents

| File | Description |
|---|---|
| `metabolomics_workflow_notebook.ipynb` | Jupyter notebook — full analysis pipeline as a starting point |
| `Guide_to_Metabolomics_Workflow.docx` | Guide explaining the workflow and how to run it from the command line |
| `children_infection.csv` | NMR metabolite dataset (all three groups) |

---

## Getting Started

### Option A — Google Colab (recommended, no installation required)

1. Go to [colab.research.google.com](https://colab.research.google.com), choose **File → Open notebook → GitHub**, and paste this repository URL.

2. Run the **Setup → Step 1** cell to install packages. When prompted, go to **Runtime → Restart session**.

3. Run the **Step 2** cell — `children_infection.csv` will be downloaded automatically from GitHub into your Colab session.

> ⚠️ Colab sessions are temporary. Download any output files you want to keep before closing the session.

### Option B — Local Jupyter

1. Clone the repository:

```bash
git clone https://github.com/UjalaBashir/Bio513_metabolomics.git
cd Bio513_metabolomics
```

2. Install dependencies:

```bash
pip install pandas numpy matplotlib scipy scikit-learn seaborn
```

3. Launch Jupyter and open the notebook:

```bash
jupyter notebook
```

---

## Output Files

All results are saved to a `results/` folder created automatically when you run the notebook:

| File | Description |
|---|---|
| `processed_data.csv` | Imputed, normalised, log-transformed and scaled matrix (used for PCA and OPLS-DA) |
| `transformed_unscaled_data.csv` | Normalised and log-transformed but not scaled (used for univariate analysis and boxplots) |
| `pqn_dilution_factors.csv` | Per-sample PQN dilution factors |
| `univariate_results.csv` | Full table of t-test and Mann-Whitney statistics with FDR correction |
| `volcano.png` | Volcano plot |
| `boxplots/` | Individual boxplots for top-ranked metabolites |
| `pca_scores.png` / `pca_biplot.png` | PCA scores plot and biplot |
| `oplsda_scores.png` / `oplsda_splot.png` | OPLS-DA scores plot and S-plot |
| `oplsda_vip.png` | VIP bar plot |
| `oplsda_permutation_q2.png` | Permutation test histogram |
| `metabolomics_report.pdf` | Automated PDF report with all figures and settings |

---

## Group Work

The lab is designed to be completed in **groups of 2–3 students**. Groups should:

- Divide exploration tasks (e.g. one person runs OPLS-DA while another builds the volcano plot)
- Discuss exercise answers together before writing them up individually
- Collaborate on interpreting results but submit individual reports

All group members should be able to explain every step of the analysis.

---

## Report Guidelines

Submit one report per student, written as a **short scientific paper** (approximately 1500–2500 words, excluding figures). The report should present your results and compare methods and relevant findings with those reported in the original article. Discuss your results in relation to the study's conclusions.

### Structure

| Section | Content |
|---|---|
| **Introduction** | Brief background on NMR metabolomics, the clinical context, and the aim of your analysis |
| **Methods** | Preprocessing choices with justification; statistical tests; multivariate modelling; validation strategy |
| **Results** | Univariate findings, PCA, OPLS-DA performance and top metabolites — reference your figures |
| **Discussion** | Biological interpretation of top metabolites; comparison with Mickiewicz *et al.*; limitations |

### Figures

Include at least **four figures** with captions:

1. Volcano plot
2. PCA scores plot
3. OPLS-DA scores plot and permutation test
4. VIP plot or S-plot
5. *(Optional)* Boxplots of top metabolites or clustered heatmap

### Assessment criteria

- Correct execution and interpretation of the analyses
- Quality and clarity of figures and captions
- Depth of biological interpretation and connection to the original article
- Critical discussion of methodological choices and their limitations
- Clarity of writing
