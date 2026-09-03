# SARS-CoV-2 Phenomics Repurposing

This repository accompanies the publication:  
**A host-centric morphological profiling approach to identify repurposed antiviral drugs**  
[Read the article in iScience](https://www.cell.com/iscience/fulltext/S2589-0042(26)02049-3)

We present an image-based drug repurposing approach that combines viral protein immunostaining with Cell Painting to identify host-targeting antivirals.

---

## Repository Contents

- **`code/`**  
  Scripts and notebooks for calculating morphology scores, analyzing dose-response data, and generating figures.  
  Includes preprocessing, scoring (PLS-DA, Pearson correlation), and visualization.  

- **`results/`**  
  Processed results from the study:  
  - Morphology and viral infectivity scores for **5,275 repurposable compounds** tested in Vero E6 cells (single dose).  
  - Morphology and infectivity data for **324 hit compounds** tested in dose–response in A549-ACE2 cells.  

- **`features/`**  

    Image-level morphological features extracted from the Cell Painting assay.

Images were analyzed using **CellProfiler v4.2.1** (Stirling et al., 2021). Cell segmentation was performed using the **Cellpose v2.0 cyto2 model** (Pachitariu & Stringer et al., 2022), integrated within the CellProfiler workflow to identify nuclei and cell boundaries. Approximately 2,125 morphological features were extracted per object using the AreaShape, Correlation, Intensity, Granularity, Location, Neighbors, and RadialDistribution modules. Single-cell measurements were aggregated to image-level (site-level) mean values, generating the profiles provided in this repository.

The feature tables contain:

- Image-level (site-level) mean morphological profiles.
- Approximately **2,125 Cell Painting features** per image site.
- Experimental metadata, with metadata columns prefixed by **`Metadata_`**.

Features are provided in their raw extracted form prior to downstream feature selection, normalization, and morphology score calculation.

- **`pipelines/`**  
  CellProfiler pipelines used for image analysis:  
  - Illumination correction  
  - Segmentation (Cellpose)  
  - Feature extraction  

---

## Fluorescence Channels

Each site was imaged in five fluorescence channels. Feature column names encode which
channel a measurement was taken on, following the CellProfiler naming pattern
`<category>_<measurement>_<channel>_<compartment>` — for example
`Intensity_MeanIntensity_HOECHST_nuclei` — where `<compartment>` is one of `nuclei`,
`cells`, or `cytoplasm`.

Four channels are shared Cell Painting stains, common to both datasets:

| Channel name | Stain | Labels |
|---|---|---|
| `HOECHST` | Hoechst 33342 | Nuclei (DNA) |
| `SYTO` | SYTO 13/14 | Nucleoli / RNA |
| `PHAandWGA` | Phalloidin/Alexa Fluor + Wheat Germ Agglutinin/Alexa Fluor 555 | Actin cytoskeleton + plasma membrane/Golgi |
| `CONC` | Concanavalin A/Alexa Fluor | Endoplasmic reticulum |

The fifth channel carries a SARS-CoV-2 viral protein immunostain:

| Dataset | Channel name | Labels |
|---|---|---|
| `Features_VEROE6/` (Vero E6, single-dose screen) | `SARS-CoV-2-S-Ab` | SARS-CoV-2 **Spike (S)** protein |
| `Features_A549-ACE2/` (A549-ACE2, dose–response) | `SARS-CoV-2-N-Ab` | SARS-CoV-2 **Nucleocapsid (N)** protein |

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

If you use this repository, please cite the following publication:

Asp, E., Rietdijk, J., Tampere, M., Axelsson, H., Njenda, D., Potdar, S., ... & Östling, P. (2026). A host-centric morphological profiling approach to identify repurposed antiviral drugs. *iScience*, 29(8).  
[https://www.cell.com/iscience/fulltext/S2589-0042(26)02049-3](https://www.cell.com/iscience/fulltext/S2589-0042(26)02049-3)
