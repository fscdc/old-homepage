# LLM4TS: Two-Stage Fine-Tuning for Time-Series Forecasting with Pre-Trained LLMs

这里我主要说明一下**Method**：

![整体架构](/pic/llm4ts/structure.jpg)

## Time-Series Alignment
对时间序列数据进行自回归处理，分析输入和输出之间的关系。


### 1. Instance Normalization
针对整个数据实例进行归一化处理，是数据预处理的一部分。

### 2. Time-Series Tokenization
通过通道独立策略加上patching处理，这是一种非常典型的数据处理方法。
![时间序列Tokenization示意图](/pic/llm4ts/patch.jpg)

### 3. Three Encodings for Patched Time-Series Data

- **Token嵌入层**：使用一维卷积基层作为token嵌入层。
- **位置层**：使用可训练的查找表标识每个patch的位置。
- **时间嵌入层**：实现双级聚合。
  - 首先，为每个时间属性（如秒、分钟等）使用一个可训练的查找表，将每个属性映射到一个高维空间中，然后将这些映射求和，形成一个统一的时间嵌入表示。
  - 每个patch可能包含多个时间戳，采用池化方法来提取最终的时间嵌入，通常使用片段中的第一个时间戳作为整个片段的代表。

### 4. Partial Freezing and Tunable Layers
冻结模型的某些部分，同时保留部分层为可训练状态，以优化模型性能。
- **Layer Normalization Tuning**
- **Low-Rank Adaptation (LoRA)**



## Forecasting Fine-Tuning Strategy
采用initial linear probing followed by full fine-tuning (LP-FT)策略，这一策略的优越性在于其双阶段方法：
- 首先优化输出层，以最小化微调中的调整量（保留特征提取器在OOD（Out-Of-Distribution）场景中的有效性）。
- 然后进行全面的微调，以使模型适应特定任务（提高ID（In-Distribution）精度）。
