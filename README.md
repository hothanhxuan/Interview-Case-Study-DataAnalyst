# Interview-Case-Study-DataAnalyst

## 🏢 Company
**Nordic Business Diversity Index (NBDI)**  
Case assignment for **Data Analyst Trainee 2026** position.

---

## 🎯 Objective
Analyze the **educational diversity** of executive management teams using data from  
`Stockholm_Large_NBDI2025.xlsx`, converted to CSV and analyzed in **Google BigQuery**.

---

## 📊 Task Overview
The goal was to evaluate how diverse executive management teams are in terms of **educational background**.  

Main objectives:
1. Clean and standardize company and executive data.  
2. Focus only on **Executive Management** (exclude Board of Directors).  
3. Normalize education fields into the following categories:
   - Business  
   - Law  
   - Engineering  
   - Sciences  
   - Humanities  
   - Medicine  
   - Arts  
   - Other / N/A  
4. Calculate for each company:
   - Number of executives  
   - Number of unique education categories  
   - Share of the most common education field  
   - **Diversity Score** = `1 - Σ(pᵢ²)`, where `pᵢ` is the share of executives per education category.

---

## 🧹 Data Preparation (in BigQuery)
1. Converted the Excel file **`Stockholm_Large_NBDI2025.xlsx`** (sheet `"Data"`) into **`Stockholm_Large_NBDI2025.csv`** using Excel or Python (`pandas.to_csv()`).
2. Uploaded the CSV file to **Google BigQuery** using the **BigQuery Web UI**.  
3. Created a dataset and table named `cosmic-axe-464811-t3.Casestudyinterview.NBDI2025`. 
4. Verified column types (string, integer, etc.) and ensured UTF-8 encoding.

---

## 🧮 Analysis Logic (BigQuery SQL)

Step 1: Clean and categorize education fields (using LOWER() syntax)

Step 2: Count and calculate proportions per company 

Step 3: Compute diversity score per company

---

## 🧰 Tools Used
Platform: Google BigQuery

Language: Standard SQL

Data Source: CSV (converted from Excel: Stockholm_Large_NBDI2025.xlsx / sheet “Data”) 

Output: NBDI2025_casestudy_interview.csv.

---

## 📈 Key Insights
Saab AB shows the highest educational diversity (Diversity Score ≈ 0.82) — 7 distinct education categories among 14 executives.

Wallenstam AB, BioArctic, and Atrium Ljungberg also rank high (≈ 0.78), reflecting balanced mixes of Business, Engineering, and Science backgrounds.

Embracer Group and Alleima exhibit moderate diversity (≈ 0.73).

Companies dominated by Business-only profiles scored lower (< 0.5).

Organizations with executives from multiple disciplines tend to have more balanced perspectives and higher diversity scores.

---

## 🗂 Repository Structure

├── solution_bigquery.sql
├── Stockholm_Large_NBDI2025.xlsx
├── Stockholm_Large_NBDI2025.csv
├── education_diversity_by_company.csv
└── README.md
