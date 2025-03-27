## Project I: 🚲 Descriptive Analysis of Bikeway Development Trends in the City of Vancouver

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
![Data Analytics Platform](https://raw.githubusercontent.com/anish-lama/Cloud-Computing/main/Images/DAP%20Design.png)

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

## 🧩 Project II: 📊 AWS Data Analytics Platform Implementation for the City of Vancouver

---

## 📌 Project Description:
The City of Vancouver is planning to migrate its data analytics workloads to the **AWS Cloud**. As a data team, we have been tasked with **designing and implementing** a Data Analytics Platform (DAP) that meets the city's operational and analytical requirements.

This project focuses on executing **Phase 2** of the platform development, emphasizing key areas such as:
- 🔍 **Data Analysis**
- 🔐 **Data Security**
- 📏 **Data Governance**
- 📈 **Data Monitoring**

The goal is to leverage services like **AWS Athena**, **AWS Glue**, **S3**, **KMS**, and **CloudWatch** to build a secure, scalable, and governed data analytics pipeline for the city’s bikeways infrastructure data.

---

### 🖼️ Data Analytics Platform Design
![Data Analytics Platform](https://raw.githubusercontent.com/anish-lama/Cloud-Computing/main/Images/DAP2.png)

---
## 🔧 Methodology

### 1. Data Collection
- Retrieved data from the AWS Glue Data Catalog (`bikeways-data-catalog-ani`) using Amazon Athena.
- Queried curated datasets stored in S3 to answer key business questions (e.g., segment length trends, speed limit extremes).

### 2. Data Security
- Implemented encryption on all S3 buckets using **AWS Key Management Service (KMS)**.
- Enabled server-side encryption and bucket versioning to maintain security and recovery options.

### 3. Data Governance
- Built a **data quality pipeline** using **AWS Glue Visual ETL** to assess:
  - Completeness (e.g., segment length coverage)
  - Uniqueness (e.g., object ID integrity)
  - Freshness (e.g., recent upgrade year data)
- Segregated and stored passed and failed records into designated folders in the transform bucket.

### 4. Data Monitoring
- Configured **AWS CloudWatch Dashboards** to monitor:
  - S3 bucket size trends (last 3 months)
  - Job runtime durations
- Set **CloudWatch Alarms** and notifications to alert when thresholds (e.g., bucket size > 500k) are crossed.

---

## 🛠️ Tools and Technologies

- **Amazon Athena** – For running SQL queries on curated data in S3.
- **AWS Glue** – Used for ETL pipelines, schema generation, and data quality checks.
- **AWS Glue Data Catalog** – Centralized metadata store for structured datasets.
- **AWS S3** – Storage for raw, transformed, and curated datasets with encryption.
- **AWS KMS** – Key management for encryption and secure access.
- **AWS CloudWatch** – Real-time data monitoring, dashboarding, and alerts.

---

## 📦 Deliverables

- ✅ SQL-based business insights on bikeway trends (e.g., average segment length, speed ranges).
- ✅ Data encryption and versioning applied to all buckets for secure storage.
- ✅ Governance framework using AWS Glue rules to validate and clean data.
- ✅ CloudWatch dashboard for continuous monitoring and real-time alerts.
- ✅ Screenshots and documentation for all configurations and implementations.

---

## 🧾 Conclusion

This project successfully demonstrates the **implementation of a secure, governed, and scalable AWS Data Analytics Platform (DAP)** for the City of Vancouver. By leveraging services like **Athena, Glue, S3, KMS, and CloudWatch**, we ensured a seamless pipeline—from data query to quality checks and monitoring.

Key deliverables such as real-time dashboards, encrypted storage, and structured querying empower the city’s data team to make faster, smarter infrastructure decisions while maintaining strong data integrity and security practices.

The DAP implementation follows best practices in cloud data management and positions Vancouver to scale and maintain its bikeway infrastructure with confidence.

---

## 🏅 AWS Cloud Foundations Certifications

**Certification:**  
![Certification Image](https://raw.githubusercontent.com/anish-lama/Cloud-Computing/main/Images/AWS%20Cloud%20Foundation%20Certificate.jpeg)

**Badge:**  
![Badge Screenshot](https://raw.githubusercontent.com/anish-lama/Cloud-Computing/refs/heads/main/Images/aws-academy-graduate-aws-academy-cloud-foundations.png)






