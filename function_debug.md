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
1/ name 对应raw/{name}.json 相当于每一个json都是一个scene 
所以才有json里面有很多个object
也对应 ADV README 里面写的
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
