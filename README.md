# NAME: AMURTHA VAAHINI.KN
# REG.NO: 212222240008
# DATE: 
# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA


### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on cinema ticket sold data.
### ALGORITHM:
1.Load the necessary libraries for data manipulation, numerical operations, visualization, and statistical testing.
2.Read the data from the CSV file into a DataFrame.
3.Convert the 'date' column to datetime format for time series analysis.
4. Set the 'date' column as the index of the DataFrame.
5.Plot the 'total_sales' data over time to visualize the original series.
6. Create a function to perform the Augmented Dickey-Fuller test to check for stationarity.
7. Apply the ADF test on the original 'total_sales' data and print the results.
8. Create a differenced version of the 'total_sales' data to remove trends and plot it.
9.Create a seasonally differenced version of the 'total_sales' data (assuming a monthly frequency) and plot it.
10.Perform a log transformation on the 'total_sales', then difference the log-transformed data, and plot it.
11.Apply the ADF test on the log-differenced 'total_sales' data and print the results.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.stattools import adfuller
```
# Load the dataset
```
data = pd.read_csv("cinemaTicket_Ref.csv")
```
# Ensure 'date' column is in datetime format
```
data['date'] = pd.to_datetime(data['date'], format='%Y-%m-%d')
```
# Set 'date' as index for time-series analysis
```
data.set_index('date', inplace=True)
```
# Plot the original time series for 'total_sales'
```
data['total_sales'].plot(title="Total Sales Over Time", figsize=(10, 6))
plt.show()
```

# Function to perform the Augmented Dickey-Fuller test
```
def adf_test(timeseries):
    print('Results of Dickey-Fuller Test:')
    dftest = adfuller(timeseries.dropna(), autolag='AIC')
    dfoutput = pd.Series(dftest[0:4], index=['Test Statistic', 'p-value', '#Lags Used', 'Number of Observations Used'])
    for key, value in dftest[4].items():
        dfoutput['Critical Value (%s)' % key] = value
    print(dfoutput)
```
# Perform ADF test on the original 'total_sales' column
```
adf_test(data['total_sales'])
```
# Apply differencing to remove trends
```
data['total_sales_diff'] = data['total_sales'] - data['total_sales'].shift(1)
data['total_sales_diff'].dropna().plot(title="Differenced Total Sales", figsize=(10, 6))
plt.show()
```

# Seasonal differencing with a window of 12 (if monthly data)
```
n = 12
data['total_sales_seasonal_diff'] = data['total_sales'] - data['total_sales'].shift(n)
data['total_sales_seasonal_diff'].dropna().plot(title="Seasonally Differenced Total Sales", figsize=(10, 6))
plt.show()
```
# Log transformation and differencing
```
data['total_sales_log'] = np.log(data['total_sales'])
data['total_sales_log_diff'] = data['total_sales_log'] - data['total_sales_log'].shift(1)
data['total_sales_log_diff'].dropna().plot(title="Log Differenced Total Sales", figsize=(10, 6))
plt.show()
```
# Perform ADF test on the transformed 'total_sales_log_diff' column
```
adf_test(data['total_sales_log_diff'])
```

### OUTPUT:


# REGULAR DIFFERENCING:
![image](https://github.com/user-attachments/assets/689b330d-124b-47ac-85fb-9aabd36c899f)


# SEASONAL ADJUSTMENT:
![image](https://github.com/user-attachments/assets/6c8ae9d9-cdb1-46fe-bb2f-33d9ddaf7c82)



# LOG TRANSFORMATION:
![image](https://github.com/user-attachments/assets/e0f71071-7d54-4d4e-b2ea-f8d77b740895)



### RESULT:
Thus the python code for the conversion of non stationary to stationary data on cinema ticket sold data.
