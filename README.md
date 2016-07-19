# Caffe Demo

## Setup Instructions
*The following process was carried out on a MacBook Air 11"*

#### 1. Install XCode command line tools
```
xcode-select --install
```

#### 2. Install [Homebrew](http://brew.sh)

#### 3. Install [Anaconda Python](https://www.continuum.io/downloads) distribution
Verify that the Anaconda distribution is the default python using
```
which python
```
The output should be something like
```
/Users/<username>/anaconda/bin/python
```

#### 4. Install [CUDA](https://developer.nvidia.com/cuda-downloads)
*Version 7.5.27 was used for this setup*

#### 5. Verify environment variables
* LD_LIBRARY_PATH should not be set
* DYLD_FALLBACK_LIBRARY_PATH should be set to provide CUDA, python and other libs
```
export DYLD_FALLBACK_LIBRARY_PATH=/usr/local/cuda/lib:/Users/<username>/anaconda/lib/:/usr/local/lib:/usr/lib
```

#### 6. Install dependencies
```
brew install -vd snappy leveldb gflags glog szip lmdb
brew tap homebrew/science
brew install hdf5 opencv
brew install --build-from-source --with-python -vd protobuf
brew install --build-from-source -vd boost boost-python
```
