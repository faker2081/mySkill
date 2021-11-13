# Linux

## 查看系统版本信息

- uname -a
- cat /proc/version
- cat /etc/issue

## 安装CUDA

https://developer.nvidia.com/cuda-80-ga2-download-archive

### 安装TensorFlow-gpu

1. ```python
   # 使用conda安装（简单）
   conda search tensorflow-gpu
   conda install tensorflow-gpu=1.15.0
   ```

## [linux 安装tensorflow（gpu版本）](https://www.cnblogs.com/softzrp/p/7823330.html)

一、安装cuda

具体安装过程见我的另一篇博客，[ubuntu16.04下安装配置深度学习环境](http://www.cnblogs.com/softzrp/p/6479442.html)

二、安装tensorflow

1.具体安装过程官网其实写的比较详细，总结一下的话可以分为两种：安装release版本和源码编译安装。因为源码编译安装比较繁琐，且需要安装谷歌自己的编译器bazel，所以我选择安装编译好的。

2.我写这篇博客的时候tensorflow更新到了1.4.0，安装编译好的一定看版本，因为每个版本依赖的底层库是不一样的。

1.4.0版本安装之前需要安装CUDA-8，cuDNN v6.0.，ibcupti-dev library

注意以上软件的版本，cuda一定要是8，cudnn得是6.0（我之前装的是1.2.0，则cudnn是v5.1就行，所以这个版本很重要，如果你的cudnn版本过低的话会报错：ImportError: libcudnn.so.6: cannot open shared object file: No such file or directory）

安装bcupti-dev library可执行

**sudo apt-get install libcupti-dev**

 

3.以上环境准备好后，安装是很简单的

如果你用的是anaconda，安装步骤如下：

```
conda create -n tensorflow python=2.7 # or python=3.3, etc.
source activate tensorflow
pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.4.0-cp35-cp35m-linux_x86_64.whl

如果是python直接安装的话：
首先需要pip，如果没有的话可以使用下面的命令安装
sudo apt-get install python-pip python-dev   # for Python 2.7
sudo apt-get install python3-pip python3-dev # for Python 3.n
```

下面使用pip安装tensorflow

$ **pip install tensorflow** # Python 2.7; CPU support (no GPU support)

$ **pip3 install tensorflow** # Python 3.n; CPU support (no GPU support)

$ **pip install tensorflow-gpu** # Python 2.7; GPU support

$ **pip3 install tensorflow-gpu** # Python 3.n; GPU support

不加版本的话默认是最新版本，如果想下特定的版本可在tensorflow后面加上版本号，例如第一个可以写成**pip install tensorflow==**1.1.0

三、测试tensorflow是否安装成功

经过一二两个步骤，应该是安装成功了，可写个tensorflow的小程序测试一下

```
# Python
import tensorflow as tf
hello = tf.constant('Hello, TensorFlow!')
sess = tf.Session()
print(sess.run(hello))
```

