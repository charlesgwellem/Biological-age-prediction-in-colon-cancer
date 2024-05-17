## Introduction

The goal of this project is to predict the biological age of the normal and healthy colon samples in the DNA methylation dataset from the [genomicClass](https://github.com/genomicsclass/coloncancermeth/blob/master/data/coloncancermeth.rda) GitHub page. The CpGs that determine the biological clock will be determined de novo using PCA and used as the predictors. A CpG is a C, followed by a G but from the  $5^1$ end to the  $3^1$ end of a DNA strand.

Epigenetic mechanisms regulate gene expression. Certain technologies enable us to measure some epigenetic endpoints. One example is DNA methylation. DNA methylation is a chemical process that occurs around genes and which is capable of silencing gene expression. In this project, I will analyse DNA methylation data for the whole genome and relate it to phenotypic variation.

It has been studied that when part of a genome is methylated, the gene close to it is not expressed. It is inherited at mitosis. Methylation often occurs at CpG islands.
When one DNA strand is methylated, so is the other. If we also have a CpG on one strand, we have it as well on the other strand. When DNA replicates, its methylation characteristics are preserved.

## Milestones

### Perform PCA

The goal of performing PCA is to identify the CPGs that are strongly predictive of age. The approach consists of identifying the principal components whose loading scores have a significant relationship with the outcome of interest which is the age. The top 24 CPGs with the highest loading scores in the PC with a significant relationship with age will be selected to serve as predictors in a linear model with age as an outcome. The model will be used to predict the age. This prediction will constitute the biological age.

Results of PCA show that PC2 has a significant correlation with age, meanwhile, PC10, and PC20 are the pcs with (near-) significant correlation with age. The next step will be to select the cpgs top 24 cpgs that have the strongest loading scores on the 2nd PC. I select 24 since there are only 27 observations in the data and selecting more than 24 features will overwhelm the model.

Now that I have CPGs that have top loading scores or influence on the PCs that have a significant correlation with the age at time of diagnosis, I can proceed to make a simple linear regression where I predict this chronological age, using the epigenetic signatures that correlate with the age.

### Linear modeling

The r-squared value is 0.93 which means the linear model accounts for 0.93% of the variation in the dataset. This is a high and sufficient number.

The plot of the fitted points vs residuals does not show a pattern, showing that the model fits well and exhibits no heteroscedasticity. The Shapiro test on the residuals show that the p value is greater than 0.05, meaning that we do not have enough evidence to reject the null hypothesis of the normal distribution of residuals. 

The high r-squared value, absence of heteroscedasticity, and normal distribution of residuals are important parameters that point to the goodness of fit.

### Conclusion

PCA can be used as feature selection to select CPG predictors of the biological age, when we have very few observations like in this case, 26. Otherwise, lasso regression and pther robust feature selectionmedthods can be used.
