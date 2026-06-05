# SARS-CoV-2 Phenomics Repurposing

This repository accompanies the manuscript:  
**Morphological cell profiling for drug repurposing against SARS-CoV-2 infection**  
[Read the preprint on bioRxiv](https://www.biorxiv.org/content/10.1101/2025.08.28.672794v1)

We present an image-based drug repurposing approach that combines viral protein immunostaining with Cell Painting to identify host-targeting antivirals.

---

## Repository Contents

- **`code/`**  
  Scripts and notebooks for calculating morphology scores, analyzing dose–response data, and generating figures.  
  Includes preprocessing, scoring (PLS-DA, Pearson correlation), and visualization.  

- **`results/`**  
  Processed results from the study:  
  - Morphology and viral infectivity scores for **5,275 repurposable compounds** tested in Vero E6 cells (single dose).  
  - Morphology and infectivity data for **324 hit compounds** tested in dose–response in A549-ACE2 cells.  

- **`features/`**  

Image-level morphological features extracted from the Cell Painting assay.

Images were analyzed using **CellProfiler v4.2.1** (Stirling et al., 2021). Cell segmentation was performed using the **Cellpose v2.0 cyto2 model** (Pachitariu & Stringer et al., 2022), integrated within the CellProfiler workflow to identify nuclei and cell boundaries. Approximately 2,000 morphological features were extracted per object using the AreaShape, Correlation, Intensity, Granularity, Location, Neighbors, and RadialDistribution modules. Single-cell measurements were aggregated to image-level (site-level) mean values, generating the profiles provided in this repository.

The feature tables contain:

- Image-level (site-level) mean morphological profiles.
- Approximately **2,000 Cell Painting features** per image site.
- Experimental metadata, with metadata columns prefixed by **`Metadata_`**.

Features are provided in their raw extracted form prior to downstream feature selection, normalization, and morphology score calculation.

- **`pipelines/`**  
  CellProfiler pipelines used for image analysis:  
  - Illumination correction  
  - Segmentation (Cellpose)  
  - Feature extraction  

---

## Scoring Methods

### Morphology Score
Quantifies the overall morphological similarity to the uninfected phenotype.  
The score is calculated as the average of:
- The **PLS-DA prediction score**  
- The **Pearson correlation coefficient** to the uninfected control cell population  

This yields a *morphology-to-uninfected-control* score.

### Viral Infectivity
Determined as the **percentage of infected cells per well**, normalized per plate to the infected controls (DMSO).

---

## Citation

If you use this repository, please cite the following preprint:

Asp, E.\*, Rietdijk, J.\*, Tampere, M., Axelsson, H., Njenda, D., Potdar, S., Kalman, A.,  
Georgieva, P., Lapins, M., Ballante, F., Soler, A., de Kort, M., Aittokallio, T.,  
Zaliani, A., Kuzikov, M., Gribbon, P., Lo, D., Carreras-Puigvert, J., Seashore-Ludlow, B.,  
Spjuth, O., & Östling, P. (2025). Morphological cell profiling for drug repurposing against SARS-CoV-2 infection. *bioRxiv*.  
[https://doi.org/10.1101/2025.08.28.672794](https://doi.org/10.1101/2025.08.28.672794)
