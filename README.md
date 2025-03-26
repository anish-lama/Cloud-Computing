# 🚲 Descriptive Analysis of Bikeway Development Trends in the City of Vancouver

## 📌 Project Title:
**Understanding Trends in Bikeway Segment Length and Speed Limits in the City of Vancouver**

---

## 🎯 Objective:
The primary goal of this project is to conduct a **descriptive analysis** of bikeway infrastructure data in Vancouver. Specifically, it examines how the **segment length** and **speed limits** of bikeways—particularly the *"Painted Lanes"* type—have changed over time based on their **year of construction**.

This analysis is powered by the **AWS cloud platform**, leveraging services such as **Amazon S3**, **AWS Glue**, and **AWS Glue Databrew** for scalable data ingestion, transformation, and summarization.

Through this analysis, we aim to identify **data-driven trends** that can help city planners understand the evolution of bikeway infrastructure and support future **transportation planning** decisions, leveraging AWS.

---

## 📂 Dataset Overview:
The dataset includes bikeway infrastructure data from the **City of Vancouver**, containing the following key features:

- `Object ID`: Unique identifier for each bikeway segment  
- `Bike Route Name`: Name of the bikeway as it appears on signage  
- `Street Name`: Name of the street where the segment is located  
- `Bikeway Type`: Type of bikeway (e.g., Painted Lanes, Local Street)  
- `Subtype`: Subclassification of the bikeway (e.g., Paint Buffer Parking)  
- `Status`: Active or Legacy  
- `Street Segment Type`: Road classification (e.g., Arterial, Residential)  
- `Overall Direction`: General direction (e.g., EW, NS)  
- `Bikeway Direction`: Direction of bike travel (One Way, Two Way)  
- `Vehicle Direction`: Vehicle travel direction (One Way, Two Way, Off-Street)  
- `Speed Limit`: Speed limit (km/h)  
- `Surface Type`: Paved or unpaved  
- `AAA Network` & `AAA Segment`: Inclusion in All Ages & Abilities network  
- `W/N Bound Type` & `E/S Bound Type`: Bikeway type by direction  
- `Snow Removal`: If the segment is part of snow removal route  
- `Segment Length`: Length of the segment (meters)  
- `Year of Construction`: Year it became active  
- `Upgrade Year`: Year of last upgrade  
- `Construction Note` & `Notes`: Additional metadata  
- `Geometry (Geom)`: Spatial representation (LineString)  
- `Geo Point 2D`: Geographic coordinates for mapping  

---
### 🖼️ Data Analytics Platform Design
![Data Analytics Platform]([https://github.com/anish-lama/Cloud-Computing/blob/b0d1c8aa6b9610d960a8507c96b54c2f3b6a9f64/Images/DAP%20Design.png](https://raw.githubusercontent.com/anish-lama/Cloud-Computing/refs/heads/main/Images/DAP%20Design.png))
---

## 🧠 Methodology

### 1. Data Collection and Preparation:
- Ingest bikeways dataset via the internet using **AWS services**
- Store raw data in **Amazon S3 (`bikeways-raw-ani`)** organized by year and quarter
- Use **AWS Glue Databrew** for initial data profiling and quality checks

### 2. Data Cleaning:
- Rename columns to **camelCase** for consistency  
- Drop columns with **>50% missing values** (e.g., Construction Note, Upgrade Year)  
- Apply **mode imputation** for categorical null values  
- Save cleaned data in **CSV and Parquet** formats to `bikeways-trf-ani`

### 3. Data Cataloging:
- Use **AWS Glue Crawlers** to generate schema from transformed data
- Create a data catalog database (`bikeways-data-catalog-ani`) for querying

### 4. Data Summarization:
- Create an **ETL pipeline** using **AWS Glue Visual ETL**
- Select fields: `speedLimit`, `segmentLength`, `yearOfConstruction`
- Group by `yearOfConstruction` and compute **averages**
- Add and **convert timestamp** from UTC to `America/Vancouver`

### 5. Data Output:
- Store summarized results in **`bikeways-cur-ani`** curated bucket
- Create **CSV and Parquet** versions in system/user-friendly structure
- Catalog the summary table as **`bike-lst-metrics`**

---

## 🛠️ Tools and Technologies

| Tool | Purpose |
|------|---------|
| **Amazon S3** | Storage for raw, transformed, and curated datasets |
| **AWS Glue Databrew** | Data profiling, cleaning, and transformation |
| **AWS Glue** | Schema generation, ETL pipeline, and Data Catalog |
| **SQL Expressions** | Used for timestamp conversion and transformations |
| **Data Formats** | CSV (User-friendly) & Parquet (System-optimized) |

---

## 📦 Deliverables

- ✅ Cleaned & transformed dataset in **Amazon S3 (`bikeways-trf-ani`)**
- ✅ Summarized analytics dataset showing **average speed limit** & **segment length** per year
- ✅ Structured schema in **AWS Glue Data Catalog**
- ✅ Fully automated **ETL pipeline** for quarterly updates
- ✅ Visual documentation and screenshots for every major step

---

## 🧾 Conclusion

This descriptive analysis project offers a robust and scalable pipeline for exploring the evolution of Vancouver’s bikeway infrastructure—specifically focusing on the *Painted Lanes* bikeways. By analyzing changes in **speed limits** and **segment lengths** over time, the City of Vancouver gains actionable insights to support urban planning and cycling infrastructure decisions.

Leveraging **AWS cloud services** has enabled efficient, automated data processing—from ingestion to summarization—ensuring the system remains flexible and maintainable for future datasets.

---



