# 🌍 Global Layoffs – Data Cleaning & Exploratory Data Analysis (SQL)

## 📌 Project Overview

This project uses **MySQL** to clean and explore a real-world dataset of global tech layoffs. The goal is to transform raw, messy data into a reliable dataset and then surface meaningful trends and insights through exploratory analysis.

---

## 📁 Files

| File | Description |
|------|-------------|
| `layoffs.csv` | Raw source dataset containing global layoff records |
| `project.sql` | Data cleaning script (Step 1) |
| `project_2.sql` | Exploratory Data Analysis script (Step 2) |

---

## 🧹 Part 1: Data Cleaning (`project.sql`)

The raw data required several cleaning steps before analysis:

1. **Remove Duplicates** – Used `ROW_NUMBER()` with `PARTITION BY` across all key columns to identify and delete exact duplicate rows
2. **Standardize Data** – Fixed inconsistent values (e.g. `Crypto`, `Crypto Currency`, and `CryptoCurrency` unified to `Crypto`), removed trailing punctuation from country names, and converted date strings to proper `DATE` type
3. **Handle Null Values** – Populated missing `industry` values by cross-referencing other rows with the same company name; left numeric nulls intact for accurate aggregation later
4. **Remove Unusable Rows** – Dropped rows where both `total_laid_off` and `percentage_laid_off` were null, as these provided no analytical value

---

## 🔍 Part 2: Exploratory Data Analysis (`project_2.sql`)

With clean data in hand, the analysis explored:

- **Scale of layoffs** – Max layoffs in a single event; companies that laid off 100% of staff
- **Company-level totals** – Which companies had the highest total layoffs overall
- **Geographic breakdown** – Layoffs by city/location and by country
- **Industry trends** – Which sectors were hit hardest
- **Funding vs. shutdown** – Companies that raised significant capital yet still went under (e.g. Quibi raised ~$2B)
- **Year-over-year trends** – Annual layoff totals from the dataset's date range
- **Top 3 companies per year** – Used `DENSE_RANK()` window function to rank companies by layoffs within each year
- **Rolling monthly totals** – Cumulative layoff count over time using a CTE + window function

---

## 🛠️ Tools Used

- **MySQL** – All querying, cleaning, and analysis
- **CTEs & Window Functions** – `ROW_NUMBER()`, `DENSE_RANK()`, `SUM() OVER()`

---

## 💡 Key Findings

- The **United States** led all countries in total layoffs by a significant margin
- The **Consumer** and **Retail** industries saw the highest cumulative layoffs
- Several well-funded startups (raising hundreds of millions) still laid off 100% of staff
- Layoff volume peaked in certain years, visible through the rolling monthly totals query

---

## 🚀 How to Run

1. Import `layoffs.csv` into a MySQL schema named `world_layoffs`
2. Run `project.sql` to clean the data and create `layoffs_staging2`
3. Run `project_2.sql` to explore the cleaned dataset
