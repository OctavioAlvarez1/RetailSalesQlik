# 🛍️ Retail Sales Dashboard - Qlik Sense Cloud

This project showcases a fully interactive dashboard built in **Qlik Sense Cloud** to analyze retail sales data. It provides key insights into sales performance, customer behavior, and product trends.

![Dashboard Overview](images/dashboard-overview.png)

## 📊 Project Overview

The objective was to create a data visualization dashboard for a retail dataset using **Qlik Sense**. The dashboard allows users to explore:

- Total and average sales
- Sales by product line, gender, and customer type
- Sales by city
- Time-based trends
- Ratings distribution

## 🗃️ Dataset

The dataset used is [`Retail Transactions.csv`](./Retail%20Transactions.csv), which contains the following fields:

- `Invoice ID`
- `Branch`, `City`
- `Customer type`, `Gender`
- `Product line`
- `Unit price`, `Quantity`, `Tax 5%`, `Total`
- `Date`, `Time`
- `Payment`
- `cogs`, `gross income`, `gross margin %`
- `Rating`

> 📌 The file is located in the root of this repository for testing and local use.

## ⚙️ Development Process

1. **Upload and Connect Data**
   - File uploaded to Qlik Sense Cloud.
   - Data preview checked for structure and correctness.

2. **Data Formatting**
   - Dates parsed using `Date#()` and `Date()` functions.
   - Time parsed using `Timestamp#()` function.

3. **Custom Load Script**
   ```qlik
   LOAD
       [Invoice ID],
       Branch,
       City,
       [Customer type],
       Gender,
       [Product line],
       [Unit price],
       Quantity,
       [Tax 5%],
       Total,
       Date(Date#(Date, 'DD/MM/YYYY')) as Date,
       Time(Timestamp#(Time, 'hh:mm:ss')) as Time,
       Payment,
       cogs,
       [gross margin percentage],
       [gross income],
       Rating
   FROM [lib://Retail Transactions.csv]
   (txt, codepage is 28591, embedded labels, delimiter is ',', msq);
