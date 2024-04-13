# A Comprehensive Overview of Backdoor Attacks in Large Language Models within Communication Networks

## Problem Description
Backdoor attacks in LLMs are classified into several types based on their trigger mechanisms:
- **Input-triggered**
- **Prompt-triggered**
- **Instruction-triggered** (maybe)
- **Demonstration-triggered**

The evaluation metrics used are ASR (Attack Success Rate) and BA (Benign Accuracy), with a high ASR indicating a successful attack, while maintaining a high BA to minimize the impact on benign functionality.


### Input-trigger
#### Layer-weight poisoning:
- **Li L et al.**, "Backdoor attacks on pre-trained models by layerwise weight poisoning," 2021. [\[2\]](https://arxiv.org/pdf/2108.13888)
- **Yang W et al.**, "Be careful about poisoned word embeddings: Exploring the vulnerability of the embedding layers in NLP models," 2021. [\[3\]](https://arxiv.org/pdf/2103.15543)

#### Stealthy and natural backdoor attack triggers:
- **Li S et al.**, "Hidden backdoors in human-centric language models," ACM SIGSAC 2021. [\[4\]](LinkToPaper4)
- **Zhang X et al.**, "Trojaning language models for fun and profit," EuroS&P 2021. [\[5\]](LinkToPaper5)
- **Pan X et al.**, "Hidden trigger backdoor attack on NLP models via linguistic style manipulation," USENIX Security 2022. [\[6\]](LinkToPaper6)
- **Lyu W et al.**, "Backdoor Attacks Against Transformers with Attention Enhancement," ICLR 2023 Workshop. [\[8\]](LinkToPaper8)
- **Zhou X et al.**, "Backdoor Attacks with Input-unique Triggers in NLP," 2023. [\[9\]](https://arxiv.org/pdf/2303.14325)
- **Chen L et al.**, "Backdoor Learning on Sequence to Sequence Models," 2023. [\[10\]](https://arxiv.org/pdf/2305.02424)

### Prompt-trigger
- The manipulation of prompts can either inject a trigger or compromise the prompt through malicious user inputs:
  - **Cai X et al.**, "Badprompt: Backdoor attacks on continuous prompts," NeurIPS 2022. [\[11\]](LinkToPaper11)
  - **Perez F et al.**, "Ignore previous prompt: Attack techniques for language models," 2022. [\[12\]](https://arxiv.org/pdf/2211.09527)
  - **Zhao S et al.**, "Prompt as Triggers for Backdoor Attack: Examining the Vulnerability in Language Models," 2023. [\[13\]](https://arxiv.org/pdf/2305.01219)

### Instruction-trigger
- **Xu J et al.**, "Instructions as Backdoors: Backdoor Vulnerabilities of Instruction Tuning for Large Language Models," 2023. [\[14\]](https://arxiv.org/pdf/2305.14710)

### Demonstration-triggered
- **Wang J et al.**, "Adversarial Demonstration Attacks on Large Language Models," 2023. [\[15\]](https://arxiv.org/pdf/2305.14950)

