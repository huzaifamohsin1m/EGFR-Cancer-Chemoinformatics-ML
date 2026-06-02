# EGFR-Cancer-Chemoinformatics-ML
An in silico data analytics and machine learning pipeline to predict chemical compound potencies against Human EGFR for oncology drug discovery.

# Building a Predictive Machine Learning Model for Human Epidermal Growth Factor Receptor (EGFR) Inhibitors in Cancer Therapeutics

**Author:** Huzaifa Mohsin 
**Status:** Undergraduate Chemistry Student (6th Semester)  
**Methodology:** In Silico Chemoinformatics & Data Analytics (No-Lab Workflow)  
**Project Goal:** To construct a robust, deployment-ready machine learning classifier capable of predicting the biological activity of novel chemical compounds against breast and lung cancer proteins.

---

## Phase 1: Data Acquisition & Target Selection
* **Target Identifier:** Human EGFR (`CHEMBL203`), a highly vital target in modern oncology and pharmaceutical R&D.
* **Database Utilized:** ChEMBL REST API (European Bioinformatics Institute).
* **Execution:** Automated data retrieval was conducted utilizing a Python-based programmatic API connection to pull thousands of historical wet-lab experimental data points directly into a computational workspace.
* **Raw Data Yielded:** 26,600 unique compound interaction records.

---

## Phase 2: Data Engineering & Curation
Raw chemical datasets are notoriously noisy. To construct a high-impact publication, the raw 26,600 rows underwent a strict programmatic data cleaning pipeline using Python:
1.  **Missing Value Mitigation:** Dropped all compound rows lacking verified biological measurement metrics (`standard_value`) or structural codes (`canonical_smiles`).
2.  **Duplicate Structural Elimination:** Identified and purged overlapping structural duplicates to prevent data leakage during subsequent machine learning training.
3.  **Feature Selection:** Curated and saved columns containing key molecular descriptors: `molecule_chembl_id`, `canonical_smiles`, and `standard_value`.
* **Cleaned Data Yielded:** 13,660 high-purity, unique chemical structures.

---

## Phase 3: Bioactivity Classification & Standardization
In quantitative drug discovery, the half-maximal inhibitory concentration ($IC_{50}$) determines a molecule's potency. To train a predictive classifier, the dataset's numerical values were mapped into standardized categorical bins according to international pharmaceutical R&D benchmarks:

$$\text{Bioactivity Class} = \begin{cases} 
\text{Active (High Potency)} & \text{if } IC_{50} \le 1000 \text{ nM} \\ 
\text{Inactive (Low Potency)} & \text{if } IC_{50} \ge 10000 \text{ nM} \\ 
\text{Intermediate} & \text{if } 1000 \text{ nM} < IC_{50} < 10000 \text{ nM} 
\end{cases}$$

### Dataset Distribution Summary:
* **Active Compounds:** 9,416 molecules
* **Inactive Compounds:** 2,363 molecules
* **Intermediate Compounds:** 1,881 molecules

*Conclusion:* The high density of active examples provides an ideal statistical landscape for a machine learning model to learn key structure-activity rules.
