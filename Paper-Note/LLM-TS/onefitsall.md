# One Fits All: Power General Time Series Analysis by Pretrained LM

## 1. 研究背景/动机
略

## 2. 创新点
任务全面，方法虽然相对简单，但微调效果良好。

## 3. 主要方法
![方法概述图](/pic/onefitsall/structure.jpg)
本研究的方法简单直接：
- **Self-attention** 和 **FFN** 被冻结，即LLM的核心部分被冻结。只训练 **positional embedding**、**input embedding**、**线性输出层** 和 **Layer Norm层**。
- 其中 **positional embedding** 和 **layer norm** 需要针对不同的下游任务进行训练，这是很自然的过程。
- **Input embedding** 是必须进行的步骤，这里利用的技术是 **linear probing**（参数较少）。
- 进行简单的均值-方差归一化。
- **Patching**，即聚合相邻时间步来形成一个token，在同样的输入长度下，这样可以覆盖更大跨度的时间范围。

### Connecting Self-Attention with PCA
作者在文章中还证明了 **self-attention** 和 **PCA** 在作用上的相似性，具体证明省略。从实验来看，二者在功能上显示出一定的相似性，这强调了预训练好的 self-attention 对于建模各种模态数据的通用性。

## 4. 数据集
使用了多种数据集进行了广泛的任务测试，详见原文。

## 5. 实验结果
- 长期预测：预测长度更长
- 短期预测：预测长度较短
- 零样本预测：未进行微调
- 少样本预测：只用极少量的训练样本进行微调
- 分类
- 异常检测
- 插补

以上七项任务均进行了测试。

## 6. 实验环境
作者论文中详细列出了计算成本。

## 7. 复现
FINISH
