# SARS-CoV-2 Phenomics Repurposing

This repository accompanies the manuscript:  
**Morphological cell profiling for drug repurposing against SARS-CoV-2 infection**

We present an image-based drug repurposing approach that combines viral protein immunostaining with Cell Painting to identify host-targeting antivirals.

---

## Repository Contents

- **Morphology and viral infectivity scores**
  - Data for **5,275 repurposable compounds** tested in Vero E6 cells at a single dose.
  - Data for **324 hit compounds** from the initial screen, tested in dose–response in A549-ACE2 cells.

---

## Scoring Methods

### Morphology Score
Quantifies the overall morphological similarity to the uninfected phenotype.  
The score is calculated as the average of:
- The **PLS-DA prediction score**  
- The **Pearson correlation coefficient** to the uninfected control cell population  

This yields a *morphology-to-uninfected-control* score.

### Viral Infectivity
Determined as the **percentage of infected cells per well**, normalized per plate to the infected control (DMSO).

---

