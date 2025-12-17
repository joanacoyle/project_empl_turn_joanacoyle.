# Employee Turnover Analytics (HR Attrition) — Joana Coyle

## Overview
This project analyzes employee turnover (attrition) using an HR dataset and builds predictive machine-learning models to identify employees at risk of leaving. The workflow combines data quality checks, exploratory data analysis (EDA), clustering, class-imbalance handling, supervised modeling, and business-focused retention strategies.

The project includes:
- Data quality validation and memory optimization
- Exploratory Data Analysis (EDA)
- K-Means clustering of employees who left
- Class imbalance handling using SMOTE
- Model training and evaluation (Logistic Regression, Random Forest, Gradient Boosting)
- ROC/AUC comparison and confusion-matrix analysis
- Risk zoning (Safe → High-Risk) with targeted retention recommendations

---

## What I Did (High Level)

### 1) Data Quality Checks
- Loaded the dataset and reviewed structure, shape, and duplicates
- Verified there were no missing values
- Identified numeric, binary, and categorical features
- Optimized memory usage by downcasting numeric columns
- Preserved an untouched copy of the original dataset

**Key observations:**
- Satisfaction ranges widely (0.09–1.00)
- Monthly workload varies significantly (~96–310 hours)
- Employees typically work on 2–7 projects
- Tenure ranges from 2–10 years

---

### 2) Exploratory Data Analysis (EDA)

**Correlation Analysis**
- Generated a correlation heatmap of numeric features
- Most relationships are weak to moderate
- Stronger correlations observed between:
  - number_project and average_montly_hours
  - number_project and last_evaluation
- Satisfaction shows a weak negative relationship with workload and tenure

**Distribution Analysis**
- Satisfaction levels show two main groups: satisfied and dissatisfied employees
- Evaluation scores cluster around mid-to-high values
- Monthly hours show two workload peaks (~150 and ~250 hours)

**Turnover Patterns**
- Employees with only 2 projects or 6–7 projects leave more often
- Most turnover occurs around 3–5 years of tenure
- Low-salary employees leave more frequently
- Employees with work accidents tend to stay more often

---

### 3) Clustering (Employees Who Left)
- Filtered employees who left the company
- Applied K-Means clustering (k=3) using:
  - satisfaction_level
  - last_evaluation

**Cluster insights:**
- High satisfaction + high evaluation → strong performers who still left
- Low satisfaction + high evaluation → capable but disengaged employees
- Medium satisfaction + medium evaluation → average employees who left

This shows that attrition is not driven by poor performance alone.

---

### 4) Preprocessing & Class Imbalance
- One-hot encoded categorical variables (department, salary)
- Performed a stratified 80/20 train-test split
- Addressed class imbalance using SMOTE on the training data
- Ensured all features were numeric and model-ready

---

### 5) Modeling & Evaluation

**Models trained**
- Logistic Regression (baseline + tuned)
- Random Forest (baseline + tuned)
- Gradient Boosting (tuned)

**Evaluation methods**
- 5-fold Stratified Cross-Validation
- Classification reports
- Confusion matrices
- ROC curves and AUC scores

**Key results**
- Logistic Regression provided a solid baseline (~79–80% accuracy)
- Gradient Boosting achieved very strong performance (AUC ≈ 0.987)
- Random Forest was the best overall model (AUC ≈ 0.995)

---

### 6) Best Model & Metric Choice
- Random Forest selected as the final model due to:
  - Highest ROC/AUC
  - Lowest false negatives
  - Excellent balance between precision and recall

**Why Recall matters**
- In employee attrition, missing a true leaver is more costly than a false alarm
- Recall ensures high-risk employees are identified early for intervention

---

### 7) Risk Zones & Retention Strategies

Employees were categorized using predicted probabilities:

- **Safe (Green):** < 20%
- **Low-Risk (Yellow):** 20–60%
- **Medium-Risk (Orange):** 60–90%
- **High-Risk (Red):** > 90%

**Findings**
- Most employees fall into the Safe zone
- A smaller but critical High-Risk group is almost certain to leave

**Key drivers (High-Risk group)**
- Satisfaction level
- Time spent at company
- Number of projects
- Average monthly hours

**Retention recommendations**
- Focus interventions around the 3–4 year tenure mark
- Balance workload to ~3–5 projects
- Provide career growth, promotions, and learning opportunities
- Monitor Medium-Risk employees closely
- Maintain culture and recognition for Safe employees

---

## Tools & Libraries Used
- Python
- pandas, numpy
- matplotlib, seaborn
- scikit-learn (modeling, metrics, GridSearchCV, ROC/AUC)
- imbalanced-learn (SMOTE)

---

## What I Learned
- How to perform structured data quality validation
- How to uncover turnover drivers using EDA
- How to handle class imbalance correctly with SMOTE
- How to compare models using ROC/AUC and confusion matrices
- How to translate model outputs into actionable business insights


