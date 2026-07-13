---
title: Co-Evolving Latent Action World Models
title_zh: 共同演化的潜在动作世界模型
authors: "Yucen Wang, Fengming Zhang, De-Chuan Zhan, Li Zhao, Kaixin Wang, Jiang Bian"
date: 2026-04-30
pdf: "https://openreview.net/pdf/391ed8836eb3e106d9610ecba14f34b26dff6813.pdf"
tags: ["query:human-aigc"]
score: 9.0
evidence: 共同演化的潜在动作世界模型
tldr: 传统潜在动作世界模型采用两阶段分离训练，限制了协同适应能力。CoLA-World首次实现了潜在动作模型与世界模型的联合训练，通过关键预热阶段对齐表示，避免了表征坍塌。实验表明，联合训练策略显著提升了世界模型的预测质量和动作控制能力，为构建通用世界模型提供了协同演化范式。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有潜在动作世界模型采用两阶段分离训练，导致训练冗余且限制了协同适应能力。
method: CoLA-World通过关键预热阶段对齐表示，首次成功实现了潜在动作模型与世界模型的联合训练。
result: 联合训练策略显著提升了世界模型的预测质量和动作控制能力，在多个任务上优于分离训练方法。
conclusion: 协同演化范式为构建通用世界模型提供了高效且有效的新途径。
---

## Abstract
Adapting pre-trained video generation models into controllable world models via latent actions is a promising step towards creating generalist world models. The dominant paradigm adopts a two-stage approach that trains latent action model (LAM) and the world model separately, resulting in redundant training and limiting their potential for co-adaptation. A conceptually simple and appealing idea is to directly replace the forward dynamic model in LAM with a powerful world model and training them jointly, but it is non-trivial and prone to representational collapse. In this work, we propose CoLA-World, which for the first time successfully realizes this synergistic paradigm, resolving the core challenge in joint learning through a critical warm-up phase that effectively aligns the representations of the from-scratch LAM with the pre-trained world model. This unlocks a co-evolution cycle: the world model acts as a knowledgeable tutor, providing gradients to shape a high-quality LAM, while the LAM offers a more precise and adaptable control interface to the world model. Empirically, CoLA-World matches or outperforms prior two-stage methods in both video simulation quality and downstream visual planning, establishing a robust and efficient new paradigm for the field.

---

## 论文详细总结（自动生成）

# 论文详细中文总结：CoLA-World（共同演化的潜在动作世界模型）

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：将预训练的视频生成模型适配为可通过潜在动作控制的世界模型（world model），是构建通用世界模型的重要方向。现有主流范式采用**两阶段分离训练**：先训练潜在动作模型（LAM），再训练世界模型（或反之），导致训练冗余，且两者无法协同适应（co-adaptation）。
- **整体含义**：该工作旨在首次实现潜在动作模型与世界模型的**联合训练**，解锁二者的协同演化循环，从而提升世界模型的预测质量和动作控制能力。

## 2. 方法论：核心思想、关键技术细节、算法流程

- **核心思想**：直接替换 LAM 中的前向动态模型为一个强大的预训练世界模型，并使两者联合训练；但直接联合易导致**表征坍塌**（representational collapse）。
- **关键技术细节**：
  - 提出 **CoLA-World**，通过一个**关键预热阶段（critical warm-up phase）**，有效对齐从零开始训练的 LAM 与预训练世界模型的表征，避免坍塌。
  - 预热后进入**协同演化循环**：世界模型作为知识渊博的“导师”，提供梯度反馈以塑造高质量的 LAM；LAM 则为世界模型提供更精确、更适应的控制接口。
- **算法流程（文字说明）**：
  1. 使用预训练的视频生成模型作为世界模型初始化。
  2. 设计 LAM 从零开始训练，并在预热阶段通过特定对齐目标（如对比学习或重建损失）使 LAM 的表征空间与世界模型的潜空间匹配。
  3. 联合优化 LAM 和世界模型：世界模型利用 LAM 产生的潜在动作进行前向预测，预测误差同时反向传播更新世界模型和 LAM。
  4. 迭代训练直至收敛。

## 3. 实验设计

- **数据集/场景**：摘要中未明确列出具体数据集或任务场景，仅提及在“视频模拟质量”和“下游视觉规划”任务上进行评估。
- **基准（Benchmark）**：未说明具体基准。
- **对比方法**：与前人的两阶段方法（先训 LAM 再训世界模型）进行比较。摘要未列出具体方法名称。

## 4. 资源与算力

- 文中**未提及**任何关于算力的信息（如 GPU 型号、数量、训练时长等）。因此无法总结算力细节。

## 5. 实验数量与充分性

- **实验数量**：摘要未给出具体的实验组数或消融实验设置。
- **充分性与客观性**：摘要仅声称 CoLA-World 在“多个任务上匹配或优于两阶段方法”，但缺少详细实验结果、统计显著性或误差分析，因此**难以判断实验的充分性和客观性**。信息有限，需等待全文发表。

## 6. 主要结论与发现

- 首次成功实现了潜在动作模型与世界模型的**联合训练**，解决了表征坍塌的关键挑战。
- 联合训练策略显著提升了世界模型的**预测质量**和**动作控制能力**。
- 协同演化范式为构建通用世界模型提供了**高效且有效的新途径**。

## 7. 优点

- **方法创新性**：首次提出并成功落地联合训练框架，克服了直接联合易坍塌的理论障碍。
- **结构简洁**：仅增加一个预热阶段即可实现协同演化，无需复杂设计。
- **性能潜力**：在模拟质量和规划能力上均能匹配或超越两阶段方法，证明联合训练的优势。

## 8. 不足与局限

- **实验细节缺失**：摘要中未提供任何量化结果、数据集名称、对比基线具体信息，导致可复现性和可信度难以评估。
- **资源/算力未披露**：缺少计算成本信息，不利于对方法实际效率的判断。
- **依赖预训练世界模型**：方法依赖一个强预训练视频生成模型作为初始化，其质量可能直接影响最终效果。
- **泛化性存疑**：未说明在除视频模拟和视觉规划外的其他任务（如强化学习、机器人控制）上的表现。
- **理论分析薄弱**：对表征对齐和防止坍塌的理论解释未在摘要中体现，可能缺乏严谨性。

（完）
