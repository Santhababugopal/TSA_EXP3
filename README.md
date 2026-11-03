# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
Date: 03-11-2026

### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.
### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
### PROGRAM:
```python

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load Gold Stock Dataset
df = pd.read_excel("/content/goldstock_100_rows.xlsx")

# Convert Date column
df['Date'] = pd.to_datetime(df['Date'])

# Sort data by date
df = df.sort_values('Date')

# Select Volume data
data = df['Volume'].values

# Find number of observations
N = len(data)

# Define lags
lags = range(35)

# Calculate mean and variance
mean_data = np.mean(data)
variance_data = np.var(data)

# Normalize the data
normalized_data = (data - mean_data) / np.sqrt(variance_data)

# Calculate autocorrelation
autocorr_values = []

for lag in lags:
    if lag == 0:
        autocorr_values.append(1)
    else:
        auto_cov = np.sum(
            (data[:-lag] - mean_data) *
            (data[lag:] - mean_data)
        ) / N

        autocorr_values.append(auto_cov / variance_data)

# Plot ACF graph
plt.figure(figsize=(10, 6))
plt.stem(lags, autocorr_values)

plt.title('Autocorrelation of Gold Trading Volume')
plt.xlabel('Lag')
plt.ylabel('Autocorrelation')
plt.grid(True)

plt.show()


```

### OUTPUT:

<img width="1236" height="673" alt="image" src="https://github.com/user-attachments/assets/23e0330f-3d2a-41b8-ba9c-27dc0a308f92" />

### RESULT:
Thus we have successfully implemented the auto correlation function in python.
