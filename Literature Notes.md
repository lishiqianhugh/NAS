# Learning Transferable Architectures for Scalable Image Recognition(NASnet)
## 方法
强化学习 Policy Gradient
## 核心工作
* 用RNN控制器采样子网络，搜索卷积神经网络的cell(Normal, Reduction)，一个cell有B（论文中为5）个blocks
* 先在cifar-10上搜索架构，再迁移到ImageNet上训练
* 将从ImageNet上学习到的特征和Faster-RCNN结合可以用在COCO上做目标检测

