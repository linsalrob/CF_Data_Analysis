[![Edwards Lab](https://img.shields.io/badge/Bioinformatics-EdwardsLab-03A9F4)](https://edwards.flinders.edu.au/)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.17934084.svg)](https://doi.org/10.5281/zenodo.17934084)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![GitHub language count](https://img.shields.io/github/languages/count/linsalrob/PhiSpy)

# CF Airway Metagenome Analysis

**Global Metagenomic Signatures Reveal Predictive Markers of Infection in Cystic Fibrosis Airways**

This repository contains all analysis code, Jupyter notebooks, and supporting documentation for our Cystic Fibrosis (CF) Airway Metagenome study, including the prediction of infection status, antibiotic exposure, and health metrics from metagenomic data.

---

## Overview

Our study integrates metagenomic sequencing, machine learning, and clinical metadata to understand microbial ecology and disease progression in people with cystic fibrosis (pwCF).

We sequenced more than 120 airway metagenomes from South Australian people with CF (pwCF) and analysed over 1,000 global CF datasets, we applied autoencoder-based dimensionality reduction and gradient-boosted random forests to identify microbial and functional features predictive of:

* **Pseudomonas culture status**
* **MDR (multidrug-resistant) Pseudomonas**
* **Fungal colonisation (Aspergillus, Candida)**
* **Antibiotic exposure and route of administration**
* **Overall health metrics derived from FEV<sub>1</sub> and medication use**

---

## Analytical Workflow

### 1. Data Preparation

Raw metagenomic reads were processed using the [`atavide-lite`](https://doi.org/10.5281/zenodo.15356766) pipeline for quality control, human read removal, taxonomic and functional annotation.

### 2. Dimensionality Reduction

We trained autoencoders to condense >30,000 taxonomic and functional variables into ~150 latent clusters (COPFs) capturing co-correlated microbial and functional signals:

Each COPF was summarised using the first principal component of its cluster to serve as a meta-feature for downstream prediction.

### 3. Predictive Modelling

For categorical outcomes (e.g. culture positivity), we used the `GradientBoostingClassifier` from scikit-learn, while for continuous outcomes (e.g. FEV<sub>1</sub> ratio), we used the `GradientBoostingRegressor`.

ROC curves, AUCs, and feature importances were visualised using matplotlib and seaborn.

### 4. Health and Medication Metrics

We defined a Medications Score via PCA combining antibiotic, antifungal, steroid, and monoclonal antibody prescriptions.

This was used to quantify overall treatment intensity and correlate with microbiome composition and virulence metrics.

### 5. Cross-Dataset Validation

We validated the predictive model across 22 global CF metagenomic datasets from NCBI BioProjects (e.g. PRJNA316588, PRJNA1081394, PRJEB51171), achieving >90% concordance with reported Pseudomonas culture outcomes.

---

## Key Analyses and Notebooks

All the notebooks are in the [Jupyter Notebooks](Jupyter/) directory.


Topic                              | Notebook / File                                                    | Description                                                                   
---------------------------------- | ------------------------------------------------------------------ | -------------------------------------------------------------------------------
Allergic Bronchopulmonary Aspergillosis   | ABPA.ipynb                     | Comparison of culture and sequencing detection of Aspergillus and Candida
Individual Microbiomes                    | EveryPerson.ipynb              | Longitudinal trajectories of individual pwCF
Sequencing Platform Comparison            | MGI_Promethion_Minion.ipynb    | Cross-platform taxonomic agreement analysis
Mutual Information between MAGs and reads | MutualInformation.ipynb        | Calculates mutual information between MAGs and metagenomic reads to investigate how the inferences overlap
Pseudomonas                               | Pseudomonas_PCA.ipynb          | Identifies COPFs predictive of *P. aeruginosa* and MDR phenotypes
Stenotrophomonas                          | Stenotrophomonas.ipynb         | Identifies COPFs predictive of *S. maltophilia* phenotypes
Data Reduction and Validation             | AutoEncoding.ipynb             | Autoencoder training and validation of COPFs
Health metrics                            | HealthPCA.ipynb                | Derives Medications Score and explores health-associated COPFs
Metadata explorer                         | Metadata.ipynb                 | Exploration of clinical metadata and correlations for the paper
Mycobacteria                              | Mycobacteria.ipynb             | Identifies COPFs predictive of *M. abscessus* phenotypes
Pseudomonas predictions                   | Pseudomonas_predictions.ipynb  | Applies trained models to global CF datasets for validation


---

## Accessing the data

We have provided an accessory [cf_analysis_lib](cf_analysis_lib/) library to facilitate loading and processing of the data used in this study into Python. 
The librbary includes functions to load metagenomic profiles, clinical metadata, and pre-trained models, as well as utility functions for analysis and visualisation that
we used in writing the paper. 

The Jupyter notebooks in the [Jupyter Notebooks](Jupyter/) directory demonstrate how to use this library to reproduce the analyses and figures from the study.


## Citation

If you use this code or framework, please cite:

> Edwards R., et al. (2025). *Predictive metagenomics reveals microbial and functional markers of infection and health in cystic fibrosis airways.* Manuscript in preparation.

and the software:

> Edwards R. (2025). *atavide-lite: Atta Pony.* Zenodo. [https://doi.org/10.5281/zenodo.15356766](https://doi.org/10.5281/zenodo.15356766)

---

## License

This repository is released under the **MIT License**.
Data used herein includes both public (SRA/ENA) and clinical data under restricted access agreements.

