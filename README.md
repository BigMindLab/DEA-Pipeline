# Differential Expression Analysis Pipeline

This guide provides an overview of what a Differential Expression Analysis report created by the BigMind team contains. For the integrated and automated analysis, we utilized functions from our custom R package, OmicsKit.

### 1. Preprocessing: Counts per Sample
#### Visualizing Samples Data
Sample metadata is crucial for connecting bioinformatics results to biological significance. The first step in our analysis is to clean the data and prepare it for downstream library requirements.

| ID | Test       | Condition | Group | Sex | Age | RIN |
|----|------------|-----------|-------|-----|-----|-----|
| 1  | Undetected | Normal    | A     | F   | 65  | 6.0 |
| 2  | Undetected | Normal    | A     | F   | 42  | 6.0 |
| 3  | Undetected | Normal    | A     | M   | 63  | 5.5 |
| 4  | Undetected | Normal    | A     | M   | 49  | 5.8 |
| 5  | Undetected | Disease   | B     | M   | 51  | 5.2 |
| 6  | Undetected | Disease   | B     | M   | 53  | 6.1 |
| 7  | Detected   | Normal    | C     | F   | 31  | 5.5 |
| 8  | Detected   | Normal    | C     | F   | 54  | 5.5 |
| 9  | Detected   | Normal    | C     | M   | 43  | 5.3 |
| 10 | Detected   | Normal    | C     | M   | 67  | 5.7 |
| 11 | Detected   | Normal    | C     | M   | 59  | 6.1 |
| 12 | Detected   | Normal    | C     | M   | 46  | 5.2 |
| 13 | Detected   | Normal    | C     | M   | 40  | 5.5 |
| 14 | Detected   | Disease   | D     | F   | 70  | 5.6 |
| 15 | Detected   | Disease   | D     | F   | 36  | 5.9 |
| 16 | Detected   | Disease   | D     | F   | 49  | 6.0 |
| 17 | Detected   | Disease   | D     | F   | 64  | 6.6 |
| 18 | Detected   | Disease   | D     | F   | 66  | 5.6 |
| 19 | Detected   | Disease   | D     | M   | 57  | 5.4 |
| 20 | Detected   | Disease   | D     | M   | 51  | 6.4 |
| 21 | Detected   | Disease   | D     | M   | 48  | 6.7 |

#### Managing Count Files
Identifying samples with abnormal counts can highlight outliers that may need to be excluded from analysis to avoid skewed results.

### 2. Exploring Confounders
Consider variables such as age, sex, batch effects, or other biological and technical factors that might impact gene expression.

#### Heatmap: Samples vs Samples
A heatmap is used to visualize the correlation between samples.

#### PCA: Principal Component Analysis
Principal Component Analysis (PCA) helps in understanding the variation between samples.

#### tSNE: t-Distributed Stochastic Neighbor Embedding
tSNE is another dimensionality reduction technique used to visualize high-dimensional data.

#### UMAP: Uniform Manifold Approximation and Projection
UMAP is used to visualize the structure of the data.

### 3. Differential Expression Analysis
DESeq2 is a widely used tool for analyzing differential gene expression in RNA-seq data. We performed our analysis by adjusting the analysis and improving filtering.

#### Display Results
| baseMean     | log2FoldChange | lfcSE       | stat       | pvalue     | padj       | ensembl       | symbol | description                                                                              | biotype       |
|--------------|----------------|-------------|------------|------------|------------|---------------|--------|------------------------------------------------------------------------------------------|---------------|
| ENSG00000000003 | 4.8597885      | -1.3065575  | 0.7629200  | -1.7125747 | 0.0867908  | NA            | TSPAN6 | tetraspanin 6 [Source:HGNC Symbol;Acc:HGNC:11858]                                       | protein_coding |
| ENSG00000000005 | 0.0306208      | 0.5719487   | 4.3949775  | 0.1301369  | 0.8964581  | NA            | TNMD   | tenomodulin [Source:HGNC Symbol;Acc:HGNC:17757]                                         | protein_coding |
| ENSG00000000419 | 183.1677539    | -0.0499737  | 0.1492696  | -0.3347882 | 0.7377848  | 0.9888945     | DPM1   | dolichyl-phosphate mannosyltransferase subunit 1, catalytic [Source:HGNC Symbol;Acc:HGNC:3005] | protein_coding |

#### Split Cases
When performing differential expression analysis of a study with 3 phenotypes, including the baseline, there are 10 mutually exclusive cases where genes can fall into.

#### Detectability
This function identifies genes with measurable expression levels across samples.

### 4. Plotting
#### Heatmap: Samples vs Genes
Heatmaps are used to visualize the expression levels of genes across different samples.

#### Volcano Plots
Volcano plots display statistical significance (p-value) versus magnitude of change (fold change).

#### Box-Scatter-Violin (BSV) Plots
BSV plots are used to visualize the distribution and expression levels of genes.

### 5. GO Enrichment
GO enrichment analysis with clusterProfiler helps interpret differential expression results by identifying biological pathways that are overrepresented in differentially expressed genes, providing insights into the underlying biological mechanisms.

#### Balloon Plots
Balloon plots visualize GO terms and their significance.

#### GO Terms Networks
GO terms networks show relationships between enriched GO terms.

### 6. Prognosis Model
Linear regression models are employed to analyze RNA-seq data and identify significant relationships between gene expression levels and clinical outcomes. These models help in developing predictive tools that can forecast disease progression or patient survival based on specific gene expression profiles. By leveraging these models, researchers can gain insights into the molecular underpinnings of disease and potential therapeutic targets.

#### ROC Curve
Receiver Operating Characteristic (ROC) curves are used to evaluate the performance of the prognosis models. The ROC curve plots the true positive rate (sensitivity) against the false positive rate (1-specificity) across different threshold settings. The area under the curve (AUC) provides a single measure of overall accuracy, with higher values indicating better predictive performance. These curves help assess the model's ability to distinguish between different clinical outcomes.
