# Time-LLM: Time Series Forecasting by Reprogramming Large Language Models

## 1. 研究背景/动机
LLM 在 NLP/CV 领域的表现非常优异，具有很强的通用性，在 zero-shot 和 few-shot 任务上也展现出了良好的性能。然而，在时序预测(ST)领域，大多数模型都具有较强的针对性，缺乏通用性。研究显示，LLM 在模式识别和复杂 token 序列理解方面具有良好的鲁棒性。

## 2. 创新点
本研究在时序预测领域首次尝试引入 LLM，采用的是一种轻量级方法，通过添加轻量级调节层，无需修改原有 LLM 参数，避免了昂贵的训练成本。这些调节层能够在少量样本上进行微调，适应当前任务。其中，时序特征的 reprogramming 是一个创新点，具有新颖性和可解释性。

## 3. 主要方法
![架构图](/pic/time-llm/structure.jpg)
架构中的 LLM 参数保持不变（Frozen），在其前后各添加了一个可训练的层（Patch Reprogramming 和 Output Projection）。这里采用通道独立策略。

### Input Embedding
如上图序号 1 和序号 2 所示，时间序列先通过 RevIN 的归一化操作，然后分 patch 进行 embedding。具体数据格式可见：
![数据格式](/pic/time-llm/data.jpg)

### Patch Reprogramming
数据通过前面的处理后仍为时序数据，因此需要转换为文本格式供 LLM 使用。这里采用了 cross-attention 来对齐不同模态，通过一个 linear 层从 V 个词中抽取 V' 个 prototypes，减少了处理的复杂性。具体架构如下图所示：
![架构细节](/pic/time-llm/reprogram.jpg)

### Prompt-as-Prefix
将时间序列数据集的一些先验信息，以自然语言的形式作为前缀 prompt，并与对齐后的时序特征拼接后输入到 LLM。这可以参照总体架构图的序号 4。一个可能的 prompt 示例：
![Prompt 示例](/pic/time-llm/prompt.jpg)

### Output Projection
丢弃前缀部分，将剩余部分扁平化处理，然后通过线性投影映射到最终结果的格式上。

## 4. 数据集
- 长期：ETTh1, ETTh2, ETTm1, ETTm2, Weather, Electricity (ECL), Traffic, and ILI
- 短期：M4 benchmark

## 5. 实验结果
- 长期、短期
- Few-shot on 10%/5%
- Zero-shot

整个效果都不错，具体数据可见原论文的Exp部分，这里省略。
## 6. 复现情况
FINISH