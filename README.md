# Pharma Drug Analysis

A full data analysis project on a pharmaceutical drug dataset containing 10,000 records across 20 features. The project covers exploratory data analysis (EDA), machine learning classification, and an interactive Power BI dashboard.

---

## Dataset

- **File:** `pharma_realistic_10000.csv`
- **Rows:** 10,000
- **Columns:** 20
- **Source:** Kaggle

| Column | Description |
|--------|-------------|
| `active_ingredient` | Active chemical compound |
| `brand_name` | Commercial drug name |
| `manufacturer` | Pharmaceutical company |
| `therapeutic_group` | Drug category (e.g. Antibiotic, Analgesic) |
| `pharmacological_class` | Mechanism of action |
| `drug_type` | Small molecule or Biologic |
| `dosage_form` | Tablet, Capsule, Syrup, Injection, Inhaler |
| `route` | Oral, IV, Subcutaneous, Inhalation |
| `indication_category` | Disease category |
| `pregnancy_category` | Safety rating A / B / C / D / X |
| `otc_or_rx` | Over-the-counter or Prescription |
| `food_interaction` | 1 = has food interaction |
| `alcohol_interaction` | 1 = has alcohol interaction |
| `is_combination_drug` | 1 = combination drug |
| `num_ingredients` | Number of active ingredients |

---

## Project Structure

```
Pharma-Drug-Analysis/
│
├── pharma_realistic_10000.csv   # Raw dataset
├── pharma_encoded.csv           # Encoded dataset for ML
│
├── eda/
│   └── therapeutic_group_EDA.py # Univariate analysis
│
├── ml/
│   └── rx_classification.py     # RX vs OTC classifier
│
├── dashboard/
│   └── pharma_dashboard.pbix    # Power BI dashboard file
│
└── README.md
```

---

## Part 1 — Exploratory Data Analysis (EDA)

### Key Findings

- **Zero missing values** and **zero duplicate rows** — dataset is clean out of the box
- **Therapeutic group:** Antibiotic (2,034) and Antihypertensive (2,005) are the most common, together accounting for ~40% of all drugs
- **Prescription drugs (RX):** 72.8% of all drugs require a prescription
- **Alcohol interaction:** 66.6% of drugs have alcohol interaction — the highest risk flag in the dataset
- **Pregnancy Category X** (contraindicated): 613 drugs, or 6.1% of the dataset
- **Top manufacturer:** Square Pharmaceuticals with 22.4% market share
- **Most common dosage form:** Tablet (48.5%)

### Run EDA

**Requirements:**
```bash
pip install pandas matplotlib seaborn
```

**Steps:**
1. Place `pharma_realistic_10000.csv` in your working directory
2. Run the analysis script:
```bash
python eda/therapeutic_group_EDA.py
```
3. Output: a 3-panel chart saved as `therapeutic_group_EDA.png`
   - Panel 1: Horizontal bar chart — drug count per therapeutic group
   - Panel 2: Donut chart — proportion breakdown
   - Panel 3: Pareto chart — cumulative percentage with 80% reference line

---

## Part 2 — Machine Learning: RX vs OTC Classification

Predict whether a drug is a **Prescription (RX)** or **Over-the-counter (OTC)** drug using two classifiers.

### Models Used

| Model | Description |
|-------|-------------|
| Random Forest | Ensemble of decision trees, handles non-linear patterns well |
| Logistic Regression | Linear baseline classifier |

### Feature Engineering

Before modelling, categorical columns were encoded:

| Method | Columns |
|--------|---------|
| Label Encoding | `pregnancy_category`, `otc_or_rx`, `drug_type` |
| One-Hot Encoding | `therapeutic_group`, `dosage_form`, `route`, `indication_category`, `manufacturer` |

### Run the Model

**Requirements:**
```bash
pip install pandas scikit-learn matplotlib numpy
```

**Step 1 — Generate encoded dataset:**
```bash
python feature_engineering.py
```
This produces `pharma_encoded.csv`.

**Step 2 — Train and evaluate models:**
```bash
python ml/rx_classification.py
```

**Step 3 — Output:**
- Console: Accuracy, F1 Score, and full Classification Report for both models
- Chart saved as `rx_classification_results.png` with 3 panels:
  - Panel 1: Accuracy & F1 comparison between models
  - Panel 2: Confusion matrix (Random Forest)
  - Panel 3: Top 15 feature importances

### Expected Results

| Model | Accuracy | F1 Score |
|-------|----------|----------|
| Random Forest | ~90–95% | ~0.90+ |
| Logistic Regression | ~80–85% | ~0.85+ |

---

## Part 3 — Power BI Dashboard

An interactive dashboard built in Power BI Desktop with the following visuals:

| Visual | Description |
|--------|-------------|
| KPI Cards | Total drugs, RX count, alcohol interaction %, X-category count |
| Bar Chart | Drug count by therapeutic group |
| Donut Charts | RX vs OTC split, manufacturer market share |
| Column Charts | Pregnancy category distribution, dosage form breakdown |
| Table | Indication category with interaction rates |
| Slicers | Filter by `otc_or_rx`, `therapeutic_group`, `manufacturer` |

**To open:**
1. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free)
2. Open `dashboard/pharma_dashboard.pbix`
3. Use the slicers on the left to filter all visuals interactively

---

## Requirements

### Python

```
pandas
numpy
matplotlib
seaborn
scikit-learn
```

Install all at once:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

### Python Version
Tested on Python 3.9+

---

## Author

**Jill**
- GitHub: [@595596295](https://github.com/595596295)

---

## License

This project is for educational and portfolio purposes.
Dataset sourced from Kaggle.
