# Azure-Adventure-Works-Data-Engineering-Project

To get hands-on experience with Azure's modern data engineering stack, I created an end-to-end project using the AdventureWorks dataset (sourced from Kaggle). I structured the project using the Medallion Architecture (Bronze, Silver, Gold) and integrated multiple Azure services for ingestion, transformation, and reporting.

---

### 🔹 **1. Data Ingestion (Bronze Layer)**

- I sourced the **AdventureWorks dataset** from [Kaggle](https://www.kaggle.com/datasets/ukveteran/adventure-works), uploaded the cleaned CSV files to my **GitHub repo** (since Kaggle isn’t directly accessible via ADF).
- Used **Azure Data Factory (ADF)** with an **HTTP connector** to pull the data from GitHub.
- The ingested raw files were stored in an **Azure Data Lake Storage Gen2 (ADLS)** account inside a **`bronze` container**.

---

### 🔹 **2. Data Transformation (Silver Layer)**

- From there, I used **Azure Databricks** to read the raw data from the bronze layer.
- Inside Databricks, I performed several transformations and applied business logic. For example:
    - **Data type conversions** (e.g., converting dates, standardizing strings)
    - **Joining sales and customer tables** to enrich order data
    - **Filtering out test/demo records**
    - **Removing duplicates** using `row_number` or `dropDuplicates`
    - **Handling nulls** and standardizing column names for consistency
- The cleaned and enriched data was then stored in the **`silver` container** in ADLS.

---

### 🔹 **3. Semantic Layer (Gold Layer)**

- I created a **serverless SQL pool in Azure Synapse Analytics** to query the transformed data from the silver layer.
- Inside Synapse:
    - I used **`OPENROWSET`** to create **views** on top of the cleaned parquet/csv files from the silver container.
    - Then, I created **external tables in a `gold` schema** pointing to those views — this formed the semantic layer for reporting.

---

### 🔹 **4. Reporting Layer**

- Finally, I connected **Synapse (gold layer)** to **Tableau** for visualization.
- Built a **Tableau dashboard** showing KPIs like:
    - Total sales by product/category
    - Sales trends over time
    - Customer segmentation by geography and revenue
    - Salesperson performance

*"I built an end-to-end Azure data pipeline using ADF for ingestion, Databricks for transformation, Synapse for querying, and Tableau for reporting — following the Medallion Architecture to organize data flow from bronze to gold layers."*
