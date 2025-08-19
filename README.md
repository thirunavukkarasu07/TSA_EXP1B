# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 19.08.2025

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Load dataset
data = pd.read_csv("C:\\Users\\admin\\time series\\housing_price_dataset.csv")

# Group by YearBuilt to create a time series of average prices per year
price_series = data.groupby("YearBuilt")["Price"].mean().reset_index()

# Convert YearBuilt to datetime for time series analysis
price_series['YearBuilt'] = pd.to_datetime(price_series['YearBuilt'], format='%Y')
price_series.set_index('YearBuilt', inplace=True)

# Original series
series = price_series['Price']

# 1. Regular Differencing
price_series['diff'] = series - series.shift(1)

# 2. Log Transformation
price_series['log'] = np.log(series)

# 3. Log Differencing
price_series['log_diff'] = price_series['log'] - price_series['log'].shift(1)

# 4. Seasonal Decomposition (using log transformed data)
result = seasonal_decompose(price_series['log'].dropna(), model='additive', period=5)

# 5. Seasonal Differencing
price_series['log_seasonal_diff'] = price_series['log_diff'] - price_series['log_diff'].shift(5)

# ---- Plotting ----
plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(series, label='Original')
plt.legend(loc='best')
plt.title('Original Data (Average Price per Year)')

plt.subplot(6, 1, 2)
plt.plot(price_series['diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')

plt.subplot(6, 1, 3)
plt.plot(result.trend, label='Trend (Decomposition)')
plt.legend(loc='best')
plt.title('Trend (from Seasonal Decomposition)')

plt.subplot(6, 1, 4)
plt.plot(price_series['log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')

plt.subplot(6, 1, 5)
plt.plot(price_series['log_diff'], label='Log Differencing')
plt.legend(loc='best')
plt.title('Log Transformation + Differencing')

plt.subplot(6, 1, 6)
plt.plot(price_series['log_seasonal_diff'], label='Log + Differencing + Seasonal Differencing')
plt.legend(loc='best')
plt.title('Log + Regular + Seasonal Differencing')

plt.tight_layout()
plt.show()
```


### OUTPUT:

ORIGINAL DATA:

<img width="1247" height="206" alt="image" src="https://github.com/user-attachments/assets/9f40275c-c3b6-4584-ac8c-cbda1789df76" />



REGULAR DIFFERENCING:

<img width="1232" height="205" alt="image" src="https://github.com/user-attachments/assets/cb9f0dba-2ef6-4f43-9aa6-21064837d7e8" />


SEASONAL ADJUSTMENT:

<img width="1242" height="203" alt="image" src="https://github.com/user-attachments/assets/805e97e4-6747-4ad2-839a-18167f5dd61d" />


LOG TRANSFORMATION:

<img width="1226" height="200" alt="image" src="https://github.com/user-attachments/assets/31d5c5cc-47de-467e-a74f-f413ac8849d5" />


<img width="1215" height="198" alt="image" src="https://github.com/user-attachments/assets/77ee235b-c977-4e28-b723-d9543850879d" />


<img width="1213" height="205" alt="image" src="https://github.com/user-attachments/assets/7274750e-a410-404b-b066-6aa8f0ae88f9" />

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
