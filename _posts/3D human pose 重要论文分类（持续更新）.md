# 3D human pose 重要论文整理（持续更新）
内容较多，提供目录便于查找
@[TOC](目录)
## 传统方法
*[1] Chunyu Wang,Yizhou Wang,Zhouchen Lin,Alan L. Yuille,Wen Gao. Robust Estimation of 3D Human Poses from a Single Image. In the Center for Brains, Minds and Machines(CBMM), 2014（用优化的方法进行2D pose到3D pose的三维重建）

*[2] Atul Kanaujia. Coupling Top-down and Bottom-up Methods for 3D Human Pose and Shape Estimation from Monocular Image Sequences. 2014

*[3] Behnam Babagholami-Mohamadabadi, Amin Jourabloo, Ali Zarghami, and Shohreh Kasaei . A Bayesian Framework for Sparse Representation-Based 3D Human Pose Estimation. In IEEE Signal Processing Letters (SPL), 2014


## 深度学习方法
### 3D Pose
#### 从单幅图像直接出3D pose
[1] Sijin Li and Antoni B Chan. 3d human pose estimation from monocular images with deep convolutional neural network. In Asian Conference on Computer Vision (ACCV), pages 332–347, 2014.

> 第一个利用该思路进行三维人体姿态估计的工作，也是使用深度学习进行三维人体姿态估计的工作。该工作首先使用一个8层的网络做一个目标检测的视觉任务。然后将用来做特征提取部分的CNN层来作为三维人体姿态估计的初始化模型，并丢弃掉目标检测网络头部分进行训练。该方法相对于传统方法明显的提高。

[2] Sijin Li, Weichen Zhang, Antoni B. Chan. Maximum-Margin Structured Learning with Deep Networks for 3D Human Pose Estimation.CVPR, 2015

> 该网络除了从图像直接回归三维关键点坐标外，还加入了一个新的分支。该分支只在训练时发挥作用，其接收三维姿态的真是标注作为输入，然后经过多层感知机提取特征。然后利用该特征作为监督来训练，整个网络看上去也是一个多任务网络。

[3] Sungheon Park, Jihye Hwang, and Nojun Kwak. 3d human pose estimation using convolutional neural networks with 2d pose information. In Proceedings of the European Conference on Computer Vision (ECCV), pages 156–169, 2016.

> 提出的整个的网络的结构与[1]类似，不同点在于该网络使用的是二维姿态估计作为另一个任务分支的监督且这两个任务一同训练。

[4] Bugra Tekin, Isinsu Katircioglu, Mathieu Salzmann, Vincent Lepetit, and Pascal Fua. Structured prediction of 3d human pose with deep neural networks. In British Machine Vision Conference (BMVC), 2016.

> 首先利用三维关键点坐标作为输入和监督来预训练一个自编码-解码器，预训练好后保留解码器。之后在主网络中输入图像经过CNN提取特征不直接回归三维人体关键点坐标，而是来预测解码器输入端的隐向量，该隐向量通过解码器解码出三维人体关键点位置，在这个过程中解码器的参数不会更新。

*[5] Albert Haque, Boya Peng, Zelun Luo, Alexandre Alahi, Serena Yeung, Li Fei-Fei. Towards Viewpoint Invariant 3D Human Pose Estimation. ECCV, 2016.(从单一深度图出3D pose）

[6] 3D Human Pose Estimation in the Wild by Adversarial Learning. CVPR 2018.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200404190410859.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)


#### 由单幅图的2D pose 出3D pose

[1] Julieta Martinez, Rayat Hossain, Javier Romero, and James J. Little. A simple yet effective baseline for 3d human pose estimation.ICCV 2017.

*[2] Hao-Shu Fang, Yuanlu Xu, Wenguan Wang, Xiaobai Liu, Song-Chun Zhu. Learning Pose Grammar to Encode Human Body Configuration for 3D Pose Estimation. AAAI 2018.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200401191236519.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[3] Unsupervised Adversarial Learning of 3D Human Pose from 2D Joint Locations. 2018.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200404184505599.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[4] Matteo Ruggero Ronchi, Oisin Mac Aodha, Robert Eng, and Pietro Perona. It’s all relative: Monocular 3d human pose estimation from weakly supervised data. In British Machine Vision Conference (BMVC), 2018.

[5] 3D Human Pose Estimation with Relational Networks. BMVC 2018. 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200405103241326.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[6] 3D Human Pose Estimation with Siamese Equivariant Embedding. Neurocomputing 2018.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406101243978.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[7] RepNet: Weakly Supervised Training of an Adversarial Reprojection Network for 3D Human Pose Estimation. CVPR 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406112951738.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[8] Lifting 2d Human Pose to 3d : A Weakly Supervised Approach. IJCNN 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406170138606.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[9] PoseLifter: Absolute 3D human pose lifting network from a single noisy 2D. 2020.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406182318764.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)

