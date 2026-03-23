🩺 Coronary Heart Disease (CHD) Statistical Analysis & Modelling

Tools: R, R Markdown, ggplot2, dplyr, tidyr, MASS

📘 Project Overview

This project investigates key biological, lifestyle, and hereditary factors associated with Coronary Heart Disease (CHD) using the SA_Heart dataset.
The analysis applies statistical and predictive modelling techniques to identify which predictors most strongly influence CHD occurrence among 462 male participants from a high-risk population in South Africa.

🎯 Objectives

Explore and visualise the dataset to understand key variable relationships.

Identify significant predictors of CHD through statistical testing.

Build and evaluate a logistic regression model to predict CHD risk.

Interpret results in a clear, business-relevant manner.

🧹 Data Preparation

Cleaned missing values and removed incomplete rows (e.g., ID-only records).

Converted character variables (e.g., sbp, ldl) to numeric and categorical formats.

Ensured consistency and accuracy of data for reliable modelling.

📊 Exploratory Data Analysis (EDA)

Histograms: Displayed variable distributions and identified outliers and skewness.

Bar plots: Highlighted categorical imbalances between participants with and without family history of CHD.

Pair plots: Showed strong correlations between LDL cholesterol, adiposity, and obesity, suggesting multicollinearity.

Box plots: Visualised group differences in continuous predictors across family history categories.

🧪 Statistical Testing — Welch t-Tests

Significant predictors: LDL cholesterol (p = 0.0005), adiposity (p < 0.001), obesity (p = 0.013), and age (p < 0.001).

Non-significant variables: systolic BP, tobacco, alcohol, and type A behaviour.

Findings indicate that hereditary and metabolic factors contribute more to CHD risk than behavioural variables.

📈 Logistic Regression Modelling

Reduced model retained tobacco, LDL, type A behaviour, and age.

Model achieved a low AIC = 502.09, indicating a strong fit.

All predictors remained statistically significant and interpretable.

⚖️ Model Evaluation

Recalibrated the threshold using the prior probability (0.346) to reflect CHD prevalence.

This improved classification sensitivity and real-world interpretability.

The ROC curve (AUC = 0.772) confirmed solid predictive power and good balance between sensitivity and specificity.

💡 Key Insights

Age, LDL cholesterol, and obesity are the most influential predictors of CHD.

Genetic predisposition amplifies the effect of metabolic risk factors.

Lifestyle variables like tobacco and alcohol showed weaker influence, suggesting hereditary and physiological drivers dominate.

🧭 Conclusion

This analysis demonstrates a data-driven approach to health risk assessment, combining rigorous statistical testing with interpretable predictive modelling.
The workflow highlights the practical application of R for data cleaning, visualisation, and logistic regression, producing insights that can guide targeted health strategies.
