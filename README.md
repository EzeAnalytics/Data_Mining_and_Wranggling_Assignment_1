# Post-Pandemic Remote Work Health Impact — Data Analysis

An exploratory data analysis of the **Post-Pandemic Remote Work Health Impact 2025** survey dataset, examining how work arrangement (remote, hybrid, onsite) relates to burnout, mental health and working hours.

Prepared for the **Advent 2026** assignment, *Data Mining and Wrangling*, Year 2 Semester 1 — Bachelor of Science in Data Science and Analytics.

---

## Table of Contents

- [Overview](#overview)
- [Dataset](#dataset)
- [Requirements](#requirements)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Analysis Workflow](#analysis-workflow)
- [Key Findings](#key-findings)
- [Limitations](#limitations)
- [Team](#team)

---

## Overview

The notebook works through a full mini data-analysis pipeline:

1. Understand the dataset and its variables
2. Clean the data (missing values, duplicates, text formatting, invalid numbers)
3. Summarize the data with descriptive statistics
4. Visualize each variable and interpret the result
5. Explore relationships between work arrangement, burnout, mental health, age, working hours and region
6. Report overall findings and limitations

The guiding question is: **do different work arrangements show different burnout and mental-health patterns?**

---

## Dataset

- **Name:** Post-Pandemic Remote Work Health Impact 2025
- **Source:** [Kaggle — Remote Work Health Impact Survey 2025](https://www.kaggle.com/datasets/pratyushpuri/remote-work-health-impact-survey-2025)
- **Collected:** June 2025
- **Size:** 3,157 rows (one row per survey respondent), 10 original columns
- **Variable types:** 2 numerical variables (`Age`, `Hours_Per_Week`) and 8 categorical/date variables (`Gender`, `Region`, `Industry`, `Job_Role`, `Work_Arrangement`, `Mental_Health_Status`, `Burnout_Level`, `Survey_Date`)

Expected input file (not included in this repository — download it from Kaggle and place it in the project root):

```
post_pandemic_remote_work_health_impact_2025-selected-columns.csv
```

---

## Requirements

- Python 3.9+
- Jupyter Notebook or JupyterLab

Python packages:

```
numpy
pandas
matplotlib
seaborn
scipy
```

Install them with:

```bash
pip install numpy pandas matplotlib seaborn scipy
```

---

## Getting Started

1. Clone or download this repository.
2. Download the dataset CSV from the Kaggle link above and place it in the same folder as the notebook, named exactly:
   `post_pandemic_remote_work_health_impact_2025-selected-columns.csv`
3. Launch Jupyter:

   ```bash
   jupyter notebook
   ```

4. Open `post_pandemic_remote_work_health_impac.ipynb` and run all cells from top to bottom.

---

## Project Structure

```
.
├── post_pandemic_remote_work_health_impac.ipynb   # Main analysis notebook
├── post_pandemic_remote_work_health_impact_2025-selected-columns.csv   # Dataset (not included, see above)
└── README.md
```

---

## Analysis Workflow

### 1. Data cleaning

- **Missing values:** `Mental_Health_Status` was the only column with missing responses (799 of them). Rather than dropping these rows, they were relabelled as `Unknown / Not Reported` to preserve the other information in each response.
- **Duplicates:** checked and none were found.
- **Text formatting:** categorical columns were stripped of leading/trailing whitespace to prevent values such as `Remote` and ` Remote` being treated as different categories.
- **Data types:** `Survey_Date` was converted from text to a proper date type.
- **Range checks:** `Age` and `Hours_Per_Week` were checked for impossible values (e.g. negative hours, ages outside 18–100); none were found.
- **Derived columns:** `Age_Group` (18-29, 30-39, 40-49, 50-59, 60+) and `Hours_Group` (≤39, 40-49, 50-59, 60+) were created to support grouped analysis.

### 2. Descriptive statistics

Summary statistics (mean, median, min, max, range) were calculated for `Age` and `Hours_Per_Week`, and value counts were produced for every categorical variable.

### 3. Visualization

Each variable was visualized individually (histograms and bar charts for demographics, work arrangement, mental health and burnout level), followed by an interpretation of what the chart shows.

### 4. Relationship analysis

Six relationships were examined using cross-tabulations, grouped averages, a correlation coefficient and a scatter plot:

| # | Relationship | Method |
|---|--------------|--------|
| 1 | Work arrangement × Burnout level | Crosstab (counts & row percentages), bar chart |
| 2 | Work arrangement × Mental health status | Crosstab (row percentages), bar chart |
| 3 | Age group × Burnout level | Crosstab (row percentages), bar chart |
| 4 | Working hours group × Burnout level | Crosstab, grouped averages, bar chart |
| 5 | Age × Working hours | Pearson correlation, scatter plot |
| 6 | Region × Working hours | Grouped averages, bar chart |

All relationships are treated as **associations**, not evidence of cause and effect.

---

## Key Findings

- **Missing data:** the main data-quality issue was 799 missing `Mental_Health_Status` values, addressed by labelling rather than deleting.
- **Burnout is common:** medium burnout is the largest group overall, with high burnout also substantial.
- **Work arrangement relates most clearly to burnout:** remote workers show the highest proportion of high burnout; onsite workers show the highest proportion of low burnout. This is the strongest pattern in the dataset.
- **Working hours don't separate burnout groups well:** average weekly hours are similar across low, medium and high burnout respondents.
- **Age and working hours are essentially unrelated:** the Pearson correlation is close to zero.
- **Region and industry show only small differences** in average working hours.

---

## Limitations

- **Self-reported survey data**, which may include reporting bias or inaccuracies.
- **Limited collection window** (June 2025), so findings may not generalize beyond that period.
- **Associations only** — none of the relationships explored demonstrate causation.
- **Large "Unknown / Not Reported" group** in `Mental_Health_Status` limits how confidently mental-health results can be interpreted.
- **Unequal group sizes** across regions, industries, job roles and work arrangements mean percentage comparisons are more reliable than raw counts.

---

## Team

**Group Members** — Bachelor of Science in Data Science and Analytics, Year 2, Semester 1

| # | Name | Registration No. |
|---|------|------------------|
| 1 | Ajak Deng Garang Deng | M25B38/031 |
| 2 | Aponi Allan Daniel | M25B38/029 |
| 3 | Ezekiel Bulima | M25B38/028 |
