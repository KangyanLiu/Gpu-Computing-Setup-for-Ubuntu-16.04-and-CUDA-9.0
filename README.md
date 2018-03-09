# Gpu-Computing-Setup-for-Ubuntu-16.04-and-CUDA-9.0
## 1. Install Ubuntu 16.04
### Create a bootable USB stick on Ubuntu
The 16.04 ISO file can be found here: http://releases.ubuntu.com/16.04/

## 2. Install CUDA and cuDNN
This and the following steps require Internet connection.

### Preparation

Install some useful packages in terminal:
``` bash
sudo apt-get update
sudo apt-get install \
  aptitude \
  freeglut3-dev \
  g++-4.8 \
  gcc-4.8 \
  libglu1-mesa-dev \
  libx11-dev \
  libxi-dev \
  libxmu-dev \
  nvidia-modprobe \
  python-dev \
  python-pip \
  python-virtualenv \
  vim
```


### Install CUDA

Download CUDA installation file: https://developer.nvidia.com/cuda-downloads

Choose Linux -> x86_64 -> Ubuntu -> 14.04 -> deb (local)  -> Download

Install CUDA in terminal (use the specific .deb file you've downloaded):
``` bash
cd ~/Downloads
sudo dpkg -i cuda-repo-ubuntu1404-8-0-local-ga2_8.0.61-1_amd64.deb
sudo apt-get update
sudo apt-get install cuda
```

Restart the computer to activate CUDA driver. Now your screen resolution should be automatically changed to highest resolution for the display!

### Install cuDNN

The NVIDIA CUDA® Deep Neural Network library (cuDNN) is aGPU-accelerated library of primitives for deep neural networks with optimizations for convolutions etc.

Register an (free) acount on NVIDIA website and login to download the latest cuDNN library: https://developer.nvidia.com/cudnn

Choose the specific version of cuDNN (denpending on support of your prefered deep learning framework)

Choose `Download cuDNN v5.1 (Jan 20, 2017), for CUDA 8.0` -> `cuDNN v5.1 Library for Linux`

Install cuDNN (by copying files :) in terminal:
```bash
cd ~/Downloads
tar xvf cudnn-8.0-linux-x64-v5.1.tgz
cd cuda
sudo cp lib64/* /usr/local/cuda/lib64/
sudo cp include/cudnn.h /usr/local/cuda/include/
sudo chmod a+r /usr/local/cuda/lib64/libcudnn*
```

### Update your .bashrc

Add the following lines to your `~/.bashrc` file (you can open it by `gedit ~/.bashrc` in terminal)
```bash
export PATH=/usr/local/cuda/bin:$PATH
export MANPATH=/usr/local/cuda/man:$MANPATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```

```bash
source ~/.bashrc
```

To check the installation, print some GPU and driver information by:
```bash
nvidia-smi
nvcc --version
```

## 4. Install TensorFlow
Follow TensorFlow official page for installation: https://www.tensorflow.org/install/
Or install whatever deep learning frameworks that you prefer :)

For example to install TF1.1 with GPU and Python 2.7:
```bash
export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.1.0-cp27-none-linux_x86_64.whl
sudo pip install --upgrade $TF_BINARY_URL
```
