# Modularising Single-Cell sequencing analysis-2024
Only one layer of the intricate regulatory system that controls signaling and cellular function is captured by scRNA-seq. Better results have been made possible by significant efforts to quantify additional modalities at single-cell resolution, such as chromatin accessibility, surface proteins, T cell receptor (TCR)/B cell receptor (BCR) repertoires, and spatial location. These features will keep expanding and with it the tools to analyze it. With over 1000 tools currently available for analyzing the single-cell sequencing results, it becomes crucial to filter the best results that could support the hypothesis at hand. There are several steps to the anlaysis of scRNA-seq data.    



## Nextflow 





## Structure Equation Modelling





















# Single-cell data analysis Date: April 2022
Single-cell expression studies have allowed us to measure RNA levels of individual cells of highly heterogeneous cellular population. The challenge to construct and infer the networks remains largely unsolved.

Each cell defined by a state 

# Data
This single-cell study corresponds to Peripheral Blood Mononuclear Cell (PBMC) single-cell RNA-seq (scRNA-seq) data from the manuscript. In particular, this study contains data from 6 scRNA-seq methods (Smart-seq2, CEL-Seq2, 10x Chromium, Drop-seq, Seq-Well, and inDrops). Each method was applied to two replicates (PBMC1 and PBMC2).
https://www.biorxiv.org/content/10.1101/632216v2

The portal contains log normalized UMI counts per 10,000 data from all these methods, except for Smart-seq2 with log normalized read counts per 10,000 data.

# Introduction
PBMC is composed of various specialized immune cells such as lymphocytes, monocytes and dendritic cells. PBMCs contain different multipotent cells that can differentiate into blood cells, endothelial cells, hepatocytes, smooth muscle cells, osteoblasts amongst others. In isolated PBMCs, T cells amount to 45–70% of the total cells making it by far the most abundant cell type. 

## Analysis based on Single Cell Portal (SCP) server data
A non-linear dimensionality reduction algorithm called tSNE is applied here which produces clusters from high dimensional, almost indistinct expression data. The probability of similarity amongst points is converted to a low dimensional space using the conditional probabilities of two probabilities say Pxy and Pjy at high dimension. Under the assumption of t-distribution, similar points are deduced
The 12 clusters defined in Fig 1 (singlecell/Images), show the relative closeness of each cell. On the right shows the clusters based on cell types. CD4+ T cells can be seen in blue in the top right quadrant.    

## CD4+ T cell Transcription Factor Expression
The expression levels of 1430 transcription factors (TFs) were evaluated. Percentage expression was visualised for these TFs in CD4+ T cells. Within the CD4+ T cells, based on the relative magnitude of expression of every TFs, 934 genes had a percentage expression of greater than 0. 482 genes showed no expression value. Based on molecular function, biological process and cellular component, 1806 functional categories (Gene Ontologies). The top 10 expressing genes can be seen in Fig 2. 

## Gene enrichment analysis
Gene enrichment analysis further revealed 119 GO molecular functions. The top 10 functions and the corresponding genes are in Fig 3. 

## 
After filtering the 1430 TFs for expressed genes, MCODE was used to evaluate the most closely linked TFs. This clustering-based method to separate the dense regions, uses vertex weighting by local neighbourhood density and outward traversal from a locally dense seed protein.

