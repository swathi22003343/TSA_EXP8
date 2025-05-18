# Ex.No: 08     MOVINTG AVERAGE MODEL AND EXPONENTIAL SMOOTHING

### AIM:
To implement Moving Average Model and Exponential smoothing Using Python.
### ALGORITHM:
1. Import necessary libraries
2. Read the electricity time series data from a CSV file,Display the shape and the first 20 rows of
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
```py
# Import necessary libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import warnings
from statsmodels.tsa.holtwinters import ExponentialSmoothing
```
Suppress warnings
```py
warnings.filterwarnings('ignore')
```
Read the AirPassengers dataset
```py
data = pd.read_csv('AirPassengers.csv')
```
Convert 'Month' to datetime format and set it as the index
```py
data['Month'] = pd.to_datetime(data['Month'], format='%Y-%m')
data.set_index('Month', inplace=True)
```
Focus on the '#Passengers' column
```py
passengers_data = data[['#Passengers']]
```
Display the shape and the first 5 rows of the dataset
```py
print("Shape of the dataset:", passengers_data.shape)
print("First 5 rows of the dataset:")
print(passengers_data.head())
```
Plot Original Dataset (#Passengers Data)
```py
plt.figure(figsize=(12, 6))
plt.plot(passengers_data['#Passengers'], label='Original #Passengers Data', color='blue')
plt.title('Original Passenger Data')
plt.xlabel('Date')
plt.ylabel('Number of Passengers')
plt.legend()
plt.grid()
plt.show()
```
Moving Average
Perform rolling average transformation with a window size of 10
```py
rolling_mean_10 = passengers_data['#Passengers'].rolling(window=10).mean()
```
Plot Moving Average
```py
plt.figure(figsize=(12, 6))
plt.plot(passengers_data['#Passengers'], label='Original #Passengers Data', color='blue')
plt.plot(rolling_mean_10, label='Moving Average (window=10)', color='orange')
plt.title('Moving Average of Passenger Data')
plt.xlabel('Date')
plt.ylabel('Number of Passengers')
plt.legend()
plt.grid()
plt.show()
```
Exponential Smoothing
```py
model = ExponentialSmoothing(passengers_data['#Passengers'], trend='add', seasonal=None)
model_fit = model.fit()
```
Make predictions for the next 30 periods (you can adjust this)
```py
predictions = model_fit.predict(start=len(passengers_data), end=len(passengers_data) + 30)
```
Plot the original data and Exponential Smoothing predictions
```py
plt.figure(figsize=(12, 6))
plt.plot(passengers_data['#Passengers'], label='Original #Passengers Data', color='blue')
plt.plot(predictions, label='Exponential Smoothing Forecast', color='orange')
plt.title('Exponential Smoothing Predictions for Passenger Data')
plt.xlabel('Date')
plt.ylabel('Number of Passengers')
plt.legend()
plt.xticks(rotation=45)
plt.grid(True)
plt.tight_layout()
plt.show()
```

### OUTPUT:

![image](https://github.com/user-attachments/assets/29797605-18f7-4c6d-9872-74cd9c1553a5)

Moving Average

![Untitled](https://github.com/user-attachments/assets/65c77ea9-571b-4afd-b1e0-2ecd6b751353)

Plot Transform Dataset

![Untitled](https://github.com/user-attachments/assets/8c7c0c7b-e32c-4621-ab0d-98becf27ef13)


Exponential Smoothing

![Untitled](https://github.com/user-attachments/assets/8e932799-faaf-43d3-b8d8-c527cde5859c)


### RESULT:
Thus we have successfully implemented the Moving Average Model and Exponential smoothing using python.
