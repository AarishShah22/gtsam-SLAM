# Implementation of SLAM using the GTSAM Library

This repository contains the implementation of 2D and 3D SLAM using the GTSAM Library. For both cases, Batch as well as Incremental methods were used and their performance was compared.

## GTSAM Installation

The Python wrapper for GTSAM can be installed in two ways:

1. Using pip to install directly:
``` 
pip install gtsam 
```
2. If that doesn't work, you can build from source. 

    a. After you successfully clone the repository and create the build folder, you’ll have to first go
    into the cython folder and install the required dependencies.
    ```
    pip install -r <gtsam_folder>/python/requirements.txt
    ```
    b. Then you’ll have to do cmake differently by specifying the the Python version you want to use
    and enable Python wrapper:
    ```
    cmake .. -DGTSAM_BUILD_PYTHON=1 -DGTSAM_PYTHON_VERSION=<your_python_version>
    ```
    c. Compile the files in build (-j means using multi-thread. 10 is the number of threads you want
    to use)
    make -j10
    d. Install it to your machine
    ```
    sudo make python-install
    ```

If neither of these work for you, you can just use it on Google Colab by running 
```
!pip install gtsam
```
in the first cell of your Jupyter notebook.

## G2O files

TODO

## 2D SLAM

TODO 

### Batch

TODO

### Incremental

TODO

## 3D SLAM

TODO

### Batch

TODO

### Incremental

TODO