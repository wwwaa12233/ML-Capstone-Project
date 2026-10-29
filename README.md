# California Housing — Machine Learning Capstone Project

This repository implements the pipeline described in the provided *Machine Learning Capstone Project Manual* using the supplied `housing.csv` dataset.

## Dataset
- **Rows / columns:** 20,640 / 10
- **Target for regression:** `median_house_value`
- **Missing values:** 207 missing entries, all in `total_bedrooms`; handled using median imputation in modeling pipelines.
- **Categorical feature:** `ocean_proximity` (one-hot encoded).

## Tasks
1. **Regression — Linear Regression:** predicts continuous `median_house_value`; evaluated with MAE, MSE, RMSE, and R².
2. **Classification — Logistic Regression:** defines class 1 as `median_house_value` greater than the dataset median ($179,700); class 0 otherwise. This is a derived teaching label because the original dataset does not contain a binary classification target. Evaluated with accuracy, confusion matrix, precision, recall, and F1.
3. **Clustering — K-Means:** uses predictor features only (excludes `median_house_value`), checks K=2 through K=8 using inertia and sampled silhouette score, and visualizes geographic coordinates by cluster.

## Main results
| Task | Model / setting | Result |
|---|---|---:|
| Regression | Linear Regression | RMSE = $70,059.19; R² = 0.625 |
| Classification | Logistic Regression | Accuracy = 0.838; F1 (class 1) = 0.839 |
| Clustering | K-Means, K=2 | Sampled silhouette = 0.408 |

These results are from a fixed 80/20 test split (`random_state=42`). Clustering silhouette is calculated on a reproducible sample of 2,500 rows to reduce computation time. K is selected by the highest sampled silhouette among the tested candidates; use the elbow plot as additional context rather than treating it as an exact rule.

## Repository structure
```text
ML-Capstone-Project/
├── data/housing.csv
├── notebooks/California_Housing_Capstone.ipynb
├── results/                  # metrics, plots, clean CSV, summaries
├── run_project.py            # complete reproducible pipeline
├── README.md
└── project_report.pdf
```

## Run locally
Python 3.10+ recommended.
```bash
python -m venv .venv
# Windows PowerShell: .venv\Scripts\Activate.ps1
# macOS/Linux: source .venv/bin/activate
pip install pandas numpy scikit-learn matplotlib seaborn jupyter
python run_project.py
```

## Run in Google Colab
1. Upload and extract the project ZIP in Colab, or upload the CSV and script into a working folder.
2. Open `notebooks/California_Housing_Capstone.ipynb` and set the working directory to the project folder.
3. Run all cells. The notebook executes `run_project.py` and displays saved results.
4. Copy the shareable Colab notebook URL into the PDF report before submitting; enable access for the grading team.

## Submission checklist
- [ ] Commit `data/`, `notebooks/`, `results/`, `run_project.py`, `README.md`, and `project_report.pdf` to a **public** GitHub repository named `ML-Capstone-Project`.
- [ ] Open the notebook in Google Colab and add the shareable notebook link to the PDF (placeholder is included).
- [ ] Verify the repository and notebook sharing permissions before submitting the GitHub URL.

## Limitations and interpretation
- The dataset target is capped at $500,001 for some records; this can limit regression accuracy at the upper end.
- The classification target is derived from the house-value median, so it demonstrates the classification workflow rather than a naturally occurring independent label.
- K-Means clusters are mathematical groupings in scaled feature space; geographic plot colors should not be interpreted as official housing regions.
