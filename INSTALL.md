# Installation

*The following is a brief summary of installation instructions. For more details, please see Caffe's original instructions in the appendix below*.

The installation instructions for Ubuntu 14.04 can be summarized as follows (the instructions for other Linux versions may be similar).  
1. Pre-requisites
 * It is recommended to us a Linux machine (Ubuntu 14.04 or Ubuntu 16.04 for example)
 * [Anaconda Python 2.7](https://www.continuum.io/downloads) is recommended, but other Python packages might also work just fine.
 * One or more graphics cards (GPU) supporting NVIDIA CUDA. GTX10xx series cards are great, but GTX9xx series or Titan series cards are fine too.
 
2. Preparation
 * copy Makefile.config.example into Makefile.config
 * In Makefile.config, uncomment the line that says WITH_PYTHON_LAYER
 * Uncomment the line that says USE_CUDNN
 * If more than one GPUs are available, uncommenting USE_NCCL will help us to enable multi gpu training.
 
3. Install all the pre-requisites - (mostly taken from http://caffe.berkeleyvision.org/install_apt.html)
 * Change directory to the folder where caffe source code is placed.
 * *sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler*
 * *sudo apt-get install --no-install-recommends libboost-all-dev*
 * *sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev*
 * Install CUDNN. (libcudnn-dev developer deb package can be downloaded from NVIDIA website) and then installed using dpkg -i path-to-deb
 * Install [NCCL](https://github.com/NVIDIA/nccl/releases) if there are more than one CUDA GPUs in the system
 * Install the python packages required. (this portion is not tested and might need tweaking)
  -- For Anaconda Python: <br> *for req in $(cat python/requirements.txt); do conda install $req; done*
  -- For System default Python: <br> *for req in $(cat python/requirements.txt); do pip install $req; done* 
 * There may be other dependencies that are discovered as one goes through with the compilation process. The installation procedure will be similar to above.

4. Compilation
 * *make* (Instead, one can also do "make -j50" to speed up the compilaiton)
 * *make pycaffe* (To compile the python bindings)

5. CAFFE_ROOT
 * Set the environmet variable CAFFE_ROOT to the caffe-jacinto path. i.e. if caffe-jacinto is located in /user/tomato/work/caffe-jacinto, the add the following entry in your ~/.bashrc
 export CAFFE_ROOT=/user/tomato/work/caffe-jacinto
 * Do not forget to source it after editing.
 source ~/.bashrc
 * Note: If you would like to use this scripts with any other caffe version other than caffe-jacinto, you can set the CAFFE_ROOT environment variable to that path.
 
5. PYTHONPATH
 * Add pycaffe to your PYTHONPATH environment variable. This can be done by adding it in your .bashrc. (if you are using bash shell). For exampe if caffe-jacinto is located in the path /user/tomato/work/caffe-jacinto, then your .bashrc should have a line that looks like this:
export PYTHONPATH=:$CAFFE_ROOT/python:$PYTHONPATH
* Source .bashrc and make sure everything is alright:
source ~/.bashrc
echo $PYTHONPATH
* Note if you face an issue with importing a module that is present in the current folder, that is probably because PYTHONPATH is set incorrectly. If this issue occurs, make sure that PYTHONPATH either starts or ends with a : as described [here.](https://stackoverflow.com/questions/33615156/why-does-pythonpath-with-trailing-colon-add-current-directory-to-sys-path)
 
6. Appendix: Caffe's original instructions
 * See http://caffe.berkeleyvision.org/installation.html for the latest
installation instructions.
 * Check the users group in case you need help:
https://groups.google.com/forum/#!forum/caffe-users
