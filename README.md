# Happy Customer Project

## Project Description
This project analyzes and predicts customer happiness using the **ACME-HappinessSurvey2020** dataset. The objective is to identify the most influential factors driving customer satisfaction and to build predictive models that help businesses proactively improve customer experience and retention.

This end-to-end data science project covers:
- Exploratory Data Analysis (EDA)
- Data preprocessing and feature engineering
- Model development and tuning
- Model evaluation and comparison
- Business recommendations based on insights

---

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

---

# Exploratory Data Analysis (EDA)

EDA was performed to understand feature behavior and relationships with customer happiness.

### Key Steps:
- Checked for missing values and data consistency
- Analyzed feature distributions (histograms, boxplots)
- Reviewed class balance of target variable
- Generated correlation matrix and heatmaps
- Compared feature averages between happy vs unhappy customers

### Key Findings:
- Dataset slightly unbalanced between happy and unhappy customers
- Courier satisfaction (X5) and delivery timeliness (X1) showed positive relationship with happiness
- No severe multicollinearity observed among predictors

EDA helped guide model selection and interpretation strategy.

---

# Data Processing & Strategy

To ensure robust and unbiased modeling:

### Data Cleaning
- Verified no missing values
- Checked for outliers in rating scale (none outside 1–5 range)
- Confirmed consistent numeric formatting

### Feature Engineering
- Maintained ordinal structure of rating variables
- No categorical encoding required (already numeric)

### Scaling
- Logistic regression performed well without heavy scaling due to similar feature ranges

### Train-Test Split
- Used stratified split to preserve class distribution
- Ensured reliable model evaluation

---

# Model Approaches

A progressive modeling strategy was applied:

## Baseline Models
- Logistic Regression
- Decision Tree Classifier

Purpose:
- Establish benchmark performance
- Maintain model interpretability

## Advanced & Ensemble Models
- Random Forest
- Gradient Boosting
- Bagging Classifier

Purpose:
- Improve predictive performance
- Capture non-linear relationships

## Hyperparameter Tuning
- Used GridSearchCV
- Performed cross-validation
- Optimized:
  - Tree depth
  - Minimum samples per split
  - Class weights
  - Number of estimators

---

# Model Performance

Models were evaluated using:

- Accuracy
- Precision
- Recall
- F1-Score
- ROC-AUC
- Confusion Matrix

## Model Performance – Key Observations 

### Logistic Regression Generalized Well on Test Data
The Logistic Regression model demonstrated strong generalization capability, meaning its performance remained consistent between training and testing datasets.  

- Training and testing metrics were closely aligned, indicating minimal overfitting.
- Stable recall and precision across datasets showed the model can reliably predict outcomes on unseen data.
- This consistency makes the model suitable for real-world deployment where new customer responses continuously arrive.

---

###  Decision Trees Showed Overfitting Risk and Limited Generalization
The initial Decision Tree model significantly overfit the training data:

- Very high training performance but noticeably lower testing performance.
- The model learned noise and specific patterns unique to the training dataset.

After hyperparameter tuning:
- Tree depth and split constraints reduced overfitting.
- However, performance declined on both training and testing datasets.
- The tuned model failed to capture stable predictive patterns, indicating limited generalization capability for this small dataset.

This suggests Decision Trees require more data to perform reliably.

---

### Ensemble Methods Did Not Outperform Logistic Regression
Ensemble models (Random Forest, Bagging, Gradient Boosting) were explored to improve predictive accuracy.

Observations:
- Slight improvements in training performance but inconsistent testing results.
- Models showed sensitivity to dataset size (only 126 observations).
- Ensemble algorithms typically require larger datasets to leverage variance reduction effectively.
- Increased complexity did not translate into meaningful performance gains.

Therefore, simpler models proved more effective for this problem.

---

### Threshold Optimization Improved Recall and Business Usability
Probability threshold tuning was applied to the Logistic Regression model using Precision–Recall analysis.

- Default threshold (0.50) was adjusted to 0.48.
- Recall improved by approximately **10%**, allowing the model to identify more unhappy customers.
- Higher recall is valuable in customer satisfaction problems because missing dissatisfied customers can lead to churn.
- Precision remained reasonably stable, preserving prediction reliability.

This adjustment aligned model performance with business priorities.

---

## Final Model Selection

### Selected Model: **Logistic Regression (Threshold = 0.48)**

**Performance:**
- Recall: **81%**
- F1 Score: **65%**
- Strong and consistent results across both training and testing datasets.

The model achieved the best balance between predictive performance, interpretability, and business applicability.

---

## Reasons for Selecting Logistic Regression 

###  Strong Generalization
- Minimal performance gap between training and testing datasets.
- Indicates low overfitting and good bias–variance balance.
- Reliable predictions expected when applied to future customer data.
- Stable evaluation metrics across validation steps.

---

