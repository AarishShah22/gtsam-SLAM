# Implementation of SLAM using the GTSAM Library

This repository contains the implementation of 2D and 3D SLAM using the GTSAM Library. The SLAM problem was solved by using Factor Graphs. For both cases, Batch as well as Incremental methods were used and their performance was compared. 

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

I have used datasets using G2O files for running SLAM. You can learn more about G2O files [here](https://github.com/RainerKuemmerle/g2o/wiki/File-Format-SLAM-2D).

The VERTEX_SE2 data represents the robot's pose data at different timesteps. The EDGE_SE2 data represents the connections between the poses (constraints).

## 2D SLAM

Use the "input_INTEL_g2o.g2o" for 2D SLAM. 

### Batch

First, we create a Pose Graph, based on the vertices and edges data given to us. Then, we optimize the entire graph as a batch. 

We construct the graph:

```
graph = gtsam.NonLinearFactorGraph()
```

Further, we use the Gauss Newton Optimizer for optimization. Optimization is essentially trying to solve the least-squares problem. The goal is to minimize the error between estimated and measured values. When a loop closure case occurs, the optimization is more constrained, thus the measurement drift is better accounted for. 

### Incremental

For the incremental solution, the poses and edges are added to the factor graph one by one. After each pose and edge pair is added to the factor graph one by one. After each pose and edge pair is added, we optimize it and then move on to the next measurement. This method is useful for real-time SLAM.

We use the ISAM solver to optimize the solutions. 

## 3D SLAM

Use the "parking-garage.g2o" for 2D SLAM. 

3D SLAM was also implemented in Batch and Incremental mode.