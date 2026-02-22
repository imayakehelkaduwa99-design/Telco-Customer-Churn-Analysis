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
  2. short_term_contract
  3. high_monthly_in_contract

 - Risk interaction features:
   1. risk_shortterm_highpay
   2. risk_lowservices_highpay

**4. Preprocessing**
- Numeric pipeline: median imputation + standard scaling
- Categorical pipeline: most-frequent imputation + one-hot encoding
- Combined using ColumnTransformer

**5. Modeling**
- Baseline models:
  1. Logistic Regression (class-weight balanced)
  2. Random Forest (class-weight balanced)
- Hyperparameter tuning using cross-validation (GridSearchCV)
- Final model selected based on performance

**6. Evaluation & Outputs**
- Metrics:
  1. ROC-AUC
  2. PR-AUC
  3. Precision, Recall, F1
- Threshold sweep to optimize classification cut-off
- Exported artificats:
  1. predictions.csv
  2. threshold_sweep.csv
  3. metrics.json
  4. ROC and Precision-Recall curves
 
**7. Business Simulation**
- Simulate retention campaigns targeting high-risk customers
- Estimate:
  1. Customers saved
  2. New churn rate
  3. Percentage churn reduction
- Visualize impact with charts

**Business Questions Answered**
This project answers the following key business questions:
1. **Who is at risk of churning?**
   - Predicted churn probabilities identify high-risk customers
  
2. **How should customers be prioritized?**
   - Customers are segmented into **Low/Medium/High** risk groups based on predicyed churn probability

3. **What drives churn risk?**
   - Contract type, service adoption, tenure, and high monthly charges combined with short-term contracts emerge as strong risk indicators.
  
4. **Why does this matter financially?**
   - Simulated retention strategies show how even small improvements in churn reduction can translate into **significant revenue savings**.
  
**KPIS & Metrics Produced**
**Model Performance KPIs**
- ROC-AUC
- PR-AUC
- Precision
- Recall
- F1 Score
- Optimal classification threshold (via threshold sweep)

**Business KPIs**
- Current churn rate
- New churn rate after simulated retention campaign
- Number of customers potentially saved
- Percentage churn reduction
- Risk segmentation distribution (Low/Medium/High)

**Models Used**
- Logistic regression (baseline, class-weighted balanced)
- Random Forest Classifier (baseline + tuned)

Model selection is based on **predictive performance and business relevance**, with emphasis on recall and PR-AUC for churn capture.

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

**Key Insights**
- Short-term (month-to-month) contracts combined with high monthly charges significantly increase churn risk.
- Customers with fewer services and low engagement are more likely to churn.
- High-recall models are more suitable for retention use cases, even if precision is slighly lower.
- Translating ML outputs into **financial impact** is crucial for business adoption.

**Tech Stack**
Python: Data cleaning, model building, and visualization.
Pandas, Numpy: Data wrangling.
Scikit-learn: Classification models and evaluation (Logistic Regression, Random Forest, etc).
Matplotlib, Seaborn: Visual storytelling.
Jupyter Notebook: Exploration and Presentation.

**Recommendations**
- Prioritize retention campaigns on **high-risk segments** identified by the model.
- Focus on:
  1. Month-to-month customers with high monthly charges
  2. Low service adoption customers

- Use churn probabilities to:
  1. Personalise offers
  2. Optimise marketing spend
  3. Improve long-term customer lifetime value (LTV)

**How to Run**
1. Clone the repository:

   git clone https://github.com/imayakehelkaduwa99-design/telco-customer-churn-analysis.git
cd telco-customer-churn-analysis

2. Install dependencies:
   pip install -r requirements.txt

3. Run the notebook or script:
   jupyter notebook Telco_Customer_Churn_Prediction_Model.ipynb

4. Outputs will be saved to:
   /outputs

Including:
1. predictions.csv
2. threshold_sweep.csv
3. metrics.json
4. roc_curve.png
5. pr_curve.png

**Portfolio Note**
This project demonstrates:
1. End-to-end ML pipeline design
2. Feature engineering for business problems
3. Model evaluation and tuning
4. Translating data science into **business impact**
5. Executive-ready insights and visual storytelling

The analysis helps Telco companies save revenue, improve retention, and boost customer lifetime value. 

**Author: Imaya Kehelkaduwa (Analytics and Data Engineering Portfolio)**
