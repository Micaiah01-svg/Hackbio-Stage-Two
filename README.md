# Bone Marrow Single-Cell RNA-Seq Analysis

## Overview

This project reproduces a standard single-cell RNA-seq (scRNA-seq) analysis pipeline using **Scanpy** and **Decoupler**. The goal was to process a human bone marrow dataset from raw counts to biologically interpretable cell type clusters, highlighting lineage-specific marker genes and overall tissue composition.

Dataset: [Bone Marrow scRNA-seq (.h5ad)](https://github.com/josoga2/sc/raw/refs/heads/main/bone_marrow.h5ad)

## What We Did

- **Data Preprocessing**
  - Filtered low-quality cells and lowly expressed genes.
  - Calculated mitochondrial gene percentages and applied QC filters.
  - Normalized and log-transformed the counts.
  - Selected highly variable genes and scaled the data.
- **Dimensionality Reduction & Clustering**
  - Performed PCA for dimensionality reduction.
  - Built a neighborhood graph and computed UMAP embeddings.
  - Identified clusters using the Leiden algorithm (resolution=0.5).
- **Marker Gene Analysis**
  - Downloaded and mapped PanglaoDB cell type markers to Ensembl IDs.
  - Identified top marker genes for each cluster.
  - Summarized key lineage markers (HSPCs, NK cells, B cells, etc.).
- **Biological Interpretation**
  - Predicted cell types for each cluster based on marker expression.
  - Assessed tissue source (bone marrow) and sample health status.

## Key Findings

- **Clusters identified** included hematopoietic stem/progenitor cells, monocytes/macrophages, NK cells, B cells, megakaryocytes, and erythroid lineage cells.
- **Tissue source confirmation:** Presence of HSPCs, erythroid precursors, megakaryocytes, and differentiated immune cells strongly suggests the sample is bone marrow.
- **Health status:** Cluster proportions indicate a likely healthy donor; no major depletion or expansion of lymphocytes, monocytes, or NK cells.
- **Interesting insight:** Largest cluster (28%) consisted of HSPCs, highlighting a strong progenitor population in this marrow sample.

## How to Run the Notebook

- Ensure Python 3.8+ is installed.
- Install required packages:

pip install scanpy decoupler python-igraph leidenalg

- Download the .h5ad dataset or let the notebook automatically download it.
- Run the notebook cells sequentially:
  - Preprocessing & QC
  - Dimensionality reduction & clustering
  - Marker gene mapping
  - Cluster interpretation & visualization
- Generated outputs:
  - UMAP plot (bone_marrow_clusters.png)
  - Processed AnnData object (bone_marrow_processed.h5ad)
  - Marker summaries per cluster
  - LinkedIn carousel PowerPoint summarizing the analysis
