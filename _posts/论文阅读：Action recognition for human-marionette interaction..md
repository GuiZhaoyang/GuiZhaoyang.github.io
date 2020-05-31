该论文在ACM MM 2012上获最佳论文提名。
# 摘要
作者提出了基于人体动作识别方法的人类-木偶交互系统，并以此开发了**交互艺术木偶戏**和**模仿木偶游戏**这两个应用。
**交互艺术木偶戏**：木偶模仿人类的动作，然后人再模仿木偶的动作。该木偶的制作涉及到了动作识别与木偶的控制系统，其中前一个方面是该文章重点。作者将开发出的智能木偶称为**i-marionette**。作者在该部分还叙述了木偶戏的艺术价值，比如反映了现实世界与虚拟世界的关联啥的（反正没有艺术细胞的我是没看懂）。因为之前的木偶戏都是人来手动控制木偶，所以这个工作是一个突破性的工作。
**模仿木偶游戏**：智能木偶**i-marionette**做一个动作，之后人来模仿木偶的动作。完成后动作识别系统会给出一个分值，代表刚才的人模仿木偶的相似程度。
## 1 引言
经典木偶戏：木偶完全由人工控制，人扮演控制者，木偶只能扮演被控者。
**交互艺术木偶戏**：木偶通过动作识别算法自动模仿人的动作，人也会模仿木偶的动作，便产生了机器与人互相影响的的艺术。作者原文说的是：人类创造技术，技术创造木偶，木偶再影响人类。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417103354940.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
**模仿木偶游戏**：同样依托于人体动作识别算法。最后系统给模仿者一个打分，分数越高代表模仿者模仿的越像。作者另外提到：人类创造了游戏，人类玩游戏随后游戏影响人类。最终，游戏控制人类（无法理解，不敢恭维）。
**识别算法**：提出了Action Trait Code (ATC)算法来实现人体动作分类。该方法包含Microsoft Kinect 传感器 并且通过Kinect SDK获得人体3D关节点。ATC通过从每个身体部位的平均速率推导出的一系列特定的速率来代表一个特定的动作。之后基于ATC的分类结果，应用一个有效的图模型学习和识别人体动作。
为了测试该算法的速度，作者在自己收集了一个数据集，该数据集由以Chinese Liyuan dance为主题的6个视频构成。测试结果表明作者的算法达到了实时性的程度。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417105422637.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
# 2 相关工作
木偶系统领域：
Murphey提出了一种运动描述语言(MDLp) 来encode木偶的动作；Sillam and Luciani创造了一种由钢琴的琴键来控制木偶动作的一套物理模型。
关于面向舞蹈的电子自动木偶领域：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417110037828.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
如图3所示这两种"模仿人"的机器人其实是通过预先设定的实现固定动作的程序来实现的。
人体动作识别和分类算法领域：
之前的一些算法实现了从视频或者图像识别人体动作，但是只能识别横向运动；Sung提出了一种使用3D骨架数据的分层最大熵马尔可夫模型（MEMM）以在非结构化环境中对非结构化人类活动进行人类检测和识别；Raptis提出了一种对舞蹈姿态进行实时分类的系统，由设计好的骨骼表示，级联分类器和一个基于动态时间扭曲的距离度量构成；Jenkins 提出了一种基于机器视觉进行姿态分类和动作识别的方法；Theodoridis在机器人系统中实现了识别攻击性动作的功能。
# 3 人体动作识别
作者将人体动作理解分为两个方面：一是通过概率模型来实现经典的动作识别任务；二是基于量化人体运动来实现动作分类任务。
## 3.1 动作识别Overview
整个流程包括三个方面：预处理，动作分类和动作识别。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417112810765.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
预处理：通过Kinect SDK将输入的视频序列转化为人体3D关节点序列。
动作分类：通过ATC[1]来实现人体动作分类。ATC通过从每个身体部位的平均速率推导出的一系列特定的速率来代表一个特定的动作。
动作识别：基于ATC的分类结果应用图模型来学习并识别人体动作。
## 3.2 Action Trait Code（ATC）
首先说明一下图4中的ATE（Action Trait Element），ATE使用预处理生成的人体3D关节序列中对应关节点的距离度量来表示一个特定关节的平均速率。（其公式说明如下，博主比较懒就不打公式了）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417115758978.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
在训练阶段，因为训练集上有多个动作序列。每个动作序列的每个关节点会产生一个表示关节平均速率的实数。所以在整个训练集上，某一个关节点会产生一系列平均速率。作者对这些平均速率执行k-means聚类算法，并规定在每个cluster的所有平均速率采用相同的编码（图5）。然后在测试阶段，每个生成的平均速率通过值比对就可以快速的用1~k编码。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417121219329.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
## 3.3 ATC encoding
假设有$N$个关节点，所以测试时每次输入的图像序列经过表示为ATE再经过聚类后得到一个维度为$N$的特征向量。假设聚类数目为$k$，则特征向量空间元素的总个数为$k^N$，也就是说这种方法最多表示$k^N$种不同的动作。
为了防止过拟合，在训练时会将得到的特征向量依据$L_2$范数再进行聚类并给定每个簇一个大概的动作类别标签，称为大类。
## 3.4 基于ATC的动作分类
根据上面的步骤，在测试时，输入图像序列转为3D joint序列。再通过ATC编码为特征向量，最后先根据于每个簇的距离度量分到大类中，之后再通过预先定义好的表查表来进一步确定类别标签。
## 3.5 基于ATC的图模型
论文[2][3]中提出的动作图通过一系列显著的姿态来表示一个动态的人体动作。这一系列显著的姿态在所有的动作表示中共享。图6所示为作者提出的改良的图模型。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417173534380.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
## 3.6 在Chinese Liyuan Basic Steps上的测试结果
Chinese Liyuan Basic Steps是在中国唐代皇家礼仪上跳的一种舞蹈。作者使用了六个不同类型的舞蹈种类的视频来测试提出的算法。每一种类型的舞蹈都包含了1~3个基本舞蹈舞步，每个基本舞蹈舞步又由一系列的复杂的动作组成。表1展示了这六种舞蹈的类型。作者的算法在这上面达到了100%的精确度。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417175329869.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
表二展示了对于每种舞蹈类型的计算时间。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020041718434894.JPG#pic_center)
作者的方法精确度达到100%的原因是因为这六个舞蹈虽然动作复杂但是可区分度非常高。作者将该舞蹈视频放在网页：
[http://www.csie.ntu.edu.tw/~d97944010/research/mm2012/](http://www.csie.ntu.edu.tw/~d97944010/research/mm2012/)
在数据集street dance database上该方法精度达到了97%且达到了实时的性能。
[street dance database](http://www.csie.ntu.edu.tw/~d97944010/research/icpr2012/)
# 4 I-MARIONETTE
## 4.1 i-Marionette
作者制造的i-marionette具有类人的外形（图7a），并有一张女性的脸（图7b）。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417191226285.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
该智能人偶的整个身体由50块身体部分组成。作者以商业人体模型作为基础，并且用将每个身体部位用钩索连接起来，铰接位置如图8所示。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417193421703.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
另外，由于每个人体部位是中空的。作者使用支架来支持中空的身体部位，如图9所示。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417193951105.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
为了使木偶能够重现人体动作，作者使用Kinect传感器收集了大量的人体运动数据。这些3D人体运动数据使得人偶能做出人的各种动作。
## 4.2 运行阶段与控制设备
图10展示了控制系统控制木偶的过程。在这个阶段，场景中会放置3个Kinect传感器来感应人体的动作。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417202137692.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
在图11所示的控制系统中，作者使用一系列支架来支撑29个电机和i-marionette的重量。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417222523937.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
作者将人体的运动分解为全局运动和局部运动。全局运动指的是整个身体的旋转和平移；局部运动指的是每个肢体关节点的角度变化。所以控制系统的电机设备也分为这两个层面（图12）。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417222905695.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
第一层控制全局运动，第二层控制局部运动。为了能与多台电机进行命令传输，所有电机通过RS485总线相连。电机控制装置的布局见图13。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417223425753.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
# 5 交互艺术木偶戏
传统的木偶戏由人单方面操控木偶（图14a）。在这种情况下人扮演着支配者的角色，木偶扮演被控对象。而人在尝试着熟练操控木偶的情况下也不自觉的被木偶影响，进而人也变成了被操控者（图14b）。（博主个人认为也就是人制造工具，人在使用工具的过程中被工具影响）。而作者对这种现象很感兴趣并且想进一步探究如果木偶是全自动的情况下会发生什么。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417224637849.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
作者提出的木偶戏中人类代表着现实世界的科学技术（图15a），木偶代表虚拟世界文化（图15b）。在木偶戏中，木偶能实时地模仿人体的动作。在开始时，木偶从代表传统文化的虚拟世界来到代表现代科技的真实世界，在图16中背景音乐是以木偶为代表的传统歌剧。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417225654583.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417225720852.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
在图17a中，人类走向木偶并向木偶施加咒语。在图17b中，木偶模仿人类。图18中，木偶摆脱人类控制并且人类开始模仿木偶。该木偶戏说明：人类创造技术，技术控制木偶，木偶影响人类。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417230521772.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417230535181.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
图19展示了在木偶戏最后人类将木偶送回虚拟世界。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020041723063299.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
# 6 模仿木偶游戏
该游戏是人来模仿木偶的游戏（图20）。在这个游戏中，木偶会跳一个复杂的舞蹈，人类要实时地模仿木偶的动作。图21展现了该游戏的人机接口。
![在这里插入图片描述](https://img-blog.csdnimg.cn/202004172310212.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200417231041667.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JfbGFjaw==,size_16,color_FFFFFF,t_70#pic_center)
图22展示了最后的打分窗口。该游戏并不单单是娱乐目的，更重要的是使人类体验被木偶影响的感觉。人在该游戏中得分越高说明人被木偶影响的越大。最终的结果是人类创造游戏，人类玩游戏，游戏影响人类。最终，人类被游戏操控了。
# 7 结论
本篇论文实现了一个基于人体动作识别算法的人类与木偶的交互系统。并以此开发了两个应用：交互艺术木偶戏和模拟木偶游戏。并用很长的篇幅探讨了人类与木偶的关系。为了解决人体动作识别问题，作者提出了用ATC实现动作分类和用一个有效的图模型来进行动作学习和识别。
[1] Shih-Yao Lin, Chuen-Kai Shie, Shen-Chi Chen, Ming-Sui
Lee, and Yi-Ping Hung, “Human Action Recognition Using
Action Trait Code,” In ICPR, 2012
[2] W. Li, Z. Zhang, and Z. Liu. Expandable data-driven
graphical modeling of human actions based on salient
postures. In IEEE Trans. on Circuits and Systems for Video
Technology, 18(11):1499–1510, 2008
[3] W. Li, Z. Zhang, and Z. Liu. Action Recognition Based on
A Bag of 3D Points, In IEEE International Workshop on
CVPR for Human Communicative Behavior Analysis, 2010.
