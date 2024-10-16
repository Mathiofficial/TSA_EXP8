## Developed By: Mathiyazhagan A
## Reg No: 212222240063
## Date: 

# Ex.No: 08     MOVING AVERAGE MODEL AND EXPONENTIAL SMOOTHING


### AIM:
To implement Moving Average Model and Exponential smoothing Using Python.

### ALGORITHM:
1. Import necessary libraries
2. Read the electricity time series data from a CSV file, Display the shape and the first 5 rows of
the dataset
3. Set the figure size for plots
4. Suppress warnings
5. Plot the first 50 values of the 'Value' column
6. Perform rolling average transformation with a window size of 5
7. Display the first 10 values of the rolling mean
8. Perform rolling average transformation with a window size of 10
9. Create a new figure for plotting,Plot the original data and fitted value
10. Show the plot
11. Also perform exponential smoothing and plot the graph
    
### PROGRAM:
```python
# Import necessary libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import warnings
from statsmodels.tsa.holtwinters import ExponentialSmoothing

# Suppress warnings
warnings.filterwarnings('ignore')

# Load the dataset
data = pd.read_csv('seattle_weather.csv')

# Convert 'DATE' to datetime format and set it as the index
data['DATE'] = pd.to_datetime(data['DATE'])
data.set_index('DATE', inplace=True)

# Focus on the 'PRCP' (Precipitation) column
precipitation_data = data[['PRCP']].resample('M').mean().dropna()

# Display the shape and the first 5 rows of the dataset
print("Shape of the dataset:", precipitation_data.shape)
print("First 5 rows of the dataset:")
print(precipitation_data.head())

# Plot Original Dataset (Monthly Precipitation Data)
plt.figure(figsize=(12, 6))
plt.plot(precipitation_data['PRCP'], label='Original Monthly Precipitation Data', color='blue')
plt.title('Original Monthly Precipitation Data')
plt.xlabel('Date')
plt.ylabel('Precipitation (inches)')
plt.legend()
plt.grid()
plt.show()

# Perform rolling average transformation with a window size of 12 (1 year)
rolling_mean_12 = precipitation_data['PRCP'].rolling(window=12).mean()

# Plot Moving Average
plt.figure(figsize=(12, 6))
plt.plot(precipitation_data['PRCP'], label='Original Monthly Precipitation Data', color='blue')
plt.plot(rolling_mean_12, label='Moving Average (window=12)', color='orange')
plt.title('12-Month Moving Average of Precipitation Data')
plt.xlabel('Date')
plt.ylabel('Precipitation (inches)')
plt.legend()
plt.grid()
plt.show()

# Apply Exponential Smoothing (Trend: Additive, No Seasonal Component)
model = ExponentialSmoothing(precipitation_data['PRCP'], trend='add', seasonal=None)
model_fit = model.fit()

# Make predictions for the next 24 periods (2 years)
predictions = model_fit.predict(start=len(precipitation_data), end=len(precipitation_data) + 23)

# Plot the original data and Exponential Smoothing predictions
plt.figure(figsize=(12, 6))
plt.plot(precipitation_data['PRCP'], label='Original Monthly Precipitation Data', color='blue')
plt.plot(predictions, label='Exponential Smoothing Forecast', color='orange')
plt.title('Exponential Smoothing Predictions for Monthly Precipitation')
plt.xlabel('Date')
plt.ylabel('Precipitation (inches)')
plt.legend()
plt.xticks(rotation=45)
plt.grid(True)
plt.tight_layout()
plt.show()


```

### OUTPUT:

### Original Data Plot:

![{8CA68E9B-4367-4CF0-A966-52BD25B6866A}](https://github.com/user-attachments/assets/58565e0d-dde7-4040-91a1-3f03425c9fb4)

### Moving Average :

![{0D982DC4-3331-405E-AAE8-50686B923134}](https://github.com/user-attachments/assets/d8e1a65e-4357-4502-a1eb-5d2a6e908173)


### Exponential Smoothing :

![{11A447A6-8109-4A6A-8BC5-2AC0245C9575}](https://github.com/user-attachments/assets/bfac51bc-17b3-4ec0-8961-863891175e2d)



### RESULT:
Thus, The Moving Average Model and Exponential smoothing using python is successfully implemented.
