# 🔬 UV-Vis Spectroscopy Prediction using Machine Learning

> Predicting UV-visible absorption spectra of molecules using Random Forest trained on 134,000 molecules from the QM9 dataset.

---

## 📌 Overview

Traditional UV-vis spectroscopy requires either **expensive lab equipment** or **slow quantum chemistry calculations** (hours per molecule). This project replaces both with an **ML model that predicts absorption wavelength in milliseconds**.

The model learns the relationship between simple molecular features and the **HOMO-LUMO gap** — the quantum property that directly determines where a molecule absorbs light.

---

## ⚛️ The Science Behind It

Every molecule absorbs UV-visible light at a specific wavelength determined by its **HOMO-LUMO gap**:

```
HOMO = Highest Occupied Molecular Orbital
LUMO = Lowest Unoccupied Molecular Orbital
Gap  = Energy difference between them
```

The absorption wavelength is calculated from the gap using:

```
λ (nm) = 1240 / (gap × 27.2114)
       = 45.563 / gap_in_Hartree
```

So by predicting the HOMO-LUMO gap with ML, we directly get the **UV-vis absorption peak** of any molecule.

---

## 🤖 The ML Model

| Property | Value |
|---|---|
| Algorithm | Random Forest Regressor |
| Dataset | QM9 (133,885 molecules) |
| Target variable | HOMO-LUMO gap (Hartree) |
| Train/Test split | 80% / 20% |
| R² score | **0.877** |
| MAE | 0.0117 Hartree |
| Tuning | GridSearchCV |
| Best params | n_estimators=300, max_features=0.8 |

### Features Used

| Feature | Description |
|---|---|
| `molecular_weight` | Total mass of the molecule |
| `num_atoms` | Number of heavy atoms |
| `num_bonds` | Number of chemical bonds |
| `num_rings` | Number of ring structures |
| `num_hydrogens` | Number of hydrogen atoms |
| `logP` | Lipophilicity (octanol-water partition) |

All features are extracted from **SMILES strings** using **RDKit**.

---

## 📊 Results

The model was tested on 7 well-known molecules:

| Molecule | Gap (Hartree) | λ_max (nm) | Region |
|---|---|---|---|
| Ethanol | ~0.47 | ~97 | Deep UV |
| Acetone | ~0.35 | ~130 | Deep UV |
| Benzene | ~0.23 | ~198 | Near UV |
| Naphthalene | ~0.19 | ~240 | Near UV |
| Aspirin | ~0.22 | ~207 | Near UV |
| Caffeine | ~0.21 | ~217 | Near UV |
| Glucose | ~0.40 | ~114 | Deep UV |

---

## 🗂️ Project Structure

```
UV-Vis-Spectroscopy-ML/
│
├── spectroscopy.ipynb        ← Main Jupyter notebook (full pipeline)
├── README.md                 ← You are here
├── .gitignore                ← Excludes large files
│
├── plots/                    ← Generated output plots
│   ├── uv_vis_spectra_all.png
│   ├── uv_vis_overlay.png
│   ├── feature_importance.png
│   └── predicted_vs_actual.png
│
│   # Not uploaded (too large for GitHub)
├── qm9.csv                   ← Download link below
└── spectroscopy_model.pkl    ← Train locally using notebook
```

---

## 🚀 How to Run

### 1. Clone the repository
```bash
git clone https://github.com/belalmuhammad38/UV-Vis-Spectroscopy-ML.git
cd UV-Vis-Spectroscopy-ML
```

### 2. Install dependencies
```bash
pip install numpy pandas matplotlib seaborn scikit-learn joblib rdkit
```

Or with conda:
```bash
conda install -c conda-forge rdkit
pip install scikit-learn joblib
```

### 3. Download the QM9 dataset
The dataset is too large for GitHub. Download it manually:
```bash
wget https://deepchemdata.s3-us-west-1.amazonaws.com/datasets/qm9.csv
```
Or just paste the link in your browser and save `qm9.csv` in the project folder.

### 4. Open the notebook
```bash
jupyter notebook spectroscopy.ipynb
```
Run all cells from top to bottom. The model will train and all plots will generate automatically.

### 5. Predict any molecule
```python
predict_uv_vis('c1ccccc1', 'Benzene')
predict_uv_vis('CC(=O)Oc1ccccc1C(=O)O', 'Aspirin')
predict_uv_vis('YOUR_SMILES_HERE', 'Your Molecule')
```

---

## 📦 Dependencies

```
Python        >= 3.8
numpy
pandas
matplotlib
seaborn
scikit-learn
rdkit
joblib
jupyter
```

---

## 💡 Inspiration

This project was inspired by **Prof. Pavlo Dral's** lecture on ML for Molecular Spectroscopy (XACS lecture series), which demonstrated how machine learning can replace expensive quantum chemistry calculations for predicting spectroscopic properties.

---

## 🔭 Future Work

- Add more molecular features (fingerprints, 3D descriptors)
- Try deep learning models (Graph Neural Networks)
- Extend to larger molecules beyond QM9's 9-heavy-atom limit
- Predict full spectral shape, not just the peak wavelength
- Incorporate experimental UV-vis data for validation

---

## 👤 Author

**Belal Muhammad**
- GitHub: 
- Kaggle: 

---

## 📄 Dataset Credit

**QM9 Dataset** — Ramakrishnan et al., *Scientific Data*, 2014.
134,000 small organic molecules with quantum chemical properties computed at the B3LYP/6-31G(2df,p) level of theory.


