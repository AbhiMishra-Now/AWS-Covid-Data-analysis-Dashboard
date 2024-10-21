# 📊 COVID-19 Data Analytics Dashboard
![293120316-969f6252-c3b5-4c0f-b408-6f650b73f070](https://github.com/user-attachments/assets/64a35a24-4100-40f6-8153-ca07d1e16ba4)



Explore and visualize COVID-19 data insights using **Amazon Web Services (AWS)** and **QuickSight**. This project leverages AWS services to analyze and present key trends related to the pandemic.

## ✨ Features
- **Interactive visualizations** showcasing pandemic metrics.
- Utilization of **AWS services**: RDS, S3, EC2, and QuickSight.
- Comprehensive **data storage**, processing, and dashboard creation.

## 🎯 Objectives
1. **Data Storage Familiarization**: Hands-on learning of AWS services like **Amazon RDS** and **S3**, understanding database creation, dataset storage, and data management.
2. **Data Processing Expertise**: Gain knowledge on processing data using **MySQL** and **AWS EC2**. Tasks included data importation, transformation, and running queries on the COVID-19 dataset.
3. **Cloud Computing Exploration**: Learn cloud computing principles, focusing on AWS and leveraging cloud resources for data analysis and visualization.

## 🚀 Getting Started

### 1️⃣ Data Collection
- Data sourced from **Our World in Data**, covering global COVID-19 metrics.

### 2️⃣ Creating a Table on Amazon RDS (MySQL)
- Log into **EC2** on Amazon Linux and install **MySQL**.
- Create a database: **CREATE DATABASE covid_data;**
- Select the database: **USE covid_data;**
- Create a table named **covid_cases** to store the dataset.
```sql
CREATE TABLE covid_cases (
    iso_code VARCHAR(10),
    continent VARCHAR(50),
    location VARCHAR(100),
    date DATE,
    total_cases INT,
    new_cases INT,
    new_cases_smoothed INT,
    total_deaths INT,
    new_deaths INT,
    new_deaths_smoothed INT,
    total_cases_per_million FLOAT,
    new_cases_per_million FLOAT,
    new_cases_smoothed_per_million FLOAT,
    total_deaths_per_million FLOAT,
    new_deaths_per_million FLOAT,
    new_deaths_smoothed_per_million FLOAT,
    reproduction_rate FLOAT,
    icu_patients INT,
    icu_patients_per_million FLOAT,
    hosp_patients INT,
    hosp_patients_per_million FLOAT,
    weekly_icu_admissions INT,
    weekly_icu_admissions_per_million FLOAT,
    weekly_hosp_admissions INT,
    weekly_hosp_admissions_per_million FLOAT,
    total_tests INT,
    new_tests INT,
    total_tests_per_thousand FLOAT,
    new_tests_per_thousand FLOAT,
    new_tests_smoothed INT,
    new_tests_smoothed_per_thousand FLOAT,
    positive_rate FLOAT,
    tests_per_case FLOAT,
    tests_units VARCHAR(50),
    total_vaccinations INT,
    people_vaccinated INT,
    people_fully_vaccinated INT,
    total_boosters INT...
);
```
### 2.5 Connecting RDS to MySQL Workbench **(Alternative)**
Step 1: Launch **MySQL Workbench** and configure the connection with **EC2 Public DNS**.
Step 2: Create DB connection using Standard TCP/IP over **SSH** and verify connection. ✅

### Step 1: Creating the DB connection

Fill in details:
- Connection Name
- Connection Method: Select 'Standard TCP/IP over SSH'
- Parameters:
  - SSH Hostname: EC2 Public DNS
  - SSH Username: EC2 User
  - SSH Key File: Private Key (xxx.pem)
  - MySQL Hostname: RDS Endpoint
  - Username: RDS Master Username
  - Password: RDS Master Password (Store in Keychain)

Step 4: Testing the Database Connection

- Validate parameters for a successful connection.

Step 5: Management and OS

- Choose SSH login based management.
- Select Operating System, MySQL Installation Type.
  
Step 6: Setting up remote SSH Configuration

Enter EC2 instance details:
- Host Name
- User Name
- SSH Private Key Path
  
**Note: These above steps serve as an alternative / simplifying the process of connecting MySQL Workbench to Amazon RDS via an Amazon EC2 instance.**

### Step 3️⃣: Uploading Files to S3
1. Access Amazon S3 Console

- Log in to your AWS account and navigate to the Amazon S3 service.
2. Create a Bucket (if not already created)

- Click on 'Create bucket'.
- Name your bucket and select the region.
- Click 'Create'.
  
3. Upload File

- Inside the bucket, click 'Upload'.
- Select the 'covid_population.csv' file from your local directory.
- Click 'Upload'.

4. Confirmation
Image area [    ]

- Once uploaded, the file 'covid_population.csv' is now available in your specified S3 bucket. 📂

### Step 4️⃣: Transfer Files Between AWS S3 and AWS EC2. ###
1. Attach AmazonS3ReadOnlyAccess Policy
   - Click "Add permissions" > "Attach policies." to IAM role
   - Filter and attach "AmazonS3ReadOnlyAccess" policy.
  
***Note: Granting "AmazonS3ReadOnlyAccess" allows reading files from S3 to the EC2 instance. 📥***
**Copying Files from S3 to EC2**
1. SSH into the EC2 Instance
   - Access the EC2 instance via SSH.
     
2. Confirm AWS CLI and Role
- Run aws sts get-caller-identity to verify the role and AWS CLI functionality.
  
3. Copy Files from S3 to EC2
- Execute aws s3 <S3_Object_URI> <Local_File_Path> to copy files from S3 bucket to the EC2 instance. 🔄

### Step 5️⃣: Transfer the S3 files to RDS ###
- Load the COVID-19 population data into the covid_cases table:
In my case,
```
mysqlimport --host=database-1.****.us-west-1.rds.amazonaws.com --user=aidan --password=**** --local --fields-terminated-by=',' --fields-enclosed-by='"' covid_data covid_cases s3://covidpopulationdata/covid_population.csv
```
### Step 6️⃣: Creating a Dashboard with QuickSight ###
***I utilized Amazon QuickSight to create a dashboard that displays key metrics and visualizations revolving around cases and deaths of COVID-19 as of December 2023 derived from my MySQL dataset. 📊***
