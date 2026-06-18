# Model Card: D2C Churn Predictor

## Model Details
* **Architecture:** Random Forest Classifier (n_estimators=100, class_weight='balanced')
* **Framework:** scikit-learn (`Pipeline`, `ColumnTransformer`)
* **Version:** 1.0.0
* **Date:** September 2025 (Snapshot Boundary)

## Intended Use
* **Primary Use Case:** To predict the binary probability (0 or 1) that an existing direct-to-consumer (D2C) customer will fail to make a purchase within the next 60 days.
* **Intended Users:** The Marketing and Customer Success teams, to proactively deploy retention workflows (e.g., discount emails, VIP support calls) before the customer abandons the brand.
* **Out-of-Scope Use Cases:** This model is not designed to predict the *monetary value* of future purchases, nor should it be used for inventory forecasting.

## Training Data
* **Source:** Proprietary database of 2,400 historical customer records.
* **Features:** 50 final engineered features covering Demographics (Age, City Tier), Web Behaviour (Sessions, Cart Adds, Inactivity), Support Interactions (Ticket Count, Resolution Time), and RFM metrics (Recency, Frequency, Monetary value).
* **Data Pre-processing:** Handled strictly via a combined Scikit-Learn Pipeline. Missing numeric values are imputed with the median and scaled via `StandardScaler`. Categorical variables are imputed with 'Unknown' and encoded via `OneHotEncoder`. 
* **Leakage Prevention:** A strict date boundary of `2025-09-30` was enforced. Any transactions occurring after this date were strictly excluded from feature generation.

## Evaluation Metrics (Test Set)
* **Accuracy:** 0.7812
* **Precision:** 0.7857
* **Recall:** 0.7333
* **F1 Score:** 0.7586

## Limitations & Ethical Considerations
* **Static Snapshot:** The model was trained on a single static time snapshot. Seasonal buying behaviours (e.g., holiday shopping surges) are not accounted for, meaning the model's accuracy may degrade significantly during Q4.
* **Cold Start Problem:** The model requires historical RFM and web session data to function. It cannot accurately predict churn risk for a customer who made their very first purchase yesterday.
* **Demographic Bias Check:** The model utilizes `age_group` and `gender` in its predictions. While useful for marketing beauty products, these features must be monitored to ensure the model does not inadvertently deny high-quality support services to specific demographic groups.