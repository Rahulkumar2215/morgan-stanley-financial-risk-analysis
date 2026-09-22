# Customer Financial Behaviour and Risk Analysis

A Python analysis of 800 bank transactions from 189 customer accounts. I cleaned the data, profiled how customers use their accounts, checked every account for risk warning signs, and ran a hypothesis test on transaction volume and balance.

Note: this is a training dataset from the Internshala Data Science program (Project Set 3). It is labelled as Morgan Stanley data but it is not real customer data from the bank.

## The data

800 transactions across 189 accounts and 180 customers, from January 2023 to June 2024. Each row has the account, date, transaction type (deposit, withdrawal, payment, transfer), amount, balance and a risk score. 2024 only runs to June, so I did not compare the two years as equals.

## Tools

Python, pandas, matplotlib, seaborn, scipy (Google Colab)

## Cleaning decisions

There were no missing values or duplicate rows, but a few things needed judgement:

- The TransactionID column was broken. Only 197 of 800 IDs were unique and the same ID appeared on unrelated transactions, so I kept every row and used AccountID as the key instead of deleting about 600 real transactions.
- 22 transaction amounts were negative, including some deposits. I took the absolute value, since direction is already given by the transaction type.
- 21 account balances were negative. These are real overdrafts, so I kept them.
- The risk score ran from -0.30 to 1.25. It spread past both ends of 0 to 1 evenly, which looks like a standardised score, so I left it unchanged.

## Key findings

- Seven accounts set off three of my four risk flags (overdraft, large withdrawal, high balance swings, high risk score). This is the priority watchlist.
- 21 accounts went overdrawn, each exactly once.
- Money-out was higher than money-in every month, but this comes from three of the four transaction types counting as money-out, not from real customer behaviour.
- High-volume accounts had about 6% higher average balances than low-volume accounts (one-sided t-test, p around 0.04). This is borderline evidence and too weak to base a decision on.
- The measures in this dataset barely move together (balance vs amount correlation of -0.005), which suggests generated data. I flagged patterns that come from the data's structure rather than behaviour.

## Files

- `financial_risk_analysis.ipynb` - the full analysis with outputs and charts
- `morgan_stanley.csv` - the dataset
- `summary_report.pdf` - plain-language summary report with recommendations

## How to run

Install the libraries with `pip install -r requirements.txt`, keep the CSV in the same folder as the notebook, and run the notebook top to bottom. It also runs in Google Colab if you upload both files.
