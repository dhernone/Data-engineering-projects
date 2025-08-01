## Tokyo Olympic Data Analytics | Azure End-To-End Data Engineering Project
- **Objective** : Design and implement a scalable, end-to-end data engineering pipeline on the Microsoft Azure platform. The pipeline will ingest, transform, and analyze a publicly available dataset of the 2021 Tokyo Olympics. \
- **Goal** : By having a robust data architecture that provides a clean, prepared dataset for downstream analytics and generates interactive data dashboards for deriving valuable insights into the Olympic Games.
- **Tools mentioned** : Azure Data Factory (ADF) , Azure Data Lake Storage Gen 2 , Azure Databricks and Tableau

### Architecture Diagram & Workflow
**1. Data Ingestion** \
This stage is responsible for reliably extracting the raw data from its source and loading it into a secure, scalable storage layer.

- **Data Source**: The project utilizes the 2021 Olympics in Tokyo dataset from Kaggle, which includes multiple Excel files containing information on athletes, teams, coaches, medals, and gender entries.
https://www.kaggle.com/datasets/arjunprasadsarkhel/2021-olympics-in-tokyo
- **Azure Data Factory (ADF)**: ADF is used as the primary orchestration tool. It is configured to create data pipelines that connect to the Kaggle dataset, extract the raw Excel files, and copy them directly into the Raw Data Store. This process ensures data is captured and stored without any modifications.
- **Azure Data Lake Storage Gen 2 (Raw Data Store)**: This is the initial landing zone for all ingested data. It acts as a "bronze layer," storing the raw, unchanged data files. This approach is critical for maintaining an auditable record of the source data and provides a stable foundation for all subsequent transformations.

**2. Transformation** \
In this stage, the raw data is cleaned, structured, and enriched to make it ready for analysis.

- **Azure Databricks**: Databricks provides a powerful, collaborative, Apache Spark-based environment for large-scale data processing. Using notebooks (e.g., Python or Scala), we will:
  - Data Cleaning: Handle missing values, correct data types, and standardize column names.
  - Data Structuring: Parse the Excel data and convert it into a more efficient format like Parquet or Delta Lake.
  - Data Enrichment: Join multiple data sources (e.g., athletes, medals, and countries) to create a single, unified view of the data. For example, joining the Medals.xlsx and Athletes.xlsx files to link medal winners to their personal information.
  - Data Loading: Store the transformed, clean data into a new location in the Data Lake.

- **Azure Data Lake Storage Gen 2 (Transformed Data)**: This serves as the "silver layer," containing the cleaned and structured data from Databricks. This dataset is now ready for efficient querying and analysis.

**3. Analytics** \
This stage focuses on using the prepared data for in-depth analysis and creating aggregated views.

- **Azure Synapse Analytics**: As a unified analytics platform, Synapse is used to query the transformed data directly from the Data Lake. It provides a serverless SQL pool, allowing for complex SQL queries on the data without managing infrastructure. This service is used to:
  - Perform Advanced Analysis: Calculate metrics like total medals by country, top-performing athletes, or gender participation rates per sport.
   Create Aggregated Tables: Build materialized views or aggregated tables that are optimized for reporting and visualization. This "gold layer" reduces query time for the final dashboards.

**4. Dashboard & Reporting** \
The final stage is about visualizing the insights derived from the data in an easy-to-understand format.

- **Tableau**: These leading business intelligence tools connect directly to the aggregated data in Azure Synapse Analytics or the Transformed Data layer in the Data Lake. They are used to build interactive dashboards that allow users to:
  - Explore Data: Filter data by country, sport, or medal type.
  - Visualize Insights: Create compelling charts and graphs, such as medal leaderboards, gender distribution heatmaps, and athlete counts by country.
  - Communicate Findings: Present key findings and tell a data-driven story about the 2021 Tokyo Olympics.
