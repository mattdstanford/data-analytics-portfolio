# Executive Summary
This project evaluates whether structural team characteristics demonstrate interpretable predictive characteristics for podium outcomes at NCAA Division I Cross Country Championships (2015–2025). Using a longitudinal dataset spanning 240 team observations and ~1,680 athletes (both sexes), I developed predictive models with Leave-One-Year-Out (LOYO) cross-validation to ensure realistic generalization to unseen competition years. The objective was not only to refine an explanatory model, but also to determine the extent of, and interpret, the impacts of model features on its predictions.
## Key Results
- Random Forest achieved mean AUC = 0.649, modestly outperforming logistic regression (AUC = 0.60)
- Removing altitude-related features reduced AUC to 0.549, indicating meaningful predictive contribution
- SHAP analysis identified altitude exposure and mean team age as consistent contributors
- Athlete age and nationality distributions shifted significantly following COVID-era eligibility changes
## Dataset Overview
Athlete-inclusion was determined via NCAA DI Cross Country competition results, courtesy of TFRRS.org. Demographic characteristics were sourced from worldathletics.org, using their in-built athlete repository search. ChatGPT was utilized to improve data compilation efficiency, and a global ruleset was developed at compilation-onset to ensure consistent formatting and to retain the ability to visually assess data integrity throughout compilation. Ultimately, the top 12 teams across 10 years (2015-2019, 2021-2025; no competitive results from 2020 due to COVID) for both sexes were compiled and delineated via sex. Athlete characteristics included: name, date of birth (if only a year was provided, a date of July 1st, XXXX was assumed), nationality (as listed on worldathletics.org), school class and associated school name at time of competition (school classes [FR, SO, JR, SR], taken from TFRRS.org results).
## Feature Engineering and Variable Design
All schools in the data set were compiled and assigned an altitude (metres), based on general internet search of their respective campus' altitudes. Athletes affiliated with those schools in a respective year's data were then assigned that school's altitude. School class was coded as an integer to allow for feature engineering (FR = 1, SO = 2, JR = 3, SR = 4). Based on a hypothesis that altitude exposure would be a meaningful feature in the predictive model, a value called "altitude exposure" was calculated, as a product of campus altitude and "years of exposure" (a conservative variable, designed as "school class - 1 year"), in the units of metre*year. "Years of exposure" was calculated as such, for 2 reasons. 1: Athlete transfer history is not easily sourced and thus athletes in the data set may have had exposure to multiple campuses' altitudes. 2: NCAA XC championships happen in the Fall, historically, which is generally the first academic semester for a new student, thus, they would have had only a handful of months at their new campus' altitude. Nationalities were placed into 4 coarse bins: USA, Europe, East Africa, and Other (any country not directly assigned to one of the three aforementioned bins).

Following completion of an athlete-level data set, a team-aggregated data set was constructed, using Year, Sex, Campus, and Team Placing as unique identifiers. Team proportions of the aforementioned nationality bins, team proportions of school classes, mean athlete-age, athlete-age SD, and altitude exposure characteristics (mean, max, sd) were generated as aggregations and assigned to each team-entry, in addition to team placing, campus altitude, and year.

## Modeling Strategy
The binary outcome of interest was whether or not a team made it on the podium (top 4 teams at NCAA XC), so all team data were assigned a binary variable of podium/non-podium, based on this criteria. An initial assessment via logistic regression was performed, using LOYO. To explore potential non-linear interactions between variables, random forest models were developed, also using LOYO for cross validation. Model-performance was assessed using ROC-AUC score. Ultimately, following interpretation of SHAP values from an initial RF model (explained below), 2 additional RF models were developed. The 3 models were: all features included, altitude exposure variables removed (but campus altitude retained), and all altitude variables removed. 

Global mean SHAP value plots and SHAP dependence plots for the strongest predictors in the all features model were generated to further assess potential non-linear effects.

## Model Performance
![RF_Models_AUC_Scores](/NCAA_Podium_Teams/figures/model_aucs.png)

A random forest model including all altitude variables performed modestly better than a logistic regression model including all variables (aucs: 0.6 vs. 0.65). The all-feature random forest model performed meaningfully better than a random forest with altitude values ommitted (aucs: 0.55 vs. 0.65), suggesting altitude to be a meaningful characteristic of teams who reach the podium at NCAA DI XC championships

## Model Interpretation
![RF_Models_AUC_Scores](/NCAA_Podium_Teams/figures/shap_summary.png)

A beeswarm plot of all SHAP values for all model features, with individual dots colored based on the magnitude of the feature's value for that specific data point. SHAP values describe, generally, the value that the inclusion of a specific feature has on the model's prediction of a team making it on the podium. A positive SHAP value indicates that, for that specific team data point, the inclusion of that feature (and that feature's value for that specific data point) pushed that data point's podium prediction closer to 1. The inverse is true to a negative SHAP value. Altitude-based features dominate model predictiveness. However, mean absolute SHAP values for all features were small to very small (ranging from 0.001-0.05). This observation is reflected in the model's AUC score, and is a product of at least 2 key factors: this data set is small (240 data points) and there are potentially numerous additional features which could not be included due to lack of access (e.g. athlete-level fitness, training programs at respective schools) or were not sourced and compiled due to time-requirements and/or availability of data (past-competition histories).

## Altitude Comparison
![RF_Models_AUC_Scores](/NCAA_Podium_Teams/figures/podium_altitudes.png)

Altitudes across podium and non-podium teams were compared. Visually, there is a meaningful difference in the range of the third quartile between podium and non-podium teams, with podium teams generally coming from campus as higher altitudes. Once again, this may partly be an artifact associated with size of the data set, but is worth noting.

## Structural Distribution Shifts
![RF_Models_AUC_Scores](/NCAA_Podium_Teams/figures/athlete_ages_per_era.png)

These data were tangentially aggregated (per athlete per era) to answer a secondary question: Has there been a shift in mean athlete age from pre-post COVID (and, if so, are there any intra-era trends in age post COVID)?

- Pre-COVID (2015–2019) Median age = 21.4
- Post-COVID (2021–2025) Median age = 22.3

A Mann-Whitney test showed a meaningful shift in age distribution from pre-post (p<.001, effect size "r" = 0.23), with athletes in the post-COVID era ~1 year older on average, based on top 12 team rosters. Linear regression was performed to assess inter-year shifts in the post-COVID era, which returned a standardized beta coefficient of .013 for 'Year', indicating no meaningful shift upwards or downwards in age across 2021-2025. This suggests a structural shift of some kind, where athletes have tended to be older on post-COVID rosters compared to pre-COVID. It is certainly plausible that this shift is explained mostly by delayed eligiblity due to COVID disruptions, although a lack of downward shift in age across post COVID years (back to pre-COVID norms) indicates additional factors may be involved.

## Limitations
- Dataset limited to top 12 teams per year
- Sample size modest (240 team observations)
- Results probabilistic, not causal
- Potential unmeasured confounders (training environment, coaching continuity, recruitment dynamics)
- Nationality binning simplifies complex demographics

The project prioritizes structural pattern detection rather than causal inference.

### Practical Takeaways
This project demonstrates several applied machine learning principles relevant to real-world analytics workflows:
- Proper cross-validation design for temporally structured data
- Use of ablation testing to quantify feature contribution
- Application of SHAP to interpret model behavior
- Integration of predictive modeling with statistical analysis
- Transparent communication of model limitations

These principles are broadly applicable to healthcare, workforce, and operational analytics contexts where interpretability and validation discipline are critical.
