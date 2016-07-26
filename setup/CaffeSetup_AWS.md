# Setup Caffe on AWS

**Instance Type:** g2.2xlarge

**OS:** Ubuntu 14.04.4

### General Dependencies

```
sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler
sudo apt-get install --no-install-recommends libboost-all-dev
```

### NVidia Cuda

##### Install linux kernel images
```
sudo apt-get install -y linux-image-extra-`uname -r` linux-headers-`uname -r` linux-image-`uname -r`
```

##### Download and install cuda

Install cuda 7.0, there's some issue with cuda 7.5 on aws

```
mkdir setup
cd setup
wget http://developer.download.nvidia.com/compute/cuda/7_0/Prod/local_installers/cuda_7.0.28_linux.run
chmod +x cuda_7.0.28_linux.run
./cuda_7.0.28_linux.run
```

*Cuda will request to install NVidia drivers, toolkit, etc. Say yes for all (samples can be skipped).*

##### Set relevant environment variables for cuda
```
echo 'export PATH=$PATH:/usr/local/cuda-7.0/bin' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH=/usr/local/cuda-7.0/lib64' >> ~/.bashrc

source ~/.bashrc
```

##### Verify NVidia installation
```
nvidia-smi
```

```
Tue Jul 26 11:09:23 2016
+------------------------------------------------------+
| NVIDIA-SMI 346.46     Driver Version: 346.46         |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GRID K520           Off  | 0000:00:03.0     Off |                  N/A |
| N/A   30C    P0    35W / 125W |     10MiB /  4095MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID  Type  Process name                               Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
```

### Install BLAS

```
sudo apt-get install libatlas-base-dev
```

### Python Headers

```
sudo apt-get install the python-dev
```

### Remaining Dependencies
```
sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev
```

### Install CUDNN
```
tar xvpf cudnn-7.0-linux-x64-v4.0-prod.tar
cd cuda
sudo cp lib64/* /usr/local/cuda-7.0/lib64/
sudo cp include/* /usr/local/cuda-7.0/include/
```

*Download **cudnn-7.0-linux-x64-v4.0-prod.tar.gz** from nvidia after sign up*

### Setup Caffe

##### Clone caffe repo
```
git clone https://github.com/BVLC/caffe.git
```

##### Install pycaffe dependencies
```
cd caffe/python
for req in $(cat requirements.txt); do sudo pip install $req; done
```

##### Modify Makefile.config
*Refer to the Makefile.config in this repo*

##### Build caffe
```
ca caffe
make clean
make all -j8
make test
make runtest
make pycaffe
```

##### Verify installation
```
python
```
```
Python 2.7.6 (default, Jun 22 2015, 17:58:13)
[GCC 4.8.2] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import caffe
>>>
```