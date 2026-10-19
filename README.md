# Ancient_Highland_Tibetan_Body_Form_Analysis

## Overview

This repository contains the R Markdown analytical workflow developed for the manuscript:

**Shaped by the Highlands: Skeletal Evidence for Body Form Variation among Ancient Tibetan Plateau Populations**

The research investigates variation in skeletal body size and proportions among ancient populations from the Tibetan Plateau, with comparisons to archaeological populations from lowland China and selected published reference samples.

Using osteometric data, the study examines patterns of estimated stature, body mass, body mass index, limb proportions, relative bi-iliac breadth, trunk-to-lower-limb proportions, and sexual dimorphism. These comparisons contribute to broader discussions of human biological variation and adaptation to high-altitude environments.

The repository provides a documented workflow linking the underlying measurements and derived variables to descriptive statistics, statistical comparisons, sensitivity analyses, and manuscript figures.

The primary aims of this repository are to:

- Document the analytical procedures used in the study.
- Provide transparent and traceable statistical workflows.
- Facilitate reproducibility of the reported quantitative results, subject to data access.
---

## 1. Repository Contents

The central analytical file is:

**`ATP_Body_Form_Analysis.Rmd`**

This R Markdown document contains the workflow from data import to the production of the revised manuscript figures and statistical tables.

### Repository structure

```text
Ancient_Highland_Tibetan_Body_Form_Analysis/
│
├── README.md
├── ATP_Body_Form_Analysis.Rmd
├── data
└── outputs
 
```

The `outputs/` subdirectories are generated when the analysis runs and are not required to be tracked in the repository.

| File | Description |
|---|---|
| `ATP_Body_Form_Analysis.Rmd` | Complete statistical analyses and manuscript figure-generation code |
| `README.md` | Research overview, repository documentation and reproducibility instructions |
| `data/README.md` | Input data descriptions, variable information and access considerations |

---

## 2. Data and Study Samples

The analyses draw on osteometric datasets representing archaeological populations from the Tibetan Plateau and lowland China, together with published comparative data.

The workflow distinguishes between individual-level measurements, anatomical measurements used to derive trunk-to-lower-limb proportions, published reference observations, and bone-level measurements from commingled archaeological material.

### Required input files

Four CSV files are expected in the `data/` directory:

| Filename | Description |
|---|---|
| `BodyForm_REVISED` | Main analytical dataset containing body size, body proportions and associated information |
| `ASTA_and_Measurements_High_and_Low.csv` | Anatomical measurements used to calculate trunk-to-lower-limb ratios |
| `STAvsRLLL.csv` | Comparative dataset containing published reference measurements and indices |
| `Right_side_only_for_summarise_dataset3.csv` | Bone-level measurements used for descriptive analysis of the Sding Chung assemblage |

Input filenames must match those specified in the R Markdown file.

The code currently expects comma-separated CSV files. Their encoding, delimiters and variable formats should be verified against the archived source files before execution.

---

## 3. Analytical Workflow

The R Markdown document follows a sequential analytical structure:

**Stage 1 — Data import and quality control**

- Import the source CSV files.
- Validate required variables and data formats.
- Standardise site-period and regional classifications.
- Document source-file checksums and sample selection.

**Stage 2 — Descriptive statistics**

- Calculate group-specific descriptive statistics by sex.
- Summarise body size and body proportion measurements.
- Report sample sizes, means, standard deviations, medians, quartiles and ranges.
- Generate the corresponding supplementary tables' data.

**Stage 3 — Statistical comparisons**

- Conduct sex-specific comparisons of body-size variables.
- Assess assumptions and select conventional or Welch ANOVA according to the documented decision rule.
- Calculate Tukey HSD or Games–Howell post hoc comparisons where applicable.
- Apply Kruskal–Wallis and Dunn comparisons to selected body proportion indices.
- Record multiple-testing adjustments and relevant diagnostics.

**Stage 4 — Sensitivity analyses**

- Repeat selected body-size comparisons after excluding `dataset3`.
- Compare results with those of the principal analytical dataset.
- Document changes in sample composition and statistical results.

**Stage 5 — Manuscript figures**

- Prepare figure-specific analytical datasets.
- Generate plots using consistent site labels, colours and formatting conventions.
- Export publication-oriented TIFF images, vector PDFs and optional PNG previews.

**Stage 6 — Reproducibility records**

- Export statistical results and data-audit tables.
- Save input-file checksums.
- Record the R session and software environment.

These steps are presented explicitly rather than compressed into a generic plotting or analysis pipeline, allowing readers to trace the processing and analytical decisions underlying individual figures.

---

## 4. Reproducing Manuscript Figures

The workflow generates revised Figures 3–11 of the manuscript.

| Figure | Analysis or visualisation | Principal data source |
|---|---|---|
| Figure 3 | Estimated stature | Main dataset |
| Figure 4 | Estimated body mass | Main dataset |
| Figure 5 | Body mass index | Main dataset |
| Figure 6 | Trunk-to-lower-limb ratio | Anatomical measurements |
| Figure 7 | Brachial index | Individual-level measurements |
| Figure 8 | Crural index | Individual-level measurements |
| Figure 9 | Crural indices across study and comparative populations | Published reference dataset |
| Figure 10 | Relative bi-iliac breadth | Individual-level measurements |
| Figure 11 | Within-trait sexual dimorphism | Main dataset |

