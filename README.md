# Predicting Hospital Length of Stay Using Regression Models in R

**Healthcare Analytics | Statistical Modeling | Predictive Analytics | R Programming**

## Project Overview

Hospital patient length of stay is an important indicator of healthcare service utilization and hospital operations. Understanding the factors associated with longer patient stays can help inform hospital resource planning and operational decision-making.

This project applies statistical regression techniques to analyze hospital patient length of stay using the **Study on the Efficacy of Nosocomial Infection Control (SENIC)** dataset.

Three modeling approaches were examined:

1. **Ordinary Least Squares (OLS)** – To establish a baseline linear regression model and evaluate classical regression assumptions.
2. **Generalized Linear Models (GLM)** – To accommodate the positive, right-skewed characteristics of patient length of stay.
3. **Generalized Additive Models (GAM)** – To investigate nonlinear relationships and evaluate whether more flexible models improve predictive performance.

The analysis includes exploratory data analysis, regression diagnostics, influential observation detection, model refinement, cross-validation, and comparative model evaluation.

The project was implemented in **R**.

## 1. Business and Analytical Problem

Hospitals must manage patient capacity, staffing, and available resources while maintaining effective healthcare services.

Longer patient stays may increase resource utilization and create additional operational challenges.

Understanding the relationship between patient length of stay and hospital characteristics can provide useful information for hospital management.

**Central Analytical Question:**

How are hospital infection rates, patient census, and nursing staff levels associated with average patient length of stay, and which regression modeling approach provides the best balance between predictive performance and interpretability?

### Potential Stakeholders

- Hospital administrators
- Healthcare operations managers
- Infection prevention and control teams
- Hospital workforce planners
- Healthcare researchers

## 2. Project Objectives

1. Explore the distribution and relationships among hospital length of stay, infection rates, patient census, and nursing staff.
2. Develop an OLS regression model and evaluate its underlying assumptions.
3. Identify unusual and influential observations affecting regression estimates.
4. Develop and compare GLMs using alternative probability distributions.
5. Investigate nonlinear relationships using polynomial regression, step functions, and regression splines.
6. Evaluate model performance using cross-validation and predictive error metrics.
7. Recommend a modeling approach based on predictive performance, interpretability, and model complexity.

## 3. Dataset

**Dataset:** Study on the Efficacy of Nosocomial Infection Control (SENIC)

The SENIC dataset originated from a multicenter study conducted in the United States during the late 1970s and early 1980s to investigate hospital-acquired infections and infection control practices.

### Variables Used

| Variable | Description | Role |
|---|---|---|
| `stay` | Average patient length of stay in days | Response variable |
| `inf` | Hospital infection rate (%) | Predictor |
| `census` | Average daily hospital patient census | Predictor |
| `nurses` | Average number of full-time equivalent nurses | Predictor |

The analysis focuses on the relationships between hospital characteristics and average patient length of stay.

**Data Quality:** No missing values were identified in the analyzed dataset.

## 4. Analytical Methodology

### Step 1: Exploratory Data Analysis

Initial data exploration included:

- Descriptive statistics
- Missing-value assessment
- Box plots and potential outlier detection
- Correlation analysis
- Scatter plot matrices
- Estimated probability density functions
- Examination of variable distributions

The analysis identified positive, right-skewed distributions for several variables, particularly patient length of stay, patient census, and nursing staff.

### Step 2: Ordinary Least Squares Regression

An OLS regression model was developed using infection rate, patient census, and nursing staff as predictors.

The analysis examined:

- Residual patterns
- Normality of residuals
- Constant error variance
- Leverage
- Cook's distance
- DFFITS
- DFBETAS
- COVRATIO

Two observations, **47 and 112**, were identified as potentially influential.

#### Regression Assumption Testing

| Statistical Test | p-value | Interpretation |
|---|---:|---|
| Breusch-Pagan test | 8.6 × 10⁻⁸ | Evidence of nonconstant error variance |
| Shapiro-Wilk test | 7.2 × 10⁻⁶ | Evidence against normally distributed residuals |

Both tests produced statistically significant results at the 5% significance level.

These findings raised concerns about the suitability of the classical OLS assumptions for the analyzed dataset.

