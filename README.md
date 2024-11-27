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

### **Phase 3: Feature Analysis and Visualization**

In this phase, we focused on analyzing the features in the dataset to assess their relevance and importance in predicting the target variable, a binary classification (0 or 1). The steps outlined below describe the methodologies used to evaluate feature importance, identify key variables, and visualize the results:

1. **Feature Correlation with Target**:  
   The first step involved analyzing the correlation between each feature and the target variable. Using the `pandas.corrwith()` function, we computed correlation coefficients between each feature and the target to identify which features exhibited strong linear relationships with the target.  
   - The absolute values of these correlations were used to prioritize features that had the most influence on the target.

2. **Visualization of Correlation**:  
   The correlation results were visualized using a horizontal bar plot to make the relationships clearer. Features with the strongest correlation to the target were highlighted, providing an intuitive understanding of which variables may have the most predictive power.

3. **Mutual Information Calculation**:  
   To account for non-linear relationships, we calculated the mutual information between each feature and the target using `mutual_info_classif` from `sklearn`. Mutual information quantifies the amount of shared information between a feature and the target, identifying features that provide the most value for predicting the target.  
   - The mutual information scores were sorted in descending order and visualized in a bar plot for easy comparison.

4. **Feature Importance Using Random Forest**:  
   We trained a Random Forest classifier to determine the importance of each feature in predicting the target. The Random Forest algorithm uses decision trees to evaluate how much each feature reduces classification error (impurity). This helped identify which features were most influential in the classification task.  
   - A bar plot was created to display the feature importance scores, sorted by importance.

5. **Comparison of Feature Selection Methods**:  
   The results from the correlation analysis, mutual information, and Random Forest feature importance were combined into one dataframe for direct comparison. This approach allowed us to cross-check which features were consistently important across multiple methods, ensuring the robustness of our feature selection process.

6. **Visualization of Feature Selection Methods**:  
   A scatter plot was generated to compare the mutual information scores with the Random Forest feature importance scores. This visualization helped identify features that were important according to both metrics and provided insight into which features should be prioritized in future modeling.

7. **Conclusion and Feature Prioritization**:  
   After analyzing the results from the correlation analysis, mutual information, and Random Forest feature importance, it became evident that some features exhibited low importance across different methods. Specifically, the following six features showed low patterns of importance across all metrics:  
   - `'Max wind gust_Spd'`
   - `'9 am_Spd'`
   - `'3 pm_Dir'`
   - `'3 pm_Spd'`
   - `'9 am_Dir'`
   - `'Max wind gust_Dir'`

   These features consistently appeared to have minimal influence on the target variable. While removing them may simplify the model, it is essential to investigate further whether they affect the model’s performance. The simplest approach would be to drop these features; however, additional analysis is required to confirm whether these features truly have no impact on the model's predictive power. This investigation will be important before making the final decision on feature removal.
   
This phase ensured that we thoroughly analyzed the features in the dataset and their relationship with the target variable. By applying multiple methods such as correlation analysis, mutual information, and Random Forest feature importance, and visualizing the results, we gained valuable insights into which features had the most predictive power. We identified six features with consistently low importance across all metrics: `'Max wind gust_Spd'`, `'9 am_Spd'`, `'3 pm_Dir'`, `'3 pm_Spd'`, `'9 am_Dir'`, and `'Max wind gust_Dir'`. While these features may be candidates for removal, further investigation is needed to determine whether they have any significant impact on the model’s performance. These steps provided a solid foundation for the next phase, where we will refine the feature selection and proceed with model building.
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
We’re just getting started! The next phase will focus on refining feature selection, followed by building and evaluating predictive models using the insights we’ve gained. Stay tuned for more updates as we progress. Your feedback and contributions are always welcome as we continue to enhance the model's accuracy and performance! 🌟
---
