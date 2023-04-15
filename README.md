# Abstract

This report provides an analysis of data-exploration performed on clinical data from patients with prostate adenocarcinoma. The data, gathered by the PanCancer Atlas, is used in four different types of data analyses including survival analysis, differential expression analysis, hierarchical clustering and heatmap visualizations, as well as a PCA analysis, to compare genetic similarities and patient traits. The purpose of this analysis is to find visible trends amongst TCGA-PRAD patients based on various patient traits and gene expression. Our findings were able to provide confirmation that most patients fall into the adenoma and adenocarcinoma subtype, and that the two most significantly expressed genes are the GLO1 and TGM4 genes.

# Introduction

Prostate adenocarcinoma is a type of cancer that forms in the prostate gland. It is the sixth most common type of cancer in the world [1], and, according to data obtained from the Pan-Cancer Atlas, has a survival rate of 98.0\% [2]. Prostate adenocarcinoma is categorized into three different subtypes: adenomas and adenocarcinomas, ductal and lobular neoplasms, and finally cystic, mucinous, and serous neoplasms. To further understand the data set, we analyzed the extent to which various visible trends exist in prostate adenocarcinoma patients based on patient traits and gene expression, in order to provide insight into what causes death amongst patients within our data set. Identifying and analyzing trends found within the data is critical for clinical advancements as it provides insights which may improve diagnosis times and treatment plans for individuals diagnosed with prostate adenocarcinoma. 

# Methods

To identify trends of prostate adenocarcinoma, four different statistical methods were used on the data, which was obtained from the cBioPortal website and GDC Data Portal, specifically the TCGA-PRAD project with "Transcriptome Profiling" as the data category. The two sources describe the same list of patients, but with different traits. Data exportation was done on R and the code can be found on the attached Github repo. The TCGA data contains traits of 551 prostate adenocarcinoma patients. All the traits stored and visualized as an array to make general observations. For the gene expression, only genes that the average expression count greater than 15000 and there are 503 genes that fall into this category. \\

## Survival Analysis

Based on first observations of the raw data, the most prominent and fully documented traits were tumor stage, ethnicity, and primary diagnosis (disease type or cancer subtype). The data related to tumor stage was obtained from cBioPortal, while the data related to two other traits were obtained from GDC Data Portal. Once the matrix with the most prominent patient traits was synthesized, survival analysis was done using survfit and ggsurvplot functions from the survival and survminer package. We also plotted Kaplan-Meier curves and calculated the p-values to see whether or not the traits are statistically significant. 

## Differential Expression

The next analysis was performed to find differences between gene expressions. In differential expression, the normalized read count data from GDC Data Portal is used to perform a statistical analysis to identify differences in expression levels between genes. After that, all the possible pairs of tumor stages were listed, which sums to 15 pairs when excluding the undefined categories (details attached in Appendix). Next, we created MA plots for each pair and obtained the  LFC$>$0 and LFC$<$0 values from each analysis. The pair with the greatest LFC$>$0 and LFC$<$0 value was chosen for further analysis using the mapIds function from AnnotationDbi to identify the top 10 upregulated genes as well as the top 10 downregulated genes, and to further determine the most significant genes. From the MA-plots, we can visualize the difference in gene expressions between two stages from each pair. The y-axis shows the log ratio and the x-axis shows the mean average of counts. The MA plots were also made to determine whether the data has been properly normalized or not. 

## Hierarchical Clustering

Hierarchical clustering then was performed to cluster the cancer by subtypes using dendograms. This was then visualized using a heatmap. Since the TCGA data contains the normalized RNA transcriptome profiling gene expressions, the clusters would look like groups of genes that are similar in expression.  \\

## Principal Component Analysis

Principal Component Analysis (PCA) is a method of data analysis which aims to compute the principal components of the data that is being analyzed. PCA provides dimension reduction of the data which makes it easier to analyze. Principal components are not related to each other, and are used to determine which factors may be useful for further analysis. The top 2 PCs were than used to create a scatter plot and to categorize the data which may correspond to specific trait.

# Result

<div align="center"><img src ="https://github.com/JoshParkSJ/prostate-adenocarcinoma-analysis/blob/main/plots/survival_tumor.png?raw=true" style="vertical-align:middle"></div>
<div align="center">Kaplan-Meier Plot of Tumor Stage</div>

<div align="center"><img src ="https://github.com/JoshParkSJ/prostate-adenocarcinoma-analysis/blob/main/plots/survival_ethnicity.png?raw=true" style="vertical-align:middle"></div>
<div align="center">Kaplan-Meier Plot of Ethnicity</div>

<div align="center"><img src ="https://github.com/JoshParkSJ/prostate-adenocarcinoma-analysis/blob/main/plots/survival_primary.png?raw=true" style="vertical-align:middle"></div>
<div align="center">Kaplan-Meier Plot of Primary Diagnosis</div>

