# Introduction

This file contains and describes examples of analysis from this project.

Please cite:

Stokes, C., Setlur, V., Cogley, B., Satyanarayan, A., & Hearst, M. (2022). Striking a Balance: Reader Takeaways and Preferences when Integrating Text and Charts. *IEEE Transactions of Visualization and Computer Graphics*.

# Setup

Data cleaning and reshaping will not be included in this file, but can be found in [data_analysis/balanceText.Rmd](data_analysis/balanceText.Rmd).

## Required libraries

To ensure all the packages required are installed, the following script will install and load the necessary packages.


```
packages = c("tidyverse", "ggplot2", "plyr", "car", "lme4", "stringr", "ggpubr", "PMCMRplus", "irr")

package.check <- lapply(
  packages,
  FUN = function(x) {
    if (!require(x, character.only = TRUE)) {
      install.packages(x, dependencies = TRUE)
      library(x, character.only = TRUE)
    }
  }
)
```

# Research Question 1: What are readers preferences when viewing charts with different amounts and semantic levels of text? How does this vary based on overall preference for textual or visual information?

To investigate this question, we conducted Friedman tests for the rank-order data and post-hoc Nemenyi's tests to examine pairwise comparisons. We also calculate the average rank positions for each variant. This process is the same for H1a through H1d. An example of H1a is shown below.


```
# friedman test
friedman.test(y=h1a$rankPosition, groups = h1a$rankVariant, blocks = h1a$participantID)

# posthoc nemenyi test
frdAllPairsNemenyiTest(y=h1a$rankPosition, groups = h1a$rankVariant, blocks = h1a$participantID)

# average rankings
aggregate(rankPosition ~ rankVariant, h1a, mean)

```


