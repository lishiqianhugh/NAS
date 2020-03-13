# Learning Transferable Architectures for Scalable Image Recognition(NASnet)
## 方法
* 强化学习Policy Gradient--更新控制器
* `梯度下降--更新子网络的参数`
## 所用数据集
* cifar-10
* ImageNet
* COCO
## 核心工作
* 用RNN控制器（Proximal Policy Optimization方法更新）采样子网络，搜索卷积神经网络的cell(Normal, Reduction)，一个cell有B（论文中为5）个blocks
* 先在cifar-10上搜索架构，再迁移到ImageNet上训练
* 将从ImageNet上学习到的特征和Faster-RCNN结合可以用在COCO上做目标检测
# ENAS
## 方法
* 随机梯度下降（SGD）--更新w
* 强化学习--更新控制器
## 所用数据集
* Penn Treebank
* cifar-10
## 核心工作
* 保留已训练的参数，实现权重共享
* 设计RNN cell
* 设计CNN 网络架构
* 设计CNN cell
## 采样子网络的方法
* 控制器采样一系列的自网络
* 每个子网络用一个minibatch的validation datase测试
* 选出最好的子网络，从头开始训练
# DARTS
## 方法
梯度下降
## 所用数据集
* cifar-10
* ImageNet
* PTB
* WikiText-2
## 核心工作
* 运用CNN和RNN都适用的搜索空间（与NASnet和ENAS相同）
* 发明可微的搜索空间，利用混合操作训练架构（所有可选操作用softmax赋权得到混合操作）
![混合操作公式]（https://github.com/lishiqianhugh/NAS/blob/master/NAS%E6%88%AA%E5%9B%BE/DARTS%E6%B7%B7%E5%90%88%E6%93%8D%E4%BD%9C%E5%85%AC%E5%BC%8F.png）
* 用梯度发更新架构参数α和各个操作内部的参数w
