# Installing faceswap
- [Installing faceswap](#installing-faceswap)
- [Prerequisites](#prerequisites)
  - [Hardware Requirements](#hardware-requirements)
  - [Supported operating systems](#supported-operating-systems)
- [Important before you proceed](#important-before-you-proceed)
- [Linux and Windows Install Guide](#linux-and-windows-install-guide)
  - [Installer](#installer)
  - [Manual Install](#manual-install)
  - [Prerequisites](#prerequisites-1)
    - [Anaconda](#anaconda)
    - [Git](#git)
  - [Setup](#setup)
    - [Anaconda](#anaconda-1)
      - [Set up a virtual environment](#set-up-a-virtual-environment)
      - [Entering your virtual environment](#entering-your-virtual-environment)
    - [faceswap](#faceswap)
      - [Easy install](#easy-install)
      - [Manual install](#manual-install-1)
  - [Running faceswap](#running-faceswap)
  - [Create a desktop shortcut](#create-a-desktop-shortcut)
  - [Updating faceswap](#updating-faceswap)
- [General Install Guide](#general-install-guide)
  - [Installing dependencies](#installing-dependencies)
    - [Git](#git-1)
    - [Python](#python)
    - [Virtual Environment](#virtual-environment)
  - [Getting the faceswap code](#getting-the-faceswap-code)
  - [Setup](#setup-1)
    - [About some of the options](#about-some-of-the-options)
  - [Run the project](#run-the-project)
  - [Notes](#notes)

# Prerequisites
机器学习本质上涉及大量的试验和错误。你让一个程序尝试数以百万计的不同设置，以找到一种算法，做你想做的事。这个过程真的很慢，除非你有加速这个过程所需的硬件。
这个过程所做的计算类型很适合显卡，而不是普通的处理器。**几乎要求你在台式机或服务器上运行训练过程，**在CPU上运行意味着可能需要几周时间来训练你的模型，而在GPU上则需要几小时。

## Hardware Requirements
**TL;DR: you need at least one of the following:**

- **A powerful CPU**
    - notebook的CPU通常可以运行软件，但不会快到足以以合理的速度进行训练。
- **A powerful GPU**
    - 目前，Nvidia的GPU被完全支持。而AMD的显卡通过plaidML被部分支持。
    - 如果使用Nvidia GPU，那么它至少需要支持CUDA计算能力3.5。(1.0版将在计算能力3.0上工作)
      要看你的GPU支持哪个版本，请参考这个列表：https://developer.nvidia.com/cuda-gpus
      晚于7xx系列的桌面卡很可能被支持。
- **A lot of patience**

## Supported operating systems
- **Windows 10**
 Windows 7和8可能工作。你的情况可能有所不同。Windows有一个安装程序，将设置你需要的一切。见：https://github.com/deepfakes/faceswap/releases
- **Linux**
  大多数基于Ubuntu/Debian或CentOS的Linux发行版都可以使用。
- **macOS**
  由于缺乏Nvidia的驱动/库，MacOS上的GPU支持是有限的。
- 所有的操作系统必须是64位的，才能运行Tensorflow。

另外，也有一个基于Debian的docker镜像。

# Important before you proceed
**如果你不熟悉命令行工具，你可能很难设置环境，也许不应该尝试本指南中描述的任何步。
开发商也不对你可能对自己的电脑造成的任何损害负责。

# Linux and Windows Install Guide

## Installer
Windows和Linux现在都有一个安装程序，为你安装一切，并创建一个桌面快捷方式，直接进入图形用户界面。你可以从 https://github.com/deepfakes/faceswap/releases 下载该安装程序。
如果你对安装程序有疑问，请继续阅读在Windows上安装facewap的更多手动方法。

## Manual Install
设置换脸对新用户来说似乎有点吓人，但它并不复杂，虽然有点耗时。建议在可能的情况下使用Linux，因为Windows会占用你20%的GPU内存，使facewap运行得慢一些，但是使用Windows是完全可以的，而且100%支持。

## Prerequisites

### Anaconda
下载并安装最新的Python 3 Anaconda，地址是：https://www.anaconda.com/download/。除非你知道你在做什么，否则你可以把所有的选项都留在默认状态。

### Git
下载并安装 Windows 版的 Git：https://git-scm.com/download/win。除非你知道自己在做什么，否则可以把所有的选项都放在默认状态。

## Setup
重新启动你的电脑，这样你刚刚安装的所有东西都会被注册。

### Anaconda
#### Set up a virtual environment
- Open up Anaconda Navigator
- Select "Environments" on the left hand side
- Select "Create" at the bottom
- In the pop up:
    - Give it the name: faceswap
    - **IMPORTANT**: Select python version 3.8
    - Hit "Create" (NB: This may take a while as it will need to download Python)
![Anaconda virtual env setup](https://i.imgur.com/CLIDDfa.png)

#### Entering your virtual environment
To enter the virtual environment:
- Open up Anaconda Navigator
- Select "Environments" on the left hand side
- Hit the ">" arrow next to your faceswap environment and select "Open Terminal"
![Anaconda enter virtual env](https://i.imgur.com/rKSq2Pd.png)

### faceswap
- If you are not already in your virtual environment follow [these steps](#entering-your-virtual-environment)
- Get the faceswap repo by typing: `git clone --depth 1 https://github.com/deepfakes/faceswap.git`
- Enter the faceswap folder: `cd faceswap`

#### Easy install
- Enter the command `python setup.py` and follow the prompts:
- If you have issues/errors follow the Manual install steps below.

#### Manual install
如果上面的简易安装成功完成，请不要按照这些步进行。
如果你使用的是Nvidia显卡，请确保你为所需版本的Tensorflow安装了正确的Cuda/cuDNN版本。
- Install tkinter (required for the GUI) by typing: `conda install tk`
- Install requirements:
  - For Nvidia GPU users: `pip install -r requirements_nvidia.txt`
  - For AMD GPU users: `pip install -r requirements_amd.txt`
  - For CPU users: `pip install -r requirements_cpu.txt`

## Running faceswap
- 如果你还没有进入你的虚拟环境，请按照[这些步](#entering-your-virtual-environment)
- 进入 faceswap 文件夹。`cd faceswap`。
- 输入以下内容查看命令列表： `python faceswap.py -h`或输入`python faceswap.py gui`启动GUI

## Create a desktop shortcut
可以添加一个桌面快捷方式，方便直接启动换脸图形用户界面。

- Open Notepad
- Paste the following:
```
%USERPROFILE%\Anaconda3\envs\faceswap\python.exe %USERPROFILE%/faceswap/faceswap.py gui
```
- 将文件保存在桌面上，称为 "faceswap.bat"。

## Updating faceswap
随着新特征的增加和错误的修复，保持facewap的最新状态是很好的。要做到这一点。
- 如果使用图形用户界面，你可以进入帮助菜单，选择 "检查更新..."。如果有更新，请到帮助菜单中选择 "更新Faceswap"。重新启动Faceswap以完成更新。
- 如果你还没有进入你的虚拟环境，请按照[这些步](#entering-your-virtual-environment)
- 进入 faceswap 文件夹。`cd faceswap`。
- 输入以下内容 `git pull --all`。
- 一旦下载了最新的版本，确保你的依赖关系是最新的。有一个脚本可以帮助解决这个问题。`python update_deps.py`。

# General Install Guide
## Installing dependencies
### Git
获取代码和保持代码库的更新需要用到Git。
从[git网站](https://git-scm.com/downloads)为你的发行版获取git。


### Python
推荐的安装方法是使用Conda3环境，因为这将处理Nvidia的CUDA和cuDNN直接安装到你的Conda环境。这是迄今为止安装项目的最简单和最可靠的方法。
- MiniConda3 is recommended: [MiniConda3](https://docs.conda.io/en/latest/miniconda.html)
  
或者，你可以为你的发行版安装Python（>=3.7-3.8 64位）（下面的链接）。如果你走这条路并且使用Nvidia GPU，你应该为你的系统安装CUDA（https://developer.nvidia.com/cuda-zone）和cuDNN（https://developer.nvidia.com/cudnn）。如果你不打算自己构建Tensorflow，请确保为当前安装的Tensorflow版本安装正确的Cuda和cuDNN包（当前版本：Tensorflow 2.2。 v1.0版本：Tensorflow 1.15）。你可以在这里检查兼容的版本。(https://www.tensorflow.org/install/source#gpu)。
    - Python distributions:
    - apt/yum install python3 (Linux)
    - [Installer](https://www.python.org/downloads/release/python-368/) (Windows)
    - [brew](https://brew.sh/) install python3 (macOS)

### Virtual Environment
  我们强烈建议你在虚拟环境中安装 faceswap。事实上，我们一般不会支持不在虚拟环境中的安装，因为排除软件包的冲突几乎是不可能的。

  如果使用Conda3，那么设置虚拟环境是相对直接的。更多信息可以在 [Conda Docs](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) 找到。

  如果使用默认的Python发行版，那么当你不使用docker时，[virtualenv](https://github.com/pypa/virtualenv)和[virtualenvwrapper](https://virtualenvwrapper.readthedocs.io)可能有所帮助。

## Getting the faceswap code
建议用 git 克隆 repo，而不是从 http://github.com/deepfakes/faceswap 下载代码并解压，因为这将使你更容易获得最新的代码（这可以从 GUI 中完成）。要克隆一个 repo，你可以使用你的发行版的 Git GUI，或者打开一个命令提示符，输入你要存储 faceswap 的文件夹，然后输入。
```bash
git clone https://github.com/deepfakes/faceswap.git
```

## Setup
进入你的虚拟环境，然后进入 faceswap 被下载到的文件夹并运行。
```bash
python setup.py
```
如果由于任何原因安装失败，你仍然可以手动安装requirements.txt中列出的软件包。

### About some of the options
   - CUDA: For acceleration. Requires a good nVidia Graphics Card (which supports CUDA inside)
   - Docker: Provide a ready-made image. Hide trivial details. Get you straight to the project.
   - nVidia-Docker: Access to the nVidia GPU on host machine from inside container.

CUDA with Docker in 20 minutes.
```
INFO    The tool provides tips for installation
        and installs required python packages
INFO    Setup in Linux 4.14.39-1-MANJARO
INFO    Installed Python: 3.7.5 64bit
INFO    Installed PIP: 10.0.1
Enable  Docker? [Y/n] 
INFO    Docker Enabled
Enable  CUDA? [Y/n] 
INFO    CUDA Enabled
INFO    1. Install Docker
        https://www.docker.com/community-edition
        
        1. Install Nvidia-Docker & Restart Docker Service
        https://github.com/NVIDIA/nvidia-docker
        
        1. Build Docker Image For faceswap
        docker build -t deepfakes-gpu -f Dockerfile.gpu .
        
        1. Mount faceswap volume and Run it
        # without gui. tools.py gui not working.
        nvidia-docker run --rm -it -p 8888:8888 \
            --hostname faceswap-gpu --name faceswap-gpu \
            -v /opt/faceswap:/srv \
            deepfakes-gpu
        
        # with gui. tools.py gui working.
        ## enable local access to X11 server
        xhost +local:
        ## enable nvidia device if working under bumblebee
        echo ON > /proc/acpi/bbswitch
        ## create container 
        nvidia-docker run -p 8888:8888 \
            --hostname faceswap-gpu --name faceswap-gpu \
            -v /opt/faceswap:/srv \
            -v /tmp/.X11-unix:/tmp/.X11-unix \
            -e DISPLAY=unix$DISPLAY \
            -e AUDIO_GID=`getent group audio | cut -d: -f3` \
            -e VIDEO_GID=`getent group video | cut -d: -f3` \
            -e GID=`id -g` \
            -e UID=`id -u` \
            deepfakes-gpu
        
        1. Open a new terminal to interact with the project
        docker exec -it deepfakes-gpu /bin/bash
	# Launch deepfakes gui (Answer 3 for NVIDIA at the prompt)
	python3.8 /srv/faceswap.py gui
```

A successful setup log, without docker.
```
INFO    The tool provides tips for installation
        and installs required python packages
INFO    Setup in Linux 4.14.39-1-MANJARO
INFO    Installed Python: 3.7.5 64bit
INFO    Installed PIP: 10.0.1
Enable  Docker? [Y/n] n
INFO    Docker Disabled
Enable  CUDA? [Y/n] 
INFO    CUDA Enabled
INFO    CUDA version: 9.1
INFO    cuDNN version: 7
WARNING Tensorflow has no official prebuild for CUDA 9.1 currently.
        To continue, You have to build your own tensorflow-gpu.
        Help: https://www.tensorflow.org/install/install_sources
Are System Dependencies met? [y/N] y
INFO    Installing Missing Python Packages...
INFO    Installing tensorflow-gpu
......
INFO    Installing tqdm
INFO    Installing matplotlib
INFO    All python3 dependencies are met.
        You are good to go.
```

## Run the project
一旦所有这些要求被安装，你就可以尝试运行facewap工具。使用`-h`或`-help`选项可以获得一个选项列表。

```bash
python faceswap.py -h
```

or run with `gui` to launch the GUI
```bash
python faceswap.py gui
```


Proceed to [../blob/master/USAGE.md](USAGE.md)

## Notes
本指南还远未完成。功能可能会随着时间的推移而改变，而且随着时间的推移，新的依赖性也会被添加和删除。
If you are experiencing issues, please raise them in the [faceswap Forum](https://faceswap.dev/forum) instead of the main repo. Usage questions raised in the issues within this repo are liable to be closed without response.
