# Ubuntu1604 配置Detectron2 cuda10.1 Driver418.56

## apt 安装 显卡驱动(最好禁用 nouveau) 以及CUDA安装

- 参考[这篇文章](https://blog.csdn.net/shinef/article/details/89153920)

1. 添加Graphic Drivers PPA

    ```bash
    sudo add-apt-repository ppa:graphics-drivers/ppa
    sudo apt-get update
    ```

2. 寻找合适的驱动版本

    ```bash
        ubuntu-drivers devices
    ```

3. 安装重启

    ```bash
    sudo apt install nvidia-
    sudo nvidia-smi
    sudo nvidia-settings
    ```

4. 安装cudu

    去nvidia官网[下载 `.run`文件](https://developer.nvidia.com/cuda-10.1-download-archive-base?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1604&target_type=runfilelocal)

    ```bash
    sudo sh cuda_10.1.105_418.39_linux.run
    ```

5. 配置环境变量

    ```bash
    export PATH=/usr/local/cuda-10.1/bin:$PATH
    export LD_LIBRARY_PATH=/usr/local/cuda-10.1/lib64:$LD_LIBRARY_PATH
    export CUDA_HOME=$CUDA_HOME:/usr/local/cuda-10.1
    ```

6. 安装cudnn

    下载[cuDNN Library for Linux](https://developer.nvidia.com/rdp/cudnn-archive)

    ```bash
    tar -xzvf cudnn-10.***.tgz
    sudo cp cuda/include/cudnn.h /usr/local/cuda/include
    sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
    sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
    ```

7. 检查

    ```bash
    nvidia-smi
    nvcc -V
    ```

## 配置Detectron2环境

如果自己能力强看[INSTALL.md](https://github.com/facebookresearch/detectron2/blob/master/INSTALL.md)，或者看[Colab Notebook](https://colab.research.google.com/drive/16jcaJoc6bCFAQ96jDe2HwtXj7BMD_-m5#scrollTo=9_FzH13EjseR)`需科学上网`。

1. 安装pytorch

    ```bash
    # install dependencies: (use cu101 because colab has CUDA 10.1)
    pip install -U torch==1.5 torchvision==0.6 -f https://download.pytorch.org/whl/cu101/torch_stable.html
    pip install cython pyyaml==5.1
    pip install -U 'git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI'
    ```

2. 安装opencv

    ```bash
    pip install opencv-python
    ```

3. 安装Detectron2

   1. 编译好了，对网有要求

        ```bash
        pip install detectron2==0.1.2 -f https://dl.fbaipublicfiles.com/detectron2/wheels/cu101/index.html
        ```

   2. 从github下载编译

        ```bash
        git clone https://github.com/facebookresearch/detectron2.git
        python -m pip install -e detectron2
        ```

## 遇到的问题

遇到问题先去issue搜一下。

1. assert get_version(fvcore, 3) >= (0, 1, 1), "Requires fvcore>=0.1.1"
    > 卸载fvcore，安装fvcore>=0.1.1
2. 编译好的包和依赖是对应的
    > 之前是依赖torch==1.4+cu100 torchvision==0.5+cu100
    > 更新之后torch==1.5 torchvision==0.6
