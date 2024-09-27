This project focuses on developing predictive models using logistic regression to classify air quality in San Nicolás based on various pollutants and meteorological factors. The study aims to understand the effect of industrial pollutants transported from Apodaca and how they influence air quality in nearby areas.

The analysis involves integrating environmental parameters such as temperature, wind speed, relative humidity, and atmospheric pressure to gain a comprehensive understanding of their correlation with PM10 and PM2.5 levels in the air.

# Air Quality Prediction Using Logistic Regression

## Model Overview

The project utilizes **Principal Component Analysis (PCA)** and **Logistic Regression Models** to predict air quality classifications based on environmental and pollutant data. The main goal is to assess how the movement of air pollutants from the industrial region of Apodaca affects the air quality in San Nicolás.

Data was collected from air quality monitoring stations between 2020 and 2023, and processed to focus on relevant variables, including PM10 and PM2.5 concentrations. Two logistic regression models were developed and validated to predict air quality based on meteorological and pollutant data.

## **Problem Statement**
The poor air quality in the Monterrey metropolitan area is a persistent issue, primarily influenced by industrial emissions, geographical factors, and meteorological conditions. The project's goal is to develop a predictive model to classify air quality in San Nicolás, based on pollutant levels and meteorological data from Apodaca.

## **Data Preparation**
### Data Integration and Cleaning
- **Data Collection**: Raw data from 2020-2023 was gathered from San Nicolás and Apodaca stations. The data initially had 31,790 and 31,792 records for Apodaca and San Nicolás, respectively.
- **Missing Data Imputation**: Missing values were filled using the average between the last recorded value and the next available value. This technique was limited to a maximum of 24 consecutive missing records (24 hours).
- **Conversion and Feature Engineering**: Certain pollutants (O3, NO2, SO2, NO, NOX) were converted from ppb to ppm. Air quality was classified according to the “Aire y Salud” index, and data was filtered based on wind direction from Apodaca to San Nicolás (200° to 250°).

### Data Filtering
- **Wind Direction Filter**: Only records where the wind from Apodaca was directed towards San Nicolás were retained. This reduced the Apodaca dataset to 289 records and the San Nicolás dataset to 174.
- **Data Consolidation**: Relevant variables from both datasets were combined, focusing on meteorological data (e.g., temperature, pressure, wind speed) and pollutant concentrations (PM10, PM2.5). The consolidated dataset had 174 records.
- **Variance-Based Column Elimination**: Columns with low variance (RAIN and SR) were removed as they contributed little to model differentiation.

### Exploratory Data Analysis
- **Visualization**: Differences in air quality proportions in San Nicolás were examined based on whether it was influenced by wind from Apodaca. Clear distinctions were observed in the distribution of PM10 and PM2.5 classifications.

## **Modeling and Validation**
### Principal Component Analysis (PCA)
- **Dimensionality Reduction**: PCA was used to simplify the meteorological data. Standardization ensured equal weight for each variable.
- **Principal Components**: PC1 explained 64.91% of the variance, while PC2 added 24.69%, combining to cover 89.6% of the total variance.
- **Component Interpretation**: 
  - PC1: Positively influenced by temperature, negatively by pressure.
  - PC2: Negatively influenced by both relative humidity and pressure.
- **Scatter Plot**: The projection of the data on PC1 and PC2 revealed no distinct grouping, suggesting that the meteorological variables are intertwined.

### Logistic Regression and Assumption Validation
- **Binary Classification**: Air quality was classified into “Good” and “Bad”, grouping all “Acceptable”, “Bad”, “Very Bad”, and “Extremely Bad” classifications under “Bad” due to data imbalance.
- **Two Models**: Separate logistic regression models were applied to predict PM10 and PM2.5 classifications, using Apodaca’s particle concentrations, wind speed, and the principal components from PCA.

#### Assumption Checks:
1. **Binary Response Variable**: Successfully transformed air quality data into a binary format for each model.
2. **Independent Observations**: Residual plots against time showed no evident patterns, confirming independence.
3. **No Multicollinearity**: VIF values were all below 5, indicating no significant multicollinearity among predictors.
4. **No Extreme Outliers**: Influential observations were identified using leverage scores and subsequently removed.
5. **Linearity of Predictors with Logit**: Box-Tidwell tests confirmed linear relationships between predictors and the logit of the response.
6. **Sufficient Sample Size**: The sample size met the required threshold for logistic regression assumptions.

## **Results**
- **Model for PM10**: Achieved an accuracy of 79%. 
  - **Equation**: `logit(p) = -1.2644 + -0.6126 * PC1 + 0.4840 * PC2 + -1.7444 * PM10_Apodaca + -1.2901 * WSR_Apodaca`.
- **Model for PM2.5**: Achieved an accuracy of 82%.
  - **Equation**: `logit(p) = 0.0931 + 0.0351 * PC1 + 0.1572 * PC2 + -1.1957 * PM2.5_Apodaca + -0.6725 * WSR_Apodaca`.
- **Confusion Matrices**: Highlighted a balanced performance in predicting both "Good" and "Bad" air quality for each pollutant type.

## **Discussion and Conclusions**
- **Wind Influence**: The analysis showed that wind direction significantly affects air quality in San Nicolás, particularly during periods when the wind from Apodaca is present.
- **Pollutant and Wind Effects**: Increased particle concentrations in Apodaca combined with higher wind speed negatively impacted air quality in San Nicolás for both PM10 and PM2.5.
- **Relative Humidity**: A key predictor in the models, relative humidity positively influenced air quality classifications, suggesting a mitigating effect on pollutant concentrations.

The results underscore the importance of considering industrial windborne pollutants and environmental factors in air quality management.

