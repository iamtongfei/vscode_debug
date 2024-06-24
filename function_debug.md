## Normal Test && Samples
```
Log {name} {obj_id}
```

name == scene id (but we don't know how many scene we have, and whether this obj occured in this scene

#### SO, we have two outcomes
#### (1) KeyError: '2' , MEANS LOG 0 2 Not Exists

```
2024-06-18 13:12:57,703 - root - WARNING - Log 0 2
==== debug ====
/Users/tongfeiguo/Downloads/adversarial_cav-master/test/data/dataset/apolloscape/multi_frame/raw/0.json
debug+++ what is f?????
<_io.TextIOWrapper name='/Users/tongfeiguo/Downloads/adversarial_cav-master/test/data/dataset/apolloscape/multi_frame/raw/0.json' mode='r' encoding='UTF-8'>
2024-06-18 13:12:57,799 - root - ERROR - Error!
2024-06-18 13:12:57,800 - root - ERROR - Traceback (most recent call last):
  File "/Users/tongfeiguo/Downloads/adversarial_cav-master/test/test_utils.py", line 199, in normal_test
    test_core(api, input_data, obj_id, attack_length, result_path, figure_path)
  File "/Users/tongfeiguo/Downloads/adversarial_cav-master/test/test_utils.py", line 143, in test_core
    result["output_data"][str(k)]["objects"][str(obj_id)][trace_name].astype(np.float32)
KeyError: '2'

```
#### (2) 有信息的
1/ name 对应raw/{name}.json 相当于每一个json都是一个scene <br>
所以才有json里面有很多个object<br>
也对应 ADV README 里面写的<br>
Format of JSON-format input trajectory data
```
{
    "observe_length": int,
    "predict_length": int,
    "time_step": float,
    "feature_dimension": int, // extra features other than x-y location coordinates
    "objects": {
        "string object id": {
            "type": int,  // 1: small vehicle 2: large vehicle 3: pedestrian 4: unknown
            "complete": bool, // all time frames are filled
            "visible": bool, // the last frame of history is filled
            "observe_trace": [observe_length * 2],
            "observe_feature": [observe_length * feature_dimension],
            "observe_mask": [observe_length],
            "future_trace": [predict_length * 2],
            "future_feature": [predict_length * feature_dimension],
            "future_mask": [predict_length],
            "predict_trace": [predict_length * 2] // Empty before inference
        }, ...
    }
}
```
2/ PRINT OUT THE ADE: 这句话在loss.py line 104, 所以这里是有一个ADE的值的
```
2024-06-18 13:12:57,800 - root - WARNING - Log 0 3
==== debug ====
/Users/tongfeiguo/Downloads/adversarial_cav-master/test/data/dataset/apolloscape/multi_frame/raw/0.json
debug+++ what is f?????
<_io.TextIOWrapper name='/Users/tongfeiguo/Downloads/adversarial_cav-master/test/data/dataset/apolloscape/multi_frame/raw/0.json' mode='r' encoding='UTF-8'>
PRINT OUT THE ADE: 
[tensor(1.4550, device='mps:0')]
2024-06-18 13:12:57,934 - root - ERROR - Error!
2024-06-18 13:12:57,935 - root - ERROR - Traceback (most recent call last):
  File "/Users/tongfeiguo/Downloads/adversarial_cav-master/test/test_utils.py", line 199, in normal_test
    test_core(api, input_data, obj_id, attack_length, result_path, figure_path)
  File "/Users/tongfeiguo/Downloads/adversarial_cav-master/test/test_utils.py", line 146, in test_core
    result["loss"][attack_goal] += float(attack_loss(*args, str(obj_id), None, type=attack_goal).item())
  File "/Users/tongfeiguo/Downloads/adversarial_cav-master/test/../prediction/attack/loss.py", line 119, in attack_loss
    raise NotImplementedError()
NotImplementedError
```

```
2024-06-18 13:12:57,935 - root - WARNING - Log 0 4
==== debug ====
/Users/tongfeiguo/Downloads/adversarial_cav-master/test/data/dataset/apolloscape/multi_frame/raw/0.json
debug+++ what is f?????
<_io.TextIOWrapper name='/Users/tongfeiguo/Downloads/adversarial_cav-master/test/data/dataset/apolloscape/multi_frame/raw/0.json' mode='r' encoding='UTF-8'>
2024-06-18 13:12:58,054 - root - ERROR - Error!
2024-06-18 13:12:58,055 - root - ERROR - Traceback (most recent call last):
  File "/Users/tongfeiguo/Downloads/adversarial_cav-master/test/test_utils.py", line 199, in normal_test
    test_core(api, input_data, obj_id, attack_length, result_path, figure_path)
  File "/Users/tongfeiguo/Downloads/adversarial_cav-master/test/test_utils.py", line 143, in test_core
    result["output_data"][str(k)]["objects"][str(obj_id)][trace_name].astype(np.float32)
KeyError: '4'

2024-06-18 13:12:58,055 - root - WARNING - Log 313 319
==== debug ====
/Users/tongfeiguo/Downloads/adversarial_cav-master/test/data/dataset/apolloscape/multi_frame/raw/313.json
debug+++ what is f?????
<_io.TextIOWrapper name='/Users/tongfeiguo/Downloads/adversarial_cav-master/test/data/dataset/apolloscape/multi_frame/raw/313.json' mode='r' encoding='UTF-8'>
PRINT OUT THE ADE: 
[tensor(1.9389, device='mps:0')]
2024-06-18 13:12:58,183 - root - ERROR - Error!
2024-06-18 13:12:58,184 - root - ERROR - Traceback (most recent call last):
  File "/Users/tongfeiguo/Downloads/adversarial_cav-master/test/test_utils.py", line 199, in normal_test
    test_core(api, input_data, obj_id, attack_length, result_path, figure_path)
  File "/Users/tongfeiguo/Downloads/adversarial_cav-master/test/test_utils.py", line 146, in test_core
    result["loss"][attack_goal] += float(attack_loss(*args, str(obj_id), None, type=attack_goal).item())
  File "/Users/tongfeiguo/Downloads/adversarial_cav-master/test/../prediction/attack/loss.py", line 119, in attack_loss
    raise NotImplementedError()
NotImplementedError
```


ADE => p.d.f. => log likehood
```
Yes, calculating the log-likelihood of the Average Displacement Error (ADE) involves understanding the probability density of the ADE. Here’s how you can approach it:

### Key Steps to Calculate Log-Likelihood of ADE

1. **Understand ADE**:
   - ADE measures the average L2 distance between the true and predicted trajectory points:
     \[
     \text{ADE} = \frac{1}{T} \sum_{t=1}^T \|\mathbf{y}_t - \mathbf{\mu}_t\|
     \]

2. **Model ADE's Distribution**:
   - To compute the log-likelihood, you need a probabilistic model of the ADE.
   - A common assumption is that the individual displacement errors \( \|\mathbf{y}_t - \mathbf{\mu}_t\| \) are Gaussian, leading to a distribution for ADE. If the errors \( \|\mathbf{y}_t - \mathbf{\mu}_t\| \) follow a Gaussian distribution, their average (ADE) will also follow a Gaussian distribution due to the Central Limit Theorem.

3. **Probability Density of ADE**:
   - If the displacement errors are normally distributed with variance \( \sigma^2 \), the ADE over \( T \) time steps will have a mean related to the true average error and a variance \( \frac{\sigma^2}{T} \):
     \[
     \text{ADE} \sim \mathcal{N}\left(\text{Expected ADE}, \frac{\sigma^2}{T}\right)
     \]
   - The probability density function (PDF) of a Gaussian random variable \( x \) is:
     \[
     f(x) = \frac{1}{\sqrt{2 \pi \sigma^2}} \exp\left(-\frac{(x - \mu)^2}{2\sigma^2}\right)
     \]

4. **Log-Likelihood Calculation**:
   - Using the PDF, the log-likelihood of the ADE is:
     \[
     \log \mathcal{L}(\text{ADE}) = \log f(\text{ADE}) = -\frac{1}{2} \left( \log(2 \pi \sigma^2) + \frac{(\text{ADE} - \mu)^2}{\sigma^2} \right)
     \]
     where \( \mu \) is the expected ADE, and \( \sigma^2 \) is the variance of the ADE.

### Example in Python

Assuming that the displacement errors follow a Gaussian distribution:

```python
import numpy as np

def compute_ade(true_trajectory, predicted_means):
    errors = np.linalg.norm(np.array(true_trajectory) - np.array(predicted_means), axis=1)
    ade = np.mean(errors)
    return ade

def log_likelihood_of_ade(ade, mu, sigma_squared, T):
    # Log-likelihood assuming ADE follows N(mu, sigma^2 / T)
    sigma_squared_ade = sigma_squared / T
    log_likelihood = -0.5 * (np.log(2 * np.pi * sigma_squared_ade) + (ade - mu)**2 / sigma_squared_ade)
    return log_likelihood

# Example usage
true_trajectory = [np.array([1, 2]), np.array([2, 3]), np.array([3, 4])]
predicted_means = [np.array([1.1, 2.1]), np.array([2.1, 3.1]), np.array([3.1, 4.1])]
expected_ade = 0.1  # Expected ADE, can be derived from training data or assumptions
sigma_squared = 0.05  # Example variance
T = len(true_trajectory)

ade = compute_ade(true_trajectory, predicted_means)
log_likelihood_ade = log_likelihood_of_ade(ade, expected_ade, sigma_squared, T)

print(f"ADE: {ade}")
print(f"Log-Likelihood of ADE: {log_likelihood_ade}")
```

### Key Points:

- **Distribution Assumption**: The calculation assumes that the ADE follows a Gaussian distribution due to the underlying errors being Gaussian.
- **Expected ADE**: The expected value of ADE (\( \mu \)) and its variance \( \sigma^2 \) must be known or estimated from data.
- **Log-Likelihood**: Uses the Gaussian PDF to compute the log-likelihood for the observed ADE.

### Summary:

To calculate the log-likelihood of the ADE:
1. **Estimate or assume** the distribution of ADE based on the error distribution.
2. **Calculate the PDF** of ADE using the Gaussian distribution.
3. **Compute the log-likelihood** using the PDF.

This approach provides a probabilistic interpretation of ADE and can be used to assess the likelihood of the observed average prediction error under the model's assumptions.

Do you have any specific details or additional constraints you want to include in this model?
```
