# FLOPs

floating point operations的缩写（s表复数），意指浮点运算数，理解为计算量。可以用来衡量算法/模型的复杂度。

Image大小为 5x5

卷积核大小为 3x3

那么一次3x3的卷积（求右图矩阵一个元素的值）所需运算量：(3x3)个乘法+(3x3-1)个加法 = 17

要得到右图convolved feature （3x3的大小）：17x9 = 153

*可以调用pytorch中的代码计算*

# mAP

mean Average Precision  跑N次的平均精度

# AR

Average Recall