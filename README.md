# In Silico Exploration of Pyrazoline Analogues as MAO-B Inhibitors

An exploratory computational project combining ligand-based machine learning, structure-based docking, and ADMET/CNS drug-likeness profiling for a small series of pyrazoline analogues targeting monoamine oxidase B (MAO-B), a target in Parkinson's disease.

> **Status:** Personal learning and portfolio project. It is **not** a validated drug-discovery result and has not been submitted for publication. All activity values are model predictions. Nothing here has been tested experimentally.

## What this project does

1. **Data:** Retrieves MAO-B IC50 data from ChEMBL (CHEMBL2039), cleans it, converts to pIC50, and saves a frozen snapshot (June 2026) so runs are reproducible.
2. **Modelling:** Trains a Random Forest on Morgan fingerprints (radius 2, 2048 bits) to predict pIC50. A Graph Neural Network (PyTorch Geometric) was also tried.
3. **Ligand design:** Nine analogues of a lead pyrazoline (meta-substitutions on the C-5 phenyl ring, a pyridyl analogue, and an N-propargyl analogue). 3D structures generated with RDKit (ETKDG + MMFF94).
4. **Docking:** Docked into MAO-B (PDB 2V5Z) using the CB-Dock2 web server. The cavity corresponding to the known active site (C1) was selected. Poses were inspected in PyMOL.
5. **ADMET / CNS profiling:** SwissADME and pkCSM predictions, plus a CNS MPO score (Wager et al.) calculated in Python.

## Summary of outputs

| Compound | Predicted pIC50 | Docking, C1 (kcal/mol) | Predicted hepatotoxicity |
|---|---|---|---|
| Lead | 10.441 | -9.8 | No |
| m-Cl | 10.286 | -10.2 | No |
| m-OCH3 | 10.391 | -9.4 | No |
| 3,4-diOCH3 | 10.375 | -9.8 | No |
| Pyridyl | 10.182 | -9.4 | Yes |
| N-Propargyl | 4.827* | -10.8 | Yes |

\*Outside the Random Forest applicability domain; treat as unreliable.

m-F, m-Br and m-CF3 were screened out by predicted pIC50 before docking and were not docked or profiled.

Random Forest performance: 5-fold CV R² = 0.672 ± 0.039 (pooled out-of-fold R² = 0.676, MAE = 0.664, RMSE = 0.942, n = 2,912).

## Limitations (please read before reusing anything)

- **No experimental validation.** Predicted pIC50 values are model outputs. The predicted values for the nine analogues differ from each other by only ~0.3 log units (excluding N-Propargyl), which is within the model's error (RMSE ≈ 0.94), so the ranking is not meaningful.
- **Docking is not validated.** No redocking of the co-crystallized ligand or enrichment test was performed. Scores come from a web server, and the active-site cavity (C1) was chosen by me because it is the known catalytic site, not because it scored best. For m-OCH3 a different cavity scored better (-9.7 vs -9.4). Differences of a few tenths of a kcal/mol are not reliable.
- **The GNN is unstable and was not used for predictions.** Test R² varied from about -0.1 to 0.43 across runs on this dataset size.
- **ADMET predictions are in silico estimates** from SwissADME and pkCSM, not experimental measurements.
- **CNS MPO** uses LogD approximated as LogP and an estimated pKa (not computed), and applies to the physicochemical scoring only.
- **Training data** was not filtered for assay type or compound duplicates beyond basic cleaning, and includes a few implausible negative pIC50 values.
- **Conformer generation** was not seeded, so 3D starting geometries may differ slightly between runs.
- No molecular dynamics, MAO-A selectivity, or reversibility analysis was done.

## Repository contents

```
[notebook].ipynb        # data pull, cleaning, RF/GNN models, analogue predictions, ligand prep
data/                   # frozen ChEMBL snapshot(s)
ligands/                # RDKit-generated ligand PDB files
docking/                # CB-Dock2 output complexes (C1 cavity)
figures/                # workflow, structures, model plots, docking views, CNS MPO chart
```

## Reproducing the analysis

```bash
pip install pandas numpy scikit-learn rdkit matplotlib torch torch_geometric
```

Load the frozen CSV in `data/` rather than re-querying ChEMBL, since ChEMBL updates change the training data and therefore the predictions. Docking and ADMET steps use web servers (CB-Dock2, SwissADME, pkCSM) and must be run manually.

## Tools and references

ChEMBL, RDKit, scikit-learn, PyTorch / PyTorch Geometric, CB-Dock2 (AutoDock Vina engine), SwissADME, pkCSM, PyMOL (visualization). Wager et al. (2010, 2016) for CNS MPO. Binda et al. for the MAO-B structure and binding-site description.

## Author

[Sanika Medhekar] | [medhekarsanika@gmail.com]