###  High Interpretability
- Model coefficients directly explain how each feature affects customer happiness.
- Odds ratios quantify impact in business-friendly terms (e.g., % increase in happiness odds).
- Stakeholders can easily understand *why* predictions are made.
- Supports transparent, explainable AI practices.

---

###  Clear Feature Impact Explanation
Logistic regression enables direct interpretation of feature influence:

- Positive coefficients → increase likelihood of happiness.
- Negative coefficients → decrease likelihood.
- Odds ratio conversion translates statistical output into actionable insights.

Example:
- Courier satisfaction increased happiness odds significantly.
- Pricing perception showed relatively smaller influence.

This clarity allows teams to prioritize operational improvements.

---

###  Balanced Precision–Recall Performance
The final model achieved a practical balance:

- **High Recall (81%)**
  - Successfully identifies most unhappy customers.
  - Reduces risk of overlooking dissatisfied users.

- **Moderate Precision (55%)**
  - Predictions remain reasonably accurate.
  - Limits excessive false alarms.

This balance is ideal for customer experience applications where detecting dissatisfaction early is more valuable than maximizing accuracy alone.

---

**Conclusion:**  
Logistic Regression provided the optimal combination of predictive stability, explainability, and business relevance, making it the most suitable model for deployment in customer happiness prediction.
---

# Feature Importance Insights

Odds ratio interpretation revealed:

- **X5 (Courier Satisfaction)** → Strongest positive driver of happiness  
- **X3 (Order Completeness)** → Significant positive impact  
- **X1 (On-Time Delivery)** → Meaningful contributor  
- **X4 (Pricing)** → Lower relative impact  

This insight helps prioritize operational improvements.

---

##  Business Recommendations 

Based on model insights and feature importance analysis, the following data-driven recommendations can help improve overall customer happiness and reduce dissatisfaction risk.

---

### 1. Improve Courier Experience
- Invest in structured courier training programs focused on:
  - Professional communication
  - Customer interaction etiquette
  - Safe and efficient delivery handling
- Introduce performance scorecards for delivery personnel based on customer feedback.
- Implement real-time delivery feedback collection after each order.
- Use customer ratings to identify high-performing couriers and replicate best practices.
- Provide incentives or recognition programs tied to customer satisfaction scores.

**Expected Impact:**  
Improved last-mile experience leading to higher customer trust and repeat usage.

---

###  2. Ensure Order Accuracy
- Improve inventory synchronization between ordering platform and warehouse systems.
- Implement barcode or automated scanning validation before shipment.
- Add a final verification checkpoint during order packing.
- Use historical error data to identify high-risk products or fulfillment stages.
- Introduce automated alerts for frequent substitution or stock mismatch issues.

**Expected Impact:**  
Reduction in returns, complaints, and negative customer experiences.

---

###  3. Maintain Delivery Timeliness
- Optimize logistics routes using data-driven routing algorithms.
- Analyze peak delivery hours and allocate courier resources dynamically.
- Provide customers with accurate real-time delivery tracking.
- Use predictive delay detection to notify customers proactively.

**Expected Impact:**  
Higher reliability perception and improved customer confidence.

---

###  4. Implement Predictive Monitoring System
- Deploy the model to generate customer happiness probability scores after each order.
- Flag customers below a defined satisfaction threshold (e.g., probability < 0.5).
- Trigger automated workflows such as:
  - Follow-up emails
  - Discount offers
  - Customer support outreach
- Integrate predictions into CRM dashboards for customer success teams.
- Track intervention outcomes to continuously improve prediction strategy.

**Expected Impact:**  
Proactive issue resolution and reduced customer churn.

---

###  5. Establish Continuous Feedback Loop
- Continuously collect survey responses after deliveries.
- Retrain models periodically with updated data.
- Monitor prediction accuracy and performance drift.
- Use A/B testing to evaluate operational improvements.
- Combine survey insights with behavioral data (purchase frequency, complaints).

**Expected Impact:**  
Sustained improvement in customer satisfaction and model reliability.

---

###  Overall Business Value

Implementing these recommendations enables organizations to:

- Detect dissatisfaction early
- Improve operational efficiency
- Enhance customer retention
- Optimize delivery operations
- Make data-driven customer experience decisions

These actions transform predictive analytics into measurable business outcomes.

# Conclusions

- Key drivers of customer happiness were successfully identified.
- Logistic regression provided strong predictive power with interpretability.
- Small structured datasets may favor simpler models over complex ensembles.
- Predictive analytics can support proactive customer retention strategies.

---

# Future Improvements

- Collect larger dataset for stronger model generalization
- Incorporate behavioral features (order frequency, complaints)
- Deploy model as API for real-time predictions
- Monitor model drift over time
- Conduct A/B testing on operational improvements

---

# Tech Stack

- Python
- Pandas
- NumPy
- Scikit-learn
- Statsmodels
- Matplotlib
- Seaborn

---


---
 This project demonstrates applied machine learning, statistical modeling, and business-focused analytics for customer experience optimization.