#### 借助单幅图的2D pose或其feature出3D pose(可能加入其他约束）
[1]Dushyant Mehta, Helge Rhodin, Dan Casas, Pascal Fua.Monocular 3D Human Pose Estimation In The Wild Using Improved CNN Supervision. 3DV, 2017（提出了MPI-INF-3DHP Dataset）

[2] Ching-Hang Chen,Deva Ramanan. 3D Human Pose Estimation = 2D Pose Estimation + Matching. CVPR, 2017

[3] Xingyi Zhou, Qixing Huang, Xiao Sun, Xiangyang Xue, Yichen Wei. Towards 3D Human Pose Estimation in the Wild: a Weakly-supervised Approach. ICCV 2017.
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020040118223062.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
*[4] Ju Yong Chang, Kyoung Mu Lee. 2D-3D Pose Consistency-based Conditional Random Fields for 3D Human Pose Estimation. 2017.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200401183921267.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[5] Semantic Graph Convolutional Networks for 3D Human Pose Regression. CVPR 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406161638705.JPG#pic_center)
[6] Generalizing Monocular 3D Human Pose Estimation in the Wild. 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406165342181.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[7] XNect: Real-time Multi-person 3D Human Pose Estimation with a Single RGB Camera. 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406172459298.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[8] xR-EgoPose: Egocentric 3D Human Pose from an HMD Camera. 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406173631503.JPG#pic_center)
[9] Multi-Person 3D Human Pose Estimation from Monocular Images. 3DV 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406181616521.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[10] Deep, robust and single shot 3D multi-person human pose estimation in complex images. 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406183124790.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
*[11] Xiaowei Zhou, Menglong Zhu, Spyridon Leonardos, Konstantinos G. Derpanis, Kostas Daniilidis. Sparseness Meets Deepness: 3D Human Pose Estimation from Monocular Video. CVPR, 2016

#### 借用其他显式的中间表示出3D Pose
[1] Francesc Moreno-Noguer. 3D Human Pose Estimation from a Single Image via Distance Matrix Regression. 2016

[2] Georgios Pavlakos, Xiaowei Zhou, Konstantinos G. Derpanis, Kostas Daniilidis. Coarse-to-Fine Volumetric Prediction for Single-Image 3D Human Pose. CVPR, 2017.（提出了3D heatmap）

*[3] Ehsan Jahangiri, Alan L. Yuille. Generating Multiple Diverse Hypotheses for Human 3D Pose Consistent with 2D Joint Detections. ICCV, 2017.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200401180215264.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
*[4] VNect: Real-time 3D Human Pose Estimation with a Single RGB Camera. SIGGRAPH 2017. 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200401184937968.JPG#pic_center)
*[5] Umar Iqbal, Andreas Doering, Hashim Yasin, Björn Krüger, Andreas Weber, and Juergen Gall. A Dual-Source Approach for 3D Human Pose Estimation from a Single Image. Extended version of CVPR-2016. 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200401190218249.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[6] Ordinal Depth Supervision for 3D Human Pose Estimation. CVPR 2018. 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200404213631103.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[7] DRPose3D: Depth Ranking in 3D Human Pose Estimation. IJCAI 2018.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200405103748617.JPG#pic_center)
[8] 3D Human Pose Estimation with 2D Marginal Heatmaps. WACV 2018. 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200405104956750.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[9] FBI-Pose: Towards Bridging the Gap between 2D Images and 3D Human Poses using Forward-or-Backward Information. 2018.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406092457903.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[10] 3D human pose estimation from depth maps using a deep combination of poses. 2018. (深度图出3D Pose)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406094324956.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[11] Occluded Joints Recovery in 3D Human Pose Estimation based on Distance Matrix. ICPR 2018.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406095525345.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[12] Synthetic Occlusion Augmentation with Volumetric Heatmaps for the 2018 ECCV PoseTrack Challenge on 3D Human Pose Estimation. ECCV 2018 Workshop.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406100513269.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[13] Adversarial 3D Human Pose Estimation via Multimodal Depth Supervision. 2018.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406101736450.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[14] OriNet: A Fully Convolutional Network for 3D Human Pose Estimation. BMVC.
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020040610405983.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[15] 3D Human Pose Machines with Self-supervised Learning.T-PAMI, 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406111726500.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[16] View Invariant 3D Human Pose Estimation. 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406112252623.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[17] Monocular 3D Human Pose Estimation by Generation and Ordinal Ranking. ICCV 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406160627255.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[18] In the Wild Human Pose Estimation UsingExplicit 2D Features and Intermediate 3D Representations. CVPR 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406161046365.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[19] Generating Multiple Hypotheses for 3D Human Pose Estimation
with Mixture Density Network. CVPR 2019
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406165629127.JPG#pic_center)
[20] Multi-task human analysis in still images: 2D/3D pose, depth map, and multi-part segmentation. 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406170538213.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[21] Geometric Pose Affordance: 3D Human Pose with Scene Constraints. 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406171146593.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[22] Patch-based 3D Human Pose Refinement. CVPR 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406171533792.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[23] Sim2real transfer learning for 3D human pose estimation: motion to the rescue. NIPS 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406173052345.JPG#pic_center)
[24] HEMlets Pose: Learning Part-Centric Heatmap Triplets for Accurate 3D Human Pose Estimation. ICCV2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406182518819.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[25]  Consensus-based Optimization for 3D Human Pose Estimation in Camera Coordinates. 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406184556372.JPG#pic_center)
[26] Learning 3D Human Shape and Pose from Dense Body Parts. 2020.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406191456352.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[27] Chained Representation Cycling: Learning to Estimate 3D Human Pose and Shape by Cycling Between Representations. AAAI 2020.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406192058461.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[28] Lightweight 3D Human Pose Estimation Network Training
Using Teacher-Student Learning. 2020.
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020040619240195.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[29] Metric-Scale Truncation-Robust Heatmaps for 3D Human Pose Estimation. 2020.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406203532482.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)

