# diabetes-analysis-statistical-inference

# Technical Report: Statistical Inference and Analysis on Diabetes Dataset

## Project Title:
**Statistical Inference and Predictive Analysis on Diabetes Risk Factors**

## Course:
**DSAI 307: Statistical Inference**

---

## 1. Introduction

Diabetes mellitus is a chronic metabolic disorder that disrupts normal glucose metabolism, posing significant public health challenges globally. Early detection and risk profiling are vital for managing and preventing diabetes progression. This project, as part of the DSAI 307 course, applies a full-stack statistical inference approach on a real-world diabetes dataset. The goal is to identify key health indicators contributing to diabetes onset using exploratory analysis, hypothesis testing, and confidence interval simulations. Techniques employed span from basic descriptive statistics to inferential modeling and simulation-based validation.

---

## 2. Dataset Overview

### 2.1 Source
- **Origin**: National Institute of Diabetes and Digestive and Kidney Diseases (NIDDK)
- **Kaggle Link**: [Diabetes Dataset](https://www.kaggle.com/datasets/hasibur013/diabetes-dataset)

### 2.2 Summary
- **Samples**: 768
- **Population**: Adult female patients of Pima Indian heritage
- **Target Variable**: Outcome (1 = Diabetic, 0 = Non-Diabetic)

### 2.3 Features
| Feature                   | Description                                                               |
|---------------------------|---------------------------------------------------------------------------|
| Pregnancies               | Number of times the patient has been pregnant                             |
| Glucose                   | Plasma glucose concentration (2-hour post-glucose test)                   |
| BloodPressure             | Diastolic blood pressure (mm Hg)                                          |
| SkinThickness             | Triceps skinfold thickness (mm)                                           |
| Insulin                   | 2-hour serum insulin (mu U/ml)                                            |
| BMI                       | Body mass index (kg/m^2)                                                  |
| DiabetesPedigreeFunction  | Genetic predisposition score (family history function)                    |
| Age                       | Age of the patient (in years)                                             |
| Outcome                   | Binary class label: 0 = Non-Diabetic, 1 = Diabetic                        |

---

## 3. Data Preprocessing

### 3.1 Data Loading
- Dataset imported in R using `read.csv()`
- Structure and summary inspected via `str()` and `summary()`

### 3.2 Handling Missing Values
- Columns with implausible zero values: `Glucose`, `BloodPressure`, `SkinThickness`, `Insulin`, `BMI`
- Replaced zeros with `NA`
- Counted NA occurrences with `colSums(is.na())`
- Strategy:
  - Drop rows with minimal NAs (Glucose, BMI)
  - Mean imputation for high-NA columns (SkinThickness, Insulin)

### 3.3 Feature Engineering
- Created `GlucoseGroup` based on median glucose value
- Recoded `Outcome` as a categorical variable

### 3.4 Final Dataset Summary
- No missing values
- Data ready for analysis

---

## 4. Exploratory Data Analysis (EDA)

### 4.1 Central Tendency & Distribution Analysis
- Used `group_by(Outcome)` to calculate means for Glucose, BMI, Age
- Boxplots and bar charts revealed higher average values among diabetic patients

### 4.2 Distributional Insights
- BMI: Right-skewed distribution (mode ~30)
- DPF: Broader spread in diabetics
- Diabetes Rate: 35% positive cases

### 4.3 Bivariate Analysis
- **Pregnancies vs Outcome**: Increasing trend
- **Glucose vs BMI**: Positive linear trend (r = 0.33)
- **Glucose vs Age**: Linear trend with age in both groups

### 4.4 Visualizations
- Boxplots, violin plots, density plots, scatter plots with regression lines, heatmaps
- Annotated insights in all visual outputs

---

## 5. Inferential Statistical Analysis

### 5.1 Hypothesis 1
**Claim**: Glucose levels differ significantly between diabetic and non-diabetic patients
- Test: Two-sample t-test
- Result: p < 0.001
- Conclusion: Reject H0; significant difference exists

### 5.2 Hypothesis 2
**Claim**: BMI levels differ between diabetic and non-diabetic patients
- Test: Two-sample t-test
- Result: p < 0.001
- Conclusion: Reject H0

### 5.3 Manual Validation
- Mean, standard deviation, standard error, t-statistic, and p-value calculated manually
- Compared against critical values from `qt()`

---

## 6. Multivariate & Correlation Analysis

### 6.1 Risk Profiles
- Used `cor()` on all numeric features
- Glucose (r = 0.48) and BMI (r = 0.31) were most correlated with Outcome
- Heatmap confirmed visual clustering around these variables

### 6.2 Custom Analytical Questions
1. **DPF vs Outcome**: Significant difference (p < 0.001)
2. **Age vs BP**: Weak correlation (r ~ 0.24)
3. **Pregnancies vs SkinThickness**: Very weak inverse correlation
4. **Insulin vs Glucose**: Moderate positive correlation (r = 0.33)
5. **Pregnancies vs BMI (Diabetics only)**: Weak negative correlation (r = -0.15)

---

## 7. Simulation Task: Confidence Intervals

### 7.1 Objective
Evaluate CI behavior for Glucose variable under different sample sizes

### 7.2 Method
- CI formula: \[ \bar{x} \pm t_{\alpha/2, df} \cdot \frac{s}{\sqrt{n}} \]
- Repeated sampling with sizes: 10, 15, 100 (with replacement)
- 25 random samples each

### 7.3 Findings
| Sample Size | Coverage Proportion | Average CI Width |
|-------------|---------------------|------------------|
| 10          | ~88%                | Largest          |
| 15          | ~92%                | Moderate         |
| 100         | ~100%               | Smallest         |

- CI width inversely proportional to sample size
- Larger samples yield tighter, more reliable estimates

### 7.4 Visuals
- CI plots for each sample size
- Boxplot comparing CI widths
- Red dashed line = true mean reference

---

## 8. Technical Tools

### Programming Environment
- **Language**: R
- **Platform**: Google Colab (R Kernel)
- **IDE**: RStudio (optional offline validation)

### Libraries Used
- `dplyr`, `ggplot2`, `tidyr`, `reshape2`
- `base` R for manual calculations

---

## 9. Challenges, Limitations, and Assumptions

### 9.1 Challenges
- Zeros encoded as data instead of missing values
- Imbalanced class labels
- Variability in small-sample simulations

### 9.2 Assumptions
- Normal distribution for t-tests and CI
- Imputed means reasonably approximate true missing values
- Homoscedasticity for t-test assumptions (not formally tested)

### 9.3 Limitations
- Female-only Pima Indian cohort limits generalizability
- Limited predictor scope (e.g., no lifestyle variables)

---

## 10. Deliverables

| File Type        | Description                                        |
|------------------|----------------------------------------------------|
| `.ipynb` / `.Rmd`| Full notebook with code and markdown              |
| `report.pdf`     | High-level technical summary report                |
| `slides.pptx`    | Canva slides summarizing insights and visuals     |
| `README.md`      | GitHub documentation                              |

---

## 11. Conclusion

This project demonstrated the use of statistical inference to extract meaningful insights from health-related data. The analysis confirms that high glucose and BMI levels are significantly associated with diabetes onset. Confidence interval simulations validate the importance of sample size in inferential accuracy. The workflow adhered to sound statistical practices and highlighted practical issues in real-world health datasets.

### Future Work
- Incorporate machine learning models (e.g., logistic regression, random forest)
- Expand dataset diversity and include lifestyle predictors
- Use non-parametric or Bayesian methods for deeper inference

---

## 12. References
- UCI Machine Learning Repository: Pima Indians Diabetes Dataset
- Wickham, H., & Grolemund, G. (2017). *R for Data Science*. O’Reilly.
- Knaflic, C. N. (2015). *Storytelling with Data*. Wiley.
- Field standard statistical methods for t-tests, CI estimation, and correlation analysis

---

**End of Report**
