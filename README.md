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
```
pip3 install torch-scatter -f https://data.pyg.org/whl/torch-1.4.0+cu101.html
```
