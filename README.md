# vscode_debug
### 01 ERROR: Could not build wheels for numpy, which is required to install pyproject.toml-based projects 
Python 3.6+
- run the code (download the requirements.txt)
```
pip install -r requirements.txt
```
- error msg
```
    × Building wheel for numpy (pyproject.toml) did not run successfully.
    │ exit code: 1
    ╰─> [888 lines of output]
        Running from numpy source directory.
```
```
    note: This error originates from a subprocess, and is likely not a problem with pip.
    ERROR: Failed building wheel for numpy
  Failed to build numpy
  ERROR: Could not build wheels for numpy, which is required to install pyproject.toml-based projects
  [end of output]
```
### 01 SOLUTION
- check the requirements.txt (see each package version required)
- check the dependency https://matplotlib.org/devdocs/devel/min_dep_policy.html
- numpy version > python version > matplotlib version
  1.17 ~ 3.7
- download the corresponding python version

### 02 python vs python3 vs pip vs pip3
For Mac User- pip3 is most recommended: </br>
I used python3, and pip3, to maintain the consistency, you should always command start with pip3 (regardless how other did)

### 03 Add new python 3.7 into vscode
- download python 3.7 from the official website
- observe the download sucusess by check the hidden file
  ```
  1, Press Command + Shift + . (the period key). This will show hidden files in the folder.
  2, To hide the files again, press Command + Shift + . again.
  ```
- from the vscode [select intepreter]: you can copy the python3.7 stored path to access and select
- path 寻找方式:</br>
  open terminal: which python 3.7 </br>
  You can use which command to find out the location of Python 3.7
  ```
  which python3  
  #/Library/Frameworks/Python.framework/Versions/3.7/bin/python3
  which python3.7
  #/Library/Frameworks/Python.framework/Versions/3.7/bin/python3.7
  ```
### 04 ERROR: Module not found
```
from layers.graph import Graph
```
cannot find the module layers
steps:
- list the current packages installed in python, find whether layers package exists
  ```
  pip3 list
  ```
- locate the layers package
```
pip show layers
# provide details about the installation path
```
this is the output
```
pip3 show layers
Name: layers
Version: 0.1.5
Summary: Layered source layouts for software development projects
Home-page: https://github.com/ribozz/layers
Author: Alex Rudakov
Author-email: ribozz+layers@gmail.com
License: 
Location: /Library/Frameworks/Python.framework/Versions/3.7/lib/python3.7/site-packages
Requires: bashutils, PyYaml
Required-by:
```
- Module Structure: Verify the structure of the 'layers' module to ensure that it contains a submodule named 'graph'. If the module structure is different, you'll need to adjust your import statement accordingly.

### 05 install torch-scatter == 1.4.0 (but the current new version 2.2.0) how you download the previouse version
<img width="762" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/fc394fe4-494c-499a-bb58-96a1cf412e53">

however when I type this command:
```
pip3 install torch-scatter==1.4.0 -f https://data.pyg.org/whl/torch-1.4.0+cu101.html
```
there is an error
```
      error: [Errno 2] No such file or directory: '/usr/local/cuda/bin/nvcc': '/usr/local/cuda/bin/nvcc'
      [end of output]
  
  note: This error originates from a subprocess, and is likely not a problem with pip.
  ERROR: Failed building wheel for torch-scatter
  Running setup.py clean for torch-scatter
Failed to build torch-scatter
ERROR: Could not build wheels for torch-scatter, which is required to install pyproject.toml-based projects
```
-- check pytorch and all version
```
pip3 list | grep torch
```
give the results
```
torch                1.10.2
torch-scatter        2.1.1
torchvision          0.11.3
```
### 06 Exception has occurred: TypeError scatter_max() got an unexpected keyword argument 'fill_value'
<img width="861" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/76b0fb14-7b7c-483e-9870-25130d786b23">

