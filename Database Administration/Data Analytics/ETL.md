Created: 2024-09-18 20:01
## Family Tree:
1. Computer
2. Database Administration
3. [[Data Analytics]]
-- -
**ETL Software Tools** are those that perform the function of extracting, transforming, and loading data, as referenced by the acronym "Extract, Transform, and Load."
## Data Extraction
In this stage, data is collected from various sources, such as databases, Excel spreadsheets, .csv files, social networks, audio, video, conversations, etc. These data may not be in the proper format and may have missing fields or blank mandatory fields.
### Characteristics:
- It involves collecting data from source systems, known as Data Sources or Operational Systems.
- Data extraction can be done by the source system itself or by any ETL tool.
- Business rules may exist during the extraction. For example, extracting customer data that indicates individuals over 60 years old and/or those with an income above a certain threshold.
### Common Types:
- **Batch/Full Extraction:** The ETL tool always extracts all data that fits the extraction rules.
- **Incremental Update:** The tool compares what has already been extracted with the data source and extracts only new or updated data.
- **Automatic Update:** The source system can notify when records have been modified, prompting the tool to extract only the new or changed data.
- **Continuous Extraction:** The data source constantly sends new data, and the tool must support capturing this continuous flow.
## Data Transformation
This is an extremely important and complex process. In this stage, the data is cleaned, manipulated, and transformed into a standardized and organized framework, free from "dirty" data. Dirty data refers to inconsistencies like a name appearing where an email should be, incomplete identification documents, or similar issues. The transformation stage ensures the data structure is within the expected norms for those conducting the final analysis.
### Characteristics:
- This process consists of several stages: standardization, cleaning, quality control, consolidation, and integrity.
- The transformation stage holds the most weight in the ETL process due to the number of steps involved.
- Depending on the language or tool used, the transformation process can be very fast or extremely slow.
### Basic Transformations:
- Data cleaning.
- Format standardization.
- Domain standardization.
- Duplicate removal.
- Data filtering.
### Advanced Transformations:
- Merging files/tables.
- Splitting files/tables.
- Calculated fields.
- Data/field enrichment.
- Field splitting or consolidation.
- Unit conversion.
- Key transformations.
- Encoding modification.
## Data Loading
After cleaning, the data must be made available somewhere. This location could range from specialized storage systems to cloud storage devices. Data must be loaded into an environment where it is kept organized, structured, and accessible. There are many storage approaches, but in general, data is stored in a **data warehouse** or **data lake**, and sometimes directly in the visualization tool repositories we are using.
### Characteristics:
- The loading process is the simplest part of the ETL flow and is guided by the type of files or target data the system supports.
- It is highly strategic. Converting source files to a new, smaller model with a higher compression rate helps maintain a Big Data environment efficiently.
- When working with large volumes of data, they are typically stored in a data warehouse or data lake.
- For smaller data sets, the ETL result can be "loaded" into the repository of the Data Analytics tool being used for data visualization, such as Power BI.