#### 处理Multi-view的3D Pose
[1] Learning Monocular 3D Human Pose Estimation from Multi-view Images. CVPR 2018.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200404183907901.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[2] Unsupervised Geometry-Aware Representation for 3D Human Pose Estimation. 2018.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200404191211113.JPG#pic_center)
[3] A generalizable approach for multi-view 3D human pose regression. 2018. 
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200404191505397.JPG#pic_center)
[4] Weakly-Supervised Discovery of Geometry-Aware Representation for 3D Human Pose Estimation. CVPR 2019 oral paper.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406114500674.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[5] Multiview-Consistent Semi-Supervised Learning for 3D Human Pose Estimation. 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406175656526.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[6] DeepFuse: An IMU-Aware Network for Real-Time 3D Human Pose Estimation from Multi-View Image.WACV 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406185122783.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[7] Cross-View Tracking for Multi-Human 3D Pose Estimation at over 100 FPS. CVPR 2020.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406211550212.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[8] Weakly-Supervised 3D Human Pose Learning via Multi-view Images in the Wild. CVPR 2020.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406213312949.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)

#### 视频序列的3D pose
[1] Agne Grinciunaite, Amogh Gudi, Emrah Tasli,, and Marten den Uyl. Human Pose Estimation in Space and Time using 3D CNN. ECCV 2016 Workshop

[2] 3D human pose estimation in video with temporal convolutions and semi-supervised training. CVPR 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406104532616.JPG#pic_center)
[3] 3D Human Pose Estimation from Deep Multi-View 2D Pose. ICPR 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406112554462.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[4] Trajectory Space Factorization for Deep Video-Based 3D Human Pose Estimation. BMVC 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406180534818.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[5] Cross View Fusion for 3D Human Pose Estimation. ICCV 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406180753250.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[6] Multi-task Deep Learning for Real-Time 3D Human Pose Estimation and Action Recognition. PAMI 2020.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406190537830.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[7] Anatomy-aware 3D Human Pose Estimation in Videos. 2020
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406202106992.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[8] PoseNet3D: Unsupervised 3D Human Shape and Pose Estimation. 2020.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406211106955.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[9] GAST-Net: Graph Attention Spatio-temporal Convolutional Networks for 3D Human Pose Estimation in Video. 2020.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406213914426.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)

### 3D Pose and Shape
[1] Federica Bogo,, Angjoo Kanazawa,Javier Romero, Michael J. Black. Keep it SMPL: Automatic Estimation of 3D Human Pose and Shape from a Single Image. ECCV, 2016.

[2] Learning to Estimate 3D Human Pose and Shape from a Single Color Image. CVPR 2018.

[3] SMPLR: Deep SMPL reverse for 3D human pose and shape recovery. 2018
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406104837186.JPG#pic_center)
[4] Skeleton Transformer Networks: 3D Human Pose and Skinned Mesh from Single RGB Image. ACCV 2018.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406105627973.JPG#pic_center)
[5] DenseBody: Directly Regressing Dense 3D Human Pose and Shape From a Single Color Image. 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406160042537.JPG#pic_center)
[6] Exploiting temporal context for 3D human pose estimation in the wild. CVPR 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406170819202.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[7] Temporally Coherent Full 3D Mesh Human Pose Recovery from Monocular Video. 2019.
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200406171832603.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
[8] Resolving 3D Human Pose Ambiguities with 3D Scene Constraints. ICCV 2019.（场景固定，即先将场景建模）
[9] Learning to Reconstruct 3D Human Pose and Shape via Model-fitting in the Loop. ICCV 2019
[10] Weakly Supervised 3D Human Pose and Shape Reconstruction with Normalizing Flows. 2020


