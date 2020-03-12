# Learning Transferable Architectures for Scalable Image Recognition(NASnet)
## 方法
强化学习 Policy Gradient
## 所用数据集
* cifar-10
* ImageNet
* COCO
## 核心工作
* 用RNN控制器采样子网络，搜索卷积神经网络的cell(Normal, Reduction)，一个cell有B（论文中为5）个blocks
* 先在cifar-10上搜索架构，再迁移到ImageNet上训练
* 将从ImageNet上学习到的特征和Faster-RCNN结合可以用在COCO上做目标检测
# DARTS
## 方法
梯度下降
## 所用数据集
* cifar-10
* ImageNet
* ·PTB·
## 核心工作
* 运用CNN和RNN都适用的搜索空间（与NASnet和ENAS相同）
* 发明可微的搜索空间，利用混合操作训练架构（所有可选操作用softmax赋权得到混合操作）
* 用梯度发更新架构参数α和各个操作内部的参数w
