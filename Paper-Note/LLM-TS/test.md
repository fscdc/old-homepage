# TEST: Text Prototype Aligned Embedding to Activate LLM's Ability for Time Series

## 1. 研究背景/动机
在LLM+TS的背景下，存在两种主要方法：LLM-for-TS 设计，即训练一个大型模型并针对下游任务进行微调；TS-for-LLM，即将时间序列转换为模型友好的表示格式，使预训练的LLM可以处理时间序列。由于轻量级等限制，本研究依然聚焦于 TS-for-LLM 策略。

## 2. 创新点
本研究没有使用通道独立策略，保留了多变量时间序列（MTS）的信息。引入软提示（soft prompt）避免了微调所需的高昂训练成本。对齐嵌入方法也是一大亮点。

## 3. 主要方法
本文模型主要分为两步：构建编码器来嵌入TS和创建可以让LLM接收嵌入的TS的prompt。

### 第一步
![示意图](/pic/test/1.jpg)
首先使用经典的滑动窗口方法将TS tokenize，即分成长度不定的子序列，每个子序列是一个标记 s（anchor instance）。然后对每个标记 s，采用弱增强（jitter-and-scale strategy）和强增强（permutation-and-jitter strategy）生成正例，并选取与 s 本身无重叠的实例作为负例。构建神经网络作为编码器将 anchor instance 嵌入成一个 M 维的嵌入向量 e，这些 e 就是最初MTS的嵌入token list。

接下来是对比学习部分：
- **Instance-wise contrast**：保证目标anchor instance与其对应的正token instance尽可能相似，与负token instance差异尽可能大。使用了特定的对比损失函数，并采取了防止嵌入空间坍塌的策略。
- **Feature-wise contrast**：打破实例之间的独立性。在嵌入后，每个minibatch中会有一个由B个instance组成的特征矩阵B×M，聚类未知，将列视为特征的软标签，并对相似特征的组进行区分。
- **Text-prototype-aligned contrast learning**：将时序嵌入向量对齐到LLM的文本表示空间，设计了一个对比损失函数，约束向量的相似性和相似的实例在文本空间也有类似的表示。

### 第二步：Soft Prompt
这些soft prompt是针对下游具体任务的嵌入，通过LLM输出和ground truth之间的loss来学习。注意，这里的prompt不再是人类语义。


![整体架构图](/pic/test/structure.jpg)

## 4. 数据集
- 分类：UCR archive中的所有128种单变量时间序列数据集
- 预测：包括天气、交通、电力、ILI 和 ETT 等8个流行的实际应用基准数据集

## 5. 实验结果
时序分类和预测性能与常见的baseline相近。

## 6. 实验环境
20 NVIDIA Tesla V100-SXM2 GPU with CUDA 11.3.

## 7. 复现情况
本机环境差跑不起来，但是model看完了
