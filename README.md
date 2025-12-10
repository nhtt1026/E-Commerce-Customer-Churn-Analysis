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

<img width="1527" height="859" alt="image" src="https://github.com/user-attachments/assets/d72bd859-8346-4321-b85b-ea13e19aeab7" />

* **Overall churn rate ~16%**  
  Indicates a meaningful revenue risk if churn drivers are not addressed.

* **Early churn is a major issue**  
  Customers in their first **0–3 months** churn at **41.8%**, highlighting problems in onboarding and early product experience.

* **Complaints have a huge impact**  
  Churn is **32%** among customers who reported complaints vs **10%** for those who did not.  
  Service dissatisfaction is a major churn trigger.

* **Inactive customers churn faster**  
  Customers who have not purchased in **0–2 days** show **23.3%** churn, which declines steadily with longer recency.  
  Recency is an effective behavioural risk flag.

* **High-value vs regular customers**  
  High-value customers represent **31%** of the base and show stronger loyalty, with longer tenure and better CSAT scores.  
  They are critical for revenue protection and retention focus.

### Customer Segments and Behaviour:

<img width="1527" height="860" alt="image" src="https://github.com/user-attachments/assets/b9141895-296a-4069-b77e-140701059c79" />

### Customer Spending:

* High-value customers generate significantly higher cashback and revenue.  
* Churned customers have the lowest order counts and lowest spending, showing weak retention behaviour before leaving.

### Digital Device and Payment Behaviour:

* The majority of customers prefer **mobile login** and **card-based payments**.  
* There is no substantial disparity across segments, indicating that the core technology experience is stable and not a primary churn driver.

### Product Preferences:

* **Mobile phones** and **laptop accessories** are the top categories across all segments.  
* Churn is highest in the mobile category, where product experience or pricing may be contributing factors.

### Coupon Usage:

* Around **76.6%** of all customers use coupons.  
* Churned customers still show roughly **80%** coupon usage, suggesting that discounting alone does not prevent churn.  
  Campaigns should be targeted, not universal.
  
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

<img width="2826" height="1488" alt="image" src="https://github.com/user-attachments/assets/84da371c-f1d7-44a1-a5fa-f1ec841894df" />

---

### 7) Key Variables in the Decision Tree Model:

<img width="2040" height="522" alt="image" src="https://github.com/user-attachments/assets/9d40f429-d809-465b-be3c-1dda99a3fde7" />

Based on the variable-importance output from the Decision Tree, the key predictors of churn are:

**Tenure:**  
- **Importance:** Train `1.0000`; Validation `1.0000` (highest).  
- **Insight:** Tenure is the dominant driver of churn. Churn is essentially an early-life problem: new customers behave very differently from established ones, so retention strategy must be tenure-based.

**Complain:**  
- **Importance:** Train `0.5345`; Validation `0.5613`.  
- **Insight:** Logged complaints are the second-strongest signal. Customers who raise issues are much more likely to churn, so speed and quality of complaint handling are critical levers.

**HighValueScore:**  
- **Importance:** Train `0.3778`; Validation `0.3715`.  
- **Insight:** The composite value score strongly separates “core revenue” customers from the rest. It should be used to prioritize which at-risk users receive more aggressive retention offers.

**NumberOfAddress:**  
- **Importance:** Train `0.3767`; Validation `0.3618`.  
- **Insight:** Customers using many delivery addresses are structurally more likely to churn, suggesting comparison shoppers / low loyalty. This segment needs clear, differentiated value to stay.

**WarehouseToHome (distance):**  
- **Importance:** Train `0.3240`; Validation `0.3306`.  
- **Insight:** Longer delivery distance meaningfully increases churn risk, especially when combined with complaints. Logistics performance is a direct churn driver, not just a cost center.

**DaySinceLastOrder (recency):**  
- **Importance:** Train `0.3189`; Validation `0.3458`.  
- **Insight:** Recency is a strong behavioural flag. Rising days since last order is an early warning for churn and should trigger re-engagement campaigns.

**SatisfactionScore:**  
- **Importance:** Train `0.2758`; Validation `0.3151`.  
- **Insight:** Lower satisfaction boosts churn even when customers do not complain. Silent dissatisfaction needs to be monitored via surveys and NPS, not only tickets.

**HighValue flag:**  
- **Importance:** Train `0.2388`; Validation `0.2380`.  
- **Insight:** Being tagged as a high-value customer is itself protective. These users churn the least and should be shielded from bad experiences and unnecessary friction.

#### Key Takeaway:

The Decision Tree confirms that **tenure, complaints, value level, and delivery experience** are the main levers behind churn.  
ABC E-Commerce should take actions on on early-tenure customers with complaints, long delivery distance, low satisfaction, or rising inactivity is expected to deliver the largest impact on churn reduction.

### 8) Churn Probability Among Segments:

<img width="2860" height="1560" alt="image" src="https://github.com/user-attachments/assets/b2240b7e-75b0-47a8-8f15-51708971027f" />

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