<div align="center"><img src ="https://github.com/JoshParkSJ/prostate-adenocarcinoma-analysis/blob/main/plots/MA.png?raw=true" style="vertical-align:middle"></div>
<div align="center">MA Plot of T2C vs T3B</div>

<div align="center"><img src ="https://github.com/JoshParkSJ/prostate-adenocarcinoma-analysis/blob/main/plots/DE_summary.png?raw=true" style="vertical-align:middle"></div>
<div align="center">Summary of Differential Expression ('T2C and T3B' Pair)</div>

<div align="center"><img src ="https://github.com/JoshParkSJ/prostate-adenocarcinoma-analysis/blob/main/plots/DE_stage.png?raw=true" style="vertical-align:middle"></div>
<div align="center">Cancer Stage Tumor Code by Frequency</div>

<div align="center"><img src ="https://github.com/JoshParkSJ/prostate-adenocarcinoma-analysis/blob/main/plots/heatmap.png?raw=true" style="vertical-align:middle"></div>
<div align="center">Heatmap and Dendogram of The 503 Most Expressed Genes</div>

<div align="center"><img src ="https://github.com/JoshParkSJ/prostate-adenocarcinoma-analysis/blob/main/plots/PCA.png?raw=true" style="vertical-align:middle"></div>
<div align="center">Scatter Plot of the PCA Result</div>

<div align="center"><img src ="https://github.com/JoshParkSJ/prostate-adenocarcinoma-analysis/blob/main/plots/TGM4.png?raw=true" style="vertical-align:middle"></div>
<div align="center">TGM4 Expression [3]</div>

<div align="center"><img src ="https://github.com/JoshParkSJ/prostate-adenocarcinoma-analysis/blob/main/plots/GLO1.png?raw=true" style="vertical-align:middle"></div>
<div align="center">GLO1 Expression [4]</div>

# Discussion

A Kaplan-Meier plot based on tumor stage, ethnicity, and primary diagnosis (tumor subtype) are shown in Figure 1, Figure 2, and Figure 3 respectively. These plots show certain variables that are statistically significant (p $\leq$ 0.05). The p-value for tumor stage was 0.00016 and for ethnicity was 0.0079. The survival rate for T2A, T2C and T4 is 100\%. The labels without the T labels (i.e first two stages labeled in pink and orange in the legend) represent unreported stages. The time (x-axis) has unit of days. The survival analysis of primary diagnosis was not considered as the p-value was too high. The rest of the analysis was carried out with the tumor stage feature, as it had the smallest p-value and was thus the most statistically significant. 

<br/>

The resulting MA plot shown in Figure 4 shows that most points lay on the y=0 line. Blue points represent significant data points. Since most points lay on the y=0 line, the data are normalized. 

<br />

The summary of the differential expressions from the 'T2C and T3B' pair is tabled in Figure 5a. Figure 5b shows American Joint Committee's Cancer Tumor Stage Code by frequency. The summary table matches the result from survival analysis because the 'T2C and T3B' pair has the highest number of LFC$>$0 and LFC$<$0. Additionally, T2C has 100\% survival rate while 6/10 dead patients are from T3B. T2A and T4 cannot be compared although both have 100\% survival rate due to the difference in number of patients. Table 1 shows the 10 most upregulated and downregulated genes according to the differential expression results. Two of the most downregulated genes from our analysis,  ENSG00000163810 (TGM4) and ENSG00000124767 (GLO1), are highly expressed in prostate cancer according to Protein Atlas [3][4].

<div align="center"><img src ="https://github.com/JoshParkSJ/prostate-adenocarcinoma-analysis/blob/main/plots/up_down_regulated.png?raw=true" style="vertical-align:middle"></div>
<div align="center">Top 10 most upregulated and downregulated genes</div>

As shown by the PCA and Hierarchical Clustering, almost all patients fall into the adenoma and adenocarcinoma category. This matches the data from GDC Data Portal [1] where 488 patients fall into the adenocarcinoma subtype. Additionally, based on the scatter plot of PCA, other subtypes are overlapping which indicates similarity of cancer subtypes between patients.


# References


[1] “Types of prostate cancer: Common, rare and more,” Cancer Treatment Centers of America, 21-Sep-2021. [Online] [Accessed: 10-Dec-2021]. 
<br />
[2] “Prostate Adenocarcinoma (TCGA, PanCancer Atlas),” CBioPortal for Cancer Genomics. [Online] [Accessed: 10-Dec-2021]. 
<br />
[3] “The Human Protein Atlas of ENSG00000124767-GLO1,” Expression of glo1 in cancer - summary. [Online]. Available: https://www.proteinatlas.org/ENS
G00000124767-GLO1/pathology. [Accessed: 10-Dec-2021].  
<br />
[4] “TGM4,” Expression of TGM4 in cancer - summary - The human protein atlas. [Online]. Available: https://www.proteinatlas.org/ENSG00000163810-TGM4/pathology. [Accessed: 10-Dec-2021]. 

