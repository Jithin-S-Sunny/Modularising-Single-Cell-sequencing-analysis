# Modularising Single-Cell sequencing analysis
The scope of single-cell sequencing just keeps getting bigger. Only one layer of the intricate regulatory system that controls signaling and cellular function is captured by scRNA-seq. But better results have been made possible by significant efforts to quantify additional modalities at single-cell resolution, such as chromatin accessibility, surface proteins, T cell receptor (TCR)/B cell receptor (BCR) repertoires, and spatial location. These features will keep expanding and with it the tools to analyze it. With over 1000 tools currently available for analyzing the single-cell sequencing results, it becomes crucial to filter the best results that could support the hypothesis at hand. There are several steps to the analysis of scRNA-seq data: 
* Pre-processing
* Quality control & Filtering
* Dimensionality reduction
* Clustering & Visualisation
* Cell-type annotation
* Differential gene expression analysis
* Trajectory inference
* Gene set enrichment analysis, amongst others.

There can be 2 major challenges for bioinformatics analysis        

Firstly, there can be timely changes
  * to the version of the tools being used or the environment (modules, libraries) changing over time. The same pipeline should run successfully in a local computer, terminal, HPC, or maybe even mainframes.   
  * new tools could be added. Timely addition of new bioinformatics analysis is common and the pipeline should be modular to accommodate it. 
  * the method used for one step could need a more thorough look, for example, feature reduction may have to be modified to include more useful features that would otherwise be discarded,
  * multiple datasets could be integrated over time. This can cause batch effects, requiring more robust correction methods.  

I propose a 2 step approach:

## Nextflow 
For straightforward, small-scale operations, shell scripts could be adequate, but Nextflow offers a strong framework for managing intricate processes with improved scalability, reproducibility, error handling, modularity, and portability. Because of these benefits, it is the best option for bioinformatics pipelines employing extensive data processing in a variety of computing settings. 

```mermaid
graph TD;
    A[Main Script] --> B[Module 1: Data Preprocessing];
    A --> C[Module 2: Quality Control];
    B --> D[Process: Data Cleanup];
    C --> D;


### The second challenge lies within the interdependency of various data analysis tools. The hidden effects of observable factors can be quantified to some extent by:

## Structure Equation Modelling (SEM)
Can bring forth the relationship between diverse outputs. Numerous observable variables (including gene expression levels, cell-type assignments, cluster identities, etc.) are present in scRNA-seq; however, these can frequently be impacted by biological processes that are not directly quantified, known as latent factors.
Latent variable examples could include:
1. Cell State: An obscure cell state that affects gene expression, such as differentiation status.
2. Unobserved factors that cause variance between samples or batches are known as batch effects.

Some types of analysis of the scRNA-seq dataset include clustering, differential expression, pathway enrichment, pseudotime analysis, cell-cell communication, etc.
One can establish causal links between these analyses with SEM. For example, latent factors such as cell differentiation stage may have an impact on pathway enrichment scores, pseudotime trajectories, and clustering outcomes.

Let's take an example of 5 independent analysis:
1. Cell Clustering (Analysis A)
2. Differential Gene Expression (Analysis B)
3. Pseudotime Ordering (Analysis C)
4. Pathway Enrichment (Analysis D)
5. Cell-Cell Communication (Analysis E)

Steps:
1. Define latent (cell differentiation state, batch effects) & observed variables (gene expression, cell clustering, pseudo-time ordering, pathway enrichment scores, etc.)
2. Specify model relationships
   a. Latent Variable Relationships:
      Cell Differentiation State -> Analysis A: Cell differentiation status affects which cluster the cell belongs to. This can be modeled as a latent variable impacting the observed cluster labels.
      Batch Effects -> Analysis B: Batch effects influence the gene expression profiles across cells, contributing to unwanted variation.
   b. Observed Variable Relationships:
      Analysis A -> Analysis C: The cell clusters determine the pseudotime trajectories, as cells belonging to similar clusters are likely to follow the same differentiation path.
      Analysis C -> Analysis D: The pseudo-time ordering influences pathway activity, indicating which pathways are active during different differentiation stages.
      Analysis C -> Analysis E: Communication: Cells at different points along the differentiation trajectory will have different cell signaling properties.
3. Create measurement equations (ME): 
      In SEM, ME describes how latent variables relate to their observed indicators. Expression levels of specific genes that are known to indicate stages of cell differentiation.
      QC Metrics: Metrics such as sequencing depth or mitochondrial gene proportion, might indicate batch effects.

                                                            Yi=λi * Latent Variable+ϵi
                                                                      or​
                             Observed variable = loading coefficient * latent variable + measurement error

4. Specify the model in the software (ex:lavaan in R)


References:
https://pmc.ncbi.nlm.nih.gov/articles/PMC10066026/
https://www.sciencedirect.com/science/article/abs/pii/B0080430767007762 

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

