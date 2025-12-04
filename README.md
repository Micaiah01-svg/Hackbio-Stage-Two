**HackBio Stage 2 Project: Single-Cell RNA-Seq Analysis of PBMCs**

**Overview**

This project reproduces a core single-cell RNA-seq analysis pipeline using **Scanpy** and **Decoupler**, starting from raw counts to biologically interpretable cell type clusters. The analysis was performed on a publicly available PBMC dataset (peripheral blood mononuclear cells).

The main goals of the project:

- Preprocess the single-cell RNA-seq data.
- Perform dimensionality reduction and clustering.
- Identify cell types using key lineage markers and PanglaoDB reference.
- Visualize the dataset using UMAP with cluster and **cell type annotations**.
- Generate a LinkedIn carousel summarizing the results.

**Data Source**

- Publicly available PBMC dataset (pbmc.h5ad) hosted on GitHub.
- Dataset contains raw counts for ~10,000 single cells and ~20,000 genes.
- The dataset represents peripheral blood mononuclear cells, not bone marrow.

**Methodology**

**1\. Data Preprocessing**

- **Filtering:** Removed low-quality cells (<200 genes) and genes expressed in <3 cells.
- **Mitochondrial filtering:** Cells with >10% mitochondrial reads were removed.
- **Normalization:** Total counts per cell were scaled to 10,000.
- **Log Transformation:** Applied log1p transformation to normalize gene expression.
- **Highly Variable Genes (HVGs):** Selected the top 2000 most variable genes.
- **Scaling:** All expression values scaled to unit variance and zero mean.

**2\. Dimensionality Reduction & Clustering**

- **PCA:** Reduced dimensionality to the top 40 PCs.
- **Neighbors graph:** Built using 10 nearest neighbors.
- **UMAP:** Visualized in 2D space.
- **Clustering:** Leiden algorithm (resolution = 0.5) to detect clusters.

**3\. Cell Type Identification**

- **Reference:** PanglaoDB marker genes for human immune cells.
- **Markers analyzed:** HSPCs (CD34), NK cells (NKG7, PRF1, GZMB), T cells (CD3D, CD4, CD8A), B cells (MS4A1, CD19), Plasma cells (SDC1), Monocytes (CSF1R, IL1B), Megakaryocytes (PF4, PPBP), Erythroid cells (HBB, GATA1).
- **Cluster annotation:** Clusters were annotated based on mean expression of key markers.

| **Cluster** | **Cell Type** |
| --- | --- |
| 0   | HSPCs |
| 1   | Monocytes |
| 2   | Monocytes |
| 3   | NK Cells |
| 4   | B Cells |
| 5   | T Cells |
| 6   | Megakaryocytes |
| 7   | Plasma Cells |
| 8   | Erythroid Cells |

**4\. Visualization**

- **UMAP with cluster IDs**: Colored by Leiden clusters.
- **UMAP with cell type labels**: Cluster centroids annotated with predicted cell types.
- **LinkedIn carousel:** Includes UMAPs, cell type table, and key biological insights. Carousel is saved locally (HackBio_SingleCell_Analysis.pptx) for immediate download.

**5\. Statistical Considerations**

- Mean expression of key markers per cluster was calculated to confirm cell type identity.
- Peripheral blood assignment justified based on:
  - Presence of expected PBMC populations: NK cells, T cells, B cells, monocytes.
  - HSPCs present but in minor proportion compared to bone marrow datasets.
  - Relative abundance patterns consistent with healthy donor peripheral blood.

**Key Biological Insights**

- Largest cluster enriched for **HSPCs**, reflecting progenitor cells in circulation.
- **Monocytes** and **NK cells** detected in expected proportions for PBMCs.
- **T cells** and **B cells** represented typical lymphocyte populations.
- **Plasma cells** and **megakaryocytes** detected at low abundance, consistent with peripheral blood.
- Sample likely represents a healthy donor with balanced immune cell composition.

**Dependencies**

- Python 3.9+
- Packages:
  - scanpy >= 1.9
  - decoupler >= 0.3
  - pandas
  - numpy
  - matplotlib
  - pptx

Install via pip:

pip install scanpy decoupler pandas numpy matplotlib python-pptx

**Workflow Instructions**

- Clone or download the repository.
- Run the notebook single_cell_pipeline.ipynb sequentially.
- Ensure internet connection to download the PBMC dataset.
- The UMAP plots will display inline.
- LinkedIn carousel (HackBio_SingleCell_Analysis.pptx) will be saved locally for immediate use.

**Expected Outputs**

- **Preprocessed AnnData object** with filtered cells and highly variable genes.
- **UMAP plots**:
  - Colored by cluster ID.
  - Annotated with cell types.
- **Cluster-to-cell type table**.
- **Downloadable LinkedIn carousel** including UMAP, cell types, and insights.
- **Key marker expression per cluster** (for reproducibility and verification).

**Notes**

- All steps are modular with clearly commented code blocks.
- Figures and outputs can be adjusted by changing plotting parameters (font size, figure size).
- Cell type assignments are based on marker gene expression; proportions should be interpreted relative to peripheral blood expectations.
- For more rigorous tissue assignment, users can compare to publicly available PBMC and bone marrow datasets.

**References**

- Wolf FA, Angerer P, Theis FJ. SCANPY: large-scale single-cell gene expression data analysis. Genome Biology (2018).
- PanglaoDB: Database for single-cell RNA-seq marker genes.
- Decoupler: Functional genomics and network-based cell type inference in Python.
