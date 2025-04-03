# COVID19-DataEngineering-AzureDataFactory


## **Project Overview**
This project processes **COVID-19 data from ECDC** to generate **meaningful insights** using **Azure Data Factory, Azure Databricks, and Power BI**. The data undergoes **ingestion, transformation, and storage in Azure SQL Database** before being visualized for analytics.

## **Objectives**
- Ingest raw COVID-19 data from **ECDC API & Azure Blob Storage**.
- Perform **data cleaning, filtering, and transformations** using **ADF Data Flows & Databricks**.
- Store **processed data** in **Azure SQL Database**.
- Create **Power BI dashboards** for real-time insights.

---

## **Data Sources & Destination**
| **Source**               | **Description** 
|--------------------------|---------------
| **ECDC API**             | Daily COVID-19 case & death reports 
| **Azure Blob Storage**   | Population dataset (Eurostat) 
| **Azure Data Lake Gen2** | Staging area for raw data 

 **Final Destination:** Azure SQL Database

---

## **Technologies Used**
- **Data Integration & Orchestration** → Azure Data Factory
- **Data Transformation** → ADF Data Flows, Databricks (PySpark)
- **Data Storage** → Azure SQL Database, Azure Data Lake Gen2
- **Visualization & Reporting** → Power BI Desktop & Power BI Service

---

## **Solution Architecture**
1️ **Ingestion:** Load data from ECDC API & Azure Blob Storage → Azure Data Lake Gen2

2️ **Transformation:** Clean, filter, aggregate, and pivot data using **ADF Data Flows & Databricks**

3️ **Storage:** Store transformed data in **Azure SQL Database**

4️ **Reporting:** Visualize insights in **Power BI Dashboards**

![](https://github.com/Arch30it/COVID19-DataEngineering-AzureDataFactory/blob/main/project%20snaps/SOLUTION_ARCH.png)

---

## **Data Processing Workflow**

### **1 Data Ingestion**
 **Datasets Ingested:**
- **Cases & Deaths Data**
- **Hospital Admissions Data**
- **COVID-19 Testing Data**
- **Population Data**

 **ADF Pipeline Activities Used:**
- **HTTP Connector** → Fetches data from ECDC API
- **Copy Activity** → Moves data from source to **Azure Data Lake Gen2**
- **Metadata Activity** → Validates data availability
- **Schedule Triggers** → Automates ingestion workflow

---

### **2 Data Transformation**

#### **Cases & Deaths Data Transformation**
- **Filter:** Extracts only European countries
- **Pivot:** Converts cases & deaths into separate columns
- **Lookup:** Maps country names to country codes (ISO 2 & 3-digit codes)
- **Derived Column:** Computes **7-day average & cumulative counts**
- **Sort & Store:** Loads transformed data into **Azure SQL Database**

#### **COVID-19 Testing Data Transformation**
- **Derived Column:** Computes **test positivity rate (%)**
- **Sort & Store:** Orders data before loading into **Azure SQL Database**

#### **Population Data Transformation (Databricks - PySpark)**
- **Filter:** Retains only European population data
- **Aggregation:** Sums population count per country
- **Join:** Combines population data with cases for **per-capita analysis**

![](https://github.com/Arch30it/COVID19-DataEngineering-AzureDataFactory/blob/main/project%20snaps/Screenshot%202025-04-03%20at%2012.21.01%E2%80%AFpm.png)


#### **Hospital Admissions Data Transformation**
- **Conditional Split:** Separates **daily vs weekly** hospital admissions
- **Join:** Merges data with a **calendar dataset** to map reporting weeks
- **Pivot:** Restructures data for easier aggregation
- **Sort & Store:** Saves transformed data in **Azure SQL Database**

![](https://github.com/Arch30it/COVID19-DataEngineering-AzureDataFactory/blob/main/project%20snaps/Screenshot%202025-04-03%20at%2011.36.00%E2%80%AFam.png)

---

### **3 Data Storage (Azure SQL Database)**
 **Final Tables Created:**
- `covid_cases_deaths`
- `hospital_admissions`
- `testing_data`
- `population_statistics`

---

### **4 Reporting via Power BI**

 **Steps to Generate Reports:**
1. **Connect Power BI to Azure SQL Database**
2. **Create Visualizations:** Charts & trend analysis
3. **Publish Report to Power BI Service**
4. **Enable Web Sharing for Stakeholders**

 **Insights Generated:**
- **Total Cases & Deaths Trend (EU Region, 2020)**
- **Hospital & ICU Admissions Breakdown**
- **COVID-19 Test Positivity Rate vs Confirmed Cases**


---

