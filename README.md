# Machine Learning-Guided Design of Novel MAO-B Inhibitors

## Overview

This repository contains the datasets, source code, and computational workflow developed for the study:

**"Machine Learning-Guided Design and Computational Evaluation of Novel Selegiline Analogues as Potential Monoamine Oxidase-B (MAO-B) Inhibitors"**

The study integrates machine learning-based activity prediction with rational analogue design, drug-likeness assessment, ADMET prediction, molecular docking, and molecular visualization to identify potential MAO-B inhibitors for Parkinson's disease.

---

## Workflow

1. Dataset collection from ChEMBL
2. Molecular descriptor calculation
3. Machine learning model development

   * Random Forest
   * XGBoost
   * Graph Convolutional Network (PyTorch Geometric)
4. Prediction of inhibitory activity (pIC50)
5. Rational design of selegiline analogues
6. Drug-likeness evaluation (SwissADME)
7. ADMET prediction (pkCSM)
8. Molecular docking using CB-Dock2 (AutoDock Vina engine)
9. Docking pose visualization using PyMOL

---

## Repository Structure

```text
.
├── data/
│   ├── raw/
│   └── processed/
│
├── notebooks/
│   ├── 01_Data_Preprocessing.ipynb
│   ├── 02_Model_Training.ipynb
│   ├── 03_Prediction.ipynb
│   └── 04_Analogue_Analysis.ipynb
│
├── models/
│
├── docking/
│   ├── receptor/
│   ├── ligands/
│   └── docking_results/
│
├── figures/
│
├── requirements.txt
└── README.md
```

---

## Software

* Python 3.x
* RDKit
* Scikit-learn
* XGBoost
* PyTorch
* PyTorch Geometric
* Pandas
* NumPy
* Matplotlib
* SwissADME (web server)
* pkCSM (web server)
* CB-Dock2
* AutoDock Vina
* PyMOL

---

## Dataset

The bioactivity dataset was obtained from the ChEMBL database and processed prior to model development.

---

## Citation

If you use this repository, please cite:

**Sanika Medhekar.** *Machine Learning-Guided Design and Computational Evaluation of Novel Selegiline Analogues as Potential Monoamine Oxidase-B (MAO-B) Inhibitors.* 


---

## Contact

**Sanika Medhekar**

Email: medhekarsanika@gmail.com
