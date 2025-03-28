# data-analyst-Omawumi 

# Project Title: Design and Implementation of DAP on AWS for the City of Vancouver

# Project Phase 1

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
### ☁️ AWS Management Console Service Used 
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
### ☁️ AWS Management Console Service Used 
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
### ☁️ AWS Management Console Service Used 
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
### ☁️ AWS Management Console Service Used 
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

## Step 5. Data Summarization
### 📌 Objective 
To summarize the data using categorical data and several metrics. 
### ☁️ AWS Management Console Service Used 
•	AWS S3 Bucket

•	AWS Glue
### 🧭 Process
The steps shown in Figure 10. below were followed as follows:
•	Extract WPRS: The prepared data was extracted from the database ‘cov-data-catalog-oma’ and table ‘cov-hr-trf-system’.

•	Change Schema: This was used to drop a column.

•	Filter WPRS: This was used to filter rows. Only rows from 2019 and above were retained.

•	Summarize WPRS: The data was grouped using the categorical column titled “Classification” and aggregated using average minimum hourly pay and average maximum hourly rate to generate metrics.

•	Add date to summarized WPRS: The report date was added to the summarized WPRS from the step above

•	Convert to LTZ: The data added to the summarized WPRS was converted to LTZ (Local time zone) 

•	Prepare to Load: The initial date added was dropped and the LTZ date version was retained. The schema was reviewed, and the titles adjusted to ensure consistency.

•	Load System and Load Users: The steps were done to ensure the file is stored in an easily accessible manner to both users and systems, with the right partitioning and compression or “no compression” for each. The convert to one file option was used to harmonize both.

•	Save and Run: The summarized job was saved and run as shown in Figure 14 below.

### Figure 10: The ETL Pipeline (WorkForcePayRatesAndSex-Summarization)

<img width="412" alt="Figure 10  ETL Pipeline" src="https://github.com/user-attachments/assets/2907f197-8bf4-4b08-8d89-411372684c4c" />

### Figure 11. Successful Job Run of Summarized Data

<img width="412" alt="Figure 11  Successful Job Run of Summarized Data" src="https://github.com/user-attachments/assets/18b0de17-84fb-49e0-8e3e-3bf4b6d377fd" />

### Figure 11.1. Summarized Data Report for Users

<img width="412" alt="Figure 11 1  Summarized Data Report for Users" src="https://github.com/user-attachments/assets/7ad26630-65a9-43e6-acfe-184a582af570" />

### Figure 11.2. Summarized Data Report for System Users.png

<img width="412" alt="Figure 11 2  Summarized Data Report for System Users" src="https://github.com/user-attachments/assets/2063de3c-0933-42c6-83a2-6a8dbcd3bdd5" />

Note Note: The summarized files were saved as Report_Date in the S3 Curated Bucket under metrics for users and metrics for the system, as shown in Figures 11.1 and 11.2. The Report_Date User folder has one output due to the choice of the single output option, while the multiple files option was selected for the system folder

### Figure 12. Automaticaaly Updated Data Catalog Table (Post-Summarization)

<img width="412" alt="Figure 12  Automatically Updatad Data Catalog Tables" src="https://github.com/user-attachments/assets/a39637ad-379c-4e05-8baf-3e4d325f4d17" />

Note: Figure 16 shows an additional table is auto-added to the WPRS data catalog in AWS Glue upon completion of the summarization process.

### ⚖️ Justification

The AWS Glue summarization job was implemented to answer the analytical question: What is the average minimum and maximum hourly pay rate for each City of Vancouver’s job classification? The job groups the cleaned dataset by the categorical column Classification and computes the average values for both MinimumHourlyRate and MaximumHourlyRate. This aggregation simplifies the dataset, enabling efficient querying and visualization of pay rate trends across job classifications in downstream tools such as Amazon Athena and QuickSight.

# ✅ Conclusion
In fulfillment of the Project’s request, this project focused on building a Data Analyst Platform for its Workforce Pay Rates and Sex data management. The pipeline is AWS-based, and key AWS console functionalities such as S3 buckets, AWS Glue and AWS Glue BrewData were used to achieve this as described in the stated steps above. The DAP was structured to ensure efficient data ingestion, availability, accessibility, security, and management, including storage. It also supports querying and analysis. It was used to answer the question, what is the average minimum and maximum hourly pay rate for each City of Vancouver’s Job classification?	The summarization stage effectively answered the question, revealing each the 68 city job classifications and their average minimum and maximum hourly pay rate.


# Project Phase 2

## 🗂️ Project Description

Sequel to the completion of Project Phase 1, Project Phase 2 seeks to leverage the AWS solutions to implement Data Analysis, Governing, Security, and Monitoring components of the AWS DAP Implementation for the City of Vancouver (COV). This submission showcases the steps taken to execute each of these processes and efficiently deploy them according to AWS best practices and well-designed Architecture to achieve the desired results.

## Data Analysis

### 📌 Objectives
•	To query the prepared city of Vancouver’s Workforce Pay Rates and Sex data in order to determine trends and answers to specific descriptive questions.

•	To analyze the WPRS data to derive meaningful, supportive insights for COV’s decision-making and pay rates trends.

