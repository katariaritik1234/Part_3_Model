# Model Error & Performance Analysis

## 1. Baseline vs. Advanced Model Comparison
Counter-intuitively, our baseline Logistic Regression model marginally outperformed the advanced Random Forest classifier out-of-the-box:
* **Logistic Regression:** 79.17% Accuracy | 75.56% Recall
* **Random Forest:** 78.12% Accuracy | 73.33% Recall

**Why this happened:** The Random Forest likely overfit to the training data. Our dataset is relatively small (2,400 rows) and heavily feature-engineered. Linear models often generalize better on structured tabular data of this size without extensive hyperparameter tuning (e.g., limiting tree depth). 

## 2. Business Cost of Errors (Random Forest)
With our current production model (Random Forest), we must analyse the specific types of errors the model makes on unseen data:

### False Negatives (Missed Churners)
* **Metric:** Our Recall is 73.33%. 
* **Business Impact:** This means we are completely missing approximately **26.6%** of customers who actually end up churning. The model categorizes them as "safe," meaning the marketing team will not send them a retention discount. 
* **Cost:** Lost Customer Lifetime Value (LTV). This is the most dangerous error for our business.

### False Positives (Wasted Budget)
* **Metric:** Our Precision is 78.57%.
* **Business Impact:** When the model tells the marketing team "This person will churn," it is wrong **21.4%** of the time. We are falsely flagging loyal customers as flight risks.
* **Cost:** Wasted promotional budget. If marketing sends a 20% discount to this group, we are needlessly sacrificing profit margins on customers who were going to buy at full price anyway.

## 3. Recommended Next Steps
To improve the model before the next fiscal quarter, Data Science should allocate time for:
1. **Hyperparameter Tuning:** Use `GridSearchCV` to constrain the Random Forest's depth and prevent overfitting.
2. **Threshold Shifting:** Since False Negatives (missing churners) are more expensive than False Positives (wasted discounts), we should artificially lower the model's decision threshold from 0.50 to 0.40 to capture more at-risk customers, sacrificing a bit of precision for a higher recall.