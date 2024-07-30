To perform Naive Out-Of-Distribution (OOD) detection for identifying change points in your 2254 data points, you can follow these steps:

### 1. Calculate the Moving Average and Standard Deviation
Compute the moving average and moving standard deviation over a specified window size. This helps to smooth the data and identify potential deviations from the normal behavior.

### 2. Compute the Z-Scores
Calculate the Z-scores for each data point using the moving average and moving standard deviation. The Z-score represents how many standard deviations a data point is from the mean.

### 3. Set a Threshold for Z-Scores
Determine a threshold for the Z-scores. Data points with Z-scores exceeding this threshold are considered potential OOD points.

### 4. Detect Change Points
Identify the points where the Z-score exceeds the threshold as change points.

Here's a Python code example to illustrate these steps:

```python
import numpy as np
import pandas as pd

# Generate some synthetic data
np.random.seed(42)
data = np.random.normal(loc=0.0, scale=1.0, size=2254)

# Add a change point in the data
data[1127:] += 3

# Parameters
window_size = 50
z_score_threshold = 3.0

# Calculate the moving average and standard deviation
rolling_mean = pd.Series(data).rolling(window=window_size).mean()
rolling_std = pd.Series(data).rolling(window=window_size).std()

# Calculate Z-scores
z_scores = (data - rolling_mean) / rolling_std

# Detect change points
change_points = np.where(np.abs(z_scores) > z_score_threshold)[0]

print(f"Change points detected at indices: {change_points}")

# Visualize the results (optional)
import matplotlib.pyplot as plt

plt.figure(figsize=(14, 7))
plt.plot(data, label='Data')
plt.plot(rolling_mean, label='Moving Average', color='orange')
plt.scatter(change_points, data[change_points], color='red', label='Change Points')
plt.legend()
plt.show()
```

### Explanation:
1. **Data Generation**: The synthetic data is generated with a normal distribution. A change point is added at the midpoint.
2. **Moving Average and Standard Deviation**: The moving average and standard deviation are computed using a window size of 50.
3. **Z-Scores Calculation**: Z-scores are computed for each data point.
4. **Change Point Detection**: Points where the absolute Z-score exceeds the threshold of 3 are identified as change points.

### Adjustments:
- **Window Size**: Adjust the window size based on the expected scale of the changes.
- **Threshold**: Fine-tune the Z-score threshold to balance sensitivity and false positives.

Feel free to modify the code to fit your specific requirements and data characteristics.
