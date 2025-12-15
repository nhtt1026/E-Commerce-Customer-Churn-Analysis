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

The Decision Tree model segments customers into clear risk groups with materially different churn probabilities. These segments translate directly into actionable retention strategies for ABC E-Commerce.

<img width="2826" height="1496" alt="image" src="https://github.com/user-attachments/assets/7ad82f5b-8c80-430e-b623-c49f28b0f279" />

### High-Risk Segments (Immediate Action Required):

#### 1. Segment A: Service & Logistics Failure (Node 11) - Tenure < 1.5, Complain ≥ 0.5, WarehouseToHome ≥ 18:

<img width="1324" height="382" alt="image" src="https://github.com/user-attachments/assets/794b2c48-78f5-4c4e-ab99-cae83f0a86a8" />

- **Churn Probability:** **92.45%**  
- **Insight**: New customers who experience both service issues and long delivery distances almost always churn. This segment represents the most critical breakdown in the early customer journey.  
- **Business Implication**: Should prioritize rapid complaint resolution, clear delivery SLA communication, and recovery incentives to prevent immediate customer loss.

#### 2. Segment B: New Customers (Node 9) - Tenure < 1.5, NumberOfAddress ≥ 5.5, No complaint:

<img width="1546" height="388" alt="image" src="https://github.com/user-attachments/assets/c40a0a62-3d99-4154-a7be-8efcfa30fbb3" />

- **Churn Probability:** **68.42%**  
- **Insight:** These customers churn despite no reported service issues, suggesting low commitment and comparison-shopping behavior rather than dissatisfaction.  
- **Business Implication:** Retention efforts should focus on differentiated value, pricing transparency, and loyalty benefits instead of service recovery tactics.

### Low-Risk Segment (Retention Budget Protection):

#### 3. Segment C: High-Value Loyal Customers (Node 7) - Tenure ≥ 1.5, HighValue ≥ 0.5:

<img width="1414" height="350" alt="image" src="https://github.com/user-attachments/assets/2163c37d-5d08-4877-b5ba-002e76d956c5" />

- **High-Value Segment:** **0% Churn Probability**  
- **Insight:** Established high-value customers show near-zero churn and represent the core revenue base of the business.  
- **Business Implication:** Avoid unnecessary discounting. Focus on experience stability, priority support, and protection from service degradation.

### Key Takeaway:

Customer churn at ABC E-Commerce happens mainly in the early stage of the customer journey.  
It is driven by **poor service experience, delivery issues, and weak customer loyalty status.**

The Decision Tree shows where the ABC E-Commerce should focus its efforts:
- Respond quickly when new customers face service or delivery problems
- Use clear value and loyalty incentives to retain low-commitment shoppers
- Protect high-value customers by maintaining a reliable and consistent shopping experience

---

# 9) Insights + Recommendations:

ABC E-Commerce’s **churn rate is ~16%**, but it is not evenly distributed. The data shows churn is driven by early lifecycle friction, service issues, and weak loyalty patterns. The Decision Tree adds clear, rule-based segments to operationalize retention actions.

---

### Key Insights:
- **Early churn is the main problem:** customers in **0–3 months** churn at **41.8%**
→ Onboarding + first orders matter most.
- **Complaints strongly predict churn:** churn is **32%** for customers who complained vs **10%** for those who did not
→ Service recovery is a retention lever.
- **Discounting alone doesn’t prevent churn:** ~**76.6%** of customers use coupons and churned users still show ~**80%** coupon usage
→ Coupons must be targeted, not universal.
- **High-risk predictive segments do exist from the Decision Tree:**
  - **Node 11:** Tenure < 1.5 + Complain ≥ 0.5 + WarehouseToHome ≥ 18 → **92.45% Churn**
  - **Node 9:** Tenure < 1.5 + NumberOfAddress ≥ 5.5 + no complaint → **68.42% Churn**
  - **Node 7:** Tenure ≥ 1.5 + HighValue ≥ 0.5 → **~0% Churn**
  
---

### Recommendations:

#### 1) Tenure-based onboarding (first 30–60 days):
- Build a simple lifecycle sequence: Welcome → 1st order reassurance → Delivery tracking clarity → Post-delivery check-in → 2nd-purchase nudge.
- Prioritize customers with **Tenure < 1.5 months** (highest churn branch in the tree).  
**Why:** Early-tenure customers churn at **41.8%**, so improving early experience gives the highest impact.

#### 2) Proactive Service Recovery (Complaint-driven churn prevention):
- Create a “fast lane” for customers who **raise a complaint** (Complain is the #2 predictor).
- Standardize recovery steps:
  - Resolution SLA + proactive follow-up
  - Compensation tied to root cause (delay, wrong item, damaged item)
- This directly addresses the highest-churn path (complaint + logistics friction).
**Why:** Complaint customers churn **~2.2x higher** (69.63% vs 69.63%), and the tree’s highest-risk path hits **92.45% churn** when complaints combine with distance.

#### 3) Logistics friction reduction for long-distance customers:
- For customers with higher **WarehouseToHome** distance:
  - Improve ETA accuracy + proactive delay messaging
  - Offer delivery alternatives where possible (pickup points, flexible slots)
- Treat delivery performance as a churn lever, not only an ops KPI.
**Why:** Logistics friction amplifies churn in the highest-risk segment.

#### 4) Retain low-loyalty new customers with value differentiation:
For customers who churn without complaints but show weak loyalty signals (e.g., many addresses):
- Push loyalty perks (points, free shipping threshold, member benefits)
- Emphasize value clarity (bundles, pricing transparency)
- Optimize for 2nd purchase conversion  
**Why:** Node 9 churn is **68.42%** without service issues → This is a loyalty problem, not a support problem.

#### 5) Replace blanket coupons with targeted offers:
- Use incentives mainly for high-risk new customers and recovery cases to protect the margin.
- Avoid discounting stable high-value customers  
**Why:** Coupon usage is already high across all segments, including churners, so untargeted discounts will leak margin.

---
