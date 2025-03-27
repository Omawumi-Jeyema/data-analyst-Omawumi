# data-analyst-Omawumi 

# Project Title: Design and Implementation of DAP on AWS for the City of Vancouver

## Project Description
This project showcases the design and implementation of a Data Analytics Platform on AWS for the City of Vancouver (COV). The platform will be used to perform descriptive analysis, starting from data ingestion, processing, analytics, storage, and data summarization, leveraging AWS solutions offered through the AWS console. Additionally, the DAP is expected to leverage key attributes of the AWS space, such as dynamic scalability, availability, and self-tailored cost-effectiveness and efficiency.

## Methodology

i.	Design:  The DAP was designed as requested using Draw.io 

ii.	Data Ingestion: The subject data [City of Vancouver's Workforce Pay Rates and Sex (WPRS)] was ingested into the AWS S3 Raw bucket directly.

iii.	Data Profiling: This ingested dataset (WPRS) was profiled using AWS Glue DataBrew.

iv.	Data Cleaning: The phase transforms the profiled dataset from dirty to clean by removing any errors, such as missing or duplicate data, and structural issues. Output is saved in the AWS S3 Transform Bucket.

v.	Data Catalog:  Using Crawler on AWS Data Glue, a data catalog comprising schema and table location was created for the WPRS dataset to aid connectivity and data analytics.

vi.	Data Summarization: The dataset is summarized using metrics created in AWS Glue and stored in a system-friendly format with multiple partitions and a user-friendly format in a single file in AWS S3 Curated Bucket.

# Data Analytics Platform
## Objective
To design and implement DAP to support COV’s migration initiative to AWS
## Descriptive Analysis
Question: What is the average minimum and maximum hourly pay rate for each City of Vancouver’s Job classification?
## Dataset Overview
The dataset represents a breakdown of the city’s workforce Pay Rates based on the below columns including the male and the female sex designation. It includes 598 rows and 10 columns of data extracted from 2019 to the 2023 City of Vancouver Workforce Payrate information as shown in Figure 1:
1.	Year: Data extraction year
2.	Exempt/Union: Union or exempt status of workforce.
3.	Classification: The classification of the job position titles
4.	PositionTitle: The job position title.
5.	DataCategory: The detail status (level of detail) of each data row
6.	MinimumHourlyRate: The minimum pay rate per hour for each gender according to each classification row.
7.	MaximumHourlyRate: The maximum pay rate per hour for each gender based on the row.
8.	Female: Count of female workforce represented within each row 
9.	Male: Count of the city’s job staff represented within each row 
10.	Total: The total number of females and males.