### ☁️ AWS Management Console Service and Resources Used
•	AWS Athena
•	AWS S3 Buckets 
•	Aws Data Glue Catalog 

### 🧭 Process

The WPRS dataset, already profiled, cleaned, and cataloged in the Project Phase 1, was queried using Athena. For the querying, three descriptive questions were set and matching SQL queries to derive the answers written as shown in Figures 14.1, 14.2, and 14.3.

### Figure 13. Overview of Data Catalog

<img width="412" alt="Figure 13  Overview of Data Catalog" src="https://github.com/user-attachments/assets/9a716fcc-a5ae-4f67-b2e1-af30af914f15" />

Note: Figure 13 represents the output of running the code: select * from “cov_hr_trf_system” on Athena to view the structured data “cov_hr_trf_system.

### Figure 14.1. Descriptive Question 1

<img width="412" alt="Figure 14 1  Descriptive Question 1" src="https://github.com/user-attachments/assets/07486b74-35bf-4199-ad06-829d82096c2e" />

Note: Business question No 1 addresses the descriptive question, What is the average minimum pay rate per hour in the City of Vancouver? Using the SQL query: select avg(minimumhourlyrate) as minimumhourlyrate_avg from "cov_hr_trf_system" limit 50; The minimum hourly rate is $35.184 in the city of Vancouver is $35 based on the queried data.

### Figure 14.2. Descriptive Question 2

<img width="411" alt="Figure 14 2  Descriptive Question 2" src="https://github.com/user-attachments/assets/03a7f0a9-2b1d-426e-ba30-ce2fba84779b" />

Note: Business question No 1 addresses the descriptive question, What is the average minimum and maximum hourly pay rate for each Exempt / Union?
Using the the SQL query: select exemptunion, avg(maximumhourlyrate) as maximumhourlyrate_avg, avg(minimumhourlyrate) as minimumhourlyrate_avg from "cov_hr_trf_system" group by exemptunion;

### Table 2. Results from Descriptive Question 2

| # | ExemptUnion             | MaximumHourlyRate_Avg | MinimumHourlyRate_Avg |
|---|--------------------------|------------------------|------------------------|
| 1 | Firefighters Un         | 67.0318                | 55.8595                |
| 2 | IATSE                   | 39.162                 | 39.162                 |
| 3 | IBEW Tech & Ins         | 50.28                  | 47.7625                |
| 4 | CUPE 1004               | 34.5601                | 34.3939                |
| 5 | Exempt                  | 59.7589                | 48.3035                |
| 6 | Senior Exempt           | 81.952                 | 65.6610                |
| 7 | CUPE 15                 | 36.6943                | 31.6673                |

Note. Table 2 displays the results from the Athena query. It shows the 7 Union Types and the minimum and maximum hourly pay rates for each.

### ⚖️ Justification

The Athena query was executed to generate a summarized view of average minimum and maximum hourly pay rates across different union classifications within the City of Vancouver workforce. By grouping the cleaned dataset by the ExemptUnion column and applying aggregation functions, the query provided clear, comparable metrics for each group. The first Athena query, which calculated the average minimum hourly pay for the entire dataset as $35.184, serves as a baseline for comparing pay levels across union groups. This analysis supports pay structure evaluation, highlights compensation trends, and informs data-driven decisions in HR and workforce planning.


# 🔐 Data Security

### 📌 Objective
•	To ensure the protection, confidentiality, encryption, and availability of the WPRS data within the DAP.

### ☁️ AWS Management Console Service and Resources Used
•	AWS Identity and Access Management (IAM) 
•	AWS Key Management Service (KMS) 
•	AWS S3 Buckets
### 🧭 Process
Security measures were implemented to secure the Workforce sensitive data within the DAP. 

Starting with creating a key using KMS for encryption and decryption. After which, permission was provided for different roles using Lab roles, creating scripts and eventually a policy. 

Additionally, versioning was done for the S3 to improve confidentiality. 

A backup S3 bucket was created, and a replication rule was implemented.

### Figure 15. Key Management Service (KMS)

<img width="412" alt="Figure 15  Key Management Service (KMS)" src="https://github.com/user-attachments/assets/69cd42ce-3920-47c7-9729-d9cc0ef11e72" />

Note. Figure 6 shows the configured KMS for encryption and decryption of the data.

### Figure 16. Implemented Encryption

<img width="412" alt="Figure 16  Implemented Encryption" src="https://github.com/user-attachments/assets/d74b2e96-6123-4ca6-836c-1d4ee41817d6" />

### Figure 17. Implemented Bucket Versioning

<img width="412" alt="Figure 17  Implemented Bucket Versioning" src="https://github.com/user-attachments/assets/ae19f503-0339-49ea-b380-db686ec543b7" />

### Figure 18 Implemented Replication Rule (“cov-wprs-rep-rul-oma”)

<img width="416" alt="Figure 18  Implemented Replication Rule" src="https://github.com/user-attachments/assets/d2fb28c3-d94d-4593-b683-76c7a150b25a" />

Note. Figure 16, 17, and 18 shows the successful encryption, versioning, and replication rule implementation.

























