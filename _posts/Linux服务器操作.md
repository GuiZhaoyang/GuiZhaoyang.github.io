# Linux服务器操作
## docker操作
**创建docker：** 在根目录下，输入：
>./deploy_container_with_gpu.sh --shm-size=8G
Enter the image name: pcalab/gpu-caffe:1.0.0-rc3  #输入你要使用的镜像名字
Enter the host name[default is "docker18"]:       #自己起个名字，可以默认不填
Enter the container name: chendi-caffe            #给你的container(虚拟机)起个方便标示的名字（请务必加入自己的姓名全拼）
BE AWARE!
When using gpu inside containers, please specify gpu id explicitly! e.g.
    CUDA_VISIBLE_DEVICES=2,3 python xxx.py
[(A)ccept/(D)ecline]: A
23871cbc20983c20938nc20978bcn237bc237unc32073nc2073nc20987nc02937nc09273nc23707nc2
Now open your browser and access your container with shipyard web UI.
>
其中，--shm-size=8G为设置共享内存的大小，如果不进行设置默认大小为64MB；image name可以通过`docker images`指令来查看
**删除docker：**

 **退出但不关闭docker：<kbd>ctrl </kbd> + <kbd> p</kbd> + <kbd> q</kbd>**
 **选定指定id的GPU运行程序，例如：** 
>CUDA_VISIBLE_DEVICES=2, 3 python train.py
>CUDA_VISIBLE_DEVICES=0  python train.py

## 环境配置
#### git安装
 > apt update
 > apt insatll git

若不更新apt，那么下载的git版本太低。
#### cocoapi安装
> export INSTALL_DIR=$PWD
> cd $INSTALL_DIR
> git clone https://github.com/cocodataset/cocoapi.git
> cd cocoapi/PythonAPI
> python setup.py build_ext install

其中，export name = $PWD的含义是将等号右边的路径赋给等号左边的变量，以后可以直接通过cd $name的方式进入预先设定的目录下。其中，\$PWD的含义是提取当下的绝对路径。

#### Tmux安装与使用
> apt-get install tmux
> tmux #进入Tmux

创建新窗口 	             （<kbd>ctrl</kbd> + <kbd>b</kbd>） + <kbd>c</kbd>
切换下一个窗口		（<kbd>ctrl</kbd> + <kbd>b</kbd>） + <kbd>n</kbd>
切换上一个窗口		（<kbd>ctrl</kbd> + <kbd>b</kbd>） + <kbd>p</kbd>