### Step 3: Generalized Linear Models

GLMs were explored to accommodate the positive and skewed distribution of patient length of stay.

The analysis considered alternative distributional specifications, including:

- Gamma
- Inverse Gaussian
- Gaussian

Candidate models were developed and compared using model selection criteria and predictive performance.

**Selected GLM:**

An Inverse Gaussian regression model with the following predictors:

`stay ~ inf + census + nurses`

The selected model achieved the following results:

| Evaluation Metric | Result |
|---|---:|
| AIC | 377.1236 |
| BIC | 390.7605 |
| Cross-validated MSPE | 2.0192 |

The selected model achieved the lowest AIC, BIC, and cross-validated MSPE among the evaluated GLM candidates.

### Step 4: Predictive Performance Evaluation

The selected GLM was evaluated using an **80% training and 20% testing split**.

The reported predictive performance included:

| Metric | Result |
|---|---:|
| Bias | 0.218 |
| Mean Squared Prediction Error (MSPE) | 1.574 |
| Mean Absolute Error (MAE) | 1.049 |

These metrics were used to evaluate the model's ability to predict hospital length of stay on the test dataset.

### Step 5: Influential Observation Analysis and Model Updating

Influence diagnostics identified observation 47 as particularly influential.

The observation was removed in an updated model, while observation 112 was retained.

The updated model demonstrated improvements in several model selection and predictive performance metrics.

This step illustrated how influential observations can affect parameter estimation and model performance.

### Step 6: Generalized Additive Models and Nonlinear Modeling

The analysis investigated whether nonlinear relationships could improve model fit and prediction.

**Nonlinearity Assessment**

CERES plots and statistical tests were used to examine departures from linearity.

Patient census demonstrated notable evidence of a nonlinear relationship with average patient length of stay.

**Nonlinear Modeling Techniques**

The analysis compared:

- Polynomial regression
- Piecewise constant step functions
- Piecewise polynomial functions
- B-splines
- Natural cubic splines

A 10-fold cross-validation procedure was used to compare model specifications.

### Step 7: Spline Model Selection

Among the nonlinear specifications evaluated, the B-spline model with six degrees of freedom was selected.

**Selected spline specification:**

`glm(stay ~ bs(census, df = 6))`

This specification provided favorable model selection and predictive performance results among the evaluated nonlinear alternatives.

### Step 8: GLM versus GAM Comparison

The final comparison evaluated differences in predictive performance and model complexity.

The GAM approach provided slightly better performance on some prediction metrics, including MSPE, NRMSE, and RMSPE.

However, the GLM performed slightly better on other metrics, including MAE, MAPE, and SMAPE.

The GAM also introduced additional complexity through nonlinear spline functions.

## 5. Key Findings

### Finding 1: Patient length of stay exhibits characteristics that challenge classical linear regression assumptions.

The analysis identified right-skewed observations, influential data points, nonconstant error variance, and departures from normality.

These characteristics motivated the exploration of GLMs as alternatives to classical OLS regression.

### Finding 2: Infection rate is associated with longer patient stays.

The selected GLM indicated that higher hospital infection rates were associated with longer expected patient stays, holding other predictors constant.

This finding highlights the relevance of hospital infection control when examining length-of-stay patterns.

### Finding 3: Hospital census is associated with patient length of stay.

Higher patient census was associated with longer expected stays in the selected model.

The nonlinear analysis also identified evidence that the relationship between census and length of stay may not be adequately described by a simple straight line.

### Finding 4: Nursing staff is an important explanatory variable.

Nursing staff was included in the selected GLM and contributed to the analysis of hospital length of stay.

The model interpretation indicated an association between higher nursing staff levels and shorter expected stays, after accounting for infection rate and patient census.

These findings represent statistical associations rather than causal effects.

### Finding 5: Flexible nonlinear models can improve predictive performance.

Spline-based modeling captured nonlinear relationships, particularly for hospital census.

The GAM provided modest improvements in some predictive metrics compared with the GLM.

However, the improvement was relatively small and involved additional model complexity.

### Finding 6: Interpretability remains important in model selection.

Although GAM offered some predictive advantages, the study recommended the **Inverse Gaussian GLM** as the primary model.

