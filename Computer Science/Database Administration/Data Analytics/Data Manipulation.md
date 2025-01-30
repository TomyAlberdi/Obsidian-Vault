Created: 2024-09-18 20:43
## Family Tree:
1. Computer
2. Database Administration
3. [[Data Analytics]]
-- -
Data Analytics often utilizes data that was originally collected for other purposes, which can affect the quality of the data. Poor data quality can lead to poor results in our analyses. Therefore, **Data Manipulation** is an ongoing process aimed at ensuring data quality. This ensures the best results, allowing us to revisit each step and make necessary adjustments. The key tasks of this process include:
- **Extraction**: Gathering data from various sources or tables that provide the necessary information for analysis.
- **Observation**: Understanding each variable to plan the necessary transformations.
- **Transformation**: Applying various techniques to "clean" the data, discarding those that contain "noise" (data that does not reflect reality or may lead to incorrect conclusions).
- **Loading**: Preparing the dataset for analysis.
- **Control**: Auditing the data to ensure it is of sufficient quality for analysis.
## ETL Process
ETL (Extract, Transform, Load) is the process by which we retrieve the data we need, apply necessary transformations, and finally load it into a dataset. Once loaded, the data is ready for application to a Data Analytics model. The steps involved are:
- **Extract**: This step involves querying data from the source systems. The main goal is to extract only the data needed for analysis. It’s important to have clear objectives and be familiar with the available data sources.
- **Transform**: After selecting and observing the data, we apply any necessary modifications or transformations to prepare it for analysis. Common transformation examples include:
    - **Cleaning**: Filling in missing data or addressing outliers.
    - **Transformation**: Adding summarized data (e.g., country averages).
    - **Integration**: Combining data from different sources.
    - **Reduction**: Reducing the data volume while retaining its analytical meaning.
    - **Discretization**: Similar to reduction but applied to numerical data.
- **Load**: This step involves loading the transformed data into an integrated dataset, ready for analysis. It’s crucial to control for any errors in the integrated and transformed data.
## Practical Scenarios
**Extracting Data**: What challenges might arise during data extraction?
Not all data will be easy to query since it may come from multiple databases with different platforms and protocols, as well as using different languages and character sets. These challenges, among others, can arise when extracting data.
Thus, it’s essential to:
1. Know the sources,
2. Ensure their reliability, and
3. Work on improving the quality of the data, understanding the types of data and the necessary transformations.
For example, if we want to analyze employee salaries, we’ll need access to internal employee databases and cross-reference them with macroeconomic databases for each market. Each of these databases comes from different origins and was created for different purposes, so transformations will likely be necessary for integration and analysis.
## Practical Tips
- **Know the database owners**: It’s useful to spend time getting to know the owners of the data sources, as this can help provide better context for the data.
- **Integration planning**: Keep in mind how you will integrate different databases and identify the variable that will serve as the ID for each table.
- **Know the data types**: As we’ve seen, understanding the types of data you’re working with helps improve the contextualization and planning of your project.
## Common Transformations
- **Changing data types**: Often, numerical data is expressed as text or uses a different thousands separator than expected.
- **Transposing**: When data is presented in a matrix, it’s often better to convert it into a flat table.
- **Handling null values**: Filling in empty values.
- **Reduction**: Reducing the volume of data while maintaining its analytical meaning.
- **Discretization**: Similar to reduction but applied to numerical data.
## Final steps before Data Analysis
At this stage, we create the dataset that will serve as input for our data model. It’s critical to review the Data Manipulation process and, if everything was executed correctly, proceed to load the data.
Consider the following:
- Were the transformations executed correctly?
- Are there any missing values or outliers after the transformation?
- Is the dataset complete, or did some variables lose records?
- After loading: Do we have all the data we need?