# COCO pose数据集标注文件详解
**注意：使用python3来描述数据集中的内容**
### 导入python
使用val2014来举例：
```python
from pycocotools.coco import COCO
import numpy as np
import skimage.io as io
import matplotlib.pyplot as plt
import pylab
import pdb
import json

pylab.rcParams['figure.figsize'] = (8.0, 10.0)

dataDir='/data3/MSCOCO'
dataType='val2014'
annFile='{}/annotations/person_keypoints_{}.json'.format(dataDir,dataType)

with open(annFile,'r') as f:
	coco_dict = json.load(f)
pdb.set_trace()
```
之后利用pdb来探索数据集中的内容，结果如下：
coco_dict为dict类型，其keys如下：
```python
['info', 
'images',
'licenses', 
'annotations', 
'categories']
 ```
 下面来依次将各个键值对取出查看其内容：
1.  `info`数据类型为dict类型，具体内容为：
 ```python
 {'description': 'This is stable 1.0 version of the 2014 MS COCO dataset.', 
'url': 'http://mscoco.org',
'version': '1.0', 
'year': 2014,
'contributor': 'Microsoft COCO group', 
'date_created': '2015-01-27 09:11:52.357475'}
 ```
 2. `images`数据类型为list，list中的每一项为dict类型。这里只拿出其中一项来查看，其他类似：
 ```python
{'license': 3,  #许可证编号
'file_name': 'COCO_val2014_000000391895.jpg', 
'coco_url': 'http://mscoco.org/images/391895', 
'height': 360, 
'width': 640, 
'date_captured': '2013-11-14 11:18:45', 
'flickr_url': 'http://farm9.staticflickr.com/8186/8119368305_4e622c8349_z.jpg', #flickr外部链接
'id': 391895}
 ```
 注意：images的id字段的值与image一一对应。
 
 3. `licenses`为许可证，为list类型长度为8，每一项都是dict类型。同样这里也只拿出一项来，其他类似：
```python
{'url': 'http://creativecommons.org/licenses/by-nc-sa/2.0/', 
'id': 1, #从1到 8
'name': 'Attribution-NonCommercial-ShareAlike License'}
```
4. `annotations`类型为list，每一项为dict，单项的内容为：
```python
{'segmentation': [[267.03, 243.78, 314.59, 154.05, 357.84, 136.76, 374.05, 104.32, 410.81, 110.81, 429.19, 131.35, 420.54, 165.95, 451.89, 209.19, 464.86, 240.54, 480, 253.51, 484.32, 263.24, 496.22, 271.89, 484.32, 278.38, 438.92, 257.84, 401.08, 216.76, 370.81, 247.03, 414.05, 277.3, 433.51, 304.32, 443.24, 323.78, 400, 362.7, 376.22, 375.68, 400, 418.92, 394.59, 424.32, 337.3, 382.16, 337.3, 371.35, 388.11, 327.03, 341.62, 301.08, 311.35, 276.22, 304.86, 263.24, 294.05, 249.19]], 
'num_keypoints': 8, 
'area': 28292.08625, 
'iscrowd': 0, 
'keypoints': [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 325, 160, 2, 398, 177, 2, 0, 0, 0, 437, 238, 2, 0, 0, 0, 477, 270, 2, 287, 255, 1, 339, 267, 2, 0, 0, 0, 423, 314, 2, 0, 0, 0, 355, 367, 2], 
'image_id': 537548, 
'bbox': [267.03, 104.32, 229.19, 320], 
'category_id': 1, 
'id': 183020}
```
注意：annotations的id字段与anno一一对应，而image_id字段与image一一对应。一个image可能对应多个anno。

5. `categories`为list，长度为1，内容如下：
```python
[{'supercategory': 'person', 
'skeleton': [[16, 14], [14, 12], [17, 15], [15, 13], [12, 13], [6, 12], [7, 13], [6, 7], [6, 8], [7, 9], [8, 10], [9, 11], [2, 3], [1, 2], [1, 3], [2, 4], [3, 5], [4, 6], [5, 7]], 
'id': 1, 
'keypoints': ['nose', 'left_eye', 'right_eye', 'left_ear', 'right_ear', 'left_shoulder', 'right_shoulder', 'left_elbow', 'right_elbow', 'left_wrist', 'right_wrist', 'left_hip', 'right_hip', 'left_knee', 'right_knee', 'left_ankle', 'right_ankle'], 
'name': 'person'}]
```
注意：由于人体姿态估计研究对象只有人，所以categories list的长度为1 。在segmentation中长度为种类数80 。
