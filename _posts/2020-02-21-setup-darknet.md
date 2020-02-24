# Installing Darknet for object detecting

''
	Created: 2020 Feb 21
	By: Jason Ng
''

## How to download and complile on Linux

## clone darknet 

1. git clone https://github.com/AlexeyAB/darknet.git
2. cd darknet
3. mkdir build-release
4. cd build-release

## before building, just modify in the Makefile

''
	GPU=1 to build with CUDA to accelerate by using GPU 
	CUDNN=1 to build with cuDNN v5-v7 to accelerate training by using GPU 
	CUDNN_HALF=1 to build for Tensor Cores 
	OPENCV=1 to build with OpenCV 4.x/3.x/2.4.x - allows to detect on video files and video streams from network cameras or 	web-cams
''

5. cmake ..

The logs: 
''
-- The C compiler identification is GNU 7.4.0
-- The CXX compiler identification is GNU 7.4.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Looking for a CUDA compiler
-- Looking for a CUDA compiler - /usr/local/cuda-10.2/bin/nvcc
-- The CUDA compiler identification is NVIDIA 10.2.89
-- Check for working CUDA compiler: /usr/local/cuda-10.2/bin/nvcc
-- Check for working CUDA compiler: /usr/local/cuda-10.2/bin/nvcc -- works
-- Detecting CUDA compiler ABI info
-- Detecting CUDA compiler ABI info - done
-- Looking for pthread.h
-- Looking for pthread.h - found
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD
-- Performing Test CMAKE_HAVE_LIBC_PTHREAD - Failed
-- Looking for pthread_create in pthreads
-- Looking for pthread_create in pthreads - not found
-- Looking for pthread_create in pthread
-- Looking for pthread_create in pthread - found
-- Found Threads: TRUE  
-- Found CUDA: /usr/local/cuda-10.2 (found version "10.2") 
-- Autodetected CUDA architecture(s):  7.5
-- Building with CUDA flags: -gencode;arch=compute_75,code=sm_75
-- Found OpenCV: /usr/local (found version "3.4.0") 
-- Found Stb: /home/jason/Documents/darknet/3rdparty/stb/include  
-- Found OpenMP_C: -fopenmp (found version "4.5") 
-- Found OpenMP_CXX: -fopenmp (found version "4.5") 
-- Found OpenMP: TRUE (found version "4.5")  
-- Found CUDNN: /usr/local/cuda-10.2/include (found version "7.6.5") 
-- CMAKE_CUDA_FLAGS: -gencode arch=compute_75,code=sm_75 --compiler-options " -Wall -Wno-unused-result -Wno-unknown-pragmas -Wfatal-errors -Wno-deprecated-declarations -Wno-write-strings -DGPU -DCUDNN -DOPENCV -fPIC -fopenmp -Ofast " 
-- ZED SDK not found
-- Configuring done
-- Generating done
-- Build files have been written to: /home/jason/Documents/darknet/build-release

''


6. make -j8

The log:

''
[100%] Linking CXX executable uselib_track
[100%] Linking CXX executable uselib
[100%] Built target uselib
[100%] Built target uselib_track

''
7. make install

''
-- Install configuration: ""
-- Installing: /home/jason/Documents/darknet/libdark.so
-- Set runtime path of "/home/jason/Documents/darknet/libdark.so" to ""
-- Installing: /home/jason/Documents/darknet/include/darknet/darknet.h
-- Installing: /home/jason/Documents/darknet/include/darknet/yolo_v2_class.hpp
-- Installing: /home/jason/Documents/darknet/uselib
-- Set runtime path of "/home/jason/Documents/darknet/uselib" to ""
-- Installing: /home/jason/Documents/darknet/darknet
-- Set runtime path of "/home/jason/Documents/darknet/darknet" to ""
-- Installing: /home/jason/Documents/darknet/uselib_track
-- Set runtime path of "/home/jason/Documents/darknet/uselib_track" to ""
-- Installing: /home/jason/Documents/darknet/share/darknet/DarknetTargets.cmake
-- Installing: /home/jason/Documents/darknet/share/darknet/DarknetTargets-noconfig.cmake
-- Installing: /home/jason/Documents/darknet/share/darknet/DarknetConfig.cmake
-- Installing: /home/jason/Documents/darknet/share/darknet/DarknetConfigVersion.cmake

''



