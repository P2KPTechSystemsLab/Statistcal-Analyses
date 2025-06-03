
# 📘 Soil Depth Effect Analysis: Transformations, Treatment, Time & Interaction

This repository provides Python code for evaluating how soil **pH varies with depth** across multiple **treatments**, **time points**, and their **interactions**, while also testing and applying **transformations** to meet statistical assumptions. The analysis uses a combination of **model diagnostics**, **parametric (Welch’s t-tests)**, and **non-parametric (Mann–Whitney U tests)**.

---

## 📁 Contents

### 1. **Data Structure**

The dataset is structured as a long-format DataFrame with the following variables:

* **pH**: Response variable
* **Depth**: Soil depth (categorical)
* **Treatment**: One of:

  * `Control`
  * `Root Mulched`
  * `Root Mixed`
  * `Leaf Mulched`
  * `Leaf Mixed`
* **Day**: Time points, 

## 🔄 2. Data Transformation & Model Diagnostics

Before formal analysis, the distribution of residuals is assessed via:

### 🧪 Transformations Tried

| Transformation | Syntax                   |
| -------------- | ------------------------ |
| Log            | `np.log(df['pH'])`       |
| Square Root    | `np.sqrt(df['pH'])`      |
| Box-Cox        | `stats.boxcox(df['pH'])` |

### 📊 Residual Diagnostic Plots

A helper function `check_model()` provides:

* Histogram + KDE of residuals
* Q–Q Plot
* Shapiro–Wilk test result

```python
def check_model(model, title):
    ...
    print(f"{title} - Shapiro-Wilk p = {p:.4f}")
```

**Goal**: improves residual normality before model fitting.

---

## 🔍 3. Analytical Breakdown

### ✅ A. Depth Effect Across Treatments

* **Objective**: Compare treatments at each depth
* **Stats**:

  * Welch’s t-test
  * Mann–Whitney U test
* **Approach**:

  * Loop over depths
  * Test all treatment pairs per depth

---

### ✅ B. Depth Effect Across Time

* **Objective**: Compare time points at each depth per treatment
* **Stats**:

  * Welch’s t-test
  * Mann–Whitney U test
* **Approach**:

  * Loop over treatments
  * For each, test all day-pairs across depths

---

### ✅ C. Depth × Treatment × Time Interaction

* **Objective**: Evaluate if treatment effects on pH vary jointly across depth and time
* **Stats**:

  * Welch’s t-test
  * Mann–Whitney U test
* **Approach**:

  * For each day, test all treatment pairs at each depth

---

## 🧪 Statistical Highlights

| Test Type          | Description                                               |
| ------------------ | --------------------------------------------------------- |
| **Welch’s t-test** | For comparing means without assuming equal variances      |
| **Mann–Whitney U** | Non-parametric test comparing medians/distribution shapes |

* Color-coded significance in summary tables (e.g., red for `p < 0.05`).
* Outputs printed and optionally exportable via `pandas`.

---

## 🖥️ Code Execution

### 📦 Requirements

```bash
pip install numpy pandas scipy statsmodels seaborn matplotlib
```

### 📂 Suggested Workflow (Notebook or Script)

```python
# 1. Run transformation section
# 2. Run model diagnostics
# 3. Run depth effect across treatment
# 4. Run depth effect across time
# 5. Run interaction: depth × treatment × time
```

---

## 📊 Outputs

* **Summary tables**: Pairwise comparisons at each level
* **Visuals**:

  * Residual histograms
  * Q–Q plots
* **Statistical summaries**:

  * P-values
  * Test statistics
  * Optional CSV/Excel export

---
## 📌 Notes

* Code avoids redundancy: logic is generalized with clean loops and mappings.
* Transformations are modular and reusable.
* Diagnostic tools ensure assumptions are verified before inference.
* Designed for scalability across other soil parameters (not just pH).

---

## 📁 Folder Structure Suggestion (Optional)

```
soil-depth-analysis/
├── data/
│   └── pH_raw_data.csv
├── notebooks/
│   └── pH_analysis.ipynb
├── src/
│   ├── transformations.py
│   ├── stats_tests.py
│   └── visualization.py
├── README.md
└── requirements.txt
```

## 📥 Optional Deliverables

✅ `.md` or `.pdf` version of this README
✅ 
✅ Zip folder of organized code and outputs

---


