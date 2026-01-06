# Predicting Employee Retention
A machine learning model to determine factors which contribution to employee attrition, in order to optimize company resources to retain existing employees.
## Overview
This project was based on a request from a vehicle company (Sailfort Motors: fictional company and dataset) to attempt to elucidate factors which contribute to employee attrition, in order to develop interventions targeting employees at risk of leaving. As this was a binary outcome, logistic modeling was most appropriate. Decision tree and random forest models were evaluated to maximize accurate classifications accross sensitivity thresholds. A random forest model was ultimately selected, and SHAP values were used to assess global feature importance, where the strongest predictors in the model were determined. Key predictors included: average number of projects assigned, length of term at the company, average number of monthly hours, and the last evaluation score received. SHAP dependence plots developed for these predictors revealed unique interactions which provide actionable insights for Sailfort.
## Key Skills Demonstrated
- Data cleaning and transformation
- Preliminary visualizations to assess important features to include in a predictive model
- Machine learning models, including decision trees and random forests, training and testing data splits, and model assessment functions in python
- Use of SHAP values to assess global importance of each model feature and use of dependence plots to reveal unique patterns for each feature and interactions with other features
- Scientific communication of findings, limitations, and suggest intervention strategies to adress human resources questions
## Results
- Initial analysis revealed employee satisfaction to be a strong predictor. However, this was removed from the final model due to it being arguably an outcome variable, as well as something which is not often tracked in an unbiased manner due to being traditionally recorded through survey.
- The final random forest model maximized roc-auc score and performed well in all other assessment metrics (precision, recall, accuracy, f1).
- Follow-up analysis of global feature importance using SHAP values revealed number of assigned projects, length of term at company, average monthly hours (coded as over/under-worked at a threshold of 175hrs/month), and last evaluation score.
- SHAP dependence plots revealed unique, actionable patterns for each of these key features, as well as patterns with their strongest feature interaction.
## Summary of Findings
SHAP dependence plots revealed key insights. These included:

- An optimal range of 3-5 assigned projects per employee, and to avoid underloading short-tenured employees, specifically
- To prepare intervention for long-tenured employees who received high last evaluation scores, as well as specifically low-scoring employees who are assigned few projects and high-scoring employees assigned numerous projects.
## Power BI Dashboard

### Note on Employee Satisfaction
Model efficacy markedly declined upon omission of employee satisfaction as a predictor. Employee dissatisfaction is very tightly correlated to employee attrition, likely resulting in a situation where a severely dissatisfied employee is determined to leave regardless. Most importantly, however, this metric often suffers from reporting bias due to it being assessed via methods such as voluntary survey. Effort should be taken to improve satisfaction tracking methods within the company, perhaps by increasing assessment frequency and incentivizing high response rates.
