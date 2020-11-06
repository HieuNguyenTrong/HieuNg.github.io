
- [Installing Sublime Text 3](#install_sublime_text_3)
- [Installing ibus-unikey in Ubuntu 18.04](#install_unikey)
- [Installing NVIDIA SDK Manager](#nvidia_sdk_manager)
- [Installing PyCharm](#installing_pycharm)
- [Installing Opencv from the Source](#installing_opencv)
- [Installing Python 2.7, 3.6](#installing_python_2_7_3_6)

# Installing Sublime Text 3

	$ wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add - 
	$ echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
	$ sudo apt-get update
	$ sudo apt-get install sublime-text


# Installing ibus-unikey in Ubuntu 18.04

- Click *GUIDELINE LINK* to see how to install.

	[GUIDELINE LINK](https://vinasupport.com/huong-dan-cai-bo-go-tieng-viet-ibus-unikey-tren-ubuntu/) 

- To Switch between English and Vietnamese by Pressing “Windows + Space”


# Installing NVIDIA SDK Manager

 - Click *DOWNLOAD LINK* to see how to install.

	[DOWNLOAD LINK](https://developer.nvidia.com/nvidia-sdk-manager)

# Installing PyCharm

	$ sudo snap install pycharm-community --classic


# Install Python 2.7, 3.6 

1. Python 2.7

	$ sudo apt update
	$ sudo apt upgrade
	$ sudo apt install python2.7
	$ sudo apt install python-pip

2. Python 3.6

	$ sudo add-apt-repository ppa:deadsnakes/ppa
	$ sudo apt update
	$ sudo apt install python3.6
	$ sudo apt install python3-pip

- To check whether it works or not	
	$ python -V

# Installing OpenCV from the Source

1. Install the required dependencies:

    $ sudo apt install build-essential cmake git pkg-config libgtk-3-dev \
        libavcodec-dev libavformat-dev libswscale-dev libv4l-dev \
        libxvidcore-dev libx264-dev libjpeg-dev libpng-dev libtiff-dev \
        gfortran openexr libatlas-base-dev python3-dev python3-numpy \
        libtbb2 libtbb-dev libdc1394-22-dev

2. Clone the OpenCV’s and OpenCV contrib repositories:

    $ mkdir ~/opencv_build && cd ~/opencv_build
    $ git clone https://github.com/opencv/opencv.git
    $ git clone https://github.com/opencv/opencv_contrib.git

3.  Once the download is complete, create a temporary build directory, and switch to it:

	$ cd ~/opencv_build/opencv
	$ mkdir build && cd build

4. Set up the OpenCV build with CMake:

    $ cmake -D CMAKE_BUILD_TYPE=RELEASE \
        -D CMAKE_INSTALL_PREFIX=/usr/local \
        -D INSTALL_C_EXAMPLES=ON \
        -D INSTALL_PYTHON_EXAMPLES=ON \
        -D OPENCV_GENERATE_PKGCONFIG=ON \
        -D OPENCV_EXTRA_MODULES_PATH=~/opencv_build/opencv_contrib/modules \
        -D BUILD_EXAMPLES=ON ..


5. Start the compilation process:

    $ make -j8

6. Install OpenCV with:

    $ sudo make install

- To verify whether OpenCV has been installed successfully, type the following command and you should see the OpenCV version:

    $ pkg-config --modversion opencv4
