# Time-Series-Analysis-Project

### Goal:
Extract any meaningful information on climate change so as to better understand what it is, what it isn’t, and how it has affected/will affect the global landscape. 

### Datasets:
1. Global Temperature Dataset https://www.kaggle.com/berkeleyearth/climate-change-earth-surface-temperature-data
2. Agricultural GDP Dataset https://data.worldbank.org/indicator/NV.AGR.TOTL.ZS?view=chart
3. CO2 Emission Dataset https://data.worldbank.org/indicator/EN.ATM.CO2E.KT?end=2019&start=2019&view=map

### Techniques:
Python, AWS boto3, time series ARIMA model, and correlation matrix.

### Key points:
Data ingestion, missing values omission, schema design, user defined function, normalization, denormalization, model building and training, prediction, visualization, and analysis.

### Project Outline:

1. Background Information
2. Data Acquisition
3. Data Cleaning
4. Big Picture
5. Time Series Prediction
6. Correlation Analysis
7. Conclusion

### Challenges and Solutions:


#### Challenge 1: Missing Values 
The data has multiple and contiguous missing rows for many regions, which I will need to either remove or impute, and the choice for that will depend on case and targets.

#### Solution for challenge 1: 
The way for dealing missing values in this project is simply dropping all NAs, for 3 reasons:

A) By observing the dataset, most NA happen on early years (roughly 1760 and earlier). It’s reasonable to discard them since the data is not up to date (one point for principle of high quality data). Except those years, we still have hundreds more valid years from then till 20 century, which is a good representative sample.

B) As the below dataframe shown, the dataset with highest NA percent is no more than 6%, so it is fine to drop that amount of rows from the dataset, as we still have a large volume data remains.

C) Compared with filling NA by other relative dimensions of values, such as mean or zero, data has been modified artificially anyway. Instead, dropping NA will have no effect on the remains data, made it real and original with a good level of accuracy.

#### Challenge 2: Data extraction

Datasets are highly intergrated (information with multiple layers are concentrated in a single variable). How to effectively extract this integrated information and maximize the use of them to help me get insights is a big challenge. 

#### Solution for challenge 2: 
To partition the integrated data, I applied many functions such as spliting columns by symbols with "lambda functions", "if conditions" and "dataframe filters". I also used "group by" and "inner join merge" to reduce rows and created new variables by specific requirements.

#### Challenge 3: Time Series Model Selection
For time series prediction, how do I choose the most fitted model in my case (trade off between coding accessibility and predicting accuracy)?

#### Solution for challenge 3:
For time series model, first of all, I chose univariated model that based only on relationships between past and present values since average temperature is the only dependent variable in my model. Based on this, I then chose the ARIMA model which considered "autoregression", "moving average" and "degree of differencing" as parameters for predicting values. These parameters represents past values, residual error from past values, and level of differencing to change the unstationary data to stationary data so that we can use similar patterns to forecast.


### Improvements:

First way to improve or enrich this ARIMA model is adding seasonality feature as I implemented by function in the early data cleaning stage. With the additin of seasonality, the ARIMA model typically become SARIMA model which stands for "Seasonal autoregressive integrated moving-average". With seasonality, the temperature prediction can be more accurate based on the trend of each particular season.

Another way to go beyond on SARIMA model is SARIMAX model. It's same as what I did before, but add new external variables as factors for predicting values, for example, in my project, I can add CO2 emission value from the integrated dataset into this model as another variable which may effect temperature. External variables is another method to increase the model accuracy besides seasonality.
