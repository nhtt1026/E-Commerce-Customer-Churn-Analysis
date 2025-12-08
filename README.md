## 1) Introduction:

ABC E-Commerce is experiencing an increase in customer churn, which impacts long-term revenue and marketing efficiency.  
This project focuses on transforming a static dataset into an analytical model using Power BI for visualization and SAS Enterprise Miner for churn prediction.  
The goal is to understand who churns and why churn occurs so that the business can improve retention performance.

---

## 2) Objectives:

1. Calculate churn rate and profile active vs churned customers  
2. Identify high-value customers and their contribution to the business  
3. Examine churn drivers, including tenure, complaint status, and recency  
4. Understand behavioural differences between segments, including product channel and coupon usage  

---

## 3) Data Source:

Dataset source: [https://www.kaggle.com](https://www.kaggle.com/datasets/ankitverma2010/ecommerce-customer-churn-analysis-and-prediction?sort=most-comments)

Number of records: ~2500 customers  
1 record equals 1 customer profile

### Key Fields Used:

| Field | Description |
|------|-------------|
| Churn | Indicating whether the customer has left |
| Tenure | Duration of relationship with the platform |
| PreferredLoginDevice | Main device used to access the platform |
| CityTier | Customer location tier |
| PreferredPaymentMode | Primary payment method |
| Gender | Gender of customer |
| HourSpendOnApp | Usage hours per month |
| NumberOfDeviceRegistered | Number of linked devices |
| PreferredOrderCat | Most purchased product category |
| SatisfactionScore | Customer satisfaction rating |
| MaritalStatus | Marital status |
| Complaint | Complaint raised in the last month |
| CouponUsed | Number of coupons used in last month |
| OrderCount | Number of completed orders |
| DaySinceLastOrder | Days since the most recent purchase |
| CashbackAmount | Cashback earned in last month |

---

## 4) Metrics and Dimensions:

### Core Metrics:

- Churn Rate = Churned Customers / Total Customers 
- Total Customers  
- % High-Value Customers
- Average Tenure (months)
- Average Order Count  
- Average Cashback  
- CSAT Score (Customer Satisfaction) 
- % Coupon Users

### Segmentation Dimensions:

- Customer Type (Active – Regular, Active – High Value, Churned – Regular)
- Product Preference
- Payment Mode, Login Device
- Complaint Status
- Days Since Last Order (Recency Bands)
- Tenure Bands

---

## 5) Churn Analysis Dashboard:

### Churn Overview:

<img width="2402" height="1432" alt="image" src="https://github.com/user-attachments/assets/f0ba221f-8d73-4053-96f0-7693a0c9b73b" />

### Customer Segments and Behaviour:

<img width="2296" height="1296" alt="image" src="https://github.com/user-attachments/assets/fcbd8639-7570-4e0f-82e3-bac1205020ea" />

---

## 6) Predictive Modeling (SAS EM):

### Model Objective:
Predict customer churn and identify variables with the strongest influence on churn behaviour.

### Analytical Flow:
- Data Cleaning and Imputation  
- Variable Selection and Transformations  
- Training/Validation Split: **70% training 30% validation**  
- Compute model performance and compare across methods  


### Performance Comparison:

| Model               | Validation Accuracy*        | Validation AUC (ROC)** | Best Use Case                                                | Selected                          |
|---------------------|----------------------------|------------------------|--------------------------------------------------------------|-----------------------------------|
| Neural Network      | **88.8%** (misclass = 0.1124) | ~ 0.95                 | Best predictive accuracy | Considered |
| Decision Tree       | **88.8%** (misclass = 0.1124) | ~ 0.93                 | Interpretability + rule-based actions | ✓ Final Model |
| Logistic Regression | **87.8%** (misclass = 0.1223) | ~ 0.90                 | Baseline benchmark | No |

\* Accuracy = 1 − validation misclassification rate, taken from Fit Statistics.
<img width="2304" height="464" alt="image" src="https://github.com/user-attachments/assets/da3f2249-69ff-4ad3-a464-7f5374ab9569" />

\** AUC values are approximated from the ROC curves; Neural Network shows the highest area under the curve, followed by Decision Tree, then Regression.
<img width="2000" height="1074" alt="image" src="https://github.com/user-attachments/assets/9d493061-d3da-4513-806e-97d435aae0c0" />

**Decision Tree** is selected as the final deployment model due to its strong predictive power and clear interpretability for business stakeholders, while the Neural Network is kept as a supporting model for high-precision churn risk scoring.

<img width="1313" height="708" alt="image" src="https://github.com/user-attachments/assets/070832e5-8545-4119-9e97-70e6b8f84b39" />

---

### Key Churn Drivers Identified:

- **Recent inactivity** — strong leading indicator  
- **Complaint behavior** — dissatisfied users churn quickly  
- **New users with low tenure** — early negative experiences lead to churn  
- **Low purchase and coupon usage** — weak retention habits  

### Business Actions Enabled:

- Early churn alerts for immediate intervention  
- Complaint recovery workflow with retention bonus  
- Recency-based reactivation campaigns  
- High-value customer protection with exclusive offers  

---

## 7) Insights and Recommendations:

### Insights:

- Recently inactive customers show highest churn probability  
- Complaints increase churn likelihood more than tenure alone  
- High-value customers deliver revenue benefits and retain longer  
- Mobile and card payment users dominate purchasing behaviour  
- Coupon usage drives engagement across all segments  

### Recommendations:

- Reinforce onboarding experience within first 3 months  
- Improve customer service resolution to protect at-risk users  
- Trigger reactivation messages at early inactivity stages  
- Maintain loyalty perks for high-value customers  
- Continue optimizing mobile purchase flow  

---

---
