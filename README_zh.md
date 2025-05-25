# EduBench:评估大语言模型在多样化教育场景中表现的综合基准数据集
<p align="center">
  📄 <a href="https://arxiv.org/pdf/2505.16160" target="_blank">Paper</a> &nbsp; | &nbsp;
  🤗 <a href="" target="_blank">Model</a> &nbsp;
  🎰 <a href="" target="_blank">Datasets</a> &nbsp;| &nbsp;
  ⚖️ <a href="" target="_blank">Apache-2.0 License</a>
</p>

# 目录
- [概述](#概述)
- [实验结果](#实验结果)
- [语言模型与数据集](#语言模型与数据集)
- [对比](#对比)
- [代码](#代码)

# 概述
- 首次提出EduBench，一个为教育场景量身定制的多样化基准数据集，包含9大教育场景和超过4000个不同的教育情景。
- 设计多维度的评估指标，针对不同的教育场景设计对应的评估指标，涵盖教师端和学生端以及12个关键维度，包括场景适应性、事实与推理准确性等。
- 通过知识蒸馏，使小模型(Qwen2.5-7B-Instruct)在仅有少量数据训练的情况下，达到与最先进大型模型(DeepSeek V3、Qwen Max)相当的性能。

# 场景与评估维度
<img src="images/distribution-radar.pdf" alt="Distribution Radar" width="800"/>
