# data-analyst
Below is the overview of the AWS projects completed

[Project 1](#project-1-descriptive-analysis-of-employee-remuneration-for-city-of-vancouver)

[Project 2](#project-2-exploratory-data-analysis-for-the-city-of-vancouver)

[Project 3](#project-3-data-analytic-platform-implementation-for-the-city-of-vancouver)

# Project 1: Descriptive Analysis of Employee remuneration for City of Vancouver 
  
- Project Description

  City of Vancouver has many ongoing undertakings concerning its organizational growth as it tries to improve matters of operation and decision making by use of big data. In this context, the construction of a Data Analytic Platform (DAP) is the appropriate way to turn the data into the right and useful information and to provide meaningful insights for the city.

- Project Title

  Key steps include data ingestion, where raw data is collected and securely stored in AWS services S3, data profiling and cleaning, during which data credibility and relevancy are checked; and data pipeline, which creates an efficient way of processing data. The platform has a capability of performing the descriptive analysis for employee remuneration who are earning more than $75,000 for the City of Vancouver

- Objective
  
  **Data Question:** What is the rate of remuneration (earning over $75000) per employees in management role for 2023 within Finance and Planning departments?
- Dataset

  The below figure shows how the data of employees is ingested from Finance and Planning departments for the year 2023.
  
  ![1_D_Vancouver_Remuneration](https://github.com/user-attachments/assets/045dbdd7-9e3d-4c61-90c7-adfc2bc446c4)

- Methodology
  - Data Collection and Preperation
    

    The below figure shows the design diagram of the S3 bucket gov-raw-nmk, which will be holding raw objects. This bucket is residing in Virginia region. The name of the dataset is 
    Employee_Remuneration, which is ingested in year 2024. This is a structured dataset as it has rows and columns. The data is produced by City of Vancouver

    _Design diagram for Employee Remuneration_

    ![2_D_DesignDiagram](https://github.com/user-attachments/assets/82297fd2-c124-44a3-a5fe-8e41f5416031)

    The below figure shows the AWS object which has employees from City of Vancouver  who has remuneration over $7500. It is stored in S3 standard bucket inside the folder     
    ingestion_year=2024. The AWS S3 storage helps in managing data efficiently. It will also be used further in data pipeline, flowing into AWS Glue and AWS Glue Databrew.

    _S3 Object for Employee Renumeration_

    ![3_D_DataIngestion](https://github.com/user-attachments/assets/dce6b76a-9f01-42c3-a398-f7930cfb6bbe)


    As per the below figure, the Lifecycle rule, Move_To_Cheaper_Storage_Class moves the object to Glacier Instant Retrieval for optimizing the cost. As the scope is set for the entire 
    bucket, it considerably reduces the cost when the object is not accessed frequently. It also makes sure that the contents are retrieved on a fast manner.

    _Lifecycle Configuration_

    ![4_D_LifecycleConfig](https://github.com/user-attachments/assets/252a2569-0c79-45a0-a944-c8dce2552c01)

  - Data Profiling
 
    The below figure depicts the design for profiling and cleaning. Firstly, the data will be fetched from gov-raw-nmk bucket and with the help of AWS Glue Databrew, it is run through 
    gov-rem-emp-prj-nmk profiling and gov-rem-emp-job-nmk cleaning processes. Lastly, the data is stored into gov-trf-nmk S3 bucket.

    _Design diagram for Profiling and Cleaning_

    <img width="700" alt="5_D_Design_ProfilingCleaning" src="https://github.com/user-attachments/assets/e808a7e4-96b0-4b37-9cf9-d31a0b6edf22" />

    Based on the overview of the below figure’s data profile, the dataset has total 386 rows and 6 columns. There are no missing cells and duplicate rows. It also shows a positive 
    correlation between remuneration and expenses. Assessing the data like this ensures that it is complete and proper integrity is maintained. This analysis helps in identifying the 
    trends and patterns related to data.

    _Data Profile Overview_

    ![6_D_DataProfile](https://github.com/user-attachments/assets/535ed201-f19c-4258-b954-5cbcd5cda1fa)

    In the below figure, the data is being cleaned using AWS Glue Databrew and is made ready for further processing. The major transformations used in the process are removing white 
    space, formatting the numerical values for decimal precision and replacing the special characters. These are made part of a recipe, where in, the data can be transferred in an 
    automated manner. AWS Databrew makes the process of data cleaning easy and it ensures that data consistency and integrity is met. It also makes the data ready for downstream 
    applications.

    _Data Cleaning_

    ![7_D_DataCleaning](https://github.com/user-attachments/assets/4cee4f5a-273a-4ae4-a593-86420f40aa31)

    The below figure mentions about the job details which processes the dataset gov-rem-emp-nmk and the output is given to S3 bucket in the format of CSV and Parquet. The partitions used 
    are Department and Year. This ensures the querying is carried out in an optimised manner. 

    _Databrew Job details_

    ![8_D_Databrew](https://github.com/user-attachments/assets/0986dd2b-8261-44fd-96fe-f4c8f868e820)

  - Data Pipeline Design
   
    The below figure shows how the processed data is traversing through the ETL (Extract, Transform and Load) pipeline using AWS Glue and how the transformed data is stored in the S3 
    bucket.

   _ Data Pipeline Design_

   ![9_D_DesignPipeline](https://github.com/user-attachments/assets/2b102ebb-81e0-448a-bcc3-37b1695de70c)

    The below figure shows the AWS Glue’s Visual Editor, which calculates the Manager Remuneration Rate of the total number of employees. By using the visual editor, it helps in creating 
    the pipeline in a simplified manner and the calculations are automated. In my case, it was really helpful when I modified the data and the tool picked up the changes with minimal 
    changes.

    _Manager Remuneration Rate Calculation_

    ![10_D_RateCalculation](https://github.com/user-attachments/assets/931da01b-6756-4059-a884-d2d4abd291cf)


    The below figure outlines the AWS Glue, which represents the ETL job gov-emp-etl-nmk, which outlines a visual data pipeline. The dataset is loaded directly from S3 bucket, and it goes 
    through various transformations like dropping columns, taking total employee count and calculate manager remuneration rate. The data processed through the system is then given to two 
    S3 buckets, System and User. The main outcomes involved in the above steps are data processing, consistency in data and the processed data is then stored onto S3 buckets.

    _Employee Remuneration ETL Pipeline_

    ![11_D_ETLPipeling](https://github.com/user-attachments/assets/736a0c8b-0b33-46de-8d1a-dd9e7c4ac451)

    The data is stored in parquet format inside the System folder. The files are stored using a compression mechanism called Snappy; this reduces costs of storage and improves the 
    performance. The files are stored in bocks of processed data along with its timestamp.  Also, user understandable files are stored in the below User directory. The format used will be 
    csv for better human readability.

    _Data Storage in System folder_

    ![12_D_DataStorage](https://github.com/user-attachments/assets/7c27fabf-4ce3-426d-a741-64d774f1a634)

    _Data Storage in User folder_

    ![13_D_Storage_User](https://github.com/user-attachments/assets/2e926833-805b-4543-8f4c-9043d5c19fe3)

[Back to Top](#data-analyst)

# Project 2: Exploratory Data Analysis for The City of Vancouver

- Project Description

  City of Vancouver has many ongoing undertakings concerning its organizational growth as it tries to improve matters of operation and decision making by use of big data. In this context, the construction of a Data Analytic Platform (DAP) is the appropriate way to turn the data into the right and useful information and to provide meaningful insights for the city.

- Project Title

  Key steps include data ingestion, where transformed data is collected and securely stored in AWS services S3, data profiling and cleaning, during which data credibility and relevancy are checked; and data pipeline, which creates an efficient way of processing data. The platform has a capability of performing the exploratory data analysis for employee remuneration who are earning more than $75,000 for the City of Vancouver

- Objective

**Data Question:** What is the remuneration distribution for employees in managerial role in Finance and Planning departments for year 2023?

- Dataset

  As part of data ingestion process, the employees data will be collected from Finance and Planning departments for the year 2023. The average and count of the remuneration will be 
calculated for both the departments.

  _Remuneration data for departments_

  ![2_Remuneration_2](https://github.com/user-attachments/assets/93ef7ad6-1b68-4717-a27c-c0ce2829c8fb)

  - Data Profiling
    
  As profiling is done previously on this dataset, we can reuse the same profiling while doing exploratory analysis.

  _Data Profiling_

  ![3_DataProfile_3](https://github.com/user-attachments/assets/f4d571b7-a468-48aa-ab03-4d9e7e56f6c2)

  - Data Cleaning

  Recipes has been modified for the existing dataset to make changes to the data. New Regular Expressions have been included to incorporate new data. The Regex will be used to change the 
  extra text associated with the title. Doing this will help in grouping the title together, when doing further data processing.

  _Data Cleaning_

  ![4_Data_Cleaning_4](https://github.com/user-attachments/assets/8ba1202f-e21d-4696-a6d3-f0ac14efef8d)

  - Data Pipeline Design
 
    The below figure shows the extraction, transformation and loading of gov-rem-etl-nmk job to process the data related to employee remuneration.

    ![5_Visual_ETL_5](https://github.com/user-attachments/assets/bf4cb6e5-5ffc-4bbd-8b3e-cee18b19fcb9)

    In the extraction phase the employee data is loaded from the S3 bucket. In the transformation phase, firstly, I removed the name column, as this is not required for the exploratory 
    process. This is done through Change Schema mechanism. Secondly, the data is filtered to incorporate only Mangers from Finance department. In the next step, the average of 
    remuneration is calculated and the column is renamed further for better readability. Meanwhile, in the other thread, the managers from Planning department is filtered and the average 
    remuneration of these employees are calculated in the next step. Also, the fields are renamed for better readability and to incorporate the join clause changes. Furthermore, both 
    these data are joined together to compare which mangers from specific department will have more remuneration. Doing this exploratory analysis will help us in determining, which 
    mangers are likely to be paid more based on the departments. Finally, the processed data is stored in S3 buckets System and User, as shown below.

    _User folder_

    ![6_UserStorage](https://github.com/user-attachments/assets/e4e24c76-02d6-4add-82cb-0a57096cce2b)

    _System Folder_

    ![7_SystemStorage](https://github.com/user-attachments/assets/8aba2b50-6b65-4898-8c2c-ec8547e35320)

[Back to Top](#data-analyst)

# Project 3: Data Analytic Platform Implementation for The City of Vancouver

- Project Description

  In this context, the implementation of a Data Analytic Platform (DAP) is the appropriate way to enrich the data, protect, governance and do observance on the data for the city of 
  Vancouver. 
  
- Data Enriching

  The process of enhancing existing information by adding missing or incomplete data is termed Data Enriching. Usually, this process is achieved by making use of external sources. As can 
  be seen from the below figure, the database used to store the data is _cov-gov-datacatalog-nmk_. This is a structured data model, and data is stored in rows and 
  columns. The dataset used is Employee remuneration and expenses, who earns over $75,000 and is generated and owned by the City of Vancouver. Using AWS’s Athena, we have created an SQL 
  query to calculate the maximum remuneration of employees who are from the Finance and Planning department. It can be clearly seen that the maximum remuneration under this category is 
  $3,216,76.16. This data will be further used for reporting purposes and the insights learned from this can be used to make informed decisions in a swift manner.

  _Maximum remuneration of employees_

  ![1_Remunation](https://github.com/user-attachments/assets/bb08dd6e-977f-4c58-985a-c1c5357359f7)


- Data Protection

  As per the recommendation from AWS for data protection, users are responsible for the management tasks and security configuration for the services one uses. The AWS account credentials    has to be protected and individual users has to be set up with AWS IAM Identity center or AWS Identity and Access Management (IAM). There are three main problems   
  that should be considered as part of Data protection, Firstly, the users shouldn’t be allowed to read what they are not supposed to read. This is called Confidentiality problem. 
  Secondly, they are not allowed to change what they are not entitled to, which is termed as Integrity problem. Thirdly, they shouldn’t block the access of good or valid users, which is   
  as Availability problem.
  
  The below figure shows that the backup folders have been created for all the raw, transform and curated buckets.

  _Backups for S3s_

  ![2_Backups](https://github.com/user-attachments/assets/b4404e2a-5ebd-4a95-8da7-92a8faee25ae)

    - Confidentiality Protection

      In Confidentiality protection, a key is generated using the Key Management Service (KMS) and the same is used to encrypt and decrypt while reading, writing and transferring the data.

      _Key Management Service_

      ![3_KMS](https://github.com/user-attachments/assets/cc7da50a-46c2-4c9d-9aa1-cda086b97a26)

      The figure below shows the encryption mechanism used for the gov-raw-nmk bucket.

      _Encryption for S3 raw bucket._

      ![4_Encryption4S3](https://github.com/user-attachments/assets/70a63204-ab22-4cc1-9bcc-2566dfec33e4)

    - Integrity Protection

      As part of the integrity protection of the data, the versioning mechanism is used for the S3 bucket gov-raw-nmk to make sure data can be recovered easily during application     
      failures.

      _Versioning for S3 raw bucket._

      ![5_versioning](https://github.com/user-attachments/assets/c4a50a0e-1c1c-4b47-8178-36a334e3f99c)


    - Availability Protection

      As part of availability protection, the figure below depicts that the data for the gov-raw-nmk bucket is replicated in the US East North Virginia region.

      _Replication Rules for S3 raw bucket_

      ![6_replrules](https://github.com/user-attachments/assets/73ea73e6-a404-4ce0-b588-6d0541990304)

      
- Data Governance

  As part of data governance, one has to ensure that the data is of high quality, that privacy is maintained in data and that personal identification information is protected. Also, the     data should comply with the international rules and regulations. Finally, the data must be protected by maintaining high confidentiality, integrity and high availability. 
  The below figure shows the Visual ETL (Extract, Transform, Load) for the government employees’ data. Based on the uniqueness of the data, it will be stored in either Passed or Failed 
  folder in S3 bucket. This segregation ensures that the data is of high quality and only good data is processed further.

  _Sensitive data protection_

  ![7_sensitive](https://github.com/user-attachments/assets/e21727c4-f31a-45bc-820f-49b27ba2b8fc)

  The extracted and transformed data is loaded onto the Passed folder in S3.

  _Data stored in S3 bucket - Passed_

  ![8_DataStored](https://github.com/user-attachments/assets/99d7da02-a28f-42e5-b63c-983e9253613f)

  The extracted and transformed data is loaded onto the Failed folder in S3.

  _Data stored in S3 bucket - Failed_

  ![9_FailedBucekt](https://github.com/user-attachments/assets/8bc1017f-0804-435e-85f0-3555ec3f70c1)

- Data Observability

  As part of data observability, the data has to be monitored, and appropriate actions have to be taken if there are any flaws found during the process. The below figure depicts the 
  bucket size in bytes of the S3 bucket used to store the employee data of the City of Vancouver.

  _Dashboard for the City of Vancouver_

  ![10_Dashboard](https://github.com/user-attachments/assets/27c91259-ffe0-4784-92fc-b03d71ba73ea)

  The below figure shows the alarm and real-time logs for the government employees data for City of Vancouver.

  _Dashboard for the City of Vancouver – Logs and Alarm_

  ![11_LogsnAlarm](https://github.com/user-attachments/assets/e0e5cf91-416f-4acc-a104-c0c2f598a35f)

  [Back to Top](#data-analyst)
