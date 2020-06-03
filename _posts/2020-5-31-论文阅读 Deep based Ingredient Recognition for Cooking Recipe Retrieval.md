---
layout:     post
title:      论文阅读 Deep-based Ingredient Recognition for Cooking Recipe Retrieval
subtitle:   图像检索
date:       2020-5-31
author:     Black
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - 多标签分类
    - 菜谱检索
    - 食材检索
    - 零样本检索
---

# 论文阅读：Deep-based Ingredient Recognition for Cooking Recipe Retrieval

阅读该论文为一个课程的阅读大作业。由于博主的研究方向也不是该方向，所以在该篇文章只关注于该篇论文的方法部分，而相关工作，数据集与实验则不是该篇文章的重点。但是如果读者是做这一方面的研究，建议去熟悉一下作者用到的几个数据集并分析在各个数据集上的实验结果。
## 面向的问题
### 1 问题简介
首先该论文处理的问题为食谱检索。具体为给出一张拍摄的含有菜肴的图像，需要在数据库中找出该菜肴的名称以及其菜谱。
### 2 应用
检索食谱可以应用在很多的食品类健康类的app上，用于来估计营养或者快速给出食谱。
## 方法
### 1 创新点

- 之前处理该类问题的一般手段是从图像出发直接预测食谱名称。这种方法首先其性能表现较差，另外不在其训练集中的食谱该方法一定预测不出正确结果。鉴于之前的方法的缺点，本文作者在预测食谱名称的同时也会预测图像中的食材种类。即在原来的单标签分类问题上扩展为一个单标签和一个多标签分类问题。这样做的好处首先是食材的种类远少于食谱的种类（因为食谱本质上是多种食材的组合），所以更容易将预测的食材结果应用到零样本检索问题上从而使得该方法可以预测未在训练集中的食谱名称；其次，预测出的食材种类也能作为辅助信息提升食谱的检索性能。下图展示了食材检索的高难度，在同一种菜肴中辅助性的食材也可能不一样。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200603102946805.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
- 将网络预测出的食材种类结合条件随机场在全局语料库上建立的概率图模型得到优化后的食材种类，然后利用该食材种类与数据库的食材种类做对比从而得到最后的检索结果。


### 2 具体方法
- 该方法的overview见下图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200603103553415.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
首先，图像送入CNN中进行特征提取，之后进入全连接层进行食谱分类与食材分类的任务。该阶段预测的食谱类别并不作为最终阶段的食谱类别的预测结果，其目的只是使得食材分类的结果以及共享特征更好。
预测出的食材分类的概率向量作为输入量输入到第二阶段，也就是零样本检索阶段。该阶段首先用使用条件随机场对所有语料库中的食材进行建模，然后依据该模型对第一阶段输出的食材成分进行调整，从而得到最终预测的食材成分向量，然后依据该向量来输出最终的检索结果。
- 第一阶段详解：作者尝试了四种不同结构的网络结构，最终选择了第四个结构（Arch-D）。下图为作者尝试的四种结构：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200603180628472.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
这四种结构本质上讨论的是这两种任务能在什么程度上进行特征的共享。作者通过实验证明第四种结构效果会好一些。单标签与多标签分类使用的损失函数都是CrossEntropy损失函数。
- 第二阶段详解：该阶段首先基于条件随机场建立了一个反应各种食材之间关系的概率图模型。并且基于这个图模型，输入一张测试图像与第一阶段输出的食材分布向量，该图模型会输出一个新的食材预测结果。
得到该食材预测结果，对其与gt类别的向量做一个点积便能得到该预测结果的得分情况。（该部分作者介绍的比较简略，但是涉及的内容却相当多，有兴趣的可以去阅读该部分引用的参考文献）

另外，本文作者也提出了一个有关食谱的新数据集VIREO Food-172，做该方向感兴趣的朋友可以去了解下。
