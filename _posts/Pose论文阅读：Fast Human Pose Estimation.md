# Fast Human Pose Estimation
## Abstruct
现在的Pose框架虽然精度以及泛化能力已经不错，但是模型过于复杂，使得参数量以及部署时消耗的内存过大。  这篇文章就是通过牺牲极少部分的精度来达到大幅度减少内存的消耗的目的。作者主要是通过用训练好的教师网络（大网络）将知识传递给学生网络（小网络）来实现这一目的，他们称他们的方法为Fast Pose Distillation（FPD）。最终使用时只需要将学生网络部署在设备上即可。  作者在MPII与LSP数据集上做了验证，证明了他们的方法的有效性。
## Introduction
现在做Pose的绝大多数在追求精度而忽略了内存的消耗，而作者从减少内存消耗而基本不减少精度方面出发提出FPD。本文作者针对Hourglass做的实验，将提前训练好的参数量大的HourglassNet作为教师网络。然后通过将Knowledge Distillation的思想应用到Pose上来训练学生网络。最后在精度与内存消耗上达到了更好的平衡。
## Related Work
### human pose
最近五年pose取得巨大的进展，但绝大部分人都是致力于使用更加复杂的模型来达到更高的精度而忽略了模型的部署消耗，从而限制了Pose研究成果在实际中的应用。
其实，也有少部分人在研究提高模型效率的问题。但他们的方法几乎都大大减少了精确度。作者的方法在精确度基本不变的情况下，大大减少了内存消耗。
### Knowledge Distillation
知识蒸馏具体传递的就是教师网络的预测输出，即将教师网络的输出也作为监督信息的一部分。拿分类任务来说，就是传递了各个类别的可能性，这相对于人工标注的数据更利于小网络的学习。因为其包含的信息变多了，也利于机器的拟合。
## Fast Human Pose Estimation
![Hourglass原始网络与裁剪后的网络](https://img-blog.csdnimg.cn/20190821202656798.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70)
首先，讲一下作者的大体思路：先分别减少Hourglass的Features数和堆叠网络的个数来观察其性能降低多少。之后，选择一个网络作为学生网络，通过知识蒸馏的方法使得其性能再提升上来。从而实现精度基本不变而部署消耗大大减少的目的。下图为作者减少Hourglass的Feature数和Stage数的对比图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190821203416792.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70)
最后作者选定了4堆叠块，128通道的HourglassNet小网络作为学生网络。训练过程如下图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019082120490996.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70)

 - 训练教师网络
 - 训练学生网络：将教师网络的预测输出作为一部分监督信息传给学生网络。也就是说，学生网络的监督信息是ground truth与教师网络预测的复合监督信息。具体来说，Loss是 $L_{fpd}=\alpha L_{pd} + (1-\alpha) L_{mse}$， 其中$L_{pd}$是教师网络输出作为监督信息而得到的损失，另一项损失便为ground truth作为监督信息得到的损失。两者的损失函数都使用MSE损失函数。
## Experiment
MPII数据集上的结果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190821210456409.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70)
LSP数据集上的结果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190821210543513.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70)
这篇论文主要内容介绍完毕，其中论文中还有许多细节在这里就不写了。有兴趣的看原文，本文纯属博主个人理解，如有不清楚或错误的地方，望指正
