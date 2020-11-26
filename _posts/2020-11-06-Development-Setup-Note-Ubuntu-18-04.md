
- [Installing CUDA 10 and cuDNN ](#installing_cuda_10_and_cudnn)
- [Installing CUDA 10.2, CuDNN 7.6.5, TensorRT 7.0 on Ubuntu 18.04](#Installing_tensorrt)
- [Installing NVIDIA driver on Ubuntu 18.04](#installing_nvidia_on_Ubuntu_18_04)
- [Installing PyCuda](#installing_pycuda)
- [Installing Sublime Text 3](#install_sublime_text_3)
- [Installing ibus-unikey in Ubuntu 18.04](#install_unikey)
- [Installing NVIDIA SDK Manager](#nvidia_sdk_manager)
- [Installing PyCharm](#installing_pycharm)
- [Installing Opencv from the Source](#installing_opencv)
- [Installing Python 2.7, 3.6](#installing_python_2_7_3_6)


## Installing CUDA 10 and cuDNN

1. Do NOT Install Nvidia Driver

During CUDA 10 installation, the driver will be installed. So just go ahead and install CUDA!

```
$ sudo add-apt-repository ppa:graphics-drivers/ppa
$ sudo apt-get update
```

Look for latest version number from nvidia website:

```
$ sudo apt-get install nvidia-driver-440

```

After reboot, run below to verify

```
nvidia-smi
```

Check installed packages

```
dpkg -l | grep nvidia
```

2. Install CUDA 10.1 following below link:

Installation Instructions from nvidia official website:

```
$ wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin
$ sudo mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600
$ wget http://developer.download.nvidia.com/compute/cuda/10.1/Prod/local_installers/cuda-repo-ubuntu1804-10-1-local-10.1.243-418.87.00_1.0-1_amd64.deb
$ sudo dpkg -i cuda-repo-ubuntu1804-10-1-local-10.1.243-418.87.00_1.0-1_amd64.deb
$ sudo apt-key add /var/cuda-repo-10-1-local-10.1.243-418.87.00/7fa2af80.pub
$ sudo apt-get update
$ sudo apt-get -y install cuda
```

Restart machine.

3. Install cuDNN

[Goto page](https://developer.nvidia.com/rdp/cudnn-download)
Download all three .deb: runtime/developer/code sample

```
$ sudo dpkg -i libcudnn7_7.6.5.32–1+cuda10.1_amd64.deb (the runtime library),
$ sudo dpkg -i libcudnn7-dev_7.6.5.32–1+cuda10.1_amd64.deb (the developer library), and
$ sudo dpkg -i libcudnn7-doc_7.6.5.32–1+cuda10.1_amd64.deb (the code samples).
```

Now we can verify the cuDNN installation (below is just the official guide, which surprisingly works out of the box):

```
Go to the MNIST example code: cd /usr/src/cudnn_samples_v7/mnistCUDNN/.
Compile the MNIST example: sudo make clean && sudo make.
Run the MNIST example: ./mnistCUDNN. If your installation is successful, you should see Test passed! at the end of the output, like this:
```

## Installing CUDA 10.2, CuDNN 7.6.5, TensorRT 7.0 on Ubuntu 18.04

1. Installing CUDA

Install CUDA directly from the offline installer

```
$ sudo apt update
$ sudo apt upgrade -y
$ mkdir installer ; cd installer
$ wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin
$ sudo mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600
$ sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
$ sudo add-apt-repository "deb http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/ /"
$ sudo apt-get update
$ sudo apt-get -y install cuda-10-2
```

2. Installing CuDNN


Download CuDNN [here](https://developer.nvidia.com/rdp/cudnn-archive) (BOTH the runtime and dev, deb). The version 7.6.5.

```
$ tar -xzvf cudnn-10.2-linux-x64-v7.6.5.32.tgz
$ sudo cp cuda/include/cudnn*.h /usr/local/cuda/include
$ sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
$ sudo chmod a+r /usr/local/cuda/include/cudnn*.h /usr/local/cuda/lib64/libcudnn*
```

To verify that cuDNN is installed and runnning properly:

Go to the writable path

```
$ cd /usr/src/cudnn_samples_v7/mnistCUDNN
```

Compile the mnistCUDNN sample

```
$ sudo make clean
$ sudo make
```

The log should be like this:

```
Linking agains cublasLt = true
CUDA VERSION: 10020
TARGET ARCH: x86_64
HOST_ARCH: x86_64
TARGET OS: linux
SMS: 30 35 50 53 60 61 62 70 72 75
/usr/local/cuda/bin/nvcc -ccbin g++ -I/usr/local/cuda/include -I/usr/local/cuda/include -IFreeImage/include  -m64    -gencode arch=compute_30,code=sm_30 -gencode arch=compute_35,code=sm_35 -gencode arch=compute_50,code=sm_50 -gencode arch=compute_53,code=sm_53 -gencode arch=compute_60,code=sm_60 -gencode arch=compute_61,code=sm_61 -gencode arch=compute_62,code=sm_62 -gencode arch=compute_70,code=sm_70 -gencode arch=compute_72,code=sm_72 -gencode arch=compute_75,code=sm_75 -gencode arch=compute_75,code=compute_75 -o fp16_dev.o -c fp16_dev.cu
g++ -I/usr/local/cuda/include -I/usr/local/cuda/include -IFreeImage/include   -o fp16_emu.o -c fp16_emu.cpp
g++ -I/usr/local/cuda/include -I/usr/local/cuda/include -IFreeImage/include   -o mnistCUDNN.o -c mnistCUDNN.cpp
/usr/local/cuda/bin/nvcc -ccbin g++   -m64      -gencode arch=compute_30,code=sm_30 -gencode arch=compute_35,code=sm_35 -gencode arch=compute_50,code=sm_50 -gencode arch=compute_53,code=sm_53 -gencode arch=compute_60,code=sm_60 -gencode arch=compute_61,code=sm_61 -gencode arch=compute_62,code=sm_62 -gencode arch=compute_70,code=sm_70 -gencode arch=compute_72,code=sm_72 -gencode arch=compute_75,code=sm_75 -gencode arch=compute_75,code=compute_75 -o mnistCUDNN fp16_dev.o fp16_emu.o mnistCUDNN.o -I/usr/local/cuda/include -I/usr/local/cuda/include -IFreeImage/include  -L/usr/local/cuda/lib64 -L/usr/local/cuda/lib64 -lcublasLt -LFreeImage/lib/linux/x86_64 -LFreeImage/lib/linux -lcudart -lcublas -lcudnn -lfreeimage -lstdc++ -lm
```

Run the mnistCUDNN sample.

```
$ ./mnistCUDNN
```

If cuDNN is properly installed and running on your Linux system, you will see a message similar to the following:
```
Test passed!
```

3. Installing TensorRT

Download TensorRT [here](https://developer.nvidia.com/nvidia-tensorrt-7x-download). The version 7.0.

Install the following dependencies, if not already present:

```
  CUDA 9.0, 10.0, or 10.2
  cuDNN 7.6.5
  Python 2 or Python 3 (Optional)
```

Download the TensorRT tar file that matches the Linux distribution you are using.
Choose where you want to install TensorRT. This tar file will install everything into a subdirectory called TensorRT-7.x.x.x.

Unpack the tar file.
```
    version=”7.x.x.x”
    os=”<os>”
    arch=$(uname -m)
    cuda=”cuda-x.x”
    cudnn=”cudnn7.x”
    tar xzvf TensorRT-${version}.${os}.${arch}-gnu.${cuda}.${cudnn}.tar.gz

    Where:
        7.x.x.x is your TensorRT version
        <os> is:
            Ubuntu-16.04
            Ubuntu-18.04
            CentOS-7.6
        cuda-x.x is CUDA version 9.0, 10.0, or 10.2.
        cudnn7.x is cuDNN version 7.6.
    This directory will have sub-directories like lib, include, data, etc…
```

```
$ ls TensorRT-${version}
```

The output should be:

```
bin  data  doc  graphsurgeon  include  lib  python  samples  targets  TensorRT-Release-Notes.pdf  uff
```

Add the absolute path to the TensorRTlib directory to the environment variable LD_LIBRARY_PATH:

```
$ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:<TensorRT-${version}/lib>
```

Install the Python TensorRT wheel file.

```
$ cd TensorRT-${version}/python
```

If using Python 2.7:

```
$ sudo pip2 install tensorrt-*-cp27-none-linux_x86_64.whl
```

If using Python 3.x:

```
$ sudo pip3 install tensorrt-*-cp3x-none-linux_x86_64.whl
```

Install the Python UFF wheel file. This is only required if you plan to use TensorRT with TensorFlow.

```
$ cd TensorRT-${version}/uff
```

If using Python 2.7:

```
$ sudo pip2 install uff-0.6.5-py2.py3-none-any.whl
```

If using Python 3.x:

```
$ sudo pip3 install uff-0.6.5-py2.py3-none-any.whl
```

In either case, check the installation with:

```
which convert-to-uff
```

Install the Python graphsurgeon wheel file.

```
$ cd TensorRT-${version}/graphsurgeon
```

If using Python 2.7:

```
$ sudo pip2 install graphsurgeon-0.4.1-py2.py3-none-any.whl
```

If using Python 3.x:

```
$ sudo pip3 install graphsurgeon-0.4.1-py2.py3-none-any.whl
```

Verify the installation:

```
$ cd <TensorRT root directory>/samples/sampleMNIST
$ make
$ ./sample_mnist
```

Add to .bashrc
```
$ gedit ~/.bashrc
```

Make sure CUDA_HOME and CUDNN_INSTALL_DIR are set.

```
export CUDA_HOME=/usr/local/cuda-10.2
export CUDNN_INSTALL_DIR=/usr/local/cuda-10.2
export LD_LIBRARY_PATH=${CUDA_HOME}/lib64

PATH=${CUDA_HOME}/bin:${PATH}
export PATH
```

## Installing NVIDIA driver on Ubuntu 18.04

1. Check the model of your NVIDIA GPU

```
$ ubuntu-drivers devices
```

2. Install NVIDIA driver

```
$ sudo ubuntu-drivers autoinstall
```

or

```
$ sudo apt install nvidia-440-server
```

3. Reboot

```
$ reboot
```

## Installing PyCUDA

Install the following CUDA dependencies:

```
$ sudo apt-get install build-essential binutils gdb
```

Install an additional dependencies that will allow to run some of the graphical (OpenGL) code included with the CUDA Toolkit:

```
$ sudo apt-get install freeglut3 freeglut3-dev libxi-dev libxmu-dev
```
Now, install the nvcc compiler which is the command-line CUDA C compiler, analogous to the gcc compiler:

```
$ sudo apt install nvidia-cuda-toolkit
```

After the package is finished installing, have to configure your PATH and LD_SYSTEM_CONFIG environment variables so that your system can find the appropriate binary executable and library files needed for CUDA.

```
$ gedit ~/.bashrc
```

Add the following at the end of the file:

```
export PATH="/usr/local/cuda/bin:${PATH}
export LD_LIBRARY_PATH="/usr/local/cuda/lib64:${LD_LIBRARY_PATH}"
```

Please ensure that you’ve correctly installed the toolkit by using this command:

```
nvcc — version
```

Install PyCUDA

Use the following commands to install PyCUDA along with its dependencies:

```
$ sudo apt-get install build-essential python-dev python-setuptools libboost-python-dev libboost-thread-dev -y$ pip install pycuda
```

Run the following program to check if everything is setup:

```
import pycuda
import pycuda.driver as drv
drv.init()print('CUDA device query (PyCUDA version) \n')print('Detected {} CUDA Capable device(s) \n'.format(drv.Device.count()))for i in range(drv.Device.count()):

    gpu_device = drv.Device(i)
    print('Device {}: {}'.format( i, gpu_device.name() ) )
    compute_capability = float( '%d.%d' % gpu_device.compute_capability() )
    print('\t Compute Capability: {}'.format(compute_capability))
    print('\t Total Memory: {} megabytes'.format(gpu_device.total_memory()//(1024**2)))

    # The following will give us all remaining device attributes as seen
    # in the original deviceQuery.
    # We set up a dictionary as such so that we can easily index
    # the values using a string descriptor.

    device_attributes_tuples = gpu_device.get_attributes().items()
    device_attributes = {}

    for k, v in device_attributes_tuples:
        device_attributes[str(k)] = v

    num_mp = device_attributes['MULTIPROCESSOR_COUNT']

    # Cores per multiprocessor is not reported by the GPU!  
    # We must use a lookup table based on compute capability.
    # See the following:
    # http://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#compute-capabilities

    cuda_cores_per_mp = { 5.0 : 128, 5.1 : 128, 5.2 : 128, 6.0 : 64, 6.1 : 128, 6.2 : 128}[compute_capability]

    print('\t ({}) Multiprocessors, ({}) CUDA Cores / Multiprocessor: {} CUDA Cores'.format(num_mp, cuda_cores_per_mp, num_mp*cuda_cores_per_mp))

    device_attributes.pop('MULTIPROCESSOR_COUNT')

    for k in device_attributes.keys():
        print('\t {}: {}'.format(k, device_attributes[k]))
```

If everything is fine, the output very similar to the following:

```
CUDA device query (PyCUDA version)

Detected 1 CUDA Capable device(s)

Device 0: GeForce GTX 1060
	 Compute Capability: 6.1
	 Total Memory: 6078 megabytes
	 (10) Multiprocessors, (128) CUDA Cores / Multiprocessor: 1280 CUDA Cores
	 ASYNC_ENGINE_COUNT: 2
	 CAN_MAP_HOST_MEMORY: 1
	 CLOCK_RATE: 1733000
	 COMPUTE_CAPABILITY_MAJOR: 6
	 COMPUTE_CAPABILITY_MINOR: 1
	 COMPUTE_MODE: DEFAULT
	 CONCURRENT_KERNELS: 1
	 ....
	 ....
	 TEXTURE_PITCH_ALIGNMENT: 32
	 TOTAL_CONSTANT_MEMORY: 65536
	 UNIFIED_ADDRESSING: 1
	 WARP_SIZE: 32
```

## Installing Sublime Text 3

- Sublime Text 3

```
$ wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
$ echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
$ sudo apt-get update
$ sudo apt-get install sublime-text
```

## Installing ibus-unikey in Ubuntu 18.04

- Click [GUIDELINE LINK](https://vinasupport.com/huong-dan-cai-bo-go-tieng-viet-ibus-unikey-tren-ubuntu/) to see how to install.

- To Switch between English and Vietnamese by Pressing “Windows + Space”


## Installing NVIDIA SDK Manager

 - Click [DOWNLOAD LINK](https://developer.nvidia.com/nvidia-sdk-manager) to see how to install.

## Installing PyCharm

- Pycharm-community

```
$ sudo snap install pycharm-community --classic
```

## Installing Python 2.7, 3.6

1. Python 2.7

```
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install python2.7
$ sudo apt install python-pip
```

2. Python 3.6

```
$ sudo add-apt-repository ppa:deadsnakes/ppa
$ sudo apt update
$ sudo apt install python3.6
$ sudo apt install python3-pip
```

- To check whether it works or not

```
$ python -V
```

## Installing OpenCV from the Source

1. Install the required dependencies:

```
  $ sudo apt install build-essential cmake git pkg-config libgtk-3-dev \
      libavcodec-dev libavformat-dev libswscale-dev libv4l-dev \
      libxvidcore-dev libx264-dev libjpeg-dev libpng-dev libtiff-dev \
      gfortran openexr libatlas-base-dev python3-dev python3-numpy \
      libtbb2 libtbb-dev libdc1394-22-dev
```

2. Clone the OpenCV’s and OpenCV contrib repositories:

```
$ mkdir ~/opencv_build && cd ~/opencv_build
$ git clone https://github.com/opencv/opencv.git
$ git clone https://github.com/opencv/opencv_contrib.git
```

3.  Once the download is complete, create a temporary build directory, and switch to it:

```
$ cd ~/opencv_build/opencv
$ mkdir build && cd build
```

4. Set up the OpenCV build with CMake:

```
$ cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D INSTALL_C_EXAMPLES=ON \
    -D INSTALL_PYTHON_EXAMPLES=ON \
    -D OPENCV_GENERATE_PKGCONFIG=ON \
    -D OPENCV_EXTRA_MODULES_PATH=~/opencv_build/opencv_contrib/modules \
    -D BUILD_EXAMPLES=ON ..
```

5. Start the compilation process:

```
$ make -j8
```

6. Install OpenCV with:

```
$ sudo make install
```    

After that, the result shoud be as below.    

![OpenCV Installing Img](/images/opencv_installing.png "OpenCV Installing Img")

To verify whether OpenCV has been installed successfully, type the following command and you should see the OpenCV version:

```
$ pkg-config --modversion opencv4
```

## Install Java JDK

```
$ java -version
$ apt install openjdk-8-jre-headless
$ sudo apt install openjdk-8-jdk

$ sudo nano /etc/environment
$ JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java"

To apply the changes
$ source /etc/environment

To rerify JAVAHOME
$ echo $JAVA_HOME

Output
/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java

```
## Install Visual Code

```
$ sudo apt update
$ sudo apt install software-properties-common apt-transport-https wget
$ wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
$ sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
$ sudo apt update
$ sudo apt install code

```


## Install Google Earth

```
$ sudo apt install gdebi-core wget
$ wget https://dl.google.com/dl/earth/client/current/google-earth-pro-stable_current_amd64.deb
$ ls google-earth-pro-stable_current_amd64.deb 
$ sudo gdebi google-earth-pro-stable_current_amd64.deb
```
