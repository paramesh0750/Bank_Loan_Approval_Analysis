# 🏦 Bank Loan Approval Analysis – Power BI Dashboard

An interactive **Power BI** dashboard that analyses bank loan applications end to end: application volume, approval and rejection trends, loan amounts by product, customer credit risk, and how long loan processing takes.

---

## 📌 Project Overview

Banks need to know *how many* loans they receive, *how many* get approved, *which products* drive the most value, and *how efficiently* applications are processed. This project models a retail bank's loan data across seven related tables and presents the key answers in a single, filterable dashboard page: **Loan Approval Dashboard**.

## 🎯 Objectives

- Track overall loan application volume and approval rate
- Compare loan products by number of applications and total amount
- Understand the credit profile of applicants
- Monitor processing efficiency (average days to a decision)
- Let users slice the data by date, loan type, status, employment and gender

## 📊 Dashboard Contents

### KPI Cards
| KPI | Description |
|---|---|
| **Total Customers** | Distinct customers in the dataset |
| **Total Applications** | Distinct loan applications |
| **Approval Rate** | Approved loans ÷ total applications |
| **Total Loan Amount** | Sum of requested loan amounts |
| **Avg Processing Days** | Average days taken to process a loan |

### Visuals
| Visual | Purpose |
|---|---|
| Donut chart | Loan applications by status (Approved / Rejected) |
| Clustered column chart | Number of applications by loan type |
| Bar chart | Total loan amount by loan type |
| Pie chart | Applicants by credit status (Good / Average / Low) |

### Slicers (Filters)
`Application Date` · `Loan Type` · `Loan Status` · `Employment` · `Document Status`

## 📈 Key Insights (from the current data)

- **40** loan applications from **30** customers, totalling **₹18.6M** in requested amount
- **70% approval rate** (28 approved, 12 rejected)
- **Home Loans** are the largest product by both count (11) and value (₹7.6M), followed by Business Loans (₹4.7M)
- Credit profile: **19 Good**, **8 Low**, **3 Average**
- Average processing time is **4.3 days**
- Applications cover **1 Jan 2026 – 14 Feb 2026**

> Figures reflect the sample dataset bundled with the report and will change if the data is refreshed.

## 🗂️ Data Model

Data is loaded from an Excel workbook (`Bank_Loan.xlsx`) with seven sheets:

| Table | Key Columns |
|---|---|
| **Customer** | Customer_ID, Name, Gender, Age, Income, Employment, Location |
| **Credit** | Credit_ID, Customer_ID, Credit_Score, Existing_Loans, Credit_History, Credit_Status |
| **Loan** | Loan_ID, Customer_ID, Loan_Type, Loan_Purpose, Loan_Amount, Loan_Term_Years, Application_Date, Loan_Status |
| **Loan_Processing** | Processing_ID, Loan_ID, Decision_Date, Processing_Days, Processing_Status, Remarks |
| **Loan_Payment** | Payment_ID, Loan_ID, Payment_Date, Payment_Amount, Payment_Status, Payment_Method |
| **Document** | Document_ID, Loan_ID, Document_Type, Document_Status, Verification_Date |
| **Property** | Property_ID, Customer_ID, Property_Area, Property_Type, Property_Value, Property_Status |

### Relationships
- `Customer` 1 : 1 `Credit` (Customer_ID)
- `Property` 1 : 1 `Credit` (Customer_ID)
- `Loan` M : 1 `Credit` (Customer_ID)
- `Loan_Processing` 1 : 1 `Loan` (Loan_ID)
- `Document` M : 1 `Loan` (Loan_ID)
- `Loan_Payment` M : 1 `Loan` (Loan_ID)

## 🧮 DAX Measures

```DAX
Total Customers = DISTINCTCOUNT(Customer[Customer_ID])

Total Applications = DISTINCTCOUNT(Loan[Loan_ID])

Approval Rate =
DIVIDE(
    CALCULATE(
        DISTINCTCOUNT(Loan[Loan_ID]),
        Loan[Loan_Status] = "Approved"
    ),
    DISTINCTCOUNT(Loan[Loan_ID])
)

Total Loan Amount = SUM(Loan[Loan_Amount])

Avg Processing Days = AVERAGE(Loan_Processing[Processing_Days])
```

## 🛠️ Tools & Skills Used

- **Power BI Desktop** – data modelling and visualization
- **Power Query** – importing and typing data from Excel
- **DAX** – KPI measures
- **Data modelling** – star-style relationships across related tables

## 🚀 How to Use

1. Clone or download this repository.
2. Open `Bank_Loan_Project.pbix` in **Power BI Desktop**.
3. If prompted, update the data source path: **Home → Transform data → Data source settings**, and point it to your local copy of `Bank_Loan_final.xlsx`.
4. Click **Refresh**, then use the slicers to explore the data.

## 🖼️ Dashboard Preview

<img width="1662" height="777" alt="image" src="https://github.com/user-attachments/assets/e305710f-f143-4f07-99f5-1c3ad74f4e95" />




## 🔮 Future Improvements

- Add trend analysis by month and quarter
- Include repayment analysis from `Loan_Payment` (paid vs. overdue)
- Analyse rejection reasons using processing remarks
- Add risk segmentation by credit score and income
- Publish to Power BI Service with scheduled refresh

## 👤 Author

Paramesh D
[GitHub](https://github.com/paramesh0750/Bank_Loan_Approval_Analysis.git)

---
