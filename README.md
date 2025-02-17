# Customer Lifetime Value Prediction
### for Implementation in Automotive Insurance Marketing

by Amira Afdhal

for Purwadhika JCDS2704

[View the model on streamlit](https://purwadhika-clv-prediction-amira.streamlit.app/)

# Business Problem

#### Introduction
Customer Lifetime Value (CLV) is a critical metric for automotive insurance companies, representing the total revenue a company expects to earn from a customer over their relationship. Predicting CLV helps insurers optimize pricing strategies, personalize marketing efforts, and improve customer retention. By leveraging machine learning models, we aim to enhance CLV prediction accuracy, enabling data-driven decision-making.

#### Stakeholders
Marketing Team at the Automotive Insurance Company: Uses CLV predictions to tailor campaigns and customer engagement strategies.

#### Problem Statements
- Can we predict Customer Lifetime Value of our existing policyholders?
- What characteristics of our policyholders influence their Customer Lifetime Value?
- How can we target our policy offers more efficiently to our policyholders?

#### CLV Formula
In the context of an **automotive insurance company**, **CLV** can be estimated as:

$$
\text{CLV} = (\text{Average Annual Premium} \times \text{Policy Duration}) - \text{Total Expected Claims Cost}
$$

Where:  
- **Average Annual Premium:** The amount a customer pays per year for their auto insurance policy.  
- **Policy Duration:** The average number of years a customer stays with the insurance company.  
- **Total Expected Claims Cost:** The estimated total amount the company expects to pay in claims for that customer.

#### Lack of Policy Duration Data
Since our dataset does not have any columns indicating the duration of a policy for a policyholder, predicting CLV will also effectively predict the policy duration of a policy held by a policyholder.

---
# Data Understanding

| Column Name               | Description |
|---------------------------|-------------|
| Vehicle Class            | Category of the vehicle (e.g., Four-Door Car, Two-Door Car, SUV). |
| Coverage                 | Type of insurance coverage (e.g., Basic, Extended, Premium). |
| Renew Offer Type         | Type of renewal offer given to the customer (e.g., Offer 1, Offer 2). |
| EmploymentStatus         | Employment status of the customer (e.g., Employed, Unemployed, Retired). |
| Marital Status          | Marital status of the customer (e.g., Single, Married, Divorced). |
| Education               | Highest level of education attained by the customer (e.g., High School or Below, Bachelor, Master). |
| Number of Policies      | Total number of policies the customer holds. |
| Monthly Premium Auto    | Amount the customer pays per month for auto insurance. |
| Total Claim Amount      | The total amount claimed by the customer. |
| Income                 | Customer’s annual income in USD |
| Customer Lifetime Value | Total revenue the customer will generate over their lifetime. |

## Data Cleansing

Data cleansing summary:
- **Check for missing values and duplicates:** 618 duplicate rows were dropped, no missing values were found
- **Show descriptive statistics**
- **Change datatypes** of some columns to correct datatypes were appropriate, the categorical columns were all changed to the 'category' dataype and `Number of Policies` was changed to 'int64' since it only takes integer values
- **Check unique values**
- **Check for normality (numerical columns):**  Using the Normal test for normality, we see that none of the columns in our dataset are normally distributed.
- **Check 0 values are true 0:**
   We see that the minimum value for `Income` is 0, and we want to make sure this is a true 0 value and not a missing value. It turns out all of the rows with `Income==0` have `EmploymentStatus=='Unemployed'` so we know that the income is truely 0 and is not a missing value.

# Conclusions and Recommendations

#### Conclusions

After tuning the **Random Forest** model, the performance has improved:  

1. **Higher R-Squared (R²)**: The value increased from 0.654 to 0.679, indicating that the model now explains more variance in the data.  
2. **Lower RMSE**: The Root Mean Squared Error decreased from 4057.41 to 3905.83, suggesting improved prediction error.  
3. **Lower MAE and MAPE**: Both Mean Absolute Error (MAE) and Mean Absolute Percentage Error (MAPE) have slightly improved, showing better overall error reduction.  

Overall, hyperparameter tuning has led to a more reliable model, improving both variance explanation and prediction error.

#### Recommendations for Modelling
- **Increase Number of Features:** Specifically get features regarding **policy duration** and other **policy features**, since feature importance shows it having the greatest influence on CLV.
- **Regression per Cluster:** Since we have already done clustering, CLV prediction might improve if prediction is done on each of the clusters instead of the whole dataset, as it might mitigate the effect of the large error values of the high CLV values and make the smaller CLV predictions have a smaller error.
- **Check for Outliers:** Large positive residuals might be **outliers affecting model performance**.  
- **Try Log Transformation:** If CLV has a skewed distribution, taking **log(CLV)** might stabilize variance.

#### Recommendations Based on Customer Cluster
- **Cluster 0:** could benefit from **discounts or budget-friendly options** to retain customers with lower income.  
- **Cluster 1:** is the **most valuable segment**—consider offering **loyalty programs** or **premium policy upgrades**.  
- **Cluster 2:** has **high income but low CLV**—target them with **upgraded insurance products** to increase their CLV.
