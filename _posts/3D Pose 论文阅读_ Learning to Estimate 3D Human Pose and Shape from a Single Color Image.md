该论文发表于CVPR 2018并获得best poseter award。
# Motivation
之前的做3D Pose和Shape的大部分都是基于优化的方法来做的，而基于深度学习的方法做的效果并不好。原因：深度学习的方法需要大量训练样本，而有SMPL 标注的数据集并不多且都是室内的，所以深度学习预测的效果并不好。
为了解决这个问题，作者提出了一种通过弱监督的方法来利用有2D keypoints和instance segmentation的大量的数据集来进行训练的网络模型，从而使得深度学习的方法在3D Pose 和Shape估计领域达到了SOTA。
# Network Architecture
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200416182151598.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
图像输入到网络中，首先经过encoder decoder（backbone为Res50）部分，也就是图中的Human2D部分，并在decoder部分输出heatmap以及instance segmentation。
每个heatmap经过argmax以及max操作取出位置信息以及置信度信息来输入之后的PosePrior部分，该部分由几个简单的全连接层构成，并输出SMPL模型的$\theta$参数。
instance segmentation 经过几个简单的卷积和max pooling后，最后经过全连接层预测出SMPL模型的$\beta$参数。
预测的$\theta$和$\beta$输入到SMPL模型提供的mesh generator生成人体3D mesh。最后通过Render来重投影回图像上并通过投影的keypoint的位置以及segmentation的信息来约束。
# 训练过程以及结果
首先在MPII，LSP以及LSP extend数据集上训练Human2D部分。之后再训练Prior部分，该部分作者首先只在SMPL的$\theta$和$\beta$参数的$L_2$损失函数的监督下训练，训练一定的iter后再加入3D mesh的损失或者3D Pose的损失（取决于你更care哪一方面），最后在整个网络一起训练。
该论文在Human3.6m和U3D数据集上均达到了SOTA水平，是18年较好的一个结果。