The GLM provided a practical balance between:

- Predictive performance
- Statistical suitability
- Model simplicity
- Interpretability

This illustrates that the model with the greatest flexibility is not necessarily the most appropriate model for every analytical application.

## 6. Practical Applications

The project demonstrates how statistical modeling can support healthcare analytics.

| Analytical Finding | Potential Application |
|---|---|
| Infection rates associated with length of stay | Support infection control monitoring |
| Hospital census associated with length of stay | Inform hospital capacity planning |
| Nursing staff associated with length of stay | Support workforce planning analysis |
| Nonlinear relationships | Improve understanding of hospital operational patterns |
| Predictive model comparison | Support evidence-informed model selection |

These applications are illustrative and would require additional validation using contemporary operational healthcare data.

## 7. Tools and Statistical Techniques

**Programming Language**
- R

**Statistical Modeling**
- Ordinary Least Squares Regression
- Generalized Linear Models
- Generalized Additive Models
- Polynomial Regression
- Regression Splines

**Model Diagnostics**
- Shapiro-Wilk Test
- Breusch-Pagan Test
- Residual Analysis
- Leverage and Influence Diagnostics
- CERES Plots

**Model Evaluation**
- Akaike Information Criterion
- Bayesian Information Criterion
- Cross-Validation
- Mean Squared Prediction Error
- Mean Absolute Error
- Root Mean Squared Prediction Error
- Normalized RMSE
- Mean Absolute Percentage Error

## 8. How to Reproduce the Analysis

1. Download or clone this repository.
2. Install R and RStudio.
3. Open the R source file provided in the repository.
4. Install the required R packages.
5. Obtain the SENIC dataset used in the analysis.
6. Update any necessary file paths.
7. Run the analytical code sequentially.
8. Review the model outputs, diagnostics, and visualizations.

Refer to the source code for the complete package requirements and data preparation procedures.

## 9. Limitations

- The SENIC dataset represents historical hospital data from the United States.
- Findings may not generalize to present-day hospital operations or healthcare systems in other countries.
- The analysis examines associations rather than causal relationships.
- The sample contains influential observations that may affect model estimates.
- Predictive results depend on the evaluated model specifications and validation procedures.
- The analysis focuses on selected hospital-level variables and does not incorporate individual patient characteristics.

## 10. Future Improvements

Potential extensions include:

- Evaluating additional model families.
- Incorporating more hospital operational and patient-level characteristics.
- Applying repeated cross-validation to assess model stability.
- Examining alternative methods for handling influential observations.
- Testing the models on more recent healthcare datasets.
- Developing interpretable visualizations for healthcare decision-makers.

## 11. Conclusion

This project demonstrates the importance of selecting statistical models based on both the characteristics of the data and the intended analytical application.

The OLS analysis identified limitations associated with nonconstant variance, non-normal residuals, and influential observations.

GLMs provided an alternative framework for modeling positive, skewed patient length-of-stay data, while GAMs demonstrated the potential value of flexible nonlinear relationships.

Considering both predictive performance and interpretability, the study recommended an **Inverse Gaussian GLM** as the primary modeling approach.

The project highlights the importance of regression diagnostics, model comparison, cross-validation, and interpretability in applied statistical analysis.

## 12. Author

**Dominique Pocholo P. de Lara**

Academic Statistical Modeling Project

**Focus Areas:**
- Statistical Modeling
- Predictive Analytics
- Regression Diagnostics
- Healthcare Data Analytics
- R Programming

## 13. References

Agresti, A. (2018). *An Introduction to Categorical Data Analysis* (3rd ed.). Wiley.

Fox, J. (2016). *Applied Regression Analysis and Generalized Linear Models* (3rd ed.). SAGE.

Hastie, T., Tibshirani, R., & Friedman, J. (2009). *The Elements of Statistical Learning* (2nd ed.). Springer.

James, G., Witten, D., Hastie, T., & Tibshirani, R. (2013). *An Introduction to Statistical Learning: With Applications in R*. Springer.

---

*This project was developed for academic and analytical purposes. Its findings should not be interpreted as causal evidence or direct clinical recommendations.*
