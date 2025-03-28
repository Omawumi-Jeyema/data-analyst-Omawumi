# data-analyst-Omawumi 

# Project Title: Design and Implementation of DAP on AWS for the City of Vancouver

## 🗂️ Project Description
This project showcases the design and implementation of a Data Analytics Platform on AWS for the City of Vancouver (COV). The platform will be used to perform descriptive analysis, starting from data ingestion, processing, analytics, storage, and data summarization, leveraging AWS solutions offered through the AWS console. Additionally, the DAP is expected to leverage key attributes of the AWS space, such as dynamic scalability, availability, and self-tailored cost-effectiveness and efficiency.

## 🔷 Methodology

i.	Design:  The DAP was designed as requested using Draw.io 

ii.	Data Ingestion: The subject data [City of Vancouver's Workforce Pay Rates and Sex (WPRS)] was ingested into the AWS S3 Raw bucket directly.

iii.	Data Profiling: This ingested dataset (WPRS) was profiled using AWS Glue DataBrew.

iv.	Data Cleaning: The phase transforms the profiled dataset from dirty to clean by removing any errors, such as missing or duplicate data, and structural issues. Output is saved in the AWS S3 Transform Bucket.

v.	Data Catalog:  Using Crawler on AWS Data Glue, a data catalog comprising schema and table location was created for the WPRS dataset to aid connectivity and data analytics.

vi.	Data Summarization: The dataset is summarized using metrics created in AWS Glue and stored in a system-friendly format with multiple partitions and a user-friendly format in a single file in AWS S3 Curated Bucket.

# Data Analytics Platform
## 📌 Objective
To design and implement DAP to support COV’s migration initiative to AWS
## 📊 Descriptive Analysis
Question: What is the average minimum and maximum hourly pay rate for each City of Vancouver’s Job classification?
## 📋 Dataset Overview
The dataset was extracted from City of Vancouver's Open Data Source (2025). It represents a breakdown of the city’s workforce Pay Rates based on the below columns including the male and the female sex designation. It includes 598 rows and 10 columns of data extracted from 2019 to the 2023 City of Vancouver Workforce Payrate information as shown in Table 1:

### Table 1
### 🏷️ Key Columns

| Column              | Description                                |
|---------------------|--------------------------------------------|
| `Year`              | Data ranges from **2019 to 2023**          |
| `ExemptUnion`       | Contains 7 different values (e.g., CUPE 15, Exempt) |
| `Classification`    | 68 different job classifications              |
| `PositionTitle`     | 152 different job titles                      |
| `DataCategory`      | Always "Detail"     |
| `MinimumHourlyRate` | Min: \$0.01, Max: \$75.31, Mean: \$35.18   |
| `MaximumHourlyRate` | Min: \$0.01, Max: \$82.92, Mean: \$40.52   |
| `Female`            | Employee count within each row; Ranges from 0 to 214     |
| `Male`              | Employee count within each row; Ranges from 0 to 561                       |
| `Total`             | Employee count within each row; Ranges from 10 to 584 (sum of Male + Female) |

## 🧩 DAP Design and Implementation
Draw.io was used to illustrate the cloud-based Data Analytics Platform (DAP) built on AWS, optimized for analyzing  COV’s workforce pay rates and gender distribution. The architecture integrates key AWS services such as S3 for data storage, AWS GlueDatabrew and Glue for cleaning, profiling and ETL processes.
### Figure 1. Design of the DAP 
<img width="468" alt="Figure 1  Design of the DAP" src="https://github.com/user-attachments/assets/53e7e69e-f8cd-46f5-9c19-05a4cf46557b" />

Note: Figure 1 represents the DAP for the dataset. The City of Vancouver’s HR Operation Team and the City of Vancouver’s HR end user will have access to the DAP using a specific virtual server (server=HSVS-Oma)- web server.  The COV HR End User and HR Data Team will have direct access to the DAP as shown in Figure 1. All elements in the design, such as the S3 Buckets, ETL pipeline, Catalog, functions, and usage, are explained in detail in the different phases (Steps 1 - 4) below. This design is continually scalable due to AWS’s scalable attributes.

## 🚪 Step 1. Dataset Ingestion
### 📌 Objective 
•	To ingest CSV file of the data into the AWS cloud
### Key AWS Service and Resources  
•	AWS S3 Bucket
### 🧭 Process
•	An S3 bucket titled ‘cov-raw-oma’ was prepared in AWS for the ingestion.

•	A subfolder titled hr was created. This is because the data is attributed to the COV Human Resources E.D.I.O Office.

•	The dataset titled “workforce_payrates_and_sex” in CSV format was uploaded directly into the prepared S3 bucket folder.

### Figure 2: Workforce Pay Rates and Sex CSV File Ingested into AWS S3 Bucket
<img width="468" alt="Figure 2  Screenshot of Ingested CSV file" src="https://github.com/user-attachments/assets/e402725a-95dd-42d2-91c6-5f557a885431" />

Note: Figure 4 shows the completed ingestion of the City of Vancouver’s Government and Finance data set ‘workforce_payrates_and_sex’ into the S3 bucket ’cov-raw-oma’. The path is s3://cov-raw-oma/hr/year=2025/

### ⚖️ Justification
This was done to ingest the data into the AWS cloud storage for easy access, query, collaboration, analytical management, storage, security, and scalability of the WPRS data.

## 🔍 Step 2. Data Profiling
### 📌 Objective 
•	To perform data profiling on the dataset to assess data quality, detect anomalies, and ensure readiness for data cleaning and transformation.
### Key AWS Service and Resources
•	AWS Glue DataBrew
•	AWS S3 Bucket
### 🧭 Process
•	A job with a project named “cov-hr-wrps-prj-oma’ and a dataset ‘cov-hr-wprs-ds-oma’ was created in AWS Glue Data Brew and the ingested dataset (from the S3 bucket- cov-raw-oma) was connected.

•	The data profile was run to create a job profile titled ‘cov-hr-wprs-prf-oma’ as shown in Figure 3.

### 🧾 Dataset Summary
- **Total Rows:** 598  
- **Total Columns:** 10  
- **Total Cells:** 5,980  

### ✅ Data Validity
- **Valid Cells:** 5,980  
- **Missing Cells:** 0  
- **Duplicate Rows:** 0  
- **Valid Rows:** 598  

### 🔢 Column Types
- **Integer Columns:** 4  
- **Float Columns:** 2  
- **String Columns:** 4  

### Figure 3: Overview of Data Profile (cov-hr-ds-prf-oma)

<img width="412" alt="Figure 3  Data Profile Overview" src="https://github.com/user-attachments/assets/195885d8-a7f0-424c-b966-a3c886da5153" />

Note: Figure 5 represents the generated WPRS dataset profile, and the displayed outcome indicates 100% valid cells and 0 missing and duplicate data.

### ⚖️ Justification
Profiling the dataset with AWS Glue DataBrew provided a clear assessment of data quality and structure before proceeding to the cleaning stage. It checked for potential issues such as data type mismatches, outliers, and missing or duplicate values, ensuring a well-informed foundation for effective data preparation.
 
## 🧹 Step 3. Data Cleaning
### 📌 Objective 
To clean the dataset by resolving any missing values, correcting data type inconsistencies, removing duplicates, and standardizing entries to ensure data integrity and consistency for downstream analysis.
### Key AWS Service and Resources
•	S3 Bucket

•	AWS Glue DataBrew
### 🧭 Process
•	Another bucket was created in S3 with the title ‘cov-trf-oma’.
•	Subfolders were created in the AWS S3 buckets. 
•	The already profiled dataset was handled using AWS Glue DataBrew. The identified structural issues were corrected. For example, Exempt/Union was changed EditUnion.
•	The cleaned data was titled ‘cov-hr-wprs-cln-oma’ and set to produce a single user CSV file and multiple Parquet files partitioned according to classification.
•	It was connected to the prepared system and user folders in the S3 bucket “cov-trf-oma”
•	The job was run to generate the required files. 

### Figure 4. Data Cleaning Recipe

<img width="412" alt="Figure 4  Data Cleaning Recipe" src="https://github.com/user-attachments/assets/72b0924c-b86c-4ee5-b62e-beb81c5ef643" />

Note. Figure 4 shows the cleaning recipe which indicates the standardization of the ExemptUnion column for consistency. 

### Figure 5. Successful Cleaning Job

<img width="412" alt="Figure 5  Successful Cleaning Job" src="https://github.com/user-attachments/assets/05faecb2-d008-4fb4-8e5e-5c2ea0b156b4" />

Note. Figure 5 confirms the successful execution of the cleaning job. 

### Figure 5.1. Cleaning Job Output Stored in S3 Bucket (User File)

<img width="412" alt="Figure 5  1  Cleaning Job Output Stored in S3 Bucket_User File" src="https://github.com/user-attachments/assets/94188023-90f1-42c6-a37b-c714d30c0519" />

### Figure 5.2. Cleaning Job Output Stored in S3 Bucket (System Files)
<img width="412" alt="Figure 5  2  Cleaning Job Output Stored in S3 Bucket_System Files" src="https://github.com/user-attachments/assets/ba1c75de-ea76-452b-b391-cdbe319b94d7" />

Note: Figures 5.1. and 5.2. show the cleaned WPRS dataset stored in single and multiple files in the user and system folders in S3 Bucket “cov-trf-oma.”  

### Figure 6. Lifecycle Rule

<img width="412" alt="Figure 5  3  Lifecycle Rule" src="https://github.com/user-attachments/assets/93645985-9097-4a56-95c7-26fa783bff56" />

Note: Figure 6. shows that cost optimization was implemented. That is, after 30 days with no call-up, the WPRS data automatically transitions to the Glacier storage as a cost-efficiency strategy

### ⚖️ Justification
The cleaning of the profiled WPRS dataset was done to improve the consistency and quality of the data before further analysis. A lifecycle rule was added for efficiency. Implementing a lifecycle rule for the cleaned WPRS dataset is a strategic approach to balancing accessibility and cost efficiency. Since payroll records are critical and often accessed by HR in the short term, storing them initially in Amazon S3 Standard ensures high availability and quick retrieval. However, as access frequency diminishes over time, automatically transitioning the data to Glacier storage after 30 days significantly reduces long-term storage costs without compromising data retention. This policy supports both operational needs and sustainable cost management within the data lifecycle.

## 🔖 Step 4 Data Cataloging
### 📌 Objective 
To create an AWS data catalog for the WPRS data that consists of structured schemas for easy connections between the data areas and support consistency.
Key AWS Console Service and Resources
•	AWS S3 Bucket

•	AWS Glue

### 🧭 Process
•	As shown in Figure 11, a new database for the dataset titled ‘cov-data-catalog-oma’ was created.
•	Structured information stored in tables (containing Schema) titled ‘cov_hr_trf_system was also created as an output of running crawler in AWS Data Glue.

### Figure 7. Database Created

<img width="412" alt="Figure 7  Database Created" src="https://github.com/user-attachments/assets/07118951-8c6a-4ac6-ab69-6afa2360fcff" />

### Figure 8. Data Catalog Table

<img width="412" alt="Figure 8  Data Catalog Table Created" src="https://github.com/user-attachments/assets/c0faff44-5dea-4fab-8ea1-ec89540fdca6" />

### Figure 9. Successful Crawler Job Run

<img width="468" alt="Figure 9  Successful Crawler Job Run" src="https://github.com/user-attachments/assets/47a8a442-dd99-4717-beed-dd6e0f451851" />

Note: Figure 7, 8, and 9 illustrate the successful setup of the AWS Glue Crawler process. Figure 7 shows the creation of the target database, Figure 8 displays the generated Data Catalog table containing the inferred schema, and Figure 9 confirms the successful execution of the crawler job.

### ⚖️ Justification

The AWS Glue Crawler was implemented to automatically detect the schema of the cleaned Workfoce Payrates and Sex dataset and catalog it into a defined database and corresponding Data Catalog table. This process eliminates the need for manual schema definition, ensures consistent metadata management, and enables seamless querying through Amazon Athena. By registering the dataset within a structured database and table in the Glue Data Catalog, the data becomes fully discoverable, queryable, and ready for integration with downstream analytics tools such as Athena and QuickSight.



















