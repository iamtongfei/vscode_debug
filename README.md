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
Solut:
<img width="862" alt="image" src="https://github.com/iamtongfei/vscode_debug/assets/152712857/ffd78592-e8c9-4663-80a9-fa55af974159">

```
conda install -c pytorch torchvision cudatoolkit=10.1 pytorch
```
