**Telco Customer Churn Analysis**

**Project Overview**
Customer Churn is one of the biggest revenue risks for subscription-based companies such as telecom companies. Acquiring new customers is significantly more expensive than retaining existing ones, so being able to **predict which customers are likely to churn and why** is critical for business performance.

This project uses the **Telco Customer Churn dataset (from Kaggle)** to:
- Build machine learning models to predict customer churn
- Segment customers into risk groups (Low/Medium/High)
- Translate model outputs into business impact and revenue-saving scenarios
- Provide actionable insights for retention strategies

The project goes beyond pure model performance and focuses on **business decision support**: who is at risk, how to prioritize them, and what the financial impact of churn retention could be.

**Problem Statement**
The telecom company faces ongoing customer churn, which directly impacts revenue and profitability. The business needs to:
1. Identify customers who are most likely to churn
2. Understand which factors drive churn risk
3. Prioritize retention efforts on the highest-risk customers
4. Estimate the **financial impact of churn reduction strategies

This project addresses these needs by building a churn prediction pipeline and converting model outputs into **risk segments and business impact simulations**.

**Data Source**
1. Dataset: **Telco Customer Churn Dataset**
2. Source: Kaggle
3. File used: Telco_Customer_Churn.csv
4. Granularity: One row per customer
5. Key fields include:
   - Customer demographics
   - Contract type and tenure
   - Services used (internet, streaming, security, etc.)
   - Billing and payment methds
   - MonthlyCharges, TotalCharges
   - Target variable: churn (Yes/No)
  
**Data Pipeline**
The end-to-end pipeline implemented in Python:
**1. Data Ingestion**
- Load Telco customer data from CSV

**2. Data Cleaning**
- Standardize and clean the churn target variable
- Coerce numeric fields (MonthlyCharges, TotalCharges, Tenure)
- Handle missing and invalid values
- Drop rows with unusable financial data where necessary

**3. Feature Engineering**
- Tenure features:
  1. tenure_years
  2. tenure_group

- Financial features:
  1. monthly_to_total_ratio

- Service adoption features:
  1. Binary flags for services (OnlineSecurity, TechSupport, etc.)
  2. service_count
  3. high_engagement

- Billing & Payment behaviour
  1. paperless
  2. autopay

- Contract features:
  1. contract_ordinal
  2. short_term_

**Two approaches were compared:**
Balanced recall model: ROC-AUC = 0.839, Recall = 0.55 (better overall discrimination).
High-recall model: ROC-AUC = 0.857, Recall = 0.81 (prioritizes capturing more churners for maximum retention).
Both models are valid - the high-recall model was chosen for business reporting since retention is the top priority.

**Visual Insights: Storytelling with Data**
1. Who is at risk? - Churn Probability Distribution
Shows the spread of churn likelihood across all customers.
Reveals distinct groups: loyal customers (low probability) and a significant cluster at high risk.
Business Value: Enables proactive targeting rather than blanket campaigns.

![Churn Probability Distribution](churn_probability.png)

2. How do we prioritize? - Customer Segmentation by Risk
Customes are grouped into Low, Medium, and High risk categories.
Low-risk customers often require minimal intervention, while high-risk customers demand urgent retention offers.
Business Value: Converts raw probabilities into clear actions for marketing and retention teams.

![Customer Segmentation](customer_segmentation.png)

3. Why does this matter? - Business Impact Simulation
A 5% reduction in churn could retain ~355 customers, translating into ~$219,000 annual revenue saved.
A 10% reduction would save ~710 customers, equal to ~$438,000 annually.
Business Value: Makes the ROI case clear for investing in churn-reduction programs.

![Business Impact Simulation](impact_simulation.png)

**Expected Business Impact**
By implemneting churn prediction and targeted retention:
1. Reduced Churn Rate - Improved long-term profitability.
2. Revenue Savings - Even modest reductions in churn protect hundres of thousands in revenue annually.
3. Smarter Customer Enagement - Focus resources on at-risk customers, avoiding wasted spend on loyal ones.
4. Stronger Lifetime Value (LTV) - Retaining customers longer increases cross-sell and upsell opportunities.
This connects **data science outputs** directly to **business outcomes**

**Tech Stack**
Python: Data cleaning, model building, and visualization.
Pandas, Numpy: Data wrangling.
Scikit-learn: Classification models and evaluation (Logistic Regression, Random Forest, etc).
Matplotlib, Seaborn: Visual storytelling.
Jupyter Notebook: Exploration and Presentation.

**Key Learnings**
High recall models are often preferred in retention use cases, even at the cost of lower precision.
Translating machine learning results into dollar impact is crucial to win business buy-in.
Visual storytelling bridges the gap between technical outputs and executive decision-making.

**How to Run**
Clone the repository and install dependencies:
git clone https://github.com/<your-username>/telco-customer-churn-analysis.git
cd telco-customer-churn-analysis
pip install -r requirements.txt
jupyter notebook Telco_Customer_Churn_Prediction_Model.ipynb

**Takeaway**
This project is more than a churn prediction model, it is a business case:
Who will churn - Prediction
Which customers matter most - Segmentation
Why the business should act - Impact simulation

The analysis helps Telco companies save revenue, improve retention, and boost customer lifetime value. 


