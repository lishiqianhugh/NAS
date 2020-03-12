# Learning Transferable Architectures for Scalable Image Recognition(NASnet)
[论文](file:///D:/Mine/科研/NAS/01_NAS/NASNet.pdf)
## 方法
强化学习
## 所做工作
* 用RNN控制器搜索卷积神经网络的cell(Normal, Reduction)
* 先在cifar-10上搜索架构，再迁移到ImageNet上训练
* 将从ImageNet上学习到的特征和Faster-RCNN结合可以用在COCO上做目标检测

