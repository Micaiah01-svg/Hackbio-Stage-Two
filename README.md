# README: HackBio Stage 2 - Single-Cell RNA-Seq Analysis

## Project Title

**Reproducing a Core Single-Cell RNA-Seq Analysis Pipeline Using Scanpy and Decoupler** 
BY MICAIAH ADEOLUWA ADEDEJI

## Overview

This project reproduces a standard single-cell RNA-seq (scRNA-seq) workflow using Python tools Scanpy and Decoupler. Starting from raw counts of a human bone marrow dataset, the workflow processes the data to identify biologically interpretable cell type clusters.

The project was completed as part of **HackBio Stage 2**, and the focus was on integrating data-driven analysis, rigorous marker gene mapping, and visualization to generate clear biological insights.

## Dataset

- **Source:** Bone Marrow single-cell dataset from GitHub (adapted from CZI).
- **Link:** [Bone Marrow Dataset](https://github.com/josoga2/sc/raw/refs/heads/main/bone_marrow.h5ad)
- **Format:** .h5ad (AnnData format, compatible with Scanpy)
- **Addendum:** The dataset uses Ensembl gene IDs; a gene symbol ↔ Ensembl mapping from BioMart ensures compatibility with Decoupler.

## Tools and Libraries

- **Python 3.x**
- **Scanpy** - preprocessing, PCA, UMAP, clustering, marker identification
- **Decoupler** - mapping marker genes to cell types
- **PanglaoDB** - curated marker database for human cell types
- **BioMart** - Ensembl gene ID ↔ gene symbol mapping
- **igraph** & **leidenalg** - for Leiden clustering
- **pandas**, **numpy**, **matplotlib** - data manipulation and plotting

## Workflow

- **Data Download and Loading**
  - Downloaded .h5ad file programmatically.
  - Loaded into Scanpy as adata.
- **Quality Control**
  - Filtered cells with fewer than 200 genes and genes expressed in fewer than 3 cells.
  - Assessed mitochondrial gene content and removed high-MT cells.
  - Filtered cells with extreme gene counts.
- **Normalization and Transformation**
  - Normalized total counts per cell to 10,000 and log-transformed.
  - Selected highly variable genes for downstream analysis.
  - Scaled data to a maximum of 10 to remove extreme values.
- **Dimensionality Reduction and Clustering**
  - PCA for linear reduction.
  - Constructed nearest-neighbor graph.
  - UMAP embedding for 2D visualization.
  - Leiden clustering (resolution = 0.5) to define clusters.
- **Marker Gene Identification**
  - Queried PanglaoDB markers and mapped to Ensembl IDs using BioMart.
  - Filtered duplicates and missing values.
  - Calculated top marker genes per cluster and key lineage marker expression.
- **Cell Type Annotation**
  - Annotated clusters based on key marker genes:
    - HSPCs (Hematopoietic Stem/Progenitor Cells)
    - Monocytes / Macrophages
    - NK Cells / Cytotoxic Lymphocytes
    - B Cells / Lymphocytes
    - Megakaryocytes / Platelets
    - Erythroid Lineage Cells
- **Biological Interpretation**
  - Assessed tissue source based on presence of progenitors and lineage populations → consistent with bone marrow.
  - Interpreted cluster proportions to infer health status → likely healthy donor.
  - Highlighted interesting findings, e.g., strong HSPC population in cluster 0 (~28%).
- **LinkedIn Carousel**
  - Generated a clean, visually appealing carousel summarizing:
    - UMAP plot
    - Annotated cell types
    - Biological interpretation
    - One key insight

## How to Run

- Clone or download the repository.
- Install required packages:
- pip install scanpy decoupler python-igraph leidenalg pandas numpy matplotlib
- Run the Jupyter notebook bone_marrow_scRNAseq.ipynb step by step.
- Output files:
  - bone_marrow_processed.h5ad → processed AnnData object
  - bone_marrow_clusters.png → UMAP with Leiden clusters
  - linkedin_carousel.pptx → LinkedIn-ready summary

## Key Learnings

- Reinforced understanding of single-cell RNA-seq workflows, including preprocessing, dimensionality reduction, and clustering.
- Learned to map curated marker databases to Ensembl gene IDs for robust cell type annotation.
- Gained practical experience in creating reproducible and interpretable bioinformatics analyses.
- Project provided a real-world example of how computational biology informs tissue-level biology.

## References

- Wolf, F.A., Angerer, P., & Theis, F.J. (2018). SCANPY: large-scale single-cell gene expression data analysis. Genome Biology, 19, 15.
- Omnipath / Decoupler Python library: <https://github.com/saezlab/decoupler>
- PanglaoDB Human Markers: <https://panglaodb.se/>
- BioMart: <http://www.ensembl.org/biomart/martview>
