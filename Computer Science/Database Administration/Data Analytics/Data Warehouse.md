Created: 2024-09-18 20:18
## Family Tree:
1. Computer
2. Database Administration
3. [[Data Analytics]]
-- -
A **data warehouse** is a data repository that:
- Provides easy access.
- Consolidates data from many sources into a single data store.
- Transforms the data into groups of information specific to business topics, such as sales, logistics, production, etc.
- Allows for easy queries, analysis, and reporting to support decision-making.
A data warehouse aims to provide:
- **Accessible information:** The contents of the data warehouse are understandable, navigable, and quickly accessible.
- **Consistent information:** Ensuring that data has a single, uniform meaning for everyone.
- **Adaptable and elastic information:** The data warehouse is designed for continuous change.
- **Data protection and governance:** Ensuring the security and proper management of data.
- **Decision-making support:** Offering valuable information to aid in decisions.
A data warehouse should offer a unified, comprehensive view of the data, often referred to as a "360-degree view."
## Differences between Transactional Systems and Data Warehouse

| Transactional                                                                                                               | Data Warehouse                                                                                                                                |
| --------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Data models are focused on efficiently and securely managing transactions (sales, purchases, customer registrations, etc.). | Data models are designed to help integrate and unify data, making it easily and simply accessible through SQL queries or visualization tools. |
| Prioritizes writing data. Ensures data is recorded.                                                                         | Prioritizes reading data. Speeds up data queries.                                                                                             |
## Architecture of a Data Warehouse
The architecture of a data warehouse consists of four main components:
### Data Source Applications  
The data sources feeding the data warehouse are typically OLTP (transactional) systems that record company transactions. These sources can be:
    - **Formal applications:** ERP, CRM, e-commerce, legacy systems developed in-house, HR systems, etc.
    - **External applications:** Such as social media, Google Analytics, market reports, or regulatory information (banks, insurance companies, food and pharmaceutical industries, taxes, healthcare, etc.).
    - **Unstructured data:** Information stored in CSV, TXT files, spreadsheets, PDFs, etc., not organized within formal OLTP applications.
### ETL Processes  
These processes run automatically and periodically (daily, weekly, monthly, hourly, etc.) and are essential for keeping the data warehouse up to date, consistent with the source systems, unified, and of high quality. The ETL (Extract, Transform, Load) processes are batch processes that:    
    - Extract information from various data sources.
    - Perform simple or complex transformations (usually involving algorithms to improve data quality).
    - Load the transformed data into the data warehouse.
### Data Warehouse Database
The third component is the data warehouse database, a data repository specifically modeled for querying large volumes of data. This is typically a relational database, potentially with an optimized engine if the data volume requires it.    
### Visualization and Data Mining Tools
The fourth component consists of visualization tools. These allow for presenting information and may include tools for visualization only or those that also define more complex data mining or data science models.
## Conclusion
In summary, a **data warehouse** is a data repository:
- Built and optimized for the easy analysis and querying of large volumes of data.
- That provides a unified, high-quality view of data regardless of its origin.
- It should offer a complete or 360-degree view of a company, as it includes all necessary data for its management.
- It is a necessary (but not sufficient) component for ensuring data governance and helps foster a data-driven culture within the organization.