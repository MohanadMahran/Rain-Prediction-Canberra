# Rain Prediction in Canberra, Australia

This project aims to develop a predictive model for forecasting whether it will rain tomorrow in Canberra, Australia, utilizing historical weather data sourced from the [Bureau of Meteorology](http://www.bom.gov.au). The project is structured into several phases, each focusing on different aspects of the data science workflow, including data extraction, preparation, analysis, model training, and evaluation.

## Project Description

Rainfall prediction is crucial for various applications, from agriculture to urban planning. By analyzing historical weather patterns, we can create a model that helps predict the likelihood of rain, thereby providing valuable insights for decision-making processes. This project will leverage machine learning techniques to analyze weather data, aiming to deliver accurate predictions based on identifiable patterns and trends.

## Project Phases

### **Phase 1: Data Extraction**

In this initial phase, we focused on gathering comprehensive historical weather data for analysis. The following steps detail the methodology and rationale behind the data extraction process:

1. **Data Source Identification**:  
   Historical weather data was sourced from the publicly accessible [Bureau of Meteorology](http://www.bom.gov.au) website, ensuring reliability and consistency of the dataset.

2. **Web Scraping Implementation**:  
   Custom Python scripts leveraging the `requests` and `BeautifulSoup` libraries were developed to scrape monthly weather data tables. This approach ensured efficient and automated retrieval of relevant information.

3. **Iterative Data Retrieval**:  
   - **URL Construction**: A dynamic URL structure was utilized to iterate through months from January to October 2024, enabling targeted data retrieval.  
   - **Content Parsing**: HTML content was parsed to locate weather data tables. If no table was found, the script flagged the missing data for further investigation.

4. **Structured Data Transformation**:  
   - **Tabular Conversion**: Extracted HTML tables were converted into Pandas DataFrames for seamless data manipulation.  
   - **Mean Data Extraction**: Statistical summaries (e.g., mean values) from the tables were isolated and stored separately for imputation and validation in later phases.

5. **Data Cleaning During Extraction**:  
   - **Exclusion of Redundant Rows**: Unnecessary rows, such as summary rows at the end of the tables, were removed to maintain data relevance.  
   - **Date Range Adjustment**: Dates were aligned across the extracted DataFrames using a custom range from January 1 to October 31, 2024, ensuring temporal consistency.

6. **Validation and Storage**:  
   - The extracted data was inspected for completeness and accuracy before being consolidated into two distinct DataFrames: one for the raw weather data and another for the mean values.  
   - The weather dataset was saved as a CSV file (`weather_data.csv`) for future use.

7. **Error Handling and Logging**:  
   - The script implemented robust error handling to manage potential issues such as missing tables or failed HTTP requests.  
   - Informative logs were generated to provide detailed feedback on the scraping process.

This phase ensured the systematic extraction and structuring of historical weather data, forming a robust foundation for subsequent cleaning, preprocessing, and analysis.

### **Phase 2: Data Cleaning and Preprocessing**

In this phase, we systematically cleaned and prepared the weather dataset to ensure its suitability for analysis and modeling. The following steps outline the methodologies and rationale behind each preprocessing action:

1. **Flattening MultiIndex Columns**:  
   The weather and mean data DataFrames contained MultiIndex columns, which were flattened into a single level for easier data manipulation and access during subsequent analysis.

2. **Incorporating Month Referencing**:  
   A new column was introduced to represent the month as a foreign key, facilitating temporal grouping and aggregation of data.

3. **Feature Selection and Dimensionality Reduction**:  
   Irrelevant or redundant features (e.g., `Date`, `Day`, `Evap`, `Sun`, and wind-related columns) were removed to simplify the dataset and focus on key variables critical for the analysis.

4. **Handling Missing Values (NaN)**:  
   Missing data was imputed using the following strategies:
   - **Numerical Columns**: Mean values were calculated for each month from the reference dataset and used for imputation.  
   - **Categorical Columns**: The mode was utilized to replace missing values, preserving the dataset’s categorical integrity.

5. **Validation of Data Types**:  
   All columns were inspected for non-numeric entries. Any anomalies were identified and printed for further review and correction, ensuring data consistency.

6. **Mapping Categorical Wind Directions to Numeric Values**:  
   Wind direction, initially represented by categorical labels, was converted to numeric degrees using a predefined mapping. This transformation facilitates mathematical analysis and reveals directional patterns.

7. **Converting Object Data Types to Numeric**:  
   All object-type columns were coerced into numeric types, with conversion errors automatically set to NaN. This step ensures compatibility with statistical and machine learning algorithms.

8. **Verification and Visualization**:  
   The final cleaned DataFrame, along with its updated data types, was displayed for thorough verification. This step guarantees data integrity and readiness for subsequent phases.
   
This preprocessing phase addresses potential sources of bias and inconsistency in the dataset, ensuring it adheres to best practices for data analysis. By reducing dimensionality, imputing missing values, and standardizing formats, we minimize noise and enhance the dataset’s overall quality. These steps are crucial for extracting meaningful insights and building robust predictive models in subsequent project phases.

---
### Column Definitions
To facilitate understanding, here are the meanings of the column headings used in the dataset:

| Heading        | Meaning                                                                 | Units                     |
|----------------|-------------------------------------------------------------------------|---------------------------|
| Min               | Minimum temperature in the 24 hours to 9 am                          | degrees Celsius           |
| Max               | Maximum temperature in the 24 hours from 9 am                        | degrees Celsius           |
| Rain              | Precipitation (rainfall) in the 24 hours to 9 am                     | millimetres               |
| Max Wind Gust_Dir | Direction of strongest gust in the 24 hours to midnight              | 16 compass points         |
| Max Wind Gust_Spd | Speed of strongest wind gust in the 24 hours to midnight             | kilometres per hour       |
| 9 am Temp         | Temperature at 9 am                                                  | degrees Celsius           |
| 9 am RH           | Relative humidity at 9 am                                            | percent                   |
| 9 am Cld          | Fraction of sky obscured by cloud at 9 am                            | eighths                   |
| 9 pm Dirn         | Wind direction averaged at 9 am                                      | compass points            |
| 9 pm Spd          | Wind speed averaged at 9 am                                          | kilometres per hour       |
| 9 pm MSLP         | Atmospheric pressure reduced to mean sea level at 9 am               | hectopascals              |
| 3 pm Temp         | Temperature at 3 pm                                                  | degrees Celsius           |
| 3 pm RH           | Relative humidity at 3 pm                                            | percent                   |
| 3 pm Cld          | Fraction of sky obscured by cloud at 3 pm                            | eighths                   |
| 3 pm Dirn         | Wind direction averaged at 3 pm                                      | compass points            |
| 3 pm Spd          | Wind speed averaged at 3 pm                                          | kilometres per hour       |
| 3 pm MSLP         | Atmospheric pressure reduced to mean sea level at 3 pm               | hectopascals              |

---
Stay Tuned 🚀
We’re just getting started! The next phase will dive deeper into advanced analytical techniques and modeling. Stay tuned for more updates as the project evolves. Your feedback and contributions are always welcome! 🌟
---
