- [Installing TensorRT 5.0.2 for YOLOv3](#Installing_tensorrt)
- [Installing CUDA 10]

## Installing CUDA 10

```
$ sudo dpkg -i cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64.deb
$ sudo apt-key add /var/cuda-repo-10-0-local-10.0.130-410.48/7fa2af80.pub
$ sudo apt-get update
$ sudo apt-get install cuda-10-0
```

## Installing TensorRT 5.0.2 for YOLOv3

1.

Download TensorRT tar file version 5.0.2.6 from this [link](https://developer.nvidia.com/nvidia-tensorrt-5x-download).

Choose suitable version of tar packages in TensorRT 5.0 GA.

Install the following dependencies, if not already present:
```
‣ Install the CUDA Toolkit v9.0 or 10.0
‣ cuDNN 7.5.0
‣ Python 2 or Python 3 (Optional)
```

Then
Follow [this](https://developer.download.nvidia.com/compute/machine-learning/tensorrt/docs/5.0/GA_5.0.2.6/TensorRT-Installation-Guide.pdf) to know how to install

```    
$ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/path/to/folder/TensorRT-5.0.2.6/lib

$ cd python
$ sudo pip2 install tensorrt-5.0.2.6-py2.py3-none-any.whl
$ sudo pip3 install tensorrt-5.0.2.6-py2.py3-none-any.whl

$ cd ..
$ cd uff

$ sudo pip2 install uff-0.5.5-py2.py3-none-any.whl
$ sudo pip3 install uff-0.5.5-py2.py3-none-any.whl

$  which convert-to-uff

$ cd ..
$ cd graphsurgeon
$ sudo pip2 install graphsurgeon-0.3.2-py2.py3-none-any.whl
$ sudo pip3 install graphsurgeon-0.3.2-py2.py3-none-any.whl

```

Make sure CUDA should be like this:

```
nvcc -V
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2018 NVIDIA Corporation
Built on Sat_Aug_25_21:08:01_CDT_2018
Cuda compilation tools, release 10.0, V10.0.130

```

If NOT

Try to do this:
```
$ gedit ~/.bashrc
```

And then,

Add this to:

```
export CUDA_HOME=/usr/local/cuda-10.0
export CUDNN_INSTALL_DIR=/usr/local/cuda-10.0
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/jason/TensorRT-5.0.2.6/lib
export LD_LIBRARY_PATH=${CUDA_HOME}/lib64
PATH=${CUDA_HOME}/bin:${PATH}
export PATH
```

After installation, go to TensorRT-5.0.2.6/sample and run

```
$ make -j8
```

The above command will create some files in the TensorRT-5.0.2.6/bin folder.

Run below command.

```
$ ./sample_mnist
```
The output should be similar to this:

```
Building and running a GPU inference engine for MNIST
Input:
@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@#-:.-=@@@@@@@@@@@@@@
@@@@@%=     . *@@@@@@@@@@@@@
@@@@% .:+%%%  *@@@@@@@@@@@@@
@@@@+=#@@@@@# @@@@@@@@@@@@@@
@@@@@@@@@@@%  @@@@@@@@@@@@@@
@@@@@@@@@@@: *@@@@@@@@@@@@@@
@@@@@@@@@@- .@@@@@@@@@@@@@@@
@@@@@@@@@:  #@@@@@@@@@@@@@@@
@@@@@@@@:   +*%#@@@@@@@@@@@@
@@@@@@@%         :+*@@@@@@@@
@@@@@@@@#*+--.::     +@@@@@@
@@@@@@@@@@@@@@@@#=:.  +@@@@@
@@@@@@@@@@@@@@@@@@@@  .@@@@@
@@@@@@@@@@@@@@@@@@@@#. #@@@@
@@@@@@@@@@@@@@@@@@@@#  @@@@@
@@@@@@@@@%@@@@@@@@@@- +@@@@@
@@@@@@@@#-@@@@@@@@*. =@@@@@@
@@@@@@@@ .+%%%%+=.  =@@@@@@@
@@@@@@@@           =@@@@@@@@
@@@@@@@@*=:   :--*@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@

Output:
0:
1:
2:
3: **********
4:
5:
6:
7:
8:
9:
```

On terminal, run python3 and then try this:

```
import tensorrt
```

If it gives no error, then tensorrt installation is complete.

2. Yolov3 to Onnx conversion

- Go to a folder:

```
TensorRT-5.0.2.6/samples/python/yolov3_onnx
```

- Installing Prerequisites

```
1. Install ONNX-TensorRT.
2. Make sure you have the python dependencies installed.
    - For python2, run `python2 -m pip install -r requirements.txt` from the root directory of this sample.
    - For python3, run `python3 -m pip install -r requirements.txt` from the root directory of this sample.
```

-  Running the Sample.
Create an ONNX version of YOLOv3 with the following command - the Python
script will also download all necessary files from the official mirrors
(only once):

```
	python yolov3_to_onnx.py
```

When running above command for the first time, the output should look like
this:

```
Downloading from https://raw.githubusercontent.com/pjreddie/darknet/
f86901f6177dfc6116360a13cc06ab680e0c86b0/cfg/yolov3.cfg,
this may take a while...
100% [......................................................................
..........] 8342 / 8342
Downloading from https://pjreddie.com/media/files/yolov3.weights, this may
take a while...
100% [......................................................................
] 248007048 / 248007048
[...]
  %106_convolutional = Conv[auto_pad = u'SAME_LOWER', dilations = [1, 1],
  kernel_shape = [1, 1], strides = [1, 1]](%105_convolutional_lrelu,
  	%106_convolutional_conv_weights, %106_convolutional_conv_bias)
  return %082_convolutional, %094_convolutional, %106_convolutional
}
```

After completing the first step, you can proceed to building a TensorRT
engine from the generated ONNX file and running inference on a sample image
(will also be downloaded during the first run). Run the second script with:

```
python onnx_to_tensorrt.py
```

Doing this for the first time should produce the following output:

```
Downloading from https://github.com/pjreddie/darknet/raw/f86901f6177dfc6116
  360a13cc06ab680e0c86b0/data/dog.jpg, this may take a while...
100% [.....................................................................
  .......] 163759 / 163759
Building an engine from file yolov3.onnx, this may take a while...
Running inference on image dog.jpg...
Saved image with bounding boxes of detected objects to dog_bboxes.jpg.
```

FINSHED !!!