example code for 1.8.0
```
pip install https://pytorch-geometric.com/whl/torch-1.8.0+cpu/torch_scatter-2.0.6-cp36-cp36m-win_amd64.whl
```
```
pip3 install https://data.pyg.org/whl/torch-1.4.0%2Bcpu/torch_cluster-1.5.2-cp36-cp36m-macosx_10_9_x86_64.whl
```
### 07 Module not found (but it is exists in the dir)
error:
```
  File "/Users/tongfeiguo/Downloads/AdvTrajectoryPrediction-master/prediction/model/GRIP/dataloader.py", line 8, in <module>
    from prediction.model.base.dataloader import DataLoader
ModuleNotFoundError: No module named 'prediction'
```
here is the code that request the module
```
from prediction.model.base.interface import Interface
```
debug process:
1. Check Relative Path:</br>
Ensure that the relative path specified in the import statement matches the directory structure of your project. In your case, it's trying to import DataLoader from prediction/model/base/dataloader.py. Verify that this file exists at the specified location relative to dataloader.py.</br>
2. Verify Module Existence:</br>
Double-check that there is indeed a module named prediction in your project, and it contains the necessary files, including __init__.py if it's intended to be a package. </br>
#### 7.1 what is __init__.py do?
If __init__.py is not empty, then whatever is in __init__.py is what will be available when you import the package (and things not imported into __init__.py won't be available at all).</br>
src: https://stackoverflow.com/questions/4142151/how-to-import-the-class-within-the-same-directory-or-sub-directory
#### python3 import module in the same dir
in order to import classes from files within the same directory, you would now write in Python 3:
```
from .user import User
from .dir import Dir
```
if you have the datastrcture:

<img width="668" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/efc74043-597e-4a24-9b2a-a6ebd02f4caf">

The other error I have is that, in terminal, if I run 
```
python3 test.py
```
all modules are not found, but if I just click "run" button, it works. Don't know why.

### 08 AssertionError: Torch not compiled with CUDA enabled
```
AssertionError: Torch not compiled with CUDA enabled
```
check this link: https://saturncloud.io/blog/what-is-assertionerror-torch-not-compiled-with-cuda-enabled/
This error occurs when you try to use Torch with CUDA, but the framework has not been compiled with CUDA support.

Solut:
<img width="862" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/ffd78592-e8c9-4663-80a9-fa55af974159">

```
conda install -c pytorch torchvision cudatoolkit=10.1 pytorch
```
Link: https://github.com/pytorch/pytorch#from-source | CUDA Version
If you want to compile with CUDA support, select a supported version of CUDA from our support matrix ([Link]([url](https://pytorch.org/get-started/locally/))), then install the following:

<img width="890" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/531656a7-4dfe-4d38-a571-ed3fa0018f26">


### 09 test.py (file not found error with model)
FQA model -- config file ??
<img width="1005" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/610fdd9f-20b0-4cca-b58d-9eff9d0c16ff">

GRIP++ model -- 'data/grip_apolloscape/model/original/best_model.pt'
<img width="898" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/df46b921-be01-4d2c-9c0b-b4f7f4510680">

### 10 Google Colab | upload local folder
Link: https://www.geeksforgeeks.org/how-to-upload-folders-to-google-colab/
zip and unzip (has video)

### 11 Python downgrade from 3.11 --> 3.7 (pip not found)
<img width="735" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/6ae6a363-74ef-496f-a272-14fdff64637d">
.step01 python 3.7 download 
.step02 pip package download
.step03 pip 3.7 util download
.step04 check version

### 12 Virtual ENV (python)
Link: https://docs.python.org/3/tutorial/venv.html

### 13 setup new vscode (windows)
.01 download vscode online
.02 sign in github
.03 download Git online (then enable git init and git clone)
.04 use vscode 'git clone' methods to clone the git repo to local 
.05 python version for env

### 14 google colab | Converting a Machine Learning Github Repo into a Colab Notebook
Link: https://www.youtube.com/watch?v=yRbvqCdfHF8

### 15 opencv package | AttributeError: module 'cv2.dnn' has no attribute 'DictValue'
Link: https://github.com/facebookresearch/nougat/issues/40
Solution:

<img width="472" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/71f50861-48d6-4359-a23b-ee11295f2c69">

### 16 running on a CPU-only machine, please use torch.load
Attempting to deserialize object on a CUDA device but torch.cuda.is_available() is False. If you are running on a CPU-only machine, please use torch.load with map_location=torch.device('cpu') to map your storages to the CPU.
Here is the code, and how I solve it:
<img width="1073" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/2422c12e-2fb8-41e5-b43e-f4d38ddcf723">

More helper links: https://stackoverflow.com/questions/75194415/please-use-torch-load-with-map-location-torch-devicecpu-to-map-your-storages

less relevent but can find the logic to understand: https://stackoverflow.com/questions/56369030/runtimeerror-attempting-to-deserialize-object-on-a-cuda-device

### 17 FileNotFoundError: [Errno 2] No such file or directory
`[Errno 2] No such file or directory: 'data/dataset/apolloscape/multi_frame/samples.txt'`
Link: https://stackoverflow.com/questions/22282760/filenotfounderror-errno-2-no-such-file-or-directory
<img width="593" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/c8aaac91-273c-4b8e-972d-22f5387a2246">

### 18 ValueError: invalid literal for int() with base 10: '1534157110.73'

original:
`#datasets[dataset_name]["samples"] = [(int(line.split(' ')[0]), int(line.split(' ')[1])) for line in lines]
`

solution:
`datasets[dataset_name]["samples"] = [(int(float(line.split(' ')[0])), int(float(line.split(' ')[1]))) for line in lines]`

Link: 
https://stackoverflow.com/questions/1841565/valueerror-invalid-literal-for-int-with-base-10

### 19 dismatch:
`
2024-03-27 15:00:02,859 - root - WARNING - Log 1534157110 44751
Traceback (most recent call last):
  File "test.py", line 180, in <module>
    main()
  File "test.py", line 173, in main
    normal(dataset_name=args.dataset, model_name=args.model, mode=args.mode, augment=args.augment, smooth=args.smooth, overwrite=args.overwrite)
  File "test.py", line 122, in normal
    normal_test(api, "data/dataset/{}/multi_frame/raw".format(dataset_name, mode), 
  File "/Users/feli/Downloads/AdvTrajectoryPrediction-master/test/test_utils.py", line 162, in normal_test
    input_data = load_data(os.path.join(data_dir, "{}.json".format(name)))
  File "/Users/feli/Downloads/AdvTrajectoryPrediction-master/test/../prediction/dataset/utils.py", line 37, in load_data
    with open(file_path, "r") as f:
FileNotFoundError: [Errno 2] No such file or directory: 'data/dataset/apolloscape/multi_frame/raw/1534157110.json'
`
in this folder we have:
<img width="264" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/0f00c5fe-0412-4a41-b0e5-4c6271bcd620">

In test.py here is the place for access the samples
<img width="793" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/7ab844f0-cde6-4479-8461-fa784c3e4b9d">

### 20 name and obj_id not fund
err msg:

<img width="926" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/8bb281b3-fdaa-4652-97b2-8e2cc9ab283f">

<img width="1368" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/49fcec2b-4a78-438a-aab0-99f8bb9bab0a">

### 20 pip install requirements.txt
error

<img width="870" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/dc947d06-69f4-4485-b622-f1520ef14ae9">

### 21 TypeError: Cannot convert a MPS Tensor to float64 dtype as the MPS framework doesn't support float64. Please use float32 instead.
link can find article here:
https://github.com/facebookresearch/segment-anything/issues/94

<img width="1008" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/e46b235f-ae43-487b-9a2d-ab06a826c67d">

### 22 replace all .cpu() ==> .to('mps)
then got the bug
TypeError: can't convert mps:0 device type tensor to numpy. Use Tensor.cpu() to copy the tensor to host memory first.

<img width="1426" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/cb0c737a-3256-4013-a3d8-6393ce7f9f4c">

底层逻辑是什么呢????
首先明白这几串.func()的含义, 我们底层逻辑是要让他支持'mps‘ 而不是cpu 所以猜测可能是固定搭配
link found the article here:
https://stackoverflow.com/questions/63582590/why-do-we-call-detach-before-calling-numpy-on-a-pytorch-tensor


<img width="996" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/1dfb8c27-76e9-4267-923a-05ee34f9768b">

As mentioned before, np.ndarray object does not have this extra "computational graph" layer and therefore, when converting a torch.tensor to np.ndarray you must explicitly remove the computational graph of the tensor using the detach() command.

所以, 这里方程是为了 convert to numpy, how to use mps device? 

### 23 TypeError: Cannot convert a MPS Tensor to float64 dtype as the MPS framework doesn't support float64. Please use float32 instead.
Here is my code: 
observe_traces[_obj_id] = torch.from_numpy(input_data["objects"][str(_obj_id)]["observe_trace"]).to('mps')

<img width="1425" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/fdbff806-875b-4d50-b1d0-da5b881062a4">





