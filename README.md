# Seoul-Bikes-Demand-Prediction
This repository contains the code and documentation for the Seoul Bikes Demand Prediction project, conducted by Beatriz Correia (Myself), Luís Pereira, Maria Pais, Sebastião Rosalino and André Novo. The project aims to predict the number of bikes rented per hour by the Seoul Bikes system, using historical rental data and weather conditions.

## Introduction
The Seoul Bikes system provides a sustainable means of transportation for citizens of Seoul, South Korea. This project leverages a dataset of bike rentals and weather conditions to develop predictive models that estimate the number of bikes needed at each rental station to optimize service efficiency.

## Business Understanding
Founded in 2015, Seoul Bikes aims to promote sustainable transportation in Seoul. The system includes stations across the city where bikes can be rented and returned. The objective of this project is to predict the number of bikes required at each station hourly to ensure optimal service availability and minimize shortages.

Key considerations include:
- Ensuring sufficient bike availability to meet demand.
- Minimizing the risk of bike shortages.
- Maximizing operational efficiency and customer satisfaction.

## Data Understanding
The dataset was obtained from the UCI Machine Learning Repository and contains hourly rental data from December 2017 to November 2018, with a total of 8760 observations and 14 variables. The dataset includes information on:

|Column | Type| Description |
|:---:|:---:| :---:| 
| **Date** |String| The day of the year, for 365 days|
| **Rented Bike Count** | Integer |Number of bikes rented per hour |
| **Hour** | Integer | Time of day |
| **Temperature(℃)** | Float | Temperature per hour |
**Humidity(%)** | Integer | Air humidity |
**Wind Speed (m/s)** | Float | Wind speed in meters per second |
| **Visibility(10m)** | Integer | Visibility per 10 meters |
**Dew Point Temperature(℃)** | Float | Temperature required for condensation of water vapor in the air to occur|
**Solar Radiation (MJ/m2)** | Float | Solar Radiation |
**Rainfall(mm)** | Float | Rainfall per millimeter |
**Snowfall(cm)** | Float | Snow per centimeter |
| **Seasons** | String | Season of the year |
| **Holiday** | String | Whether or not it's a national holiday |
| **Functioning Day** | String | Whether or not the rental service was operating |

## Data Preparation
### Data Import and Initial Processing
The dataset was imported into a Jupyter Notebook using the Pandas library. The Date variable was converted from string to datetime format for better handling. Checked and confirmed that there were no missing values or duplicate records.

### Exploratory Data Analysis
Descriptive statistics were calculated for numerical variables. The distribution of the target variable (Rented Bike Count) was analyzed, revealing a right-skewed distribution with outliers. Categorical variables (Seasons, Holiday, Functioning Day) were explored to understand their distribution.

### Feature Engineering
Created additional variables such as Rainfall_scale and Snowfall_scale to categorize the intensity of these weather conditions. Converted categorical variables into dummy/indicator variables for model compatibility.

### Handling Outliers
Identified and analyzed outliers in variables like Wind Speed, Rainfall, and Snowfall. Decided to retain outliers as they represent real extreme weather conditions important for the analysis.

### Data Splitting
The dataset was split into training and testing sets in an 80:20 ratio to validate the models' performance.


## Modeling
Various regression techniques were used to predict bike rentals:
* Linear Regression: A basic linear regression model to establish a baseline performance.
* LASSO Regression: Applied LASSO (Least Absolute Shrinkage and Selection Operator) to introduce regularization and prevent overfitting by penalizing the absolute size of the coefficients.
* Ridge Regression: Used Ridge regression to address multicollinearity among predictors by penalizing the squared size of the coefficients.
* Decision Tree Regressor: Implemented a Decision Tree model to capture non-linear relationships between the features and the target variable.
* Extra Trees Regressor: Applied the Extra Trees algorithm, which builds multiple decision trees and averages their results to reduce variance and improve predictive performance.
* Random Forest Regressor: Utilized Random Forest, an ensemble learning method that builds numerous decision trees and averages their outputs to improve accuracy and control overfitting.
The best model was found to be the Extra Trees Regressor with a log-transformed target variable, achieving an R² score of 0.866, MAPE of 31.79%, and RMSE of 239.89.

## Model Training and Hyperparameter Tuning
For each model, hyperparameters were tuned using cross-validation to optimize performance. Models were evaluated using metrics such as R^2 (coefficient of determination), MAPE (Mean Absolute Percentage Error), and RMSE (Root Mean Square Error).
* Log Transformation: To handle the skewness of the target variable, a log transformation was applied to Rented Bike Count, which improved model performance.

## Evaluation
Model evaluation was based on:
R^2: Proportion of variance explained by the model.
MAPE: Mean absolute percentage error.
RMSE: Root mean square error.
The Extra Trees Regressor model performed the best, providing accurate predictions while minimizing errors.

## Conclusion
The project successfully developed a predictive model for bike rentals, achieving the initial objectives. Key findings include:

* Hour of the day and season are significant predictors of bike rentals.
* Weather conditions like temperature and wind speed also influence rentals.
* The best performing model was the Extra Trees Regressor with log-transformed target variable.

As for the problem in question, the best model is then exported and applied to a Django API (not available in this repository) which according to the conditions would return the minimal number of bikes needed.
To ensure the availability of bikes and prevent shortages, the Mean Absolute Error (MAE) was used to define a margin of error. The MAE for the best model was 137 bikes. This means that to meet the demand accurately, it is recommended to add a buffer of 137 bikes to the predicted count. This buffer accounts for the average prediction error and helps maintain service reliability, ensuring enough bikes are available during peak times and various weather conditions.



