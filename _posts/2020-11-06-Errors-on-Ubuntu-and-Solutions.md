
- [Pycharm/Python Issues](#pycharm_python_issue)
- [TensorRT Issues](#tensorrt_issue)
- [CUDA, cuDNN Issues](#cuda_cudnn_issues)

## Pycharm/Python Issues

1. Pycharm error

`ModuleNotFoundError: No module named 'sklearn.utils.linear_assignment_'`

![sklearn error](/images/sklearn_error.png)

- Solution:

```
$ sudo pip3 install scikit-learn==0.22.2
```

2. nvcc -V command error

- Solution: We should add the path for CUDA

```
$ gedit ~/.bashrc  
```

Add this:

```
export CUDA_HOME=/usr/local/cuda-10.2
export CUDNN_INSTALL_DIR=/usr/local/cuda-10.0
export LD_LIBRARY_PATH=${CUDA_HOME}/lib64

PATH=${CUDA_HOME}/bin:${PATH}
export PATH
```

Check again:

```
$ nvcc -V
```

An output should be like this:

```
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2019 NVIDIA Corporation
Built on Wed_Oct_23_19:24:38_PDT_2019
Cuda compilation tools, release 10.2, V10.2.89
```

## TensorRT Issues

```
ImportError: libnvinfer.so.5: cannot open shared object file: No such file or directory
```

- Solution:

```
$ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/jason/TensorRT-5.0.2.6/lib
```


## CUDA, cuDNN Issues

```
This sample requires CUDNN, but it could not be found.
Please install CUDNN from https://developer.nvidia.com/cudnn or specify CUDNN_INSTALL_DIR when compiling.
For example, `make CUDNN_INSTALL_DIR=/path/to/CUDNN/` where /path/to/CUDNN/ contains include/ and lib/ subdirectories.
```

- Solution

Open Nano Environment

```
$ sudo nano /etc/environment
```

Check and add information as below:

```
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/usr/local/cuda-10.0/bin"
CUDA_INSTALL_DIR="/usr/local/cuda-10.0"
CUDNN_INSTALL_DIR="/usr/local/cuda-10.0"
```

And then

Press
```
Step 1. Ctr o to save
Step 2. Enter
Step 3. Ctrl x to exit,
```
Reboot

```
$ sudo reboot
```
