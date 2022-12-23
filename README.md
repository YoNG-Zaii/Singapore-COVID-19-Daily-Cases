# Singapore COVID-19 Daily Cases with ARIMA

This data science project uses ARIMA model to forecast Singapore's COVID-19 daily cases.

## Data Collection

* Source: [Singapore's COVID-19 Case Numbers](https://data.gov.sg/dataset/covid-19-case-numbers?resource_id=400a3eb4-8702-4050-9700-988bfea7a20f)
* Period: 23rd Jan 2020 - 22nd Dec 2022

## Exploratory Data Analysis

General analysis
* Change the the data type of the 'date' column to datetime.
* Visualise the imported and local cases respectively using line graphs.
* Combine both imported and local cases for each day.
* Visualise the combined cases using line graph.

Specific analysis (1st Jan 2022 - 30th Apr 2022)
* Decompose the time-series data into trend, seasonality, and residuals.
* Visualise the seasonal decomposition of the data.

## Feature Transform

Due to the seasonality present in the data, we apply logarithmic transformation to make the data more stationary.

## ARIMA Model

Next, we find all the parameters needed to construct an ARIMA model.

### The order of differencing, d

Here are the steps involved to determine the value of d:
* Perform Augmented Dickey Fuller (ADF) test on original series, 1st differenced, and 2nd differenced data.
* Plot Autocorrelation Function (ACF) on original series, 1st differenced, and 2nd differenced data.
* Due to overdifferencing, we will increase the MA term by 1.

### The order of the AR term, p

Here is the step involved to determine the value of p:
* Plot Partial Autocorrelation Function (PACF) original series, 1st differenced, and 2nd differenced data.

### The order of the MA term, q

Here is the step involved to determine the value of q:
* Review the 1st order ACF plot.

### Model Training

Based on ARIMA(2, 1, 2),
* Plot the residuals of the model.
* Visualise and compare the actual and predicted values.

### Out of Time Cross Validation

Based on ARIMA(2, 1, 2),
* Split the original data into 90% train and 10% test data.
* Train the ARIMA model with the 90% train data.
* Test the ARIMA model's accuracy with the 10% test data.

### Parameter Tuning

* Tune the d, p, q parameters with different values to find the best model.
* Use Akaike’s Information Criterion (AIC) to estimate which combination of parameters produce the best model.

### Accuracy Metrics

After determining the best model, we use the following metrics to evaluate that model:
* Mean Absolute Percentage Error (MAPE)
* Mean Absolute Error (MAE)
* Root Mean Squared Error (RMSE)
* Correlation between the Actual and the Forecast (Corr)
* Lag 1 Autocorrelation of Error (ACF1)

## Conclusion

Even though the ARIMA model (with logarithmic values) is about 94.22% accurate in predicting the next 12 observations,
the model might still underfit. So, other models such as GARCH model or other external indicators such as vaccination rate can be used to produce
a more accurate model.
