# Interpretable Leaf Vein Analysis Using Classical Machine Vision

### From Image Enhancement to Feature-Based Classification

An interpretable computer vision pipeline for extracting, measuring, and analysing leaf vein networks from grayscale imagery. The project combines classical image processing, handcrafted structural features, dimensionality reduction, clustering, and machine-learning validation without relying on an end-to-end deep neural network.

**Authors:** Sajedabanu Patel and Annur Anika  
**Course:** ENGI 9804 - Image Processing and Applications  
**Program:** Master of Science in Computer Science  
**Institution:** Memorial University of Newfoundland  
**Completed:** August 2026

## Project motivation

Leaf veins contain useful structural information for plant phenotyping and biological image analysis, yet faint secondary veins, uneven illumination, image noise, and changing vein thickness make reliable extraction difficult. This project develops a transparent pipeline in which every processing decision can be inspected, measured, and explained.

## Pipeline

| Stage | Method | Purpose |
| --- | --- | --- |
| Standardization | Resize to 512 x 512 and normalize intensity | Create a consistent image representation |
| Noise reduction | Gaussian, median, and bilateral filtering | Compare denoising against structural preservation |
| Enhancement | CLAHE, unsharp masking, and top-hat transformation | Improve local contrast and reveal weaker veins |
| Segmentation | Global, Otsu, adaptive thresholding, and Canny edges | Isolate candidate vascular structures |
| Refinement | Opening, closing, and connected-component analysis | Remove artefacts and reconnect fragmented veins |
| Network analysis | Skeletonization, endpoints, and junctions | Convert the segmentation into a topology-aware representation |
| Feature extraction | 11 geometric and topological descriptors | Quantify venation structure across the dataset |
| Statistical learning | PCA, K-Means, and Random Forest | Explore variation, group similar images, and validate feature consistency |

## Key results

- Processed **900 grayscale leaf images** from the CHAMBASA dataset.
- Generated **11 interpretable structural descriptors**, including segmented area, skeleton length, vein density, coverage, endpoint density, junction density, and connectivity.
- Selected bilateral filtering as the strongest balance between noise suppression and vein-boundary preservation in the evaluated example.
- Produced continuous vein representations using adaptive thresholding followed by morphological refinement.
- Recorded a mean **five-fold cross-validation accuracy of 96.0%** when a Random Forest predicted the four K-Means cluster assignments.

> **Interpretation note:** the Random Forest predicts clusters derived from the same handcrafted feature space. The reported accuracy therefore measures internal feature consistency; it does not represent plant-species classification against independent botanical labels.

## Repository structure

```text
.
|-- notebooks/
|   `-- leaf_vein_analysis.ipynb
|-- docs/
|   `-- Leaf_Vein_Analysis_Project_Report.pdf
|-- data/
|   `-- README.md
|-- .gitignore
|-- CITATION.cff
|-- requirements.txt
`-- README.md
```

## Run the notebook

1. Clone the repository and enter its directory.
2. Create a Python environment and install the dependencies:

   ```bash
   python -m venv .venv
   source .venv/bin/activate  # Windows: .venv\Scripts\activate
   pip install -r requirements.txt
   ```

3. Place the CHAMBASA images in `data/CHAMBASA/` and a representative image at `data/sample_leaf.jpg`, or set these environment variables:

   ```bash
   export LEAF_DATASET_PATH="/path/to/CHAMBASA"
   export LEAF_SAMPLE_IMAGE="/path/to/sample_leaf.jpg"
   export LEAF_RESULTS_DIR="/path/to/results"
   ```

4. Start Jupyter and run the notebook from top to bottom:

   ```bash
   jupyter lab notebooks/leaf_vein_analysis.ipynb
   ```

The notebook retains its completed outputs for review. Its configuration cell now supports local paths and environment variables; the original Colab-specific execution metadata has been removed.

## Limitations and future work

- Extremely low-contrast tertiary veins may disappear during segmentation.
- Strong shadows or reflections can create false vascular structures.
- Morphological refinement trades noise removal against preservation of very thin veins.
- Skeletonization preserves topology but removes vein-width information.
- The current validation uses feature-derived clusters rather than biological species labels.

Future work can add graph-theoretic descriptors, adaptive parameter selection, multiscale features, independent species labels, and hybrid models that combine interpretable features with learned representations.

## Dataset and reuse

The CHAMBASA images are **not redistributed** in this repository. Obtain the dataset from its authorized source and follow its access and reuse conditions.

The repository does not currently grant a software or report license. Contact the authors before reuse beyond applicable copyright exceptions.

## Citation

Please cite the project as:

> Sajedabanu Patel and Annur Anika. *Interpretable Leaf Vein Analysis Using Classical Machine Vision: From Image Enhancement to Feature-Based Classification*. ENGI 9804 project report, Memorial University of Newfoundland, 2026.

