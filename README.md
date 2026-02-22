# RESHAPE-MP-Analysis
## Diagnostic Accuracy Analysis for the RESHAPE Cluster-Randomized Trial
Contains a truncated and focused version of the code that was used to analyze diagnostic accuracy in the RESHAPE dataset.

---

### Overview
This repository contains the core R code used to analyze diagnostic accuracy outcomes in the Reducing Stigma in Mental Health Core Providers (RESHAPE) cluster-randomized trial. The analysis evaluates whether incorporating mental health service users as co-facilitators in a training program improves primary healthcare workers' diagnostic accuracy for depression and alcohol use disorder compared to standard Implementation as Usual (IAU).

---

### Key Features
- **Cluster-level metrics**: Calculates sensitivity, specificity, PPV, NPV, and accuracy by cluster and trial arm
- **GEE with small-sample corrections**: Implements Kauermann-Carroll (KC) corrected standard errors for clustered data (26 clusters)
- **Joint hypothesis tests**: Multivariate Wald tests for sensitivity/specificity and PPV/NPV pairs
- **Link function comparison**: Both logit (odds ratios) and identity (risk differences) link functions
- **Comprehensive output**: Generates all tables referenced in the statistical analysis report (Tables 4-19)

---

### Requirements
- R (version 4.2.1 or higher)

**Required packages:**

```r
install.packages(c("foreign", "tidyverse", "geepack", "geesmv", "broom", "stringr", "ggplot2"))
```

---

### File Structure

```
RESHAPE-MP-Analysis/
├── README.md
└── RESHAPE MP Primary Analytic Code.Rmd
```

---

### Code Structure

The script is organized into 12 sections corresponding to the statistical analysis report:

| Section | Description | Output |
|----------|-------------|--------|
| 1–2 | Data preparation | `dep_data`, `aud_data` |
| 3 | Cluster-level metrics | `dep_cluster`, `aud_cluster` |
| 4 | GEE function with KC correction | Core modeling function |
| 5 | Overall accuracy models (logit) | Table 7 |
| 6 | Sensitivity/specificity models | Table 8 |
| 7 | PPV/NPV models | Table 9 |
| 8 | Joint hypothesis tests | Table 10 |
| 9 | Identity link models | Tables 11–13 |
| 10 | Cluster line plots | Figures 1–2 |
| 11 | Arm-level summaries | Tables 5–6 |
| 12 | Cluster-level summaries | Tables 16–19 |
---

### Key Functions

#### `run_gee_kc()`

Core GEE function with Kauermann–Carroll (KC) small-sample correction.

- Fits GEE model using `geepack`
- Applies KC correction via `GEE.var.kc()` from `geesmv`
- Returns:
  - Parameter estimates  
  - KC-corrected standard errors  
  - t-statistics  
  - p-values  

Uses degrees of freedom:

```
df = (# clusters) - (# parameters) - 1
```

---

#### `calculate_cluster_metrics()`

Computes diagnostic accuracy metrics for each cluster:

- Sensitivity = TP / (TP + FN)  
- Specificity = TN / (TN + FP)  
- PPV = TP / (TP + FP)  
- NPV = TN / (TN + FN)  
- Accuracy = (TP + TN) / N  

---

### Output Objects

| Object | Description | Corresponding Table |
|--------|------------|---------------------|
| `all_accuracy` | Overall accuracy GEE results | Table 7 |
| `all_sens_spec` | Sensitivity/specificity results | Table 8 |
| `all_ppv_npv` | PPV/NPV results | Table 9 |
| `all_joint` | Joint hypothesis tests | Table 10 |
| `all_identity_acc` | Identity link accuracy results | Table 11 |
| `dep_summary`, `aud_summary` | Arm-level summaries | Tables 5–6 |
| `dep_iau_summary` | Depression IAU cluster summary | Table 16 |
| `dep_reshape_summary` | Depression RESHAPE cluster summary | Table 17 |
| `aud_iau_summary` | AUD IAU cluster summary | Table 18 |
| `aud_reshape_summary` | AUD RESHAPE cluster summary | Table 19 |

---

### Methodological Notes

- **Clusters:** 26 randomization units (municipalities or groups of facilities)
- **Small-sample correction:** Kauermann–Carroll (KC) for individual parameter tests
- **Joint tests:** Robust sandwich covariance matrices (KC unstable for multivariate Wald tests)
- **Link functions:**
  - Logit (primary analysis; odds ratios)
  - Identity (risk difference comparison)

---
