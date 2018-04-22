---
layout: default
title: Deep Learning Box Setup and Installation
meta: Setting up your own Deep learning Box
category: DeepLearning
---

# Deep Learning Box: Setup and Installation

<span class="figcaption_hack">The Silent Beast</span>

After a lot of hesitation, I finally took the plunge to get my own Deep learning
Box.Without any further ado, let’s take a dive into the specifications.

### **Table of contents:**

> Specifications<br> Software Installation

*****

#### **Specifications:**

The links are from amazon but I bought it from a local store.

> GPU : [Gigabyte-Geforce-NVIDIA1080TI 11GB
> OC](https://www.amazon.com/Gigabyte-GeForce-GAMING-Graphic-N108TGAMINGOC-11GD/dp/B06XXJMDTM)**CPU
:
[i7–8700](https://www.amazon.com/Intel-i7-8700K-Processor-Unlocked-BX80684i78700K/dp/B07598VZR8)K****Motherboard
: [Asus Z370
A-Prime](https://www.amazon.com/PRIME-LGA1151-Motherboard-Generation-Processors/dp/B075RJHN2D)<br>
Liquid CPU Cooler : [Water 3.0 Thermaltake 240
RGB](https://www.amazon.com/Thermaltake-Extreme-Liquid-Cooling-CLW0224-B/dp/B00O08FWTM)<br>
RAM : [Corsair 32GB(16GB*2) Vengeance LPX
RGB](https://www.amazon.com/CORSAIR-Vengeance-2x16GB-PC4-24000-Systems/dp/B01HKF4FNK)<br>
SSD : [Samsung M.2 960 EVO 500
GB](https://www.amazon.com/Samsung-960-EVO-Internal-MZ-V6E500BW/dp/B01M20VBU7)<br>
HDD : [WD Blue
4TB](https://www.amazon.com/Blue-Desktop-Hard-Disk-Drive/dp/B013HNYV8I)<br> PSU
: [Cooler Master
V1000](https://www.amazon.com/Cooler-Master-V1000-Modular-Silencio/dp/B00CGY4ETG)<br>
Cabinet : [Thermaltake Full-Tower
71RGB](https://www.amazon.com/Thermaltake-Tempered-Vertical-Pre-installed-CA-1I7-00F1WN-01/dp/B074ZN21M8)

> Some super-helpful blogposts that helped me greatly in building my DL box are
> the following:<br> * [Tim Dettmers](http://timdettmers.com/about/) on [Which
GPU(s) to Get for Deep
Learning](http://timdettmers.com/2017/04/09/which-gpu-for-deep-learning/)<br> *
[Slav Ivanov](https://blog.slavv.com/@slavivanov) on [The 1700$ great Deep
Learning
Box](https://blog.slavv.com/the-1700-great-deep-learning-box-assembly-setup-and-benchmarks-148c5ebe6415)<br>
* [Carlos E.Perez](https://medium.com/@IntuitMachine) on [Building a 270*
Teraflops DL
Box](https://medium.com/intuitionmachine/building-a-270-teraflops-deep-learning-box-of-under-10-000-2d790b0ae2ec)<br>
* [Yvan Scher](https://medium.com/@yvanscher) on [Building your own DL
Box](https://medium.com/@yvanscher/building-your-own-deep-learning-box-bc5b222e84ee)<br>
* [James Jeon](http://www.cswithjames.com/) on [$1150 Personal Deep Learning
Box](http://www.cswithjames.com/deeplearningbox/)<br> * [Brendan
Fortuner](https://towardsdatascience.com/@bfortuner) on [Building your own DL
box](https://towardsdatascience.com/building-your-own-deep-learning-box-47b918aea1eb)

If you are in India, remember things are even pricier. I was running into approx
300–350$ monthly gpu server bills. My build set me back about 3000$ approx.

*****

**Software Installation:**Now that we are done with the hardware configs. Let’s
jump straight into the software installation part. It’s gonna be a long read, so
hold on to your seats.

> Posts which aided me in the software installation:<br> * [Cuda installation
> guide](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#introduction)<br>
* [CudNN installation
guide](https://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html)

**Operating system:**Linux should be the first thing on your mind as most of the
widely used DL software is first designed to work on Linux and then on other
operating system. I went with [Ubuntu 16.04
LTS](https://www.ubuntu.com/download/desktop) . You are free to choose your own.
Although I would suggest to choose among Ubuntu, Fedora, RHEL, OpenSuse.

You can install your OS by bootable USB. If you haven’t done it before, you can
go through any of the three options. If you are creating your liveUSB on:<br> 1.
Ubuntu : See [here](https://askubuntu.com/a/876142).<br> 2. MacOS : See
[here](https://tutorials.ubuntu.com/tutorial/tutorial-create-a-usb-stick-on-macos#0).<br>
3. Windows: See
[here](https://tutorials.ubuntu.com/tutorial/tutorial-create-a-usb-stick-on-windows#0).

The 1st step is complete. Let’s move to the second. Hang in there.

**Pre-installation checks:**Verify if you have Nvidia device with the following
command.You should have something similar in output:


To check which distribution and release number of Ubuntu you are running:

    sritanu@combalgorythm:~$ uname -m && cat /etc/*release
    x86_64
    DISTRIB_ID=Ubuntu
    DISTRIB_RELEASE=16.04
    DISTRIB_CODENAME=xenial
    DISTRIB_DESCRIPTION=”Ubuntu 16.04.4 LTS”
    NAME=”Ubuntu”
    VERSION=”16.04.4 LTS (Xenial Xerus)”
    ID=ubuntu
    ID_LIKE=debian
    PRETTY_NAME=”Ubuntu 16.04.4 LTS”
    VERSION_ID=”16.04"
    HOME_URL=”
    "
    SUPPORT_URL=”
    "
    BUG_REPORT_URL=”
    "
    VERSION_CODENAME=xenial
    UBUNTU_CODENAME=xenial

Verify the gcc distribution that you are running:

    sritanu@combalgorythm:~$ gcc — version
    gcc (Ubuntu 5.4.0–6ubuntu1~16.04.9) 5.4.0 20160609

Verify the kernel header:

    sritanu@combalgorythm:~$ uname -r
    4.13.0–38-generic

Kernel headers and development packages can be installed with:

    sritanu@combalgorythm:~$ sudo apt-get install linux-headers-$(uname -r)
    [sudo] password for sritanu:
    Reading package lists… Done
    Building dependency tree
    Reading state information… Done
    linux-headers-4.13.0–38-generic is already the newest version (4.13.0–38.43~16.04.1).
    0 upgraded, 0 newly installed, 0 to remove and 1 not upgraded.

The 2nd step is done. Hope you all are still with me.

**Deep learning stack:**Now, we need to install three major things to make most
of the DL software work:<br> * Nvidia driver<br> * CUDA<br> * CuDNN

I will also discuss the problems I ran into and you might too while installing
the above. It’s pretty common to mess up with Cuda installation.Don’t worry.

So,Cuda is a parallel computing platform to run general purpose code on our gpu
and CuDNN is a deep learning neural network library built on top of Cuda.

Let’s take a look at the first two:

Download the CUDA [toolkit](https://developer.nvidia.com/cuda-toolkit) . I would
recommend you to download the local deb file not the runfile as you may run into
trouble and then, go to the directory you downloaded and run the following
commands:

    sudo dpkg -i cuda-repo-ubuntu1604–9–1-local_9.1.85–1_amd64.deb
    sudo apt-key add /var/cuda-repo-<version>/7fa2af80.pub
    sudo apt-get update
    sudo apt-get install cuda

Now, restart your machine.

    sudo reboot

Add the following to your PATH and LD_LIBRARY_PATH. You might want to add them
permanently, by appending the following to your .profile at the end:


Log out and log in. Fire up the terminal and check the following:

    sritanu@combalgorythm:~$ nvcc -V
    nvcc: NVIDIA (R) Cuda compiler driver
    Copyright © 2005–2017 NVIDIA Corporation
    Built on Fri_Nov__3_21:07:56_CDT_2017
    Cuda compilation tools, release 9.1, V9.1.85

    sritanu@combalgorythm:~$ cat /proc/driver/nvidia/version
    NVRM version: NVIDIA UNIX x86_64 Kernel Module 390.48 Thu Mar 22 00:42:57 PDT 2018
    GCC version: gcc version 5.4.0 20160609 (Ubuntu 5.4.0–6ubuntu1~16.04.9)

    sritanu@combalgorythm:~$ nvidia-smi
    Sun Apr 15 21:08:54 2018
    + — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — -+
    | NVIDIA-SMI 390.48 Driver Version: 390.48 |
    | — — — — — — — — — — — — — — — -+ — — — — — — — — — — — + — — — — — — — — — — — +
    | GPU Name Persistence-M| Bus-Id Disp.A | Volatile Uncorr. ECC |
    | Fan Temp Perf Pwr:Usage/Cap| Memory-Usage | GPU-Util Compute M. |
    |===============================+======================+======================|
    | 0 GeForce GTX 108… Off | 00000000:01:00.0 On | N/A |
    | 0% 55C P0 65W / 250W | 268MiB / 11175MiB | 0% Default |
    + — — — — — — — — — — — — — — — -+ — — — — — — — — — — — + — — — — — — — — — — — +

    + — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — -+
    | Processes: GPU Memory |
    | GPU PID Type Process name Usage |
    |=============================================================================|
    | 0 26010 G /usr/lib/xorg/Xorg 151MiB |
    | 0 26571 G compiz 70MiB |
    | 0 26843 G …-token=15A70A4045B9DE3251ADD064926806A1 43MiB |
    + — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — — -+

Chances are you already have the third-party libraries but you might want to run
the following to verify:

    sudo apt-get install g++ freeglut3-dev build-essential libx11-dev libxmu-dev libxi-dev libglu1-mesa libglu1-mesa-dev

Cuda provides you with some read-only sample files to test the installation.
Copy them to some folder where you have also the write rights, for example, I
have it in my Downloads folder:

    sritanu@combalgorythm:~$ cuda-install-samples-9.1.sh ~/Downloads

Get in the `NVIDIA_CUDA-9.1_Samples` directory and run `make` .

When, it’s complete, do the following and test some commands. You should be
getting similar outputs to ./deviceQuery and ./bandwidthTest . If not, it’s
highly likely that you/your system have messed up somewhere.

    sritanu@combalgorythm:~/Downloads$ cd NVIDIA_CUDA-9.1_Samples/bin/x86_64/linux/release/

    sritanu@combalgorythm:~/Downloads/NVIDIA_CUDA-9.1_Samples/bin/x86_64/linux/release$ ./deviceQuery
    ./deviceQuery Starting...

    CUDA Device Query (Runtime API) version (CUDART static linking)

    Detected 1 CUDA Capable device(s)

    Device 0: "GeForce GTX 1080 Ti"
      CUDA Driver Version / Runtime Version          9.1 / 9.1
      CUDA Capability Major/Minor version number:    6.1
      Total amount of global memory:                 11175 MBytes (11718230016 bytes)
      (28) Multiprocessors, (128) CUDA Cores/MP:     3584 CUDA Cores
      GPU Max Clock rate:                            1633 MHz (1.63 GHz)
      Memory Clock rate:                             5505 Mhz
      Memory Bus Width:                              352-bit
      L2 Cache Size:                                 2883584 bytes
      Maximum Texture Dimension Size (x,y,z)         1D=(131072), 2D=(131072, 65536), 3D=(16384, 16384, 16384)
      Maximum Layered 1D Texture Size, (num) layers  1D=(32768), 2048 layers
      Maximum Layered 2D Texture Size, (num) layers  2D=(32768, 32768), 2048 layers
      Total amount of constant memory:               65536 bytes
      Total amount of shared memory per block:       49152 bytes
      Total number of registers available per block: 65536
      Warp size:                                     32
      Maximum number of threads per multiprocessor:  2048
      Maximum number of threads per block:           1024
      Max dimension size of a thread block (x,y,z): (1024, 1024, 64)
      Max dimension size of a grid size    (x,y,z): (2147483647, 65535, 65535)
      Maximum memory pitch:                          2147483647 bytes
      Texture alignment:                             512 bytes
      Concurrent copy and kernel execution:          Yes with 2 copy engine(s)
      Run time limit on kernels:                     Yes
      Integrated GPU sharing Host Memory:            No
      Support host page-locked memory mapping:       Yes
      Alignment requirement for Surfaces:            Yes
      Device has ECC support:                        Disabled
      Device supports Unified Addressing (UVA):      Yes
      Supports Cooperative Kernel Launch:            Yes
      Supports MultiDevice Co-op Kernel Launch:      Yes
      Device PCI Domain ID / Bus ID / location ID:   0 / 1 / 0
      Compute Mode:
         < Default (multiple host threads can use ::cudaSetDevice() with device simultaneously) >

    deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 9.1, CUDA Runtime Version = 9.1, NumDevs = 1
    Result = PASS

    sritanu@combalgorythm:~/Downloads/NVIDIA_CUDA-9.1_Samples/bin/x86_64/linux/release$ ./bandwidthTest
    [CUDA Bandwidth Test] - Starting...
    Running on...

    Device 0: GeForce GTX 1080 Ti
     Quick Mode

    Host to Device Bandwidth, 1 Device(s)
     PINNED Memory Transfers
       Transfer Size (Bytes) Bandwidth(MB/s)
       33554432   12582.4

    Device to Host Bandwidth, 1 Device(s)
     PINNED Memory Transfers
       Transfer Size (Bytes) Bandwidth(MB/s)
       33554432   12801.8

    Device to Device Bandwidth, 1 Device(s)
     PINNED Memory Transfers
       Transfer Size (Bytes) Bandwidth(MB/s)
       33554432   344177.4

    Result = PASS

    NOTE: The CUDA Samples are not meant for performance measurements. Results may vary when GPU Boost is enabled.

Now, at any time you run into any problem during Cuda installation , it might be
helpful to start from the beginning by doing the following:


**Problems faced while installing Cuda:**The problem I faced when I installed
Cuda for the first time was that I ran into a [Login
Loop](https://askubuntu.com/questions/762831/ubuntu-16-stuck-in-login-loop-after-installing-nvidia-364-drivers)
. This [answer](https://askubuntu.com/a/848668) worked for me. Also, you might
face [network connectivity problems in the login
screen](https://askubuntu.com/questions/16376/connect-to-network-before-user-login).
This [solution](https://askubuntu.com/a/796962) worked for me.

We’re done with the second part. Going to move to the third one.

Now let’s install CuDnn.

1.  Register yourself for the [NVIDIA Developer
Program](https://developer.nvidia.com/accelerated-computing-developer), if you
aren’t.
1.  Go to: [NVIDIA cuDNN home page](https://developer.nvidia.com/cudnn), click
Download and complete a short survey.
1.  Accept the T&C . Select the cuDNN version compatible with your Cuda version. I
went with [cuDNN v7.0.5 Library for
Linux](https://developer.nvidia.com/compute/machine-learning/cudnn/secure/v7.0.5/prod/9.1_20171129/cudnn-9.1-linux-x64-v7)
.
1.  Go to the downloaded directory and run the following:

    sritanu@combalgorythm:~/Downloads$ tar -xzvf cudnn-9.1-linux-x64-v7.tgz
    cuda/include/cudnn.h
    cuda/NVIDIA_SLA_cuDNN_Support.txt
    cuda/lib64/libcudnn.so
    cuda/lib64/libcudnn.so.7
    cuda/lib64/libcudnn.so.7.0.5
    cuda/lib64/libcudnn_static.a

    sritanu@combalgorythm:~/Downloads$ cd cuda

    sritanu@combalgorythm:~/Downloads/cuda$ sudo cp lib64/* /usr/local/cuda/lib64/

    sritanu@combalgorythm:~/Downloads/cuda$ sudo cp include/* /usr/local/cuda/include/

**Deep learning software:**

**Install Anaconda:**Anaconda is an awesome python package manager and we will
be using Python3.

1.  Download the 64-bit python3.6 version from
[here](https://www.anaconda.com/download/#linux) . You can also curl/wget .
1.  Run:

    $ bash Anaconda3–5.0.1-Linux-x86_64.sh

3. Add anaconda to your PATH:

    $

4. Verify if you have installed anaconda correctly and see what packages have
been installed.


5. Now, depending on the software and it’s version you require for your project
create a virtual environment in anaconda by the following:

    $ conda create --name env python=3

env is the name of your environment you can use any name of your choice.

6. We will now activate the virtual environment and install all the deep
learning software needed. Run the following:


7. Your command prompt prefix will change to :

    (env) $

8. When you want to deactivate the environment, run:

    $ source deactivate

Activate your virtual environment before installing the following DL software:

**Install **[Theano](http://deeplearning.net/software/theano/)**:**

    conda install theano pygpu

You might run into the following error while importing theano.

    RuntimeError: To use MKL 2018 with Theano you MUST set “MKL_THREADING_LAYER=GNU” in your environement.

Two solutions:

Either, run the following and downgrade mkl :

    $ conda install mkl=2017

Or, add this to your `~/.bashrc` file: `export MKL_THREADING_LAYER=GNU `then
re-open your terminal.

**Install **[Tensorflow](https://www.tensorflow.org/)**:**

The DL framework by Google.

1.  Install tensorflow-gpu from conda:

    $ conda install -c anaconda tensorflow-gpu

2. Validate your install as mentioned
[here](https://www.tensorflow.org/install/install_linux#ValidateYourInstallation)
.

**Install **[Keras](https://keras.io/)**:**

Keras is a high level neural network which can use either one of the three :
Tensorflow or Theano or CNTK as its [backend](https://keras.io/backend/).

    $ pip install keras

**Install **[Pytorch](http://pytorch.org/)**:**

Pytorch is a relatively new DL framework which is my current favourite due to
these
[reasons](https://towardsdatascience.com/pytorch-vs-tensorflow-spotting-the-difference-25c75777377b).
Run the following to install it:

    $ conda install pytorch torchvision cuda80 -c soumith

The above command might result into ridiculously slow package download and
installation. You may install it directly via pip.

    $ pip install torch torchvision

[Jupyter notebook](http://jupyter.org/)**:**

It’s an open source web-based IDE and it’s the defacto standard for data science
development.

Run **conda list **and check** **if jupyter is installed in the virtual
environment. If not, then install it.<br> Install it by:

    $ conda install jupyter

Run it by:

    $ jupyter notebook

**Other important softwares:**

1.  Install git:

    sudo apt-get install git

2. If you are working on gpu servers, its highly likely that you will just have
a terminal to work with and no ide at all. Learn nano/vim. Vim has a steep
learning curve but it’s worth the effort.

You can install vim by:


Learn vim by simply typing vimtutor in your terminal.There are a lot of good
tutorials on vim on the web.

Make your vim awesome by installing plugins and make it full blown editor for
python development. You can follow this [post](http://moelove.info/vim/) .

3. Install Atom/SublimeText. I prefer [Atom](https://atom.io/). Download .deb
[file](https://atom.io/) and install it.

4. [Visual Code](https://code.visualstudio.com/) : You do have an option to
install it while installing Anaconda

5. [PyCharm CE](https://www.jetbrains.com/pycharm/download/) : Brilliant python
IDE

That’s it folks. Enjoy!!
