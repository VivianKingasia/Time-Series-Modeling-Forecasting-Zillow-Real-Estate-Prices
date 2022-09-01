
# Time-Series-Modeling-Forecasting-Zillow-Real-Estate-Prices

## 1 Business Understanding
### 1.1 Introduction
Knowing the best moves to make and risks to manage in the real estate industry is very vital to succeeding in the field.
According to People's Capital Group, residential properties have an average annual return of 10.6% and commercial properties have a 9.5% average return.

### 1.2 Problem Statement
The stakeholder in this project is a real estate investment firm that is looking to construct residential homes in top five locations in the US.
This project therefore is a time series analysis on a Zillow dataset on various locations around the United States.

<b>In our time series analysis, the metric of success to determine model viability will be RMSE/MSE.</b>

### 1.3 Main Objective
Conduct a time series analysis to predict the five best locations to invest in based on ROI.


### 1.4 Supplementary Objectives
    - Provide effective real estate investment recommendations to the stakeholder.
    - Increase the real estate investor’s customer base.


### 1.5 Problem Questions
    
- What are the five best locations to invest in around the US?
- What makes these locations so lucrative?
- Does urbanization affect the prices of houses?
- Where are the locations of the houses with the highest price volatility?
- Can future median house prices be effectively predicted?

## 2 Data Understanding
The data used in this project was sampled from different states in USA. It contains historic median house prices from the period between April 1996 to April 2018 (22 Years).
The data was obtained from the <a href= 'https://www.zillow.com/research/data/'>zillow website</a>

    - The dataset has 14723 rows and  272 columns.
    - 219 columns are type Float64.
    - 49 columns are type Int64.
    - 4 columns are type Object.

Out of the 272 columns, there are 4 categorical columns and the rest are numerical.

### Column names and description:
    - RegionID - Unique region identifier
    - RegionName - Names of the Regions (Zipcodes)
    - City - City names for the regions
    - State - Names of the states
    - Metro - Names of metropolitan areas
    - County Name - Names of counties
    - Size Rank - Rank of Zipcodes by urbanization
    - Date Columns (265 Columns) - Meidan house prices across the years 

## 3 Data Preparation

### Data cleaning
#### Validity
First, we renamed RegionName to Zipcode, because it contains zipcodes of specific geographical areas.

#### Completeness
    - Our data set had 157934 missing values, but data did not contain any duplicates.
    - The Metro column had 1043 missing values, which were replaced by the string 'missing'.

#### Consistency
The data has no duplicates hence it's consistent.

#### Uniformity
Zip Codes were  converted  into a string because it's a categorical datatype.
A '0' was placed at the beginning of every zip code that had 4 digits, instead of 5.

### Methods
2 columns were created:
    - Return on Investment (ROI)
    - Coefficient of variation (CV)

The dataframe was converted into a time series.
The dataset was de-trended through 1-lag diffrencing.
Seasonality was removed through 12-lag differencing.
ACF and PACF plots were used to check for autocorrelation, which was found at multiple lags, meaning the series wasn't random.

## 4 Modelling
    - Seasonality and trend were examined.
    - A <b>Dickey Fuller</b> test that produced a p_value, greater than 0.05, confirmed that the data <b>wasn't stationary</b>
    - Since there was seasonality the best model to use was the SARIMAX.
    - The model had a high AIC so we did a random search for the optimal pdq parameters to reduce AIC and improve the performance of the model
    - Since there was still correlation in the residuals the model was further improved by increasing the order which improved the model significantly.

### Evaluation

Two forecasts methods were used to compare test data with predicted data:
- Non dynamic forecast which produced a mean absolute percentage error of 0.005
- Dynamic forecast which produced a mean absolute percentage error of 0.08

### Challenging the model
The fb prophet model was used, producing a mean absolute percentage error of 0.5


## 5 Conclusions
### EDA
    - Does Urbanization Affect Median House Prices? <b>no</b>
    - Which cities fetch the highest median house prices?:
        - Atherton (California)
        - Palm Beach(Florida)
        - Snowmass Village (Colorado)
    - What top 5 Zipcodes have the highest ROI?:
        - Upper East Side- New York(10021)
    - Sea Island- Georgia State (31561)
        - Manhattan -New York(10014)
        - Brooklyn New York(11217)
        - Hanalei- Hawaii (96714).
New York state has the most zip codes with the highest ROI.

        - Which zipcodes have high price volatility?
        - 02116 Boston- Massachusetts
        - 56041 New Ulm- Minnesota
        - 16102 New Castle- Pennsylavia
        - 43103 Ohio- Colombus
        - 31027 Dublin-Georgia
Real estate investors have to be careful when investing in these areas.

    - What is the trend of median houseprices over the years?
         - There is an ascending trend.
         - There is no monthly seasonality.
         - There was a downward spike around the price of houses in 2008 which can be explained by the global recession that affected the housing market in the US.
     
### Modeling conclusions
    - There is a difference in the forecast between our model and the prophet model.
    - The prophet model has a higher MAPE than our dynamic model. It is therefore the forecasting model we would deploy.

## 6 Recommendations
    - The company should focus on locations with great beaches and outdoor activities since houses in these locations fetch the highest prices as this is seen from cities in California ,Florida and Colorado.
    - Investors should consider investing in New York,Hawaii and Georgia states since they have the highest Return On Investment although there is a risk involved since the future predictions indicate a drop in prices in the future especially for New York.
    - The firm should avoid investing in cities like Boston,New Ulm,New Castle,Ohio,Dublin since the price fluctuations are very high therefore the risk involved is very high.
    - Level of urbanization doesn't affect house prices so investors shouldn't  consider it when looking for investments.

