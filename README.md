# data-analyst
Below is the overview of the AWS projects completed

# Project 1: Descriptive Analysis of Employee remuneration for City of Vancouver
- Project Description
  City of Vancouver has many ongoing undertakings concerning its organizational growth as it tries to improve matters of operation and decision making by use of big data. In this context, the construction of a Data Analytic Platform (DAP) is the appropriate way to turn the data into the right and useful information and to provide meaningful insights for the city.
  
- Project Title
  Key steps include data ingestion, where raw data is collected and securely stored in AWS services S3, data profiling and cleaning, during which data credibility and relevancy are checked; and data pipeline, which creates an efficient way of processing data. The platform has a capability of performing the descriptive analysis for employee remuneration who are earning more than $75,000 for the City of Vancouver

- Objective
  
  **Data Question: ** What is the rate of remuneration (earning over $75000) per employees in management role for 2023 within Finance and Planning departments?
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
 
    The below figure depicts the design for profiling and cleaning. Firstly, the data will be fetched from gov-raw-nmk bucket and with the help of AWS Glue Databrew, it is run through gov- 
    rem-emp-prj-nmk profiling and gov-rem-emp-job-nmk cleaning processes. Lastly, the data is stored into gov-trf-nmk S3 bucket.

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

  
# Project 2: Exploratory Data Analysis
- Project Description
- Project Title
- Objective
- Dataset
- Methodology
  - Data Collection and Preperation
  - Descriptive Statistics
  - Data Visualization
  - Survival Analysis
  - Insights and Findings
  - Conclusion
- Tools and Technologies
- Deliverables


# Project 3: Diagonostic Analysis
# Project 4: Data Wrangling
# Project 5: Data Quality Control


