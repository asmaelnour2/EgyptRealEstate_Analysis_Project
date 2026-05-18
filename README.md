# 🏢 Egypt Real Estate End-to-End Data Engineering & BI Project

An end-to-End Data Engineering and Business Intelligence platform built to extract, clean, model, and visualize over **19,000+ real estate listings** in Egypt. The project transforms raw, unformatted scraped web data into a fully optimized corporate Data Warehouse using a SQL Server **Star Schema**, culminating in a dynamic, high-performance **Power BI Dashboard** for strategic investment insights.

---

## 📌 Project Architecture & Pipeline

The project follows a standard 4-tier data architecture pattern:
1. **Bronze Layer (Raw Data):** Initial exploratory data analysis (EDA) on raw scraped CSV files.
2. **Silver Layer (Data Cleaning & Transformation):** Processing and Feature Engineering via Python (Pandas/Regex).
3. **Gold Layer (Data Warehouse):** Implementing a structured relational Star Schema database inside Microsoft SQL Server.
4. **BI Analytics (Semantic Layer):** Developing interactive, automated executive reports using Power BI Desktop.

---

## 🚀 1. Data Exploration & Insights (EDA)
- **Initial Dataset Size:** 19,924 raw listing records.
- **Key Challenges Identified:**
  - Critical metrics like `price`, `size`, `bedrooms`, and `bathrooms` were stored as dirty text fields wrapped with strings/commas.
  - The `location` field was bundled into a single messy text string containing various hierarchical levels.
  - High missing value ratio (~72.6%) discovered in the `down_payment` column. By cross-referencing metrics, a crucial business insight emerged: the majority of listed properties were marked for **Cash payment**, naturally rendering the down payment column redundant.

---

## 🧼 2. Data Cleaning & Feature Engineering (Python)
Using Python (`Pandas`, `NumPy`, `Re`), data was systematically cleaned and filtered into a finalized subset of **19,385 pristine rows**:
- **Numeric Normalization:** Extracted metrics from text strings and parsed `price` and `size_sqm` into analytical decimal types.
- **Geographical Parsing:** Split single combined location text strings into unified standalone columns: `governorate` and `city`.
- **Advanced Feature Engineering:** Engineered flags from textual descriptions to isolate highly demanded luxury metrics such as `has_maid` room flag and `is_studio` architectural apartment layout.
- **Data Integrity:** Dropped invalid rows, achieving an exceptionally high data retention rate of 97.3%.

---

## 🗄️ 3. Data Warehousing & Modeling (SQL Server)
To ensure extreme report performance, the cleaned data was migrated into an enterprise-level relational **Star Schema** within **Microsoft SQL Server**. 

### Database Schema Design:
- **`fact_real_estate` (Fact Table):** Houses primary numerical metrics (`price`, `size_sqm`, `bedrooms_count`, `bathrooms_count`) along with relational foreign keys.
- **`dim_locations` (Dimension):** Normalized lookup containing geography granularities (`Governorate`, `City`).
- **`dim_properties` (Dimension):** Contains property profiles (`Property Type`, Luxury flags like Studio/Maid).
- **`dim_payments` (Dimension):** Standardized lookup for payment behaviors (`Cash` vs. `Installment`).
- **`dim_date` (Dimension):** Full comprehensive time-series mapping derived directly from the listing timestamps.

---

## 📊 4. Interactive Power BI Dashboards
The Power BI semantic layer connects directly to the SQL Server Data Warehouse. Leveraging a sleek, modern **Dark Theme Layout**, the application features fluid navigation menus spanning three comprehensive reporting chapters:

### 🗂️ 1. Welcome Page (Gatekeeper)
- An elegant, interactive corporate cover interface designed for clean application entry, containing integrated dynamic action buttons linking seamlessly to specific sub-reports.

### 📈 2. Overview Insights (The Big Picture)
- **KPI Metrics Cards:** Highlights total market volume (19.3K listings), an average market price baseline of 14.86M EGP, and an overall mean size metric of 205 SQM.
- **Properties by Payment Method (Donut Chart):** Visualizes payment mechanics, showcasing the sheer dominance of cash transactions across active listings.
- **Available From Trend (Area Time-Series Chart):** Maps market seasonality, showing massive surges in listings during the Q2/Q3 summer months.

### 🏢 3. Property Analysis (Product Deep-Dive)
- **Average Price by Type (Multi-Row Card):** Hierarchically ranks property formats, showing standalone villas dominating the premium spectrum (~36M EGP) down to studio layouts.
- **Volume Shares (Treemap):** Breaks down product shares, proving that standard Apartments and Chalets hold the highest liquidity and market volume.
- **Structural Breakdowns (Matrix/Bar Charts):** Maps out exact bedroom and bathroom counts against pricing curves to capture the highly coveted "3 Bed, 3 Bath" market sweet spot.

### 🗺️ 4. Location Analysis (Geographical Matrix)
- **Governorate Volumes (Horizontal Bar Chart):** Pinpoints the economic focus, proving Cairo dominates market activity, followed directly by coastal expansion in Matrouh (North Coast) and Giza.
- **City Densities (Column Chart):** Deep-dives into urban hotspots, capturing rapid expansion clusters across New Cairo City and regional luxury hubs like Sidi Abdel Rahman.
- **Price vs. Size Multi-Axis Table:** Correlates spatial costs, empowering investors to differentiate high-yield seasonal coastal metrics from sustainable multi-generational urban settings.

---

## 🛠️ Tech Stack & Skills Utilized
- **Languages:** Python (Pandas, Re, NumPy, SQLAlchemy), SQL (T-SQL, Schema Design).
- **Database Engine:** Microsoft SQL Server (Data Modeling, Relationships, Integrity Constraints).
- **BI Visualization:** Power BI Desktop (DAX, Power Query, Advanced Navigation UI/UX).
- **Engineering Disciplines:** Extract-Transform-Load (ETL Pipelines), Relational Star Schema Modeling, Strategic Business Intelligence.

---
## 📂 Repository Structure
```text
├── Data/
│   └── egypt_real_estate_listings.csv     # Raw Scraped Dataset (Bronze Layer)
|   └──  final_cleaned_real_estate.csv
├── Notebooks/
│   ├── exploration.ipynb                  # Initial EDA Notebook
│   ├── cleaning.ipynb                     # Silver Layer Transformation Logic
│   └── sql.ipynb                          # SQL Data Warehouse Creation Script
├── Dashboard/
│   └── RealestateDashboard.pbix           # Compiled Interactive Power BI Report
└── README.md
