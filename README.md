# Happy Customer Project

## Project Description
This project analyzes and predicts customer happiness using the **ACME-HappinessSurvey2020** dataset. The objective is to identify the most influential factors driving customer satisfaction and to build predictive models that help businesses proactively improve customer experience and retention.

This end-to-end data science project covers:
- Exploratory Data Analysis (EDA)
- Data preprocessing and feature engineering
- Model development and tuning
- Model evaluation and comparison
- Business recommendations based on insights


# Dataset Overview

- Dataset: **ACME-HappinessSurvey2020.csv**
- Observations: 126 customer responses
- Features: 6 survey-based attributes
- Target Variable: Binary happiness indicator  
  - `1` = Happy  
  - `0` = Unhappy  

### Feature Descriptions (1–5 Rating Scale)

- **X1** – Order delivered on time  
- **X2** – Order contents as expected  
- **X3** – Ordered everything wanted  
- **X4** – Paid a good price  
- **X5** – Satisfaction with courier  
- **X6** – App ease of ordering  

All features are ordinal ratings, making the dataset structured and suitable for classification modeling.


# Exploratory Data Analysis (EDA)

EDA was performed to understand feature behavior and relationships with customer happiness.

### Key Steps:
- Checked for missing values and data consistency
- Analyzed feature distributions (histograms, boxplots)
- Reviewed class balance of target variable
- Generated correlation matrix and heatmaps
- Compared feature averages between happy vs unhappy customers

### Key Findings:
- Courier satisfaction (X5) and delivery timeliness (X1) showed positive relationship with happiness
- On-time order delivery (mean = 4.33) and ease of ordering through the app (mean = 4.25) received the highest customer ratings, while expectation of content had the lowest average rating (mean = 2.5), indicating a key improvement area; all features were rated on a consistent 1–5 scale
- No severe multicollinearity observed among predictors

EDA helped guide model selection and interpretation strategy.

# Model Approaches
A progressive modeling strategy was applied:
## Baseline Models
- Logistic Regression
- Decision Tree Classifier

## Advanced & Ensemble Models
- Random Forest
- Gradient Boosting
- Bagging Classifier
- XGBoost

## Hyperparameter Tuning
- Used GridSearchCV
- Performed cross-validation

## Feature Engineering Approach (Approach 4)
To better represent overall customer sentiment, an additional engineered feature was introduced based on survey responses.
- A new feature avg_X was created representing the average rating across X1–X6.
- Assumption: a generally happy customer would provide an average rating around 3 or higher.
- This aggregated feature captures overall satisfaction and simplifies customer sentiment into a single measurable signal.

# Model Performance
Models were evaluated using:
- Accuracy
- Precision
- Recall
- F1-Score
- precision_recall_curve
- Confusion Matrix

## Comparison of Model Effectiveness and Generalization

### Overfitting Tendencies
- Many of the advanced models (Decision Tree untuned, Random Forest, Bagging, XGBoost, AdaBoost) exhibited significant overfitting. Their training performance was very high (e.g., F1-score > 0.8), but this dropped substantially on the test set (e.g., F1-score < 0.6). This indicates that these models learned the training data too well and failed to generalize to new, unseen data.

### Logistic Regression Models
- The Logistic Regression model showed much better generalization. The difference between training and test set metrics was relatively small, suggesting they are not overfitting. Although their raw performance metrics (Accuracy, F1-score) are not as high as the overfit training scores of other models, their consistent performance makes them more reliable.

### Impact of X_mean Feature
- The statsmodels Logistic Regression using only X_mean as a predictor achieved a remarkable recall of **0.905** on the test set. This highlights the potential simplicity in predicting happiness if an aggregate score is sufficiently informative. 

### Optimal Threshold Application
- Applying an optimal threshold (**0.45**) to the Logistic Regression model (with all features) significantly boosted recall on the test set to **0.810**, while maintaining a reasonable F1-score of **0.680**. This demonstrates the importance of threshold tuning for specific optimization goals.

## Final Model Selection
- Logistic Regression with all features and an optimal threshold of **0.45** also performed strongly with a test recall of **0.810** and a slightly better precision of **0.59**, offering a good balance.
- Strong and consistent results across both training and testing datasets Indicates low overfitting and good bias–variance balance
- The model achieved the best balance between predictive performance, interpretability, and business applicability.
   Model coefficients directly explain how each feature affects customer happiness.

# Feature Importance Insights
**Logistic Regression (Odds and Percentage Change)**:
- X5 ('I am satisfied with my courier') showed the largest positive impact, increasing the odds of a happy customer by ~33% for every one-unit increase in rating.
- X1 ('my order was delivered on time') followed closely, increasing the odds by ~31%.
- X3 ('I ordered everything I wanted to order') increased the odds by ~28%.
- X4 ('I paid a good price for my order') increased the odds by ~21%.
- X6 ('the app makes ordering easy for me') had a small positive impact, increasing the odds by ~8%.
- X2 ('contents of my order was as I expected') had a negative impact, decreasing the odds by ~9%.

**Decision Tree Feature Importance**: The Decision Tree identified X2 (0.260), X3 (0.219), and X1 (0.162) as the most important features. This differs slightly from logistic regression, which highlights that different models might value features differently based on their internal mechanisms.

### Most Important Features
Based on the statsmodel Logistic Regression (which offers interpretable coefficients), X5 (courier satisfaction) and X1 (on-time delivery) are the most important features positively impacting customer happiness. X3 (ordered everything wanted) and X4 (good price) are also significant. X2 ('contents as expected') is important, albeit negatively correlated, indicating it's still a significant factor in dissatisfaction.

### Question to Remove
X6 ('the app makes ordering easy for me') is the strongest candidate for removal in the next survey. Its impact on customer happiness, as measured by the odds ratio in logistic regression, is the smallest among all positive predictors (8% increase). More importantly, its removal from the sklearn Logistic Regression model resulted in virtually no change in performance metrics, indicating it provides minimal unique predictive value to this model.

### Important Business Consideration about Feature Elimination
Feature elimination does not imply that app usability is unimportant operationally. Rather, it indicates that within this dataset, app ease of ordering does not significantly differentiate happy and unhappy customers.


## Overall Insights and Actionable Recommendations
### Enhance Courier Experience
The courier interaction is the final brand touchpoint and has the biggest impact on satisfaction. Couriers should be trained in customer communication and professionalism, their performance should be tracked using customer ratings, high satisfaction scores should be incentivized, and best practices from top performers should be replicated. This approach leads to the fastest and largest improvement in customer happiness.

### Improve Delivery Reliability (X1)
On-time delivery builds trust and reliability. Delivery routes should be optimized using data, real-time tracking updates should be provided, customers should be notified proactively about delays, and courier capacity should be increased during peak hours. Implementing these actions reduces frustration and strengthens customer trust.

### Reduce Expectation Gaps (X2 — Risk Factor)
Customers become unhappy when orders do not match their expectations. Product descriptions and images should be improved, inventory should be synced in real time, order verification should be added before shipment, and customers should be notified early about substitutions. These measures result in fewer complaints and a smoother customer experience.

### Increase Data Collection
The small dataset size (126 rows) limits the effectiveness of complex models and their ability to generalize. Collecting significantly more customer feedback data is crucial for improving predictive accuracy and model robustness.

# Conclusions

- Key drivers of customer happiness were successfully identified.
- Logistic regression provided strong predictive power with interpretability.
- Small structured datasets may favor simpler models over complex ensembles.
- Predictive analytics can support proactive customer retention strategies.


