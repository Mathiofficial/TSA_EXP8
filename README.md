### Developed By: Mathiyazhagan A
### Reg No: 212222240075
### Date: 

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

![Uploading MV.png…]()


### Exponential Smoothing :

![Uploading ES.png…]()





### RESULT:
Thus, The Moving Average Model and Exponential smoothing using python is successfully implemented.
