# Visitor-Counts-Precision

This project utilizes pedestrian traffic data from various blocks in Manhattan at different time intervals. I establish interpretable models, investigating the impact of different features on pedestrian flow.

**Data**: new_feature_matrix.npy

#### Summary

##### Time Sensitive

The visit counts exhibit a high degree of autocorrelation. As shown in Figure "Autocorrelation_zipcode.png", the trend of autoregressive plots varies across different regions. There are the following three main differences:

1. Different descending trends: Some exist fluctuations after lag 3, while others are consistently declining. This might occur in situations where some area experience periodic events leading to cyclical fluctuations in pedestrian flow, while other areas do not.
2. Different amplitudes: Some maintain around 0.5 even up to lag 9, while others have already dropped to 0 or even negative values. This might occur in situations where the pedestrian flow in non-core areas remains relatively constant, while in core areas (tourist attractions, transportation hubs, etc.) pedestrian flow is significantly influenced by time.
3. Some regions exhibit negative correlation with each other. This might occur in situations where two areas compete as tourist attractions.

##### Model

For intuitive interpretability, I chose linear regression as the foundational model.

Firstly, due to autocorrelation, the independent variables include passenger flow within 9 days. Secondly, because Total_Population and Median_Household_Income remain constant and are unique numbers for each area, I only use Total_Population and categorize it into three levels: high, medium, and low, transforming it into a categorical variable. Finally, I input the passenger flow within 9 days, the Total_Population of the area, and the case rate as features into the model, with the dependent variable being the passenger flow of the next day.

Except from the meaning of linear regression coefficients, I also use SHAP to analysis model. The SHAP (SHapley Additive exPlanations) library is for interpreting the output of machine learning models. It provides a unified framework based on Shapley values from cooperative game theory, allowing users to understand the impact of each feature on model predictions. SHAP values offer a consistent and theoretically grounded approach to feature importance analysis, aiding in model debugging, explanation, and trustworthiness assessment.

I found that the model parameters differ between the comprehensive model for all regions and the individual model for a specific region, indicating the unique characteristics of each small area:

1. In unified model, lag_1 and lag_6 are the most important variables.
2. In individual model for first region, case_rate, lag_1 and lag_6 are the most important variables, while lag_1 changed from positive correlation to negative correlation compared to unified model.

##### Week summaries

**Week 1-3**: Exploring the dataset, data preprocessing, and initial attempts at model prediction with unified model.

**Week 4-6**: Try and compare the merits of different models (Linear Regression, XGBoost, Random Forest, Neural Networks), fitting models separately to different regions for comparison.

**Week 7-10**: Analyze time sensitivity (overall and partial), utilize the SHAP library to analyze variable importance, establish the final model, and output results.
