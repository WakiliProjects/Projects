# Global Health & Wellbeing: Life Expectancy Analysis & Prediction

Predicted life expectancy across 193 countries within a 2-year margin at 88% accuracy (R²), showcasing that education and healthcare access are stronger drivers of longer lifespans than a country's wealth.

---

## 📌 Introduction

This project involved an open-ended task that required formulating our own analytical questions, conducting in-depth analysis, and documenting every step of the process. The goal was to combine technical machine learning techniques with thoughtful interpretation to uncover meaningful insights from global health data.

Key objectives included:
- Formulating analytical questions around life expectancy and its determinants
- Performing in-depth exploration and analysis across 193 countries (2000–2015)
- Explaining methodologies and results clearly
- Proposing potential improvements for future work

---

## 🔎 Analysis

Our analysis followed a structured approach:
1. **Data Preparation:** Cleaned and preprocessed the WHO Life Expectancy dataset to ensure accuracy and consistency.
2. **Model Implementation:** Applied a linear regression model first, then tested polynomial regression to improve performance.
3. **Training & Testing Split:** Split the data (80/20) into training and testing sets to avoid overfitting and ensure generalisability.
4. **Visualisation:** Used multiple techniques — including elbow plots, histograms, correlation charts, and scatter plots — to uncover patterns and support model evaluation.

---

## 🧭 Exploration

The exploration process involved several steps:

- **Library Import & Initial Exploration:** Loaded relevant libraries and reviewed the dataset structure.
- **Data Cleaning:** Removed missing/null values to maintain data integrity.
- **Categorical Encoding:** Converted categorical variables (Country, Status) into numerical formats using **Ordinal Encoding** to ensure model compatibility.
- **Correlation Analysis:** Calculated correlations between all features and life expectancy, identifying Schooling and Income composition of resources as the strongest positive drivers.
- **Visualisation:**
  - Scatter plots for bivariate relationships (Alcohol vs Life Expectancy, GDP vs Life Expectancy)
  - Histograms for distribution checks
  - Bivariate heatmap to examine the relationship between GDP and life expectancy
  - Correlation bar chart for feature selection
- **Clustering:** Applied **K-Means clustering** (k=2) to group countries by alcohol consumption and life expectancy, validated with an elbow plot.
- **Model Training:**
  - Implemented a **linear regression model** as the baseline
  - Conducted parameter tuning with **polynomial regression** (degree 3) to capture non-linear patterns
- **Model Evaluation:** Measured performance using:
  - **Mean Absolute Error (MAE)**
  - **Mean Squared Error (MSE)**
  - **R² (Coefficient of Determination)**

---

## 📊 Results

| Model | R² | MAE (years) |
|---|---|---|
| Linear Regression | 0.75 | 2.94 |
| Polynomial Regression (degree 3) | 0.88 | 2.00 |

---

## 📋 Conclusion

This project demonstrated how careful data cleaning, thoughtful model selection, and robust evaluation metrics can lead to meaningful insights from global health data.

Key takeaways:
- **Education and healthcare access** are stronger drivers of longer lifespans than a country's wealth alone.
- **Adult Mortality and HIV/AIDS** have the strongest negative impact on life expectancy.
- The polynomial regression model improved prediction from 75% to 88% (R²) by capturing non-linear relationships, predicting life expectancy within ~2 years of the actual value.
- **GDP alone is not enough** — how money is spent on healthcare and education matters more than raw economic output.

---

## 📈 Future Improvements

Potential enhancements include:
- Experimenting with additional machine learning models (e.g., decision trees, random forests)
- Performing cross-validation for more robust model evaluation
- Refining data visualisations for greater clarity
- Automating data cleaning steps for reproducibility
- Exploring feature engineering (e.g., log-transforming skewed features like GDP)

---

## 🛠️ Tools & Libraries

**Python:** pandas, scikit-learn, matplotlib, seaborn, Jupyter Notebook

## 🚀 How to Run

1. Ensure Python 3.x is installed
2. Install dependencies: `pip install pandas scikit-learn matplotlib seaborn`
3. Open `Life_Expectancy_Analysis.ipynb` in Jupyter Notebook or VS Code
4. Run all cells sequentially
4. Run all cells sequentially
