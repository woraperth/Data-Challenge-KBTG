# Data-Challenge-KBTG
Data prediction challenges for Techjam Online Audition by KBTG

## Challenges Description
1. Predict NPL (Non-Performing Loan) from credit card information
2. Merchant Prediction
3. Churn Detection with Account’s Activities and Transactions
4. Account Type Prediction from Deposit Transactions
5. Gender Prediction from Credit Card Transactions

## Software used for creating model:
- Jupyter Notebook in local machine
- Jupyter Notebook in DataScientist Workbench

## Programming Tools:
- Python 3
- Python Libraries: Pandas, Numpy, Scikit-learn, XGBoost

## Model file:
- For each question 1-5, there is 1 Jupyter Notebook file for the model named "Wrangling Q_"
- Q1-4 used Scikit-learn 18 (in local machine)
- Q5 used Scikit-learn 17 and XGBoost (in DataScientist Workbench)

### More notes about Q5:
The transaction data is loaded in MySQL, then features are extracted with the following SQL:
```sql
SELECT DISTINCT(card_no),
AVG(txn_amount) AS avg_txn,
MAX(txn_amount) AS max_txn,
MIN(txn_amount) AS min_txn,
MAX(mer_cat_code) AS max_cat_code
CASE 
    WHEN (AVG(txn_hour) >= 9 AND AVG(txn_hour) <= 18)
               THEN 1
               ELSE 0 
    END as pay_when_work,
CASE 
    WHEN SUM(mer_id) > 0
               THEN 1
               ELSE 0 
    END as has_mer_id
FROM transactions t1
WHERE txn_date = '2016-08-03'
GROUP BY card_no
```
and buy_men, buy_women, buy_cosmetic features are extracted in this fashion:
```sql
SELECT DISTINCT(card_no),
1 AS buy_men
FROM transactions
WHERE mer_cat_code IN ('5621', '5631')
```
