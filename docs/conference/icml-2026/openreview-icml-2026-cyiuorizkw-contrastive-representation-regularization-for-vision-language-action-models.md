---
title: Contrastive Representation Regularization for Vision-Language-Action Models
title_zh: 视觉-语言-动作模型的对比表示正则化
authors: "Taeyoung Kim, Jimin Lee, Myungkyu Koo, Dongyoung Kim, Kyungmin Lee, Changyeon Kim, Younggyo Seo, Jinwoo Shin"
date: 2026-04-30
pdf: "https://openreview.net/pdf/0cc7ec26fa9f47ae531d226ac90d7d42c7e48b94.pdf"
tags: ["query:human-aigc"]
score: 4.0
evidence: 用于机器人操作的VLA模型
tldr: 针对VLA模型表示对控制信号不敏感的问题，提出机器人状态感知对比损失(RS-CL)，通过状态间相对距离作为软监督对齐表示，提升了机器人操作性能。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: VLA模型表示对机器人控制信号不敏感。
method: 提出RS-CL损失利用状态距离对齐表示。
result: 实验验证了表示正则化提升操作性能。
conclusion: 所提方法简单有效，可推广至多种VLA模型。
---

## Abstract
Vision-Language-Action (VLA) models have shown strong capabilities in robot manipulation by leveraging rich representations from pre-trained Vision-Language Models (VLMs).
However, their representations arguably remain suboptimal, lacking sensitivity to robotic signals such as control actions and proprioceptive information. 
To address the issue, we introduce Robot State-aware Contrastive Loss (RS-CL), a simple and effective representation regularization for VLA models, designed to bridge the gap between VLM representations and robotic signals.
In particular, RS-CL aligns the representations more closely with the robot's proprioceptive states by using relative distances between the states as soft supervision.
Complementing the original action prediction objective, RS-CL enhances control-relevant representation learning, while being lightweight and fully compatible with standard VLA training pipelines.
Our empirical results demonstrate that RS-CL substantially improves the performance of state-of-the-art VLA models; it pushes the prior art to 69.7% achieving the state-of-the-art performance on the RoboCasa-Kitchen benchmark, and boosts success rates from 45.0% to 58.3% on challenging real-robot manipulation tasks.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究背景**：视觉-语言-动作（VLA）模型利用预训练的视觉-语言模型（VLM）的丰富表征，在机器人操作中展现了强大能力。
- **核心问题**：VLA模型的表征仍存在不足，主要表现为对机器人控制信号（如控制动作、本体感知信息）不够敏感，导致表征无法充分捕获与操作相关的关键信息。
- **研究动机**：提出一种轻量且有效的表征正则化方法，弥合VLM表征与机器人信号之间的鸿沟，从而提升VLA模型在操作任务上的性能。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：通过对比学习，使VLA模型的表征与机器人本体感知状态（proprioceptive states）的距离关系对齐，从而增强表征对控制信号的敏感性。
- **关键技术细节**：
  - 提出 **机器人状态感知对比损失（Robot State-aware Contrastive Loss, RS-CL）**。
  - 在训练过程中，使用不同状态之间的**相对距离**作为**软监督**信号，指导表征学习：即鼓励模型在表征空间中保持与真实状态空间相似的相对距离关系。
  - RS-CL作为辅助损失，与原始的**动作预测目标**（如行为克隆损失）联合优化，不改变主流VLA训练流程。
  - 该损失计算效率高（轻量级），可无缝集成到现有VLA训练管线中。
- **公式/算法流程（文字说明）**：
  1. 从同一批次中采样若干机器人状态（如关节角度、末端执行器位姿）对应的表征。
  2. 计算真实状态下两两之间的欧氏距离（或相似度）。
  3. 计算对应表征向量两两之间的余弦相似度（或对比度量）。
  4. 使用KL散度或均方误差等损失函数，迫使表征相似度分布接近真实状态距离分布。
  5. 总损失 = 动作预测损失 + λ × RS-CL。

## 3. 实验设计

- **数据集/场景**：
  - **RoboCasa-Kitchen 基准**：一个包含多种厨房操作任务的仿真基准。
  - **真实机器人操作任务**：在挑战性的真实机器人上执行操作（具体任务未详述）。
- **基准方法**：与多个先进的VLA模型对比（文中提到将先前最优模型性能提升至69.7%）。
- **对比方法**：文中未明确列出全部对比方法，但暗示包括标准VLA模型（不加RS-CL的基线）以及先前SOTA。

## 4. 资源与算力

- **未明确说明**：论文摘要及元数据中未提及使用的GPU型号、数量、训练时长等具体算力信息。
- **建议**：需要查阅完整论文以获取硬件配置细节。

## 5. 实验数量与充分性

- **实验数量**：
  - 提供了**一个大型仿真基准（RoboCasa-Kitchen）**的实验结果。
  - 提供了**一组真实机器人操作任务**的实验结果。
  - 可能包含消融实验（不同λ权重、对比损失变体等），但摘要未详述。
- **充分性评估**：
  - 优点：覆盖了仿真和真实场景，验证了方法有效性。
  - 不足：实验覆盖范围有限（仅一个仿真基准+一个真实设置），缺少在更多不同机器人形态、不同数据集上的验证。
  - 公平性：文中强调“将先前最优性能提升至69.7%”，表明直接与SOTA对比，但未披露基线复现细节，可能存在偏差。

## 6. 主要结论与发现

- RS-CL作为表征正则化项，显著提升了VLA模型在机器人操作中的性能：
  - 在RoboCasa-Kitchen上达到**69.7%** 的SOTA结果。
  - 在真实机器人上，成功率从**45.0%提升至58.3%**（绝对提升13.3个百分点）。
- 所提方法**简单、有效、轻量**，可与多种VLA模型兼容，无需修改主干网络或训练范式。

## 7. 优点（方法和实验设计亮点）

- **方法层面**：
  - 创新性地利用状态间相对距离作为软监督，避免了人工标注或对比学习中的硬正负样本划分。
  - 轻量级计算，不影响训练效率。
  - 直接针对表征对控制信号不敏感的问题，目标明确。
- **实验层面**：
  - 同时提供仿真基准和真实机器人实验，增强了结果的可信度。
  - 展示了明确的性能提升，且达到SOTA，说服力较强。

## 8. 不足与局限

- **实验覆盖局限**：仅使用单一仿真基准和一组真实任务，缺乏在多样化环境（如不同机器人型号、不同操作类型）上的验证，泛化性有待检验。
- **偏差风险**：可能只在特定VLA架构下有效，论文未讨论对其他架构（如基于Diffusion的VLA）的适用性。
- **应用限制**：RS-CL依赖状态距离的合理定义，对于高维或部分可观测状态（如视觉状态）可能不够直观。
- **算力信息缺失**：未报告训练资源，不利于复现及评估实用性。
- **消融实验不透明**：未明确说明是否进行了λ参数敏感性分析或对比损失变体比较，实验细节不够充分。

（完）
