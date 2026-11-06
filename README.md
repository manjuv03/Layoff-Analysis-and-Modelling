# Layoff Analysis and Modelling

**Exploring and Modelling Tech Layoffs, March 2020 – December 2022**

## Overview

This project analyses 876 layoff events from 772 companies in 32 countries, recorded between March 2020 and December 2022. It cleans the data, explores which companies, industries and locations were hit hardest, measures correlations, groups layoff sizes with k-means, and tries random forest, linear regression and naive Bayes models to predict how many people a company lays off. A Power BI dashboard summarises the findings.

## Repository layout

| Path | Content |
| --- | --- |
| `LayOffAnalysis.ipynb` | All code (R), with outputs |
| `LayOffAnalysis.R` | The same analysis as a plain R script |
| `Layoffs.csv` | The dataset |
| `Visualizations/` | Plots from the notebook and the Power BI dashboard |
| `LICENSE` | MIT |

## Dataset

| File | Rows × columns | Columns | Dates |
| --- | --- | --- | --- |
| `Layoffs.csv` | 876 × 9 | company, location, industry, total_laid_off, percentage_laid_off, date, stage, country, funds_raised | 12 Mar 2020 – 9 Dec 2022 |

The data covers 27 industries. Missing values (8 in total) are replaced with 0.

## How to run

1. Install R and RStudio (or Jupyter with the R kernel)
2. Install the packages: `install.packages(c("tidyverse", "wordcloud", "corrplot", "caret", "NbClust", "randomForest", "e1071"))`
3. Change the path in `read.csv("/content/Layoffs.csv")` to `Layoffs.csv`
4. Run `LayOffAnalysis.R` or the notebook top to bottom

## Notebook structure

| Section | Content |
| --- | --- |
| Data cleaning | Summary, missing values, box plots, duplicate check, column renaming |
| EDA | Top 5 companies and industries by people laid off, company word cloud |
| Correlation | Correlation matrix as a circle plot and a heat map |
| Feature engineering | Combined feature, log transform, standard scaling, label-encoded location, industry and stage |
| Split | First 70% of rows for training (613), last 30% for testing (263) |
| Models | k-means clustering, random forest, linear regression, naive Bayes |

## Key results

| Question | Method | Result |
| --- | --- | --- |
| Do bigger-funded companies lay off more people? | Pearson correlation | r = 0.17: only a weak link between funds raised and layoffs |
| Do layoff sizes fall into groups? | k-means (k = 3, chosen by NbClust majority vote) | 838 small events (mean 126 people), 36 large (mean 1,752) and 2 very large (mean 10,500) |
| Can we predict how many people are laid off? | Random forest (500 trees) | Test RMSE 221; 32.6% of variance explained |
| | Linear regression on funding stage | Test RMSE 355; R² = 0.09, so stage alone explains little |

The largest single events are Meta (11,000 people), Amazon (10,000) and Uber (7,525).

## Results in figures

**The Power BI dashboard** shows layoffs by country, company, location and funding stage. The SF Bay Area and post-IPO companies account for the most people laid off.

![Layoff dashboard](Visualizations/Layoff%20Dashboard.png)

**Three layoff-size clusters**: most events are small, with a few very large ones.

![K-means clustering](Visualizations/K-Means%20Clustering.png)

**Correlations between the numeric columns are weak.**

![Correlation matrix](Visualizations/coorelation%20matrix.png)

## Notes

The random forest uses every column, including a feature built as `funds_raised + laid_off`, which contains the target. Its scores are therefore optimistic; dropping that feature would give a fairer estimate.

## Authors

Manju Swaroop V and Sukrutha G
