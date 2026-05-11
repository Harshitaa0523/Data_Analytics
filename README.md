**Goal** Predictlikelihood of customer discontinuing their relationship with the bank (customer churn)and analysis of the contributing factors.

**Objectives**
•Transform raw data into meaningful features.
•Create derived features like Income_to_Credit_Ratioand  Trans_Inactivity_Ratio.
•Analyze correlation between features and target (Credit_Limit).

**Data Exploration and Analysis**
•The Structure of the Dataset contains 10,167 entries and 20 columns with the data being a mixture of categorical and numerical feature.
•There is some unnamed column as well with all null values will be removed from the dataset in the later part of the model preparation

**Data Exploration Analysis**
**• High Positive Correlation**
1. Features which are graded in red are high correlation with each other.
2. Total_Trans_Amtand Total_Trans_Cthas a high positivecorrelation of 0.81 indicating that as the transcationincrease the transaction amount also increases.
3. Credit_Limitand Avg_Utiization_ratiohas a correlation of negative 0.48 indicating an inversely proportional relationship with each other.
This suggests that as the credit limit decreased the avg utilization ratios will increase and vice versa.
**• Low or zero Correlation**
1. Some feature has zero correlation or near zero correlation with each other, indicating weak or no linear relationship. This features can be dropped while training our model.
2. Example of these include clientnumwhich shows no correlation with other features.
**• Missing Values**
1. The data contains a lot of missing values which can lead to bad model prediction.•A column naming Unnamed has the highest number of missing values, so we have dropped the column and remove all the missing values before the training our model.

**Data Cleaning**
For identfying the outliers, box plot of all the numerical_features was created.•As we can see customer_age, credit_limit, and Total_Amt_Chng column has the highest amount of outliers•Customer_age displays the age distribution above 100.•Credit_limit shows several outliers with a high consistency.•Total_Amt_Chng shows several outliers with a high value to them.

**• Removal of Duplicate**
At the beginning of the dataset, the total length of the dataset was 10167.•When calculated, the dataset has approximately 32 duplicate samples which was removed while training the model.•The dataset length after removal was 10132.

**• Outliers**
•For the identifying outliers, Lower bound and upper bound was calculated.
•An assumption was made while calculating the upper and lower bound.
•The IQR multiplier was increased from 1.5 to 2.5.
•As shown in the box plot, credit_limit, customer_age, and total_amt_chng has the highest number of the outliers.

**Churn Segamentation Hypothesis**
Churn SegementationHypothesis1. High-Risk Churn Customers• High Income-to-Credit Ratio(above 0.5).• Younger (Under 25) or older (75+) age groups.• Low credit limits (Credit_Limitbelow a certain threshold).2. Low-Risk Churn Customers• Balanced Income-to-Credit Ratio(0.2–0.5).• Middle-aged (25-50or 50-75) groups with stable income.

**Key Insights from Correlation Analysis**
**Correlation Results**-Incomeshows the strongest positive correlation with Credit_Limit(0.56).
•Avg_Utilization_Ratiohas a negative correlation (-0.48).Scatter Plots:
•Correlation between Incomeand Credit_Limit.
•Correlation betweenAvg_Utilization_Ratioand Credit_Limit.

**Feature Engineering Process**
**Columns Referenced**
Customer_Age:Used to group customers into age categories like Under 25, 25-50, etc.This was achieved using binning with the pd.cut()function.
Income_Category:Mapped to numerical values to represent customer income levels more effectively (e.g., "Less than $40K" → 20,000).A derived column, Income, was created based on this mapping.
Credit_Limit:Used alongside Incometo calculate the derived feature Income_to_Credit_Ratio.This ratio helps analyze customer financial behavior, such as how much credit they are utilizing relative to their income.
Categorical Features:Columns like Gender, Education_Level, Marital_Status, and Card_Categorywere identified for one-hot encoding to transform categorical data into a numerical format suitable for machine learning.
Numerical Features:Columns such as Total_Trans_Amt, Total_Trans_Ct, and Avg_Utilization_Ratiowere normalized using StandardScalerto ensure consistent scaling.

**Model Selection and Implementation**
**1. Preprocessing and Linear Regression Model**
•Data Preprocessing:•Separated numerical and categorical features.
•Applied pipelines for handling missing values and transformations
•Numerical Features:Mean imputation, Standard Scaling.
•Categorical Features:Most Frequent imputation, One-Hot Encoding.
•Model Performance:Mean Squared Error (MSE): 32,099,586.45; R² Score: 0.62
**2. Optimized Model: K-Nearest NeighborsModel Enhancements**:
•Added feature selection using SelectKBest(6 features).
•Implemented KNeighborsRegressorwith:
•11 neighbors, uniform weights, Euclidean distance.
•Model Performance:•Mean Squared Error (MSE): 19,522,741.51
•R² Score: 0.77Comparison:​
•KNN outperformed Linear Regression with better accuracy and reduced error.
**3. Classification Model Development and Evaluation**
Feature Engineering:•Created a new Boolean feature: Churn_Prediction.
•Applied the condition:
•High Credit-to-Income ratio > 0.5.
•Age between 25 and 75.Models Implemented:
•Logistic Regression:Accuracy: 99.82%
•K-Nearest Neighbors (KNN):Accuracy: 98.44%
Outcome:Logistic Regression outperformed KNN with higher recall and balanced metrics.

**Model Evaluation**
•KNN Regression demonstrates low errors but a low R² score, indicating accurate predictions with limited explanatory power, while Linear Regression shows high errors and a very negative R² score, suggesting poor performance and a poor fit for the data.ModelMSERMSEMAER2KNN regression 0.020.120.020.09Linear regression91095705.359544.417736.69-5322860461.38ModelAccuracyPrecisionRecallF1-scoreLogistic regression 1.01.00.900.95KNN classification0.981.000.100.19

•The KNN Classification model does not perform well in the area of True Positive detection. It was able to correctly identify 3 positives but it completely missed the actual 26 (False Negatives), without committing any False Positives. Logistic Regression performs better, as it correctly classifies 26 positives and only 3 are miss-classified as False Negatives with no False Positives. 

**Future Scope**
1. Incorporating additional behavioral features, addressing class imbalance with advanced resampling techniques
2. Exploring robust algorithms like Gradient Boosting or Random Forest to enhance prediction accuracy and recall.
