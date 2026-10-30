# A Data-Driven Framework for Student Success and Employability Analytics

An end-to-end higher education Business Intelligence solution built using **Microsoft Excel**, **Power Query**, and **Microsoft Power BI**. The project cleans raw, fragmented student lifecycle records, models them in a Star Schema, and provides interactive executive dashboards to track enrollment demographics, attendance risks, academic performance (CGPA), and campus recruitment outcomes.

---

## 📌 Project Overview
* **Project Title:** A Data-Driven Framework for Student Success and Employability Analytics
* **Dataset Name:** Edu Pulse: Student Academic and Career Analytics Dataset
* **Cohort Size:** 1,000 Students across 7 Academic Departments (CIVIL, CSE, EEE, ECE, IT, MECH, MBA)
* **Tools & Technologies:** Microsoft Excel, Power Query, Power BI Desktop, DAX (Data Analysis Expressions)

---

## 🎯 Business Objectives
* **Data Cleansing & Standardization:** Eliminate missing values, duplicate entries, inconsistent casing, and invalid compensation records.
* **Attendance & Risk Oversight:** Segment attendance trends into operational risk bands (`Good`, `Average`, `Poor`) to flag at-risk cohorts prior to term clearance.
* **Academic Benchmark Tracking:** Monitor departmental CGPA progression and assess institutional scholarship aid coverage.
* **Employability & Career Analytics:** Benchmark placement conversion rates (%), salary tiers (Mean & Maximum CTC in LPA), recruiter hiring shares, and internship-to-job conversion rates.

---

## 🏗️ Repository Structure

```text
MS Excel & Power BI - Mini Project/
│
├── 01_Original_Dataset/
│   └── Edu Pulse - Student Academic and Career Analytics Dataset.xlsx                  # Raw institutional source data
│
├── 02_Cleaned_Dataset/
│   └── Edu Pulse - Student Academic and Career Analytics Dataset - Cleaned.xlsx        # Cleaned and standardized dataset
│
├── 03_Data_Model/
│   ├── Edu Pulse - Student Academic and Career Analytics Dataset - Data Model.jpg      # Star Schema architecture diagram
│
├── 04_Power_BI_File/
│   └── Edu Pulse - Student Academic and Career Analytics Dataset.pbix                  # Master Power BI report
│
├── 05_Dashboard_Reports/
│   └── Edu Pulse - Student Academic and Career Analytics Dataset - Dashboard.pdf       # Multi-page executive PDF report
│
├── 06_Documentation/
│   └── Edu Pulse - Student Academic and Career Analytics Dataset - Documentation.docx  # Full project technical documentation
│
├── .gitignore
└── README.md
```

---

## 🧹 Data Cleansing Transformations (Excel / Power Query)

| Field Name | Data Issue | Cleansing Method / Formula |
| :--- | :--- | :--- |
| **`City`** | Missing and blank location entries | `=IF(ISBLANK(E2), "Unknown", E2)` |
| **`Department`** | Inconsistent text casing | `=UPPER(F2)` |
| **`Family_Income`** | Null / blank income entries | `=MEDIAN(I2:I1001)` followed by `=IF(ISBLANK(I2), $L$2, I2)` |
| **`Present_Days`** | Incomplete daily attendance logs | Derived via `=IF(ISBLANK(D2), ROUND(C2 * $F$1, 0), D2)` using institutional mean ratio |
| **`Practical_Marks`** | Missing laboratory assessment scores | `=IF(ISBLANK(E2), G2 - F2, E2)` |
| **`Participation_Type`**| Blank extracurricular records | Replaced using statistical mode: `=IF(ISBLANK(E2), INDEX(E$2:E$6938, MODE(MATCH(E$2:E$6938, E$2:E$6938, 0))), E2)` |
| **`Company_Name`** | Ambiguous unplaced/placed recruiters | `=IF(I2="Placed", IF(ISBLANK(J2), "Unknown", J2), "Not Applicable")` |
| **`Package_LPA`** | Package values for non-placed students | Set to 0: `=IF(OR(I2="Not Eligible", I2="Not Placed"), 0, K2)` |

---

## 📐 Data Model (Star Schema)

The architecture utilizes `Student_Master` as the central dimension table connected via **1-to-Many (1:*)** single-directional relationships:
* `Student_Master` (1) ───► (*) `Academic_Performance` on `Student_ID`
* `Student_Master` (1) ───► (*) `Attendance_Summary` on `Student_ID`
* `Student_Master` (1) ───► (*) `Career_Readiness` on `Student_ID`
* `Student_Master` (1) ───► (*) `Student_Engagement` on `Student_ID`

---

## 📊 Executive Dashboards

### Dashboard 1: Student Demographics & Academic Performance
*Focus: Enrollment geographic dispersion, gender breakdown by major, admission pathways, scholarship disbursement, academic scores, and attendance risk tiers.*
* **Key KPIs:** 1,000 Total Students | 516 Scholarship Holders (51.6%) | 100% Academic Success Rate
* **Core Visuals:** Geographic Map (City distribution), Pie Chart (Admission Type: 62% Merit vs. 38% Management), Donut Chart (Scholarship Recipient breakdown), Clustered Bar (Gender by Department), Clustered Column (CGPA by Department: 6.97 – 7.07), and 100% Stacked Column (Attendance Tiers: Good, Average, Poor).

### Dashboard 2: Student Engagement and Campus Placement Outcomes
*Focus: Extracurricular club engagement, recruitment conversion rates, salary distribution, recruiter hiring shares, and internship-to-placement pipeline efficacy.*
* **Key KPIs:** 61.3% Career Placement Rate (165 Placed / 269 Eligible) | ₹10.31 LPA Average Salary Package | ₹17.64 LPA Highest Salary Package
* **Core Visuals:** Treemap (Club Participation: E-Cell 758, Coding Club 756, Sports Club 754, Robotics Club 748, NSS 736), Placement Achievement Gauge (61.3%), Company-Wise Package Matrix (Accenture, Amazon, Cognizant, Deloitte, Google, IBM, Infosys), and Internship Domain vs. Placement Outcome Clustered Column Chart.

---

## 💡 Strategic Institutional Insights
1. **Attendance Risk Interventions:** Mechanical (34.1%), CSE (33.5%), and Civil (28.6%) display notable student cohorts with "Poor" (<70%) attendance. Early-warning alerts should be triggered when attendance drops below 75% to prevent potential term clearance issues.
2. **High-Yield Internship Domains:** Internship selection strongly influences placement outcomes. Software (67.6% conversion), Core Engineering (63.2%), and Data Analytics (62.5%) produce higher conversion rates than Management internships (54.8%).
3. **Recruiter Diversification:** Hiring is currently centered on major IT and consulting partners (Infosys: 22, Amazon: 20, Accenture: 19, Google: 18). Expanding recruiter outreach into specialized core engineering and product companies can help place the remaining 38.7% eligible candidate pool.

---

## 🚀 How to Run the Project
1. Clone this repository:
   ```bash
   git clone https://github.com/<your-username>/MS-Excel-Power-BI-Mini-Project.git
   ```
2. Open `Edu Pulse - Student Academic and Career Analytics Dataset.pbix` in **Power BI Desktop**.
3. If source paths need updating, click **Transform Data** ──► **Data Source Settings** and link to `Edu Pulse - Student Academic and Career Analytics Dataset - Cleaned.xlsx`.
4. Access detailed technical rules and data dictionary in `06_Documentation/`.

