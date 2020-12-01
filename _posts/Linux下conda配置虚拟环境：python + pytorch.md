# Linux下conda配置虚拟环境：python + pytorch

默认已经安装好conda

## 创建虚拟环境
### conda创建并激活虚拟环境
命令：
> conda create -n your_env_name python=2.7/3.6
> source activate your_env_name

其中，-n中n表示name，即你创建环境的名字。
之后如果忘记自己创建的环境的名字，可以查看conda中的环境：
> conda env list

之后选择你创建的环境激活。之后进入pytorch官网选择你要安装的版本以及操作系统、CUDA版本号，便可以得到下载的命令。比如本人得到的命令是：
> conda install pytorch torchvision cuda80 -c pytorch

若不知道自己CUDA的版本号，可以输入下面命令查询：
> cat /usr/local/cuda/version.txt

若希望快速下载，可以把源换为国内的镜像源，从而提高下载速度。在下载前输入：
> vim ~/.condarc

打开文件后，输入：
> channels:
>   \- https://mirrors.ustc.edu.cn/anaconda/pkgs/main/
>   \- https://mirrors.ustc.edu.cn/anaconda/cloud/conda-forge/
>   \- https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
>   \- defaults
> show_channel_urls: true

若配置好环境后需要别的包，用conda或者pip下载皆可

