# Hematological Risk Classification MVP

**Thesis:** AN ENHANCEMENT OF DECISION TREE ALGORITHM THROUGH ENTROPY-BASED FEATURE OPTIMIZATION APPLIED IN HEMATOLOGICAL RISK CLASSIFICATION

This is a presentation-ready Python MVP that follows the supplied thesis flowchart:

`Hematological Dataset → Data Processing → Entropy Computation → Feature Optimization → Decision Tree Construction → Classification & Evaluation → Output`

## What the MVP demonstrates

1. **Input** — CBC/hematological features: Hemoglobin (HGB), WBC, RBC, Platelets (PLT), MCV, MCH, MCHC.
2. **Data Processing** — numeric conversion, missing-value removal, duplicate removal, and dataset preview.
3. **Entropy Computation** — explicit Shannon entropy calculation.
4. **Information Gain** — each candidate feature is scored using entropy reduction after quantile discretization.
5. **Feature Optimization** — redundant/low-gain features are filtered and the top features are selected.
6. **Decision Tree Construction** — an entropy-criterion Decision Tree is trained using only selected features.
7. **Comparison** — baseline Decision Tree using all features is compared with the optimized tree.
8. **Classification & Evaluation** — accuracy, weighted precision/recall/F1, class distribution, and confusion matrix.
9. **Prediction Demo** — enter a new CBC record and receive the predicted dataset class plus model probability.
10. **Matplotlib UI** — charts are embedded directly into a Tkinter desktop interface.

## Dataset used for the reference implementation

A public **Anemia Types Classification** dataset contains CBC variables including HGB, PLT, WBC, RBC, MCV, MCH, MCHC, PDW and PCT and a `Diagnosis` label. Kaggle describes it as CBC data labeled with anemia type and lists an Apache 2.0 license. See:

- Kaggle dataset: https://www.kaggle.com/datasets/ehababoelnaga/anemia-types-classification
- GitHub CSV mirror used by the download helper: https://github.com/Nader-ezeldin/anemia-classification/blob/main/diagnosed_cbc_data_v4.csv

The GitHub mirror is used only as a convenient downloadable CSV source. Verify the dataset license/provenance before formal thesis publication.

### Important distinction for your defense

The public reference dataset is primarily a **diagnosis/anemia classification dataset**, not a clinically validated "Low/Moderate/High risk" label set. The MVP therefore treats `Diagnosis` as the machine-learning target. The UI's Low/Moderate/High grouping is only a **presentation/demo mapping** in `app/config.py`; it is not a medical severity standard and should not be claimed as clinically validated.

The included `sample_hematology.csv` is synthetic and is only a fallback so the application can run offline immediately.

## Installation

### Windows

1. Install Python 3.10+.
2. Open PowerShell in this project folder.
3. Create a virtual environment:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
```

4. Install dependencies:

```powershell
pip install -r requirements.txt
```

5. Run:

```powershell
python run.py
```

If PowerShell blocks activation, run the project without activation using `.venv\Scripts\python.exe run.py` after installation.

## Getting the public dataset

With internet access:

```powershell
python download_dataset.py
```

Then launch the app and click **Load CSV Dataset**. Select:

`data/diagnosed_cbc_data_v4.csv`

The loader keeps the thesis-relevant CBC features and the `Diagnosis` target.

## Presentation flow for tomorrow

### 1. Dashboard
Show the number of records, classes, baseline accuracy, optimized accuracy, and selected feature count.

### 2. Data Processing
Explain:
- missing-value handling
- duplicate removal
- numeric conversion
- cleaned dataset preview

### 3. Entropy / Features
Explain the mathematical idea:

`Entropy(S) = -Σ pᵢ log₂(pᵢ)`

and:

`Information Gain = Entropy(parent) - Σ(weighted child entropy)`

The chart ranks HGB/WBC/RBC/PLT/MCV/MCH/MCHC by information gain. Features with weak gain are excluded from the optimized tree.

### 4. Decision Tree
Show that the final tree uses the selected features and uses `criterion='entropy'`.

### 5. Evaluation
Show baseline vs optimized accuracy and the confusion matrix. Avoid claiming that the model is clinically accurate or ready for diagnosis.

### 6. Classify New
Enter sample CBC values and show the predicted dataset class and model confidence.

## Suggested thesis mapping

| Flowchart | MVP module | Demonstration |
|---|---|---|
| Input | `data/` + CSV loader | CBC dataset |
| Data Processing | `app/data_processing.py` | Cleaning |
| Entropy Computation | `app/entropy_optimizer.py` | Entropy + information gain |
| Feature Optimization | `app/entropy_optimizer.py` | Feature ranking/selection |
| Decision Tree Construction | `app/model.py` | Entropy decision tree |
| Classification & Evaluation | `app/evaluation.py` + GUI | Metrics/confusion matrix |
| Output | GUI dashboard | Classification report + prediction |

## Project structure

```text
hematological-risk-mvp/
├── app/
│   ├── config.py
│   ├── data_processing.py
│   ├── dataset.py
│   ├── entropy_optimizer.py
│   ├── evaluation.py
│   ├── gui.py
│   └── model.py
├── data/
│   ├── README.md
│   └── sample_hematology.csv
├── docs/
│   └── thesis_demo_notes.md
├── models/
├── download_dataset.py
├── requirements.txt
├── run.py
└── README.md
```

## Notes / limitations

- This is an **MVP for academic demonstration**, not a clinical decision-support product.
- Model probability is a tree's estimated class probability, not a calibrated medical confidence score.
- The risk grouping in the UI is a demo mapping and must not be presented as a medical risk guideline.
- For your actual thesis evaluation, use your approved dataset, document preprocessing, train/test split, feature-selection threshold, and evaluation protocol.
- For reproducibility, keep the random seed at 42 unless your methodology specifies otherwise.
