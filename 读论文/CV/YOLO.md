闭集检测中，主流的方法都是基于transformer和YOLO来做的。因为上周看的开放集检测论文YOLO-world是基于YOLO做的，所以这周我学了下YOLO。

# 目标检测的分类

## 0 two-stage方法

如R-CNN系算法（region-based CNN），其主要思路是先通过启发式方法（selective search）或者CNN网络（RPN)产生一系列稀疏的候选框，然后对这些候选框进行分类与回归，two-stage方法的优势是准确度高

## 1 one-stage方法

如Yolo和SSD，其主要思路是均匀地在图片的不同位置进行密集抽样，抽样时可以采用不同尺度和长宽比，然后利用CNN提取特征后直接进行分类与回归，整个过程只需要一步，所以其优势是速度快，但是均匀的密集采样的一个重要缺点是训练比较困难，这主要是因为正样本与负样本（背景）极其不均衡，导致模型准确度稍低

# YOLO系列

YOLO的发展过程，在v10的相关工作中已经介绍的很好了，如下。

YOLOv1、YOLOv2和YOLOv3确定了典型的检测架构，该架构由三部分组成，即骨干、颈部和头部[43,44,45]。YOLOv4 [2] 和 YOLOv5 [19] 引入了 CSPNet [57] 设计来取代 DarkNet [42]，并结合了数据增强策略、增强的 PAN 和更多种类的模型尺度等。 YOLOv6 [27] 分别提出了用于颈部和骨干的 BiC 和 SimCSPSPPF，具有锚点辅助训练和自蒸馏策略。YOLOv7 [56] 引入了用于丰富梯度流路的 E-ELAN，并探索了几种可训练的免费赠品袋方法。YOLOv8 [20] 提出了用于有效特征提取和融合的 C2f 构建块。Gold-YOLO [54]提供了先进的GD机制来增强多尺度特征融合能力。YOLOv9 [59] 建议 GELAN 改进架构，PGI 增强训练过程。

这周时间有限，我就学了下YOLOv1的原理，然后直接看v10（5月24号上传的arxiv，上周刚中稿CVPR）。

## v1基本原理

目标检测在双阶段中，需要利用匈牙利算法匹配锚框和边界框，而且需要nms去除冗余的预存框。

v1版本，由于在输出中可以直接预测某个类的概率，从而去除了匈牙利匹配的过程

![image-20240703212531670](C:\data\notebook\读论文\CV\YOLO.assets\image-20240703212531670.png)

![image-20240703212549076](C:\data\notebook\读论文\CV\YOLO.assets\image-20240703212549076.png)

![image-20240703212606009](C:\data\notebook\读论文\CV\YOLO.assets\image-20240703212606009.png)

![image-20240703212710109](C:\data\notebook\读论文\CV\YOLO.assets\image-20240703212710109.png)
