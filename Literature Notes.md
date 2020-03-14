#  *Learning Transferable Architectures for Scalable Image Recognition(NASnet)(2018)*
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

# *SMASH One-shot(HyperNetworks)(2017)*

## 方法

* 梯度下降

## 所用数据集

* cifar-10
* cifar-100
* STL-10
* ModelNet10
* ImageNet32×32

## 核心工作

* 设计HyperNet用来生成W
* 一次训练，训练所有参数；每一个minibatch训练一个采样的子网络
* 结束训练后对所有随机产生的子网络评估测试集上的误差，选出最好的重新训练
* 在训练过程中使用Dropout来使得模型去掉大量分支后（评估时）仍具有鲁棒性

![SMASH_Algorithm](https://github.com/lishiqianhugh/NAS/blob/master/Screenshots/NASP_Algorithm.png)

## 合理性解释

 one-shot模型可以自动学习到网络中哪些操作最有用，并会逐渐依赖这些操作。去掉不重要的操作对模型的预测准确率有很小的影响；但去掉最重要的操作会对模型的预测产生非常大的影响。

# *ENAS*

## 方法
* 随机梯度下降（SGD）--更新w
* 强化学习--更新控制器
## 所用数据集
* Penn Treebank
* cifar-10
## 核心工作
* 保留已训练的参数，实现权重共享
* 设计RNN cell （每个结点有一个输入，最后将游离结点cat）
* 设计CNN 网络架构 （每个结点可以从前面所有结点选任意个结点的输出作为输入）
* 设计CNN cell （每个结点有两个输入，最后将游离结点cat）
## 采样子网络的方法
* 控制器采样一系列的自网络
* 每个子网络用一个minibatch的validation datase测试
* 选出最好的子网络，从头开始训练
# *DARTS*
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

  ![混合操作公式](https://github.com/lishiqianhugh/NAS/blob/master/Screenshots/DARTS_mixed_formula.png)

* 用梯度发更新架构参数α和各个操作内部的参数w

# *NASP*

## 方法

近端学习

## 所用数据集

* cifar-10
* ImageNet
* PTB
* WikiText-2

## 核心工作

* 对比DARTS和NASP
* 在DARTS连续训练架构的基础上，利用近端的方法，离散出每对结点当前最好的一个操作单独更新w。从而减少了训练复杂度
* 先在cifar-10和PTB上搜索架构并训练，并分别迁移到ImageNet和WikiText-2上

![NASP_Algorithm](https://github.com/lishiqianhugh/NAS/blob/master/Screenshots/NASP_Algorithm.png)

# *HM-NAS*

## 方法

与DARTS类似，只不过多加了一级架构可训练的参数，并加入了mask操作

## 所用数据集

* cifar-10
* ImageNet

## 核心工作

* 在DARTS的基础上发明了多级架构编码机制，即在cell中除了每条边上的各个操作有权重参数，一个cell里的每条边也有权重参数，同样用softmax表示。这样使得搜索空间更加灵活，更有可能找到最优的子架构
* 发明了分级mask机制，对{α，β，w}分别设计mask，`然后训练mask`，从而在已训练好的supernet上通过剪枝找到最好的子网络
* 不用重新从头训练（retrain from scratch），而是进行fine-tuning

![HM-NAS_Algorithm](https://github.com/lishiqianhugh/NAS/blob/master/Screenshots/HM-NAS_Algorithm.png)

## 思考

将搜索本身看作一个深度神经网络进行训练，得到架构最优参数

# *Auto-FPN*

## 所用数据集

* Pascal VOC
* COCO
* BDD
* VisualGenome
* ADE

## 核心工作

目前主要的NAS目标检测架构是将图像分类的架构迁移得来的，该文提出了一种直接搜索目标检测架构的方法