Figures 3–5 show body-size comparisons, including individual observations and group distributions. Figures 6–8 address anatomical body proportions. Figures 9–11 extend the analysis to comparative crural indices, relative pelvic breadth and sexual dimorphism.

---

## 5. Statistical Methods and Analytical Decisions

The workflow incorporates conventional parametric and non-parametric approaches according to the analytical requirements of individual variables.

### Body-size comparisons

Estimated stature, body mass and BMI are compared separately by sex across archaeological site-period groups.

The code records residual normality diagnostics and median-centred Brown–Forsythe tests. Its original decision rule selects Welch ANOVA when the Brown–Forsythe test indicates significant variance heterogeneity; otherwise, conventional one-way ANOVA is used.

Where applicable, pairwise comparisons are calculated using Tukey HSD or Games–Howell procedures.

Holm adjustments are applied across the three body-size traits within each sex.

The workflow records both unadjusted omnibus significance, used to trigger the original post hoc calculations, and Holm-adjusted omnibus significance, used to determine which comparisons are annotated in Figures 3–5.

### Body proportion comparisons

Brachial index, crural index and trunk-to-lower-limb ratio are analysed using sex-specific Kruskal–Wallis tests, with Dunn pairwise comparisons where applicable.

Relative bi-iliac breadth is primarily summarised descriptively, with an exploratory Wilcoxon rank-sum comparison under the conditions specified in the code.

### Sexual dimorphism

Sexual dimorphism is expressed as the percentage difference between male and female group means relative to their arithmetic midpoint:


SDpercentage =[(X̄ₘₐₗₑ - X̄fₑₘₐₗₑ) / ((X̄ₘₐₗₑ + X̄fₑₘₐₗₑ) / 2)] × 100

The metric is calculated separately for stature, body mass and BMI.

Results should be interpreted within each trait rather than as directly equivalent absolute differences across different anatomical or body-size variables.

---

## 6. Software Requirements

The analyses are implemented in **R**, using R Markdown for executable documentation.

Required packages include:

- `readr`
- `dplyr`
- `tidyr`
- `purrr`
- `ggplot2`
- `tibble`
- `stringr`
- `scales`
- `knitr`
- `rmarkdown`

RStudio is recommended but not required.

A supported Pandoc installation is required to render the complete R Markdown document.

### Installation

Install the required packages if they are not already available:

```r
install.packages(c(
  "readr",
  "dplyr",
  "tidyr",
  "purrr",
  "ggplot2",
  "tibble",
  "stringr",
  "scales",
  "knitr",
  "rmarkdown"
))
```

### Running the analysis

1. Download or clone the repository.
2. Place the required, appropriately authorised CSV files in the `data/` directory.
3. Open the project in RStudio or start an R session from the repository root.
4. Execute the R Markdown file.

```r
rmarkdown::render(
  "ATP_Body_Form_Analysis.Rmd",
  clean = TRUE
)
```

Alternatively, open the R Markdown document in RStudio and select **Knit**.

The workflow reads the input files without modifying them and creates the required output directories automatically.

### Reproducibility environment

The analysis records the R environment through `sessionInfo()`.

A verified `renv.lock` file has not yet been generated. Package versions should be locked and tested after the workflow has been executed successfully with the final datasets.

---

## 7. Output Files

Successful execution generates three principal output categories.

**`outputs/figures/`**

Publication-oriented figures, including LZW-compressed TIFF files, PDF versions and optional PNG previews.

**`outputs/tables/`**

Descriptive statistics, omnibus test results, pairwise comparisons, sensitivity analyses and sexual dimorphism summaries.

**`outputs/audits/`**

Data-quality and reproducibility records, including:

- Input-file MD5 checksums.
- Source and sample-selection inventories.
- Repeated archaeological context identifier reports.
- Numeric conversion and import parsing checks.
- RBIB calculation and data-availability comparisons.
- Reference-group mapping checks.
- Figure-specific observational coverage audits.
- R session information.

These files are generated automatically and are excluded from version control by default.

---

## 8. Citation

If using or adapting this analytical workflow, please cite the appropriate version of the repository and the associated research publication once available.

**Associated manuscript**

Cao, D., et al. *Shaped by the Highlands: Skeletal Evidence for Body Form Variation among Ancient Tibetan Plateau Populations*. American Journal of Biological Anthropology. Manuscript under revision.

Final bibliographic information, a version-specific repository citation and any archival DOI will be added following publication and release.

---

## 9. Contact and Maintenance

**Doudou Cao**

Hong Kong Institute for the Humanities and Social Sciences  
The University of Hong Kong

Email:dcao@hku.hk

Research profile: https://ihss.hku.hk/portfolio/doudou-cao/
and https://caroldoudoucao.github.io/

For questions about the analytical workflow, reproducibility or potential data access, please refer to the repository's Issues section or the researcher's contact information.

---

*This repository is maintained as part of the documentation and reproducibility materials associated with the study of body form variation among ancient Tibetan Plateau populations.*
