# Regression Analysis on Customer Tips in NYC Taxi and Limousine Data
A case study on linear regression applied to NYC Taxi and Limousine Comission data to assess tipping outcomes, with follow-up validation checks to determine measurement bias.
## Overview
This project checked for potential intervention options to improve tipping for taxi and limousine drivers with minimal opportunity cost, while preserving ethical practice. OLS regression was utilized due to tips being quantifiable and continuous. Initial regression analysis suggested that tip averages differed between customers who paid with cash versus with credit card, where credit card payments trended higher. However, follow-up checks to confirm whether tips were correctly tracked for cash-payers and credit card-payers revealed that cash tips are uniformly not tracked, demonstrating substantial measurement bias in modeling outcomes. Thus, results from the predictive model should not be considered valid, and improvements should be made to tip tracking by the NYC TLC.
## Key Skills Demonstrated
- Data cleaning
- Linear Regression with categorical predictors
- Multicolinearity assessment with VIF
- Residual normality and homoscedasticity checks
- Reconstruction of reported transaction totals to check for hidden tip amounts
- Determination of measurememt bias
- Scientific communication of limitations and future suggestions for improvement
## Summary of Findings
- Apparent difference in tip amounts between cash and credit card payments are driven by differences in data tracking between both.
- Cash tips are not directly recorded in the data set, nor do they appear to be hidden within another component of the total transaction amount.
## Limitations
- Zero-inflation associated with tip amounts can impact model fitting and interpretation.
- The model used is entirely based on observational data and cannot make claims about causality.
