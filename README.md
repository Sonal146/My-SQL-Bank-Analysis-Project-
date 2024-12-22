# Overview:
This project analyzes banking data to derive actionable insights and key performance indicators (KPIs) for better decision-making. Using SQL, various queries and aggregations have been implemented to address important business questions. The dataset includes customer details, loan data, repayment statuses, and other financial metrics critical for portfolio management and customer analysis.

The analysis focuses on extracting meaningful trends in lending, customer segmentation, payment behaviors, and geographic performance, which are essential for strategic planning in the banking sector.

![image](https://github.com/user-attachments/assets/076040ce-7c05-422b-abd6-323129de3c31)


# Objectives:
The main objectives of this project are:

To calculate key metrics such as total loan amounts, average interest rates, and repayment statuses.

To identify trends in loan issuance and repayment over time.

To segment customers based on loan grades, verification statuses, and home ownership.

To uncover geographic and categorical patterns in the data, including top loan purposes and state-wise memberships.

To provide a comprehensive view of the bank's portfolio performance for strategic decision-making.

#  Business Questions and SQL Code:

## 4.1 Total Loan Amount
Question: What is the total loan amount issued by the bank?


SELECT 
    CONCAT(FORMAT(SUM(loan_amnt) / 1000000, 0), 'M') AS total_loan_amount
FROM mastertable;

## 4.2 Total Funded Amount
Question: What is the total funded amount by the bank?

SELECT 
    CONCAT(FORMAT(SUM(funded_amnt) / 1000000, 0), 'M') AS total_funded_amount
FROM mastertable;

## 4.3 Total Number of Customers
Question: How many unique customers does the bank serve?

 
    COUNT(DISTINCT member_id) AS total_customers
FROM mastertable;

## 4.4 Average Interest Rate:

Question: What is the average interest rate across all loans?


SELECT 
    CONCAT(ROUND(AVG(int_rate), 2), '%') AS Average_interest_rate
FROM mastertable;

## 4.5 Total Revolve Balance:
Question: What is the total revolving balance of customers?


SELECT 
    CONCAT(FORMAT(SUM(revol_bal) / 1000000, 0), 'M') AS total_revol_balance
FROM mastertable;


## 4.6 Year-Wise Loan Status:
Question: How does the loan amount trend year over year?


SELECT 
    `issue_d - year` AS Year,
    CONCAT(FORMAT(SUM(loan_amnt) / 1000000, 0), 'M') AS Total_loan_amount
FROM mastertable
GROUP BY `issue_d - year`
ORDER BY `issue_d - year`;

## 4.7 Month-Wise Loan Status:
Question: How does the loan amount trend across months?


SELECT 
    `last_pymnt_d - month` AS payment_month,
    CONCAT(FORMAT(SUM(loan_amnt) / 1000000, 0), 'M') AS total_loan_amount
FROM mastertable
GROUP BY `last_pymnt_d - month`
ORDER BY FIELD(`last_pymnt_d - month`,
'January','February','March','April','May','June','July',
'August','September','October','November','December');

## 4.8 Grade and Sub-Grade Wise Loan Amount:
Question: What is the loan amount distribution by grade and sub-grade?

SELECT 
    grade,
    sub_grade,
    CONCAT(FORMAT(SUM(loan_amnt) / 1000000, 0), 'M') AS Loan_Amount
FROM mastertable
GROUP BY grade, sub_grade
ORDER BY grade, sub_grade;

## 4.9 Verification Status and Total Payment:
Question: How do verification statuses impact total payments?

SELECT 
    verification_status,
    CONCAT(FORMAT(SUM(total_pymnt) / 1000000, 0), 'M') AS Total_Payment
FROM mastertable
WHERE verification_status IN ('Verified', 'Not Verified')
GROUP BY verification_status;

## 4.10 Top 5 Loan Purposes by Funded Amount:
Question: What are the top 5 loan purposes by funded amount?

SELECT 
    purpose,
    SUM(funded_amnt) AS total_funded_amount
FROM mastertable
GROUP BY purpose
ORDER BY total_funded_amount DESC
LIMIT 5;

## 4.11 State-Wise Number of Members:
Question: How many members are there in each state?

SELECT 
    addr_state AS State,
    COUNT(DISTINCT member_id) AS Number_of_Members
FROM mastertable
WHERE addr_state IS NOT NULL
GROUP BY addr_state  
ORDER BY Number_of_Members DESC;

