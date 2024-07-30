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



Sure, here's the mathematical explanation formatted for GitHub Markdown:

### Mathematical Explanation

1. **Moving Average and Standard Deviation**:
   - The moving average (\(\mu_t\)) and standard deviation (\(\sigma_t\)) are computed over a sliding window of size \(w\):
     ```math
     \mu_t = \frac{1}{w} \sum_{i=t-w+1}^{t} x_i
     ```
     ```math
     \sigma_t = \sqrt{\frac{1}{w} \sum_{i=t-w+1}^{t} (x_i - \mu_t)^2}
     ```

2. **Z-Score Calculation**:
   - The Z-score for each data point \(x_t\) is calculated as:
     ```math
     z_t = \frac{x_t - \mu_t}{\sigma_t}
     ```
   - This represents how many standard deviations the data point \(x_t\) is from the moving average \(\mu_t\).

3. **Thresholding**:
   - A threshold is set (commonly 2 or 3). Data points where the absolute value of the Z-score exceeds this threshold are flagged as potential change points:
     ```math
     \text{change\_points} = \{ t \mid |z_t| > \text{threshold} \}
     ```

### Literature Review

1. **Box, G. E. P., & Jenkins, G. M. (1976). Time Series Analysis: Forecasting and Control**:
   - This book introduces methods for analyzing time series data, including moving averages and standard deviations, which are fundamental to the Z-score method.

2. **Page, E. S. (1954). Continuous Inspection Schemes. Biometrika, 41(1/2), 100-115**:
   - Introduces the Cumulative Sum (CUSUM) control chart, which is a sequential analysis technique for monitoring change detection. Z-score-based methods share a similar objective.

3. **Montgomery, D. C. (2009). Introduction to Statistical Quality Control**:
   - Discusses various control chart methods, including Shewhart control charts, which use standard deviations to detect outliers in process control.

4. **Shumway, R. H., & Stoffer, D. S. (2017). Time Series Analysis and Its Applications**:
   - Provides comprehensive coverage of time series analysis techniques, including those based on moving averages and standard deviations.

5. **Hawkins, D. M., Qiu, P., & Kang, C. W. (2003). The Changepoint Model for Statistical Process Control. Journal of Quality Technology, 35(4), 355-366**:
   - Explores models specifically designed for detecting change points in data streams.

### Summary
The use of Z-scores for change point detection is supported by a well-established statistical foundation. By leveraging the properties of the normal distribution and the concept of standard deviations, Z-scores can effectively highlight deviations and shifts in time series data. This method is both intuitive and practical, making it a popular choice in various fields including quality control, financial analysis, and anomaly detection.
