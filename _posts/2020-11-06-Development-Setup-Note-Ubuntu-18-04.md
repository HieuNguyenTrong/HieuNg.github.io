- [Installing CUDA 10 and cuDNN ](#installing_cuda_10_and_cudnn)
- [Installing NVIDIA driver on Ubuntu 18.04](#installing_nvidia_on_Ubuntu_18_04)
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

## Installing NVIDIA driver on Ubuntu 18.04

1. Check the model of your NVIDIA GPU
```
$ ubuntu-drivers devices
```
2. Install NVIDIA driver 
```
$ sudo ubuntu-drivers autoinstall 
or 
$ sudo apt install nvidia-440-server
```
3. Reboot
```
$ reboot
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

- Click *GUIDELINE LINK* to see how to install.

	[GUIDELINE LINK](https://vinasupport.com/huong-dan-cai-bo-go-tieng-viet-ibus-unikey-tren-ubuntu/) 

- To Switch between English and Vietnamese by Pressing “Windows + Space”


## Installing NVIDIA SDK Manager

 - Click *DOWNLOAD LINK* to see how to install.

	[DOWNLOAD LINK](https://developer.nvidia.com/nvidia-sdk-manager)

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
- After that, the result shoud be as below.    

![OpenCV Installing Img](/images/opencv_installing.png "OpenCV Installing Img")

- To verify whether OpenCV has been installed successfully, type the following command and you should see the OpenCV version:
```
$ pkg-config --modversion opencv4
```
