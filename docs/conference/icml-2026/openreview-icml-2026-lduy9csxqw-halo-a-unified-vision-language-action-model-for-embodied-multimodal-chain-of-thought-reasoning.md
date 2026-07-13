---
title: "HALO: A Unified Vision-Language-Action Model for Embodied Multimodal Chain-of-Thought Reasoning"
title_zh: HALO：面向具身多模态思维链推理的统一视觉-语言-动作模型
authors: "Quanxin Shou, Fangqi Zhu, Shuang Chen, Puxin Yan, Zhengyang Yan, Yikun Miao, Xiaoyi Pang, Zicong Hong, Ruikai Shi, Hao HUANG, Jie ZHANG, Song Guo"
date: 2026-04-30
pdf: "https://openreview.net/pdf/f0a4b4b3d1775cb04d6e602c68bf3c4914033562.pdf"
tags: ["query:human-aigc"]
score: 6.0
evidence: 结合世界演化的多模态思维链VLA模型
tldr: 针对VLA模型在长时域和分布外场景中缺乏显式多模态推理的问题，提出HALO统一框架，同时实现文本推理、视觉子目标预测和动作预测，通过多模态思维链提升鲁棒性。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: VLA模型在长时域任务中缺乏显式推理。
method: 统一文本推理、视觉子目标预测与动作预测。
result: 在模拟器上展示了对复杂任务的性能提升。
conclusion: 多模态思维链增强VLA的鲁棒性和泛化性。
---

## Abstract
Vision–Language–Action (VLA) models perform well in robotic manipulation, but often struggle in long-horizon or out-of-distribution scenarios due to the lack of explicit mechanisms for multimodal reasoning and anticipating how the world evolves under action.
Recent works introduce textual chain-of-thought or visual subgoal prediction within VLA models, but still fail to offer a unified human-like framework for joint textual reasoning, visual foresight, and action prediction.
To this end, we propose HALO, a unified VLA model that enables embodied multimodal chain-of-thought (EM-CoT) reasoning through textual reasoning, fine-grained visual subgoal prediction, and EM-CoT-augmented action prediction.
We instantiate HALO with a Mixture-of-Transformers (MoT) architecture that decouples semantic reasoning, visual foresight, and action prediction into specialized experts with seamless cross-expert collaboration.
To enable HALO learning at scale, we introduce an automated pipeline to synthesize EM-CoT training data along with a carefully crafted training recipe.
Extensive experiments demonstrate that: (1) HALO achieves superior performance in both simulated and real world, surpassing baseline policy $\pi_0$ by 25.9\% on the RoboTwin benchmark; (2) all proposed components of the training recipe and EM-CoT design help improve task success rate; and (3) HALO exhibits strong generalization under aggressive unseen environment randomization with our proposed EM-CoT reasoning.

---

## 论文详细总结（自动生成）

# HALO：面向具身多模态思维链推理的统一视觉-语言-动作模型

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：现有的视觉-语言-动作（VLA）模型在机器人操作任务中表现良好，但在长时域（long-horizon）或分布外（out-of-distribution）场景中往往表现不佳，根本原因在于缺乏显式的多模态推理机制，无法有效预测动作如何影响世界演化。
- **背景**：近期工作尝试在VLA模型中引入文本思维链（chain-of-thought）或视觉子目标预测，但未能提供一个统一的人类式框架，同时实现文本推理、视觉预判和动作预测。
- **核心问题**：如何构建一个统一的VLA模型，能够进行具身多模态思维链（Embodied Multimodal Chain-of-Thought, EM-CoT）推理，从而提升在复杂、未知环境下的鲁棒性和泛化能力。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：提出HALO统一框架，在单一模型中同时执行三个任务：文本推理（textual reasoning）、细粒度视觉子目标预测（fine-grained visual subgoal prediction）、以及EM-CoT增强的动作预测（action prediction）。这模仿了人类在决策时“思考-预判-行动”的完整过程。
- **关键技术细节**：
  - **架构**：采用混合专家Transformer（Mixture-of-Transformers, MoT）架构，将语义推理、视觉预判和动作预测解耦为专门的专家模块，并通过无缝的跨专家协作实现信息融合。
  - **自动化数据合成管线**：为支持HALO的大规模训练，设计了自动化的EM-CoT训练数据合成流程，并配合精心设计的训练方案（training recipe）。
  - **训练策略**：包含特定的数据增强、损失函数设计等，以提升模型学习效率和推理质量（具体公式未在摘要中详细给出，但提及“carefully crafted training recipe”）。
