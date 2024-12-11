# data-analyst
Below is the overview of the AWS projects completed

# Project 1: Descriptive Analysis
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



 
    
  - Descriptive Statistics
  - Data Visualization
  - Survival Analysis
  - Insights and Findings
  - Recommendations
- Tools and Technologies
- Deliverables
  
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


