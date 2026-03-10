# Ex.No: 05  IMPLEMENTATION OF TIME SERIES ANALYSIS AND DECOMPOSITION
### Date: 10-3-2026


### AIM:
To Illustrates how to perform time series analysis and decomposition on the monthly average temperature of a city/country and for airline passengers.

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the decomposition process for the required data.
4. Plot the data according to need, either seasonal_decomposition or trend plot.
5. Display the overall results.

### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Step 1: Load the dataset
data = pd.read_csv(r"/content/global_sports_footwear_sales_2018_2026.csv",
                   parse_dates=['order_date']) # Changed 'Date' to 'order_date'

# Step 2: Select one company (Example: Nike)
data = data[data['brand'] == 'Nike'] # Changed 'Ticker' to 'brand' and 'AAPL' to 'Nike'

# Step 3: Set order_date as index
data.set_index('order_date', inplace=True) # Changed 'Date' to 'order_date'

# Step 4: Select revenue_usd
data = data[['revenue_usd']] # Changed 'Close' to 'revenue_usd'

# Step 5: Convert daily data to monthly average
data_monthly = data.resample('MS').mean()

# Step 6: Fill missing values
data_monthly = data_monthly.fillna(method='ffill')

# Step 7: Perform seasonal decomposition
decomposition = seasonal_decompose(data_monthly['revenue_usd'], # Changed 'Close' to 'revenue_usd'
                                   model='additive',
                                   period=12)

# Step 8: Plot decomposition
plt.figure(figsize=(10,12))

# Original Time Series
plt.subplot(411)
plt.plot(data_monthly['revenue_usd']) # Changed 'Close' to 'revenue_usd'
plt.title("ORIGINAL TIME SERIES DATA (MONTHLY REVENUE USD)") # Updated title
plt.ylabel("Revenue (USD)") # Updated ylabel

# Trend Plot
plt.subplot(412)
plt.plot(decomposition.trend)
plt.title("LINEAR TREND PLOT")
plt.ylabel("Revenue (USD)") # Updated ylabel

# Seasonal Plot
plt.subplot(413)
plt.plot(decomposition.seasonal)
plt.title("SEASONALITY PLOT")
plt.ylabel("Revenue (USD)") # Updated ylabel

# Residual Plot
plt.subplot(414)
plt.plot(decomposition.resid)
plt.title("RESIDUAL PLOT")
plt.ylabel("Revenue (USD)") # Updated ylabel

plt.tight_layout()
plt.show()
```
### OUTPUT:
<img width="885" height="506" alt="Screenshot 2026-03-10 112613" src="https://github.com/user-attachments/assets/953498df-39de-4f0e-b064-81e6c4b260a3" />
<img width="872" height="552" alt="image" src="https://github.com/user-attachments/assets/5759170e-6ee6-493a-ae57-d66ab7d54db0" />
### RESULT:
Thus we have created the python code for the time series analysis and decomposition.