- **算法流程描述**：输入多模态观察（图像+文本指令）→ MoT中的语义推理专家生成文本推理→ 视觉预判专家预测未来子目标（图像级）→ 动作预测专家结合推理与子目标输出动作序列。整个流程构成端到端的统一模型。

## 3. 实验设计

- **数据集/场景**：
  - **模拟器**：RoboTwin benchmark（具体任务未知，但包含多种机器人操作场景）。
  - **真实世界**：进行了真实机器人操作实验（具体场景未详述）。
- **Benchmark**：RoboTwin benchmark。
- **对比方法**：
  - 主要对比基线策略 `π_0`（推测为一种VLA基线方法）。
  - 消融实验中比较了是否使用EM-CoT各组件（文本推理、视觉子目标、训练方案等）的效果。

## 4. 资源与算力

- 论文摘要及元数据中**未明确说明**使用的GPU型号、数量、训练时长等具体算力信息。仅在方法部分提及“大规模训练”和“自动化数据合成管线”，但未提供训练资源细节。
- **注意**：若需获取详细信息，需查阅原论文全文。

## 5. 实验数量与充分性

- 从摘要可推断的实验组数：
  - **主要性能对比**：在模拟器RoboTwin上与基线π₀对比，提升25.9%。
  - **消融实验**：验证了训练方案和EM-CoT设计的所有组件均有助于提高任务成功率。
  - **泛化实验**：在激进的未见环境随机化（unseen environment randomization）下测试HALO的强泛化能力，并证明EM-CoT推理在此类场景中的有效性。
- **充分性评价**：以上实验覆盖了主要性能、消融和泛化三方面，较为全面。但未提及在多个不同数据集/benchmark上的对比，可能局限在RoboTwin单一基准；也未报告统计显著性检验或多次运行的标准差。实验设计客观，但全面性有待正文补充。

## 6. 主要结论与发现

1. **性能优势**：HALO在模拟器和真实世界中均取得了优越性能，在RoboTwin基准上比基线π₀提升25.9%的成功率。
2. **组件有效性**：训练方案和EM-CoT设计的每个子模块（文本推理、视觉子目标预测、跨专家协作）均对提升任务成功率有贡献。
3. **强泛化能力**：在激进的未见环境随机化下，HALO凭借EM-CoT推理表现出强大的泛化能力。

## 7. 优点

- **方法创新**：首次提出统一的多模态思维链VLA框架，同时实现文本推理、视觉预判和动作预测，更接近人类决策模式。
- **架构设计**：混合专家Transformer（MoT）解耦不同能力，专家间高效协作，可能带来更好的可扩展性和可解释性。
- **自动化数据合成**：解决了多模态思维链训练数据匮乏的问题，使大规模学习成为可能。
- **实验验证充分**：同时包括模拟和真实世界实验，并进行了消融和泛化测试，验证了各组件贡献和鲁棒性。

## 8. 不足与局限

- **实验覆盖有限**：仅报告了在RoboTwin一个模拟基准上的结果，未在更多标准机器人操作benchmark（如CALVIN、MetaWorld等）上验证，可能影响结论的普适性。
- **资源信息缺失**：未提供训练算力和时间，难以评估方法的可复现性和成本。
- **真实世界实验细节不足**：未说明真实场景的具体任务、物体种类、环境变化程度等，泛化性能的真实范围不清晰。
- **偏差风险**：自动化数据合成管线可能引入特定分布偏差，若训练数据与测试环境差异较大，泛化能力可能下降。
- **应用限制**：当前框架依赖视觉子目标的预测质量，在低图像质量或动态环境下可能受限；且MoT架构的推理速度可能较慢，影响实时性。

（完）
