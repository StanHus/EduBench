# EduBench: A Comprehensive Benchmark Dataset for Evaluating Large Language Models in Diverse Educational Scenarios

<p align="center">
  📄 <a href="https://arxiv.org/pdf/2505.16160 " target="_blank">Paper</a> &nbsp; | &nbsp;
  🤗 <a href="https://huggingface.co/DirectionAI/EDU-Qwen2.5-7B" target="_blank">Model</a> &nbsp; |
  🎰 <a href="https://huggingface.co/datasets/DirectionAI/EduBench" target="_blank">Datasets</a> &nbsp; | &nbsp;
  ⚖️ <a href="" target="_blank">MIT License</a>
</p>

# Table of Contents
- [Overview](#overview)
- [Framework](#framework)
- [Dataset Construction](#dataset-construction)
  - [Evaluation Metrics Design](#evaluation-metrics-design)
  - [Dataset Generation](#dataset-generation)
  - [Data Evaluation](#data-evaluation)
- [Experiments and Analysis](#experiments-and-analysis)
  - [Evaluation Results](#evaluation-results)
  - [Model-Human Evaluation Consistency Analysis](#model-human-evaluation-consistency-analysis)
  - [Model Distillation](#model-distillation)
 

# Overview
<div align="center">
  <img src="images/distribution-radar.jpg" alt="Distribution Radar" width="1200"/>
  <br>
  <strong>The left section displays our 9 educational scenarios, showing their multidimensional educational contexts and corresponding metrics along the vertical axis. The right section presents human evaluation results on EduBench.</strong>
</div>

<br>

Introducing EduBench 📚, a diversified benchmark dataset 🌟 specifically tailored for educational scenarios, covering 9 major educational contexts 🏫 and over 4,000 different educational situations 🔍, providing a fresh perspective for model evaluation in the education domain.

We designed multidimensional evaluation metrics 🛠️, comprehensively covering 12 key dimensions 🧠 from both teacher and student perspectives, ensuring in-depth assessment of scenario adaptability, factual and reasoning accuracy, and more.

Moreover, through knowledge distillation technology 🔬, we enabled smaller models like Qwen2.5-7B-Instruct to achieve performance comparable to state-of-the-art large models such as DeepSeek V3 and Qwen Max with only minimal data. EduBench is not just a benchmark—it's a game changer 🚀 for educational model development!

---

# Framework
<div align="center">
  <img src="images/framework.jpg" alt="Framework" width="1200"/>
  <br>
  <strong>The left part illustrates our data curation process; the middle part presents our three main evaluation principles and our exploration of the consistency between large language models and human judgments; the right part demonstrates how our data enhances the performance of small models.</strong>
</div>

# Dataset Construction

We first classify educational scenarios into the following two categories based on their target users:

**I. Student-Oriented Scenarios**

- Question Answering (Q&A)  
- Error Correction (EC)  
- Idea Provision (IP)  
- Personalized Learning Support (PLS)  
- Emotional Support (ES)  

**II. Teacher-Oriented Scenarios**

- Question Generation (QG)  
- Automatic Grading (AG)  
- Teaching Material Generation (TMG)  
- Personalized Content Creation (PCC)  

---

## Evaluation Metric Design

Based on the defined educational scenarios, we have designed a comprehensive evaluation metric system. Each scenario includes 4 sub-indicators, resulting in a total of 12 core evaluation indicators.

### 1. Scenario Adaptability

Measures whether the model's response is contextually appropriate and meets the expectations of the educational scenario.

- **Instruction Following & Task Completion**  
- **Role & Tone Consistency**  
- **Content Relevance & Scope Control**  
- **Scenario Element Integration**

### 2. Factual & Reasoning Accuracy

Evaluates the accuracy of factual information and the rigor of reasoning processes within the model’s responses.

- **Basic Factual Accuracy**  
- **Domain Knowledge Accuracy**  
- **Reasoning Process Rigor**  
- **Error Identification & Correction Precision**

### 3. Pedagogical Application

Assesses whether the model's responses reflect effective teaching principles and support student learning.

- **Clarity, Simplicity & Inspiration**  
- **Motivation, Guidance & Positive Feedback**  
- **Personalization, Adaptation & Learning Support**  
- **Higher-Order Thinking & Skill Development**

---

## Dataset Generation

As an example, we use the **Error Correction (EC)** scenario to generate data by running the following code:
```bash
python ./code/generation/EC.py
```

## Dataset Evaluation

To evaluate the dataset, simply run the following code (make sure to adjust the API configuration as needed):
```bash
python ./code/evaluation/evaluation.py
```

## Experiments and Analysis

### Evaluation Results

| Evaluator       | Model                  | Q&A  | PLS  | EC   | IP   | AG   | TMG  | ES   | QG   | PCC  | Average |
|-----------------|------------------------|------|------|------|------|------|------|------|------|------|---------|
| **DeepSeek R1** | DeepSeek R1            | **9.81** | **9.83** | **9.05** | **9.11** | 7.74 | **9.46** | **9.71** | **9.22** | **9.73** | **9.29** |
|                 | DeepSeek V3            | 9.67 | 9.12 | 8.97 | 8.82 | **8.32** | 9.31 | 9.34 | 8.65 | 9.23 | 9.05 |
|                 | Qwen Max               | 9.07 | 9.11 | 8.86 | 8.84 | 7.99 | 9.15 | 9.40 | 8.89 | 9.29 | 8.96 |
|                 | Qwen2.5-14B-Instruct   | 8.94 | 8.79 | 8.68 | 8.23 | 7.83 | 9.06 | 8.52 | 8.35 | 8.80 | 8.58 |
|                 | Qwen2.5-7B-Instruct    | 8.34 | 9.01 | 8.64 | 8.16 | 6.64 | 9.33 | 8.75 | 8.23 | 9.06 | 8.46 |
| **DeepSeek V3** | DeepSeek R1            | 9.49 | **9.65** | **9.27** | **8.75** | **7.27** | **9.45** | **9.38** | **9.33** | **9.71** | **9.14** |
|                 | DeepSeek V3            | **9.68** | 9.04 | 9.14 | 8.53 | 7.05 | 9.34 | 9.00 | 9.06 | 8.92 | 8.86 |
|                 | Qwen Max               | 9.18 | 8.88 | 9.06 | 8.52 | 7.23 | 9.24 | 9.04 | 9.05 | 9.29 | 8.83 |
|                 | Qwen2.5-14B-Instruct   | 9.07 | 8.72 | 8.97 | 8.30 | 6.77 | 9.21 | 8.74 | 9.02 | 8.80 | 8.62 |
|                 | Qwen2.5-7B-Instruct    | 9.15 | 9.07 | 9.01 | 8.47 | 6.44 | 9.21 | 8.85 | 8.69 | 9.00 | 8.65 |
| **GPT-4o**      | DeepSeek R1            | 9.32 | **9.38** | 9.05 | 8.78 | 8.51 | **9.25** | **9.15** | 8.98 | **9.08** | **9.06** |
|                 | DeepSeek V3            | 9.22 | 9.15 | **9.14** | 8.77 | 8.54 | 9.12 | 9.05 | **9.00** | 8.95 | 8.99 |
|                 | Qwen Max               | **9.50** | 9.17 | 9.01 | 8.69 | **8.70** | 8.99 | 8.96 | 8.92 | 9.05 | 8.99 |
|                 | Qwen2.5-14B-Instruct   | 9.34 | 9.25 | 8.92 | 8.51 | 8.11 | 8.99 | 9.11 | 8.77 | 8.82 | 8.87 |
|                 | Qwen2.5-7B-Instruct    | 9.22 | 9.17 | 8.92 | **8.84** | 8.04 | 9.05 | 9.00 | 8.62 | 8.94 | 8.87 |
| **QwQ-Plus**    | DeepSeek R1            | **9.85** | **9.87** | **9.24** | **9.05** | **8.78** | **9.75** | **9.85** | **9.09** | **9.88** | **9.49** |
|                 | DeepSeek V3            | 9.59 | 9.43 | 9.06 | 8.66 | 8.18 | 9.29 | 9.66 | 8.47 | 9.24 | 9.06 |
|                 | Qwen Max               | 9.90 | 9.25 | 9.03 | 8.78 | 8.11 | 9.54 | 9.56 | 8.79 | 9.70 | 9.18 |
|                 | Qwen2.5-14B-Instruct   | 9.83 | 9.21 | 9.05 | 8.23 | 7.88 | 9.22 | 9.45 | 8.48 | 9.02 | 8.94 |
|                 | Qwen2.5-7B-Instruct    | 9.02 | 9.28 | 8.79 | 8.82 | 7.16 | 9.33 | 9.31 | 8.69 | 9.35 | 8.78 |
| **Human**       | DeepSeek R1            | 7.17 | **9.11** | **8.71** | **8.80** | **8.42** | **8.86** | **9.15** | **8.79** | **9.35** | **8.71** |
|                 | DeepSeek V3            | 7.45 | 8.12 | 8.16 | 8.17 | 7.84 | 7.56 | 8.08 | 8.01 | 7.03 | 7.82 |
|                 | Qwen Max               | **7.72** | 7.94 | 8.21 | 8.15 | 7.89 | 7.99 | 7.85 | 8.39 | 8.42 | 8.06 |
|                 | Qwen2.5-14B-Instruct   | 7.66 | 7.38 | 7.92 | 7.56 | 7.55 | 7.84 | 7.31 | 7.91 | 7.36 | 7.61 |
|                 | Qwen2.5-7B-Instruct    | 6.78 | 7.63 | 7.93 | 7.74 | 6.79 | 7.86 | 7.79 | 7.55 | 7.42 | 7.50 |

<div align="center">
  <img src="images/eval_matric.png" alt="eval_matric" width="800"/>
  <br>
  <strong>Table 2: Shows the average scores at the metric level under different evaluators.</strong>
</div>

**Model Evaluation Results**  
DeepSeek R1 demonstrated the best overall performance across different metrics, while Qwen2.5-7B-Instruct performed worst in Table 2. Additionally, DeepSeek R1 excelled in "Higher-Order Thinking & Skill Development," whereas Qwen2.5-7B-Instruct performed poorly in "Error Identification & Correction Precision," with significant gaps compared to other models. In specific scenarios, DeepSeek R1 remained the top performer, and in areas like "Emotional Support" and "Personalized Content Creation," Qwen2.5-7B-Instruct outperformed Qwen2.5-14B-Instruct.

**Human Evaluation Results**  
In Table 2, DeepSeek R1 and Qwen2.5-7B-Instruct still showed the best and worst performances respectively, consistent with model-based evaluations. Unlike model evaluations, human annotators expressed significantly lower satisfaction with all five models in terms of "Reasoning Process Rigor." Specifically, Qwen2.5-7B-Instruct scored only 5.90 on this metric. By contrast, DeepSeek R1 consistently performed well in "Motivation, Guidance & Positive Feedback," even when other models struggled in this area. At the scenario level, Table 1 shows that DeepSeek R1 remains far ahead; among the Qwen series, the performance gap between the 7B and 14B versions is relatively small, making the 7B model a more cost-effective choice in resource-constrained environments.

---

### Model Distillation

<div align="center">
  <img src="images/distill_result.png" alt="distill_result" width="800"/>
</div>

The figure above compares the distilled model's performance against other models across various metrics:

- **Dataset Construction**: To fully leverage the advantages of different generative models across educational scenarios, we adopted a multi-source distillation process. For each task, we selected the model with the best performance from the test set as the answer generator and used it to respond to educational questions, thereby building a training dataset for distilling models. Through this distillation process, we obtained a training set containing 4,000 samples covering all nine educational scenarios and various subtasks.
- **Performance**: After distillation, the 7B model significantly improved on 10 out of 12 metrics, with its overall performance becoming comparable to the current state-of-the-art models. Notably, in the "Reasoning Process Rigor" metric, the model outperformed all other models including DeepSeek R1 and Qwen Max.

---

### Consistency Analysis Between Model and Human Evaluation

<div align="center">
  <img src="images/Kendall.png" alt="kendall" width="800"/>
</div>

The above figure shows Kendall's W between different evaluation models and human assessments:

- **Consistency Among Evaluation Models**: Models exhibited high consistency, with almost all Kendall's W values above 0.5 and most around 0.6, indicating strong agreement. DeepSeek V3 showed the highest consistency with other models, with its ranking of averaged model scores closely matching those of other evaluators.
- **Consistency Between Humans and Models**: Model evaluation scores were not entirely aligned with human judgments, possibly due to limited understanding of the evaluation criteria by models. Overall, DeepSeek V3 showed the highest correlation with human evaluation, while GPT-4o showed the lowest. This pattern may be attributed to DeepSeek V3's relatively larger model size and broader training data distribution.
