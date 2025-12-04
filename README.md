**Bone Marrow Single-Cell RNA-Seq Analysis - HackBio Stage 2**

**Overview**

This notebook demonstrates a **complete single-cell RNA sequencing (scRNA-seq) analysis pipeline** on human bone marrow cells. It uses **Scanpy** for data processing and visualization, **Decoupler** for cell type annotation, and generates a **LinkedIn carousel presentation** summarizing key results.

The goals are:

- Explore cellular diversity in bone marrow
- Identify key cell types and lineage-specific marker genes
- Generate clear visualizations and a professional presentation

**Stepwise Tutorial**

**Step 1: Install Dependencies**

The notebook requires the following Python packages:

- scanpy: for scRNA-seq processing
- pandas and numpy: for data manipulation
- decoupler: to access curated gene sets (PanglaoDB) for cell type annotation
- igraph and leidenalg: for clustering
- python-pptx: to create PowerPoint presentations
- matplotlib: for plotting

pip install scanpy pandas matplotlib decoupler-python python-pptx igraph leidenalg

**Step 2: Download and Load the Dataset**

- Automatically downloads the .h5ad bone marrow dataset if not already present
- Loads it into an **AnnData object**, the standard data structure for scRNA-seq analysis in Python

**Explanation:** The dataset contains gene expression counts per cell, plus metadata (cell types, donor info, disease stage, etc.).

**Step 3: Preprocess the Data**

- **Filter low-quality cells:** removes cells with too few genes
- **Filter low-expression genes:** removes genes expressed in very few cells
- **Check mitochondrial content:** high mitochondrial RNA may indicate stressed or dying cells
- **Normalize counts:** ensures comparability across cells
- **Log-transform:** reduces skew in expression values
- **Select highly variable genes (HVGs):** focuses on genes that capture biological variability
- **Scale data:** standardizes expression for downstream analyses

**Explanation:** This step ensures that only high-quality, biologically informative data is analyzed.

**Step 4: Dimensionality Reduction & Clustering**

- **PCA (Principal Component Analysis):** reduces dimensionality while retaining key variation
- **Compute neighbors:** builds a graph connecting similar cells
- **UMAP (Uniform Manifold Approximation and Projection):** projects cells into 2D space for visualization
- **Leiden clustering:** identifies groups of similar cells

**Explanation:** PCA and UMAP reduce complexity, while Leiden clusters reveal biologically meaningful cell populations.

**Step 5: Cell Type Annotation**

- **Retrieve PanglaoDB markers:** curated gene sets for human cell types
- **Map markers to Ensembl IDs:** ensures consistency with the dataset
- **Assign predicted cell types to clusters:** matches clusters to known cell types

Example predicted cell types:

- Cluster 0 → Hematopoietic Stem/Progenitor Cells (HSPCs)
- Cluster 1 → Monocytes / Macrophages
- Cluster 3 → NK Cells / Cytotoxic Lymphocytes
- Cluster 4 → B Cells / Lymphocytes
- Cluster 6 → Megakaryocytes / Platelets
- Cluster 8 → Erythroid Lineage Cells

**Explanation:** Each cluster is labeled with a likely cell type based on known marker gene expression.

**Step 6: Key Marker Gene Expression**

- Calculates the average expression of **lineage-specific markers** per cluster
- Examples: CD34 for HSPCs, CD3D for T cells, MPO for myeloid cells

**Explanation:** Helps confirm the identity of clusters and interpret their biological roles.

**Step 7: Generate UMAP Visualizations**

- **UMAP 1 - Clusters:** cells colored by Leiden cluster ID
- **UMAP 2 - Cell Type Labels:** cells labeled with predicted cell types

**Adjustments:**

- Labels are positioned for readability
- Colormap chosen for clarity
- Both visualizations are saved locally

**Step 8: Create LinkedIn Carousel Presentation**

- Uses **python-pptx** to generate a downloadable PowerPoint file
- Slides include:
  - Project title, author, and tools used
  - UMAP with clusters
  - UMAP with cell type annotations
  - Predicted cell types per cluster (table)
  - Biological interpretation of cell types
  - Key insights

**Explanation:** This carousel is **downloadable immediately** after running the notebook. It summarizes the analysis in a professional, shareable format.

**Step 9: Save Processed Data**

- Saves preprocessed AnnData object for reuse
- File: bone_marrow_processed.h5ad

**Explanation:** Preserves the cleaned, normalized, and annotated data for future analysis without re-running the pipeline.

**Key Insights**

- Largest cluster corresponds to HSPCs → strong progenitor population
- Minor populations like NK cells and monocytes are detectable → functional diversity
- Marker gene expression confirms cluster identities

**Step 10: How to Run the Notebook**

- Open the notebook in Jupyter or Colab
- Run **all cells sequentially**
- Outputs:
  - UMAP plots (clusters and annotated)
  - LinkedIn carousel presentation (SingleCell_Carousel.pptx)
  - Processed AnnData object (bone_marrow_processed.h5ad)

**Author**

**Micaiah Adedeji Adeoluwa**

- HackBio Stage 2 Project
- Focus: Single-Cell Genomics, Cell Type Annotation, Computational Biology
