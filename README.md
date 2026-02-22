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
