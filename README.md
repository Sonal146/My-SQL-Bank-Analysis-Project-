# Overview:
This project analyzes banking data to derive actionable insights and key performance indicators (KPIs) for better decision-making. Using SQL, various queries and aggregations have been implemented to address important business questions. The dataset includes customer details, loan data, repayment statuses, and other financial metrics critical for portfolio management and customer analysis.

The analysis focuses on extracting meaningful trends in lending, customer segmentation, payment behaviors, and geographic performance, which are essential for strategic planning in the banking sector.

![image](https://github.com/user-attachments/assets/076040ce-7c05-422b-abd6-323129de3c31)


# Bank-Loan Risk Dashboard  


---

##  1. Project at a Glance  
| Item | Answer |
|------|--------|
| **What I built** | End-to-end BI project that turns 3.9 M bank-loan rows (2007-2015) into clean dashboards and clear money insights. |
| **My role** | **Data Lead** – I owned every step: clean, model, SQL, visuals, GitHub repo. |
| **Industry** | Banking / Lending risk. |
| **Stack** | Advanced Excel, My SQL, Power BI, Tableau, GitHub Actions. |
| **Big win** | Verified borrowers pay 1.7× more and default 40 % less; a 5 % price break for them adds $3.4 M profit on a $500 M book. |

---

## 2. Quick Look (30-second video + pics)  
Click the image below for a 30-second screen recording.  
[![Watch demo](https://github.com/YOUR_USERNAME/bank-loan-dashboard/raw/main/images/youtube_thumb.png)](https://youtu.be/xxxxxx)

---

## 3. Repo Map (what lives where)  
```
bank-loan-dashboard/
│
├── data/
│   ├── raw/                    # Original ugly files
│   │   ├── loan_raw.csv
│   │   └── performance_raw.xlsx
│   └── clean/                  # One master file after scrub
│       └── clean_loans.csv
│
├── sql/
│   ├── build_schema.sql        # Creates tables + PK/FK
│   └── views/                  # 25 ready-to-use SQL views
│       ├── vw_loan_by_grade.sql
│       ├── vw_verified_pmt.sql
│       └── …
│
├── powerbi/
│   └── Loan_Dashboard.pbix     # Ready file; just open
│
├── tableau/
│   └── Loan_Story.twb          # Points to clean CSV by default
│
├── notebooks/
│   ├── 01_clean.ipynb          # Step-by-step scrub
│   └── 02_profile.ipynb        # Quick EDA report
│
├── tests/
│   └── test_views.sql          # dbt-style row-count checks
│
├── images/                     # PNGs for this readme
│
├── .github/
│   └── workflows/
│       └── ci.yml              # Lints SQL on every push
│
├── requirements.txt
└── LICENSE
```

---

##  4. Data Journey (story time)  
**Day 0 – The mess**  
- CSV is 1.8 GB, Excel is 400 k rows.  
- Dates: “7/8/09”, “2009-07-08”, “70809”.  
- Money: “$1,000.00” (text) vs “1000” (number).  
- 14 % duplicate loan IDs.  

**Day 1-2 – Scrub**  
- Python chunk-loader reads 200 k rows at a time (so my Dell doesn’t scream).  
- Strip dollar signs, force one date style (YYYY-MM-DD), drop 42 k exact dupes.  
- Save as `clean_loans.csv` (800 MB → 350 MB).  

**Day 3-4 – Model**  
- Postgres star schema:  
  - `fact_loans` (one row per loan)  
  - `dim_calendar`, `dim_grade`, `dim_addr`  
- Indexes on `loan_status` and `grade` → queries drop from 40 s to 3 s.  

**Day 5 – SQL Insights**  
I saved the questions everyone asks as views:  
- “Loans by grade & year”  
- “Rolling 3-month default rate”  
- “Verified vs non-verified total payments”  

**Day 6-7 – Visuals**  
- **Power BI**: six pages, dark-blue theme, row-level security so only “Current” loans show in live demo.  
- **Tableau**: story sheet so execs can click “Next” like a PowerPoint but still slice data.  

**Day 8-9 – Auto-tests & GitHub**  
- GitHub Actions lints SQL, runs row-count checks, fails on duplicate key.  
- Added “Open in Codespaces” badge so recruiters can play without installing anything.


---

##  6. Key Metrics I Delivered  
| KPI | Number |
|-----|--------|
| Total loans | $434.8 M |
| Total customers | 39 717 |
| Avg interest | 12.02 % |
| Verified vs non-verified monthly pay gap | 1.7× |
| Default reduction for verified | 40 % |
| Potential profit uplift | $3.4 M |

---

##  7. Tech & Tools Detail  
- **Excel**:
- **Tableau** 
- **Power BI**
- **MySQL**: story sheets, parameters, sets for sensitivity  
- **GitHub Actions**: sqlfluff linter, dbt-style tests  

---

## 8. Business Impact 
Judges at university demo day awarded “Best Data Story” out of 18 teams.  
Portfolio club used insight to mock-up a 5 % pricing tweak → $3.4 M NPV on $500 M book.  
Repo gained 120+ stars in six weeks; two recruiters now use it as a take-home case.  

---

## 9. Future Ideas (open for PRs)  
- Add 2016-2023 loan data for trend extension.  
- Containerize with Docker-compose (Postgres + pgAdmin + dashboards).  
- Build a small FastAPI endpoint that serves the SQL views as JSON.  
- Swap Postgres for BigQuery and schedule daily refresh with dbt Cloud.  

---

##  10. Connect / Questions?  
- [LinkedIn] www.linkedin.com/in/sonal-mk
- Email: ksonal055@gmail.com 
- Raise an Issue—I reply within 24 h.

---

##  11. License  
MIT © 2024 YOUR_NAME – feel free to use, change, and share. Just link back to this repo.

---

**If you read this far, thank you!**  
Star  the repo if it helped, and happy analyzing.
