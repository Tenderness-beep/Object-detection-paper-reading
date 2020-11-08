# 01 YOLO Series
## 基于神经网络的目标检测
* Two-stage: 第一阶段网络先生成proposal, 第二阶段进行分类和坐标回归
* One-stage: 只是用一级网络完成分类和回归任务
速度快，受欢迎
## YOLO v1
### grid
网格
只要求物体的中心在某个grid内
### Bounding box
* 每次都预测出B个Bounding Box，包含5个量，分别是物体的中心位置，长宽和置信度。
* 框还要预测物体的类别

### Bounding box的细节
输出位置是正实数，大小可能很大可能很小。模型可能在不同大小的物体上有不同的泛化能力。
x和y除掉grid的宽度和高度，w和h除以整张照片的宽度和高度。

### Condifence的计算
$$C = Pr(Obj)*IOU_{truth}^{pred}$$

### Loss的计算
![](https://i.imgur.com/bMP9ACE.jpg)
* w和h开根号：在一定程度上缓解小目标对于预测w和h的敏感度
* $\lambda_{coord}和\lambda_{noord}$：负责预测object的bounding box的数量会远远大于不负责预测object的bounding box。设置不同的lambda可以减少类别不平衡带来的误差。
### 缺点
* 没个grid只能识别一种物体
* 准确度有限
