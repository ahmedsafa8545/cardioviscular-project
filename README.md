# Data Mining Course Project — Cardiovascular Disease Dataset 🫀

A data mining project analyzing a Kaggle **Cardiovascular Disease Dataset** (1,200 patient records, 12 clinical/lifestyle features) through exploratory analysis, feature selection, and multiple clustering techniques, culminating in a unified diagnostic support pipeline.

## Project Overview

The project investigates patient health records to understand patterns associated with cardiovascular disease and to group patients into meaningful risk profiles. It combines:

- Exploratory data analysis (on both raw and cleaned data)
- Data cleaning & preprocessing (outlier removal, feature engineering, encoding, scaling)
- A **Genetic Algorithm** for feature subset selection
- **K-Medoids (PAM) clustering** for patient segmentation
- **Hierarchical clustering** for comparison
- A **Fuzzy Inference System** for risk assessment
- A final **unified system** that integrates preprocessing, clustering, and fuzzy inference into one pipeline

## Repository Contents

| File | Description |
|---|---|
| `Inital_EDA.ipynb` | Initial exploratory analysis of the **raw, uncleaned** dataset — data quality checks, distributions, and outlier identification |
| `Data_Mining_Project.ipynb` | Main project notebook — preprocessing, EDA on cleaned data, genetic algorithm, K-Medoids clustering, hierarchical clustering, fuzzy inference system, and the unified pipeline |
| `datasets/mining_dataset.csv` | Original raw dataset (1,200 rows, 12 columns) |
| `datasets/mining_unscaled.csv` / `cardio_cleaned_unscaled.csv` | Cleaned dataset (outliers removed, BMI added) in original units |
| `datasets/mining_scaled.csv` / `cardio_cleaned_scaled.csv` | Cleaned dataset after standard scaling, used for clustering |
| `kmedoids_elbow_silhouette.png` | Elbow method & silhouette score plots used to choose the optimal number of clusters |
| `kmedoids_pca_cardio.png` | PCA projection of the K-Medoids clustering result |
| `kmedoids_profiles.png` | Cluster profile comparison plots |

## Dataset

- **Source:** Kaggle — Cardiovascular Disease Dataset
- **Domain:** Healthcare
- **Size:** 1,200 patients, 12 features
- **Features:** `age`, `gender`, `height`, `weight`, `ap_hi` (systolic BP), `ap_lo` (diastolic BP), `cholesterol`, `gluc` (glucose), `smoke`, `alco` (alcohol), `active` (physical activity), `cardio` (target — presence of cardiovascular disease)
- **Class balance:** Nearly balanced — ~50.6% negative vs ~49.4% positive for `cardio`

## Notebook Structure

### `Inital_EDA.ipynb`
Explores the raw dataset before any cleaning:
- Load & inspect (1,200 rows × 12 columns, no nulls, all numeric)
- Missing values check
- Descriptive statistics — reveals `age` is stored in **days**, and blood pressure columns contain physically impossible values (e.g. negative or extreme `ap_hi`/`ap_lo`)
- Target variable distribution (`cardio`) — near-perfect class balance
- Age distribution (days vs. converted years)
- Blood pressure outlier detection
- Categorical feature distributions (gender, cholesterol, glucose)
- Height & weight distributions
- Correlation heatmap on raw data
- Summary table linking each finding to the preprocessing action it motivates

### `Data_Mining_Project.ipynb`

**Section 1 — Introduction:** dataset description and project goals.

**Section 2 — Data Preprocessing:**
- Convert `age` from days to years
- Detect and remove medically impossible outliers (blood pressure, weight)
- Feature engineering: add `BMI` column
- Encode categorical features (`gender` remapped to 0/1; `cholesterol`/`gluc` treated as ordinal)
- Standard scaling for distance-based algorithms

**Section 3 — Exploratory Data Analysis & Visualization** (on cleaned data), including:
1. Age distribution by disease status
2. Correlation heatmap
3. Cholesterol levels by disease status
4. Blood pressure distribution by disease status
5. Lifestyle factors & gender breakdown
6. BMI distribution by disease status

**Section 4 — Genetic Algorithm: Feature Subset Selection**
- Searches for the smallest, most predictive subset of features for classifying `cardio`
- Includes fitness function, genetic operators (selection, crossover, mutation), a baseline (all features) for comparison, and a fitness evolution plot

**Section 5 — K-Medoids (PAM) Clustering**
- Chosen over K-Means for its robustness to outliers and interpretability (medoids are real patients)
- Optimal *k* selection via Elbow method + Silhouette score
- PCA visualization of clusters
- Cluster profile table and clinical interpretation (e.g. "Hypertensive", "Obese", "High-Risk" segments derived from the data)

**Section 6 — Hierarchical Clustering**
- Agglomerative clustering with dendrograms compared across multiple linkage methods

**Section 7 — Fuzzy Inference System**
- A rule-based fuzzy system for cardiovascular risk assessment

**Section 7 (System Integration) — Unified Pipeline**
- Combines preprocessing (age conversion, BMI, gender encoding, scaling), K-Medoids cluster assignment, and the fuzzy inference system into a single end-to-end function

## Requirements

```
pandas
numpy
scipy
matplotlib
seaborn
scikit-learn
scikit-learn-extra
scikit-fuzzy
```

Install `scikit-learn-extra` separately for K-Medoids support:
```bash
pip install scikit-learn-extra
```

## Usage

1. Install dependencies:
   ```bash
   pip install pandas numpy scipy matplotlib seaborn scikit-learn scikit-learn-extra scikit-fuzzy
   ```
2. Run the initial exploration first (optional, for raw-data context):
   ```bash
   jupyter notebook Inital_EDA.ipynb
   ```
3. Run the main project notebook end-to-end:
   ```bash
   jupyter notebook Data_Mining_Project.ipynb
   ```
   This regenerates the cleaned/scaled datasets in `datasets/` and the clustering plots (`kmedoids_*.png`).
