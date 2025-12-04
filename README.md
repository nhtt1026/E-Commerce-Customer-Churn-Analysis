# ABC E-Commerce Customer Churn Analysis

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

- Churn Rate  
- Total Customers  
- Percentage of High Value Customers  
- Average Tenure  
- Average Order Count  
- Average Cashback  
- Customer Satisfaction Score  
- Percentage of Coupon Users  

### Segmentation Dimensions:

- Customer Type  
- Tenure Band  
- Days Since Last Order Band  
- Product Category  
- Preferred Login Device  
- Preferred Payment Mode  

---

## 5) Dashboard Overview:

### Executive Churn Overview:

<img width="2402" height="1432" alt="image" src="https://github.com/user-attachments/assets/f0ba221f-8d73-4053-96f0-7693a0c9b73b" />

### Customer Segments and Behaviour:

<img width="2296" height="1296" alt="image" src="https://github.com/user-attachments/assets/fcbd8639-7570-4e0f-82e3-bac1205020ea" />

---

## 6) Insights and Recommendations:

### Insights:

- Early tenure customers show the highest churn  
- Customers who lodge complaints churn at a significantly higher rate  
- High-value customers generate strong revenue and remain loyal  
- Higher churn risk observed among customers with very recent inactivity  
- The majority of customers use coupons and shop via mobile using card-based payment methods  

### Recommendations:

- Improve onboarding journey and first 3 months engagement  
- Strengthen complaint handling and service recovery programs  
- Utilize recency triggers for timely promotional campaigns  
- Invest in loyalty benefits for high-value customers  
- Continue optimizing the mobile and card experience for higher conversion  

---
