# Gpu-Computing-Setup-for-Ubuntu-16.04-and-CUDA-9.0
## 1. Install Ubuntu 16.04
### Create a bootable USB stick on Ubuntu
The 16.04 ISO file can be found here: http://releases.ubuntu.com/16.04/

## 2. Install Nvidia Gpu driver
``` bash
sudo add-apt-repository ppa:graphics-drivers
sudo apt-get update
sudo apt-get install nvidia-384 
```
Current long-lived branch release is nvidia-384.
Restart the computer to activate Gpu driver.
## 3. Install some dependencies
```bash
sudo apt-get update
sudo apt-get upgrade  
sudo apt-get install build-essential cmake g++ gfortran 
sudo apt-get install git pkg-config python-dev python3-dev 
sudo apt-get install software-properties-common wget
sudo apt-get autoremove 
sudo rm -rf /var/lib/apt/lists/*
```
## 4. Install CUDA 9.0 
Download CUDA 9.0 from https://developer.nvidia.com/cuda-90-download-archive

``` bash
sudo dpkg -i cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64.deb
sudo apt-get update
sudo apt-get install cuda

echo 'export PATH=/usr/local/cuda/bin:$PATH' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH' >> ~/.bashrc
source ~/.bashrc 
```
Restart the computer to activate CUDA driver.

## 5. Install cudnn 7.0.5
Download cudnn 7.0.5 from https://developer.nvidia.com/cudnn
``` bash
cd ~/Downloads/
tar xvf cudnn-9.0-linux-x64-v7.tgz
cd cuda
sudo cp */*.h /usr/local/cuda/include/
sudo cp */libcudnn* /usr/local/cuda/lib64/
sudo chmod a+r /usr/local/cuda/lib64/libcudnn*
```
## 6. Install python stuff
```bash
sudo apt-get update && apt-get install -y python-numpy python-scipy python-nose python-h5py python-skimage python-matplotlib python-pandas python-sklearn python-sympy

sudo apt-get clean && sudo apt-get autoremove

sudo rm -rf /var/lib/apt/lists/*

sudo apt-get update

sudo apt-get install git python-dev python3-dev python-numpy python3-numpy build-essential python-pip python3-pip python-virtualenv swig python-wheel libcurl3-dev

sudo apt-get install -y libfreetype6-dev libpng12-dev

pip3 install -U matplotlib ipython[all] jupyter pandas scikit-image
```
## 7. Install openBLAS
```bash
mkdir ~/git
cd ~/git
git clone https://github.com/xianyi/OpenBLAS.git
cd OpenBLAS
make FC=gfortran -j16
sudo make PREFIX=/usr/local install 
```
## 8. Install TensorFlow for Python3
```bash
pip3 install --upgrade tensorflow-gpu==1.5
```
## 9. Install an IDE for testing.
```bash
sudo apt-get install spyder3
```
Use following code in Python3 to test.
```bash
import tensorflow as tf
a = tf.constant(1234)
b = tf.constant(5678)
sess = tf.Session()
sess.run(a+b)
sess.close()
```
## 10. Real-time Gpu usage monitor.
```bash
watch nvidia-smi
```





