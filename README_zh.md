# EduBench:评估大语言模型在多样化教育场景中表现的综合基准数据集
<p align="center">
  📄 <a href="https://arxiv.org/pdf/2505.16160" target="_blank">Paper</a> &nbsp; | &nbsp;
  🤗 <a href="" target="_blank">Model</a> &nbsp;
  🎰 <a href="" target="_blank">Datasets</a> &nbsp;| &nbsp;
  ⚖️ <a href="" target="_blank">MIT License</a>
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

总体框架如下:
<div align="center">
  <img src="images/framework.jpg" alt="Distribution Radar" width="1200"/>
</div>
左侧部分展示了我们的数据整理流程；中间部分展示了我们的三个主要评估原则，以及我们对大语言模型与人类评判一致性问题的探究；右侧部分展示了我们的数据如何提升小型模型的性能。

# 场景与评估维度
<div align="center">
  <img src="images/distribution-radar.jpg" alt="Distribution Radar" width="1200"/>
</div>
左侧部分展示了我们的9个教育场景，沿着展示了它们的多维教育背景和相应的指标。右侧部分展示了EduBench上的人工评估结果。

# 实验结果
## 评估结果
<div align="center">
  <img src="images/eval_domain.png" alt="eval_domain" width="800"/>
  <br>
  <strong>表1：展示了不同评估模型评估的场景级平均得分。</strong>
</div>

<div align="center">
  <img src="images/eval_matric.png" alt="eval_matric" width="800"/>
  <br>
  <strong>表2：展示了不同评价模型在不同指标下评价的指标级平均得分。</strong>
</div>

模型评估结果
DeepSeek R1 在不同指标中展现出最佳的整体表现，而 Qwen2.5-7B-Instruct 在表2 中表现最差。此外，DeepSeek R1 在“高阶思维与技能发展”（Higher-Order Thinking & Skill Development）方面表现最优，而 Qwen2.5-7B-Instruct 在“错误识别与纠正精度”（Error Identification & Correction Precision）方面表现最不理想，这两款模型与其他模型之间存在明显差距。在具体场景中，DeepSeek R1 仍然是表现最好的模型，而在如“情感支持”（Emotional Support）和“个性化内容生成”（Personalized Content Creation）等场景中，Qwen2.5-7B-Instruct 的表现优于 Qwen2.5-14B-Instruct，如表中所示。

人工评估结果
在表2中，DeepSeek R1 和 Qwen2.5-7B-Instruct 依然分别展现出最佳和最差的表现，这一结果与基于模型的评估结果一致。与模型评估不同的是，在“推理过程严谨性”（Reasoning Process Rigor）这一指标上，人工标注者对所有五款模型的表现满意度明显下降。其中，Qwen2.5-7B-Instruct 在该指标上的表现尤其糟糕，得分仅为 5.90。相比之下，DeepSeek R1 在“激励、引导与积极反馈”（Motivation, Guidance & Positive Feedback）这一指标上始终表现出色，即使其他模型在此项上表现不佳。在具体场景层面，从表1可以看出，DeepSeek R1 仍然遥遥领先；而通义千问系列中 7B 与 14B 版本之间的性能差距相对较小，使得 7B 模型在资源受限的场景下成为一个更具性价比的选择。
## 模型蒸馏
<div align="center">
  <img src="images/distill_result.png" alt="distill_result" width="800"/>
</div>

上图比较了蒸馏模型与其他模型在各项指标上的表现：

- 数据集构建：为了充分利用不同生成模型在各种教育场景中的优势，我们采用了一个多源蒸馏流程。对于每个任务，我们从测试集中选择表现最优的模型作为回答生成器，并使用它来回答教育领域的问题，从而构建用于蒸馏模型的训练数据集。通过该蒸馏流程，我们获得了包含 4,000 个样本的训练集，覆盖了全部 9 个教育场景中的各类子任务。
- 性能表现：在经过蒸馏之后，7B 模型在 12 项指标中的 10 项上都有显著提升，其整体表现已与当前最先进的模型相当。值得注意的是，在“推理过程严谨性”（Reasoning Process Rigor）这一指标上，该模型的表现优于包括 DeepSeek R1 和 Qwen Max 在内的所有其他模型。

## 模型评估与人类评估分析
<div align="center">
  <img src="images/Kendall.png" alt="kendall" width="800"/>
</div>

上图展示了不同评估模型与人工评估之间的Kendall's W，我们可以发现：

- 评价模型之间的一致性：模型表现出高度的一致性，几乎所有模型的Kendall's W值都在0.5以上，大多数在0.6左右，显示出很强的一致性。DeepSeek V3显示出与其他模型的最高一致性，其响应模型的平均得分排名与其他模型的一致性非常接近。
- 人类和模型之间的一致性：模型的评估评分与人类判断并不完全一致，这可能是由于他们对评估指标的理解有限。总体而言，DeepSeek V3与人类评估的相关性最高，而GPT-4 o显示最低。这种模式可能归因于DeepSeek V3相对较大的模型大小和广泛的训练数据分布。

# 讨论

