## Normal Test && Samples

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
