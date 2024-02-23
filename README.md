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
