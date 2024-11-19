# Rain Prediction in Canberra, Australia

This project aims to develop a predictive model for forecasting whether it will rain tomorrow in Canberra, Australia, utilizing historical weather data sourced from the [Bureau of Meteorology](http://www.bom.gov.au). The project is structured into several phases, each focusing on different aspects of the data science workflow, including data extraction, preparation, analysis, model training, and evaluation.

## Project Description

Rainfall prediction is crucial for various applications, from agriculture to urban planning. By analyzing historical weather patterns, we can create a model that helps predict the likelihood of rain, thereby providing valuable insights for decision-making processes. This project will leverage machine learning techniques to analyze weather data, aiming to deliver accurate predictions based on identifiable patterns and trends.

## Project Phases

### Phase 1: Data Extraction
- **Objective**: Accumulate comprehensive historical weather data for the past 10 months.
- **Methodology**:
  - Utilize web scraping techniques or APIs to gather relevant data from the Bureau of Meteorology.
  - Ensure the extraction process captures essential weather attributes such as temperature, humidity, wind direction, and precipitation.
- **Expected Outcome**: A structured Pandas DataFrame that consolidates all extracted weather data, ready for preprocessing.

### Phase 2: Data Cleaning and Preprocessing
- **Objective**: Prepare the dataset for analysis to ensure data quality and integrity.
- **Tasks**:
  - Identify and handle missing values through imputation or removal.
  - Convert data types to appropriate formats (e.g., dates to datetime objects).
  - Normalize and scale numerical features as required.
  - **Data Wrangling Changes**: 
    - Adjusted temperature measurements to ensure consistency (e.g., converting to degrees Celsius).
    - Created new features such as `rainy_day` to indicate whether it rained (1) or not (0).
    - Combined and derived additional features (e.g., total daily rainfall from hourly data).
  - Encode categorical variables for model compatibility.
- **Expected Outcome**: A clean, well-structured DataFrame, free from inconsistencies, suitable for feature analysis.

### Phase 3: Exploratory Data Analysis (EDA) and Feature Correlation
- **Objective**: Investigate relationships between features and the target variable (`RainTomorrow`).
- **Methodology**:
  - Conduct statistical tests (e.g., Chi-Square) for categorical features to assess independence.
  - Utilize visualizations (e.g., heatmaps, bar plots) to represent relationships and correlations.
  - Identify significant features that influence the likelihood of rain.
- **Expected Outcome**: Insights into feature importance and correlations that inform model selection.

### Phase 4: Model Training
- **Objective**: Implement and train various classification models to predict `RainTomorrow`.
- **Models to Explore**:
  - Linear Classification
  - K-Nearest Neighbors (KNN)
  - Decision Trees
  - Logistic Regression
  - Support Vector Machine (SVM)
- **Methodology**:
  - Split the dataset into training and testing subsets.
  - Train each model using the training data and optimize hyperparameters as necessary.
- **Expected Outcome**: A set of trained models ready for evaluation against the testing dataset.

### Phase 5: Model Evaluation
- **Objective**: Assess the performance of each model using a comprehensive set of evaluation metrics.
- **Metrics to Utilize**:
  1. Accuracy Score
  2. Jaccard Index
  3. F1-Score
  4. LogLoss
  5. Mean Absolute Error (MAE)
  6. Mean Squared Error (MSE)
  7. R² Score
- **Methodology**:
  - Evaluate each model on the testing dataset using the defined metrics.
  - Compare model performance to identify strengths and weaknesses.
- **Expected Outcome**: A detailed performance report outlining the effectiveness of each model.

### Phase 6: Model Selection and Finalization
- **Objective**: Determine the most effective model for deployment based on evaluation results.
- **Criteria for Selection**:
  - Model accuracy and reliability, as indicated by evaluation metrics.
  - Balance between precision and recall (especially important for classifying rare events like rain).
- **Expected Outcome**: Selection of the optimal model for deployment, along with a strategy for future monitoring and updates.

## Data Source and Quality Notes

### Data Availability
The weather observations used in this project are sourced from the Bureau of Meteorology's "real-time" system. While most data is generated and handled automatically, some quality checking has been performed. However, erroneous values may still appear. Observations can occasionally be unavailable due to various reasons, and caution is advised when interpreting the data.

### Summary Statistics
Summary statistics such as mean, lowest, highest, and total values are calculated based on the available data at the time of preparation. Not all statistics are applicable to every field.

### Column Definitions
To facilitate understanding, here are the meanings of the column headings used in the dataset:

| Heading        | Meaning                                                                  | Units                     |
|----------------|--------------------------------------------------------------------------|---------------------------|
| Date           | Day of the month                                                        |                           |
| Day            | Day of the week (first two letters)                                     |                           |
| Min Temp       | Minimum temperature in the 24 hours to 9 am                             | degrees Celsius           |
| Max Temp       | Maximum temperature in the 24 hours from 9 am                           | degrees Celsius           |
| Rain           | Precipitation (rainfall) in the 24 hours to 9 am                       | millimetres               |
| Evap           | "Class A" pan evaporation in the 24 hours to 9 am                      | millimetres               |
| Sun            | Bright sunshine in the 24 hours to midnight                             | hours                     |
| Max Wind Gust  | Direction of strongest gust in the 24 hours to midnight                 | 16 compass points         |
| Max Wind Speed | Speed of strongest wind gust in the 24 hours to midnight                | kilometres per hour       |
| 9 am Temp      | Temperature at 9 am                                                     | degrees Celsius           |
| 9 am RH        | Relative humidity at 9 am                                               | percent                   |
| 9 am Cld       | Fraction of sky obscured by cloud at 9 am                               | eighths                   |
| 3 pm Temp      | Temperature at 3 pm                                                     | degrees Celsius           |
| 3 pm RH        | Relative humidity at 3 pm                                               | percent                   |
| 3 pm Cld       | Fraction of sky obscured by cloud at 3 pm                               | eighths                   |
| 3 pm Dirn      | Wind direction averaged over 10 minutes prior to 3 pm                   | compass points            |
| 3 pm Spd       | Wind speed averaged over 10 minutes prior to 3 pm                       | kilometres per hour       |
| 3 pm MSLP      | Atmospheric pressure reduced to mean sea level at 3 pm                  | hectopascals             |

## Project Setup
- **Dependencies**: List of required libraries (e.g., `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`).
- **Installation Instructions**: Steps to set up the environment.

## Usage
- Detailed instructions on how to run the code, including any command-line arguments or configuration settings needed.

## Contributing
- Guidelines for contributing to the project, including coding standards and submission processes.

## License
- Information about the project's license and usage rights.

## Updates
- A section for tracking progress and updates for each phase.
