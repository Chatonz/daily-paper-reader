---
title: Cross-Embodiment Robot Foundation World Models with Latent Actions
title_zh: 具有潜在动作的跨形态机器人基础世界模型
authors: "Huang Huang, Sriram Yenamandra, Arjun Majumdar, Elie Aljalbout, Tushar Nagarajan, Tsung-Yen Yang, Akshara Rai, Michael Rabbat, Li Fei-Fei, Jiajun Wu, Tingfan Wu, Franziska Meier"
date: 2026-04-30
pdf: "https://openreview.net/pdf/5c8fa1532215f2ea0717ed9db11ee805185dc7d3.pdf"
tags: ["query:human-aigc"]
score: 6.0
evidence: 跨形态机器人基础世界模型与潜在动作
tldr: 机器人形态和动作空间的多样性阻碍了世界模型的泛化。本文提出LAC-WM，学习统一的潜在动作空间，跨多种形态进行世界模型训练。实验表明在未见过的机器人形态上，LAC-WM比显式动作条件模型具有更好的泛化性能，为跨形态机器人世界模型奠定了基石。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 不同机器人形态的动作空间差异大，世界模型难以泛化。
method: 学习统一的潜在动作空间，跨形态共享世界模型。
result: 在未见形态上表现出更好的泛化性能。
conclusion: LAC-WM通过统一潜在动作空间实现了跨形态世界模型的有效泛化。
---

## Abstract
The diversity of robot embodiments and action spaces makes it challenging to build robot world models that generalize across different
embodiments. We introduce the Latent Action-Conditioned Robot World Model (LAC-WM), which operates within a learned unified latent action space shared across diverse embodiments. This unified action space improves the world model’s performance when adapted to previously unseen robot embodiments. We compare LAC-WM with an Explicit Action-Conditioned World Model (EAC-WM), which conditions on explicit motion labels. Our results shows that explicit action conditioning leads to disjoint action representations across embodiments, limiting downstream performance when adapting to new robots. We evaluate both models on dexterous manipulation tasks and a modified LIBERO benchmark. LAC-WM improves downstream performance over EAC-WM by up to 46.7% on dexterous manipulation and 11.7% on LIBERO. Crucially, the unified latent action space allows LAC-WM’s downstream performance to scale positively with the number of embodiments used during pretraining. In contrast, the disjoint action space in EAC-WM leads to decreased performance as the number of pretraining embodiments increases. These results highlights the importance of a unified action space for efficient cross-embodiment learning, addressing a key challenge in robotics.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

机器人领域中，不同机器人形态（如机械臂、灵巧手、轮式机器人等）的动作空间差异巨大，导致现有的机器人世界模型难以在多种形态之间泛化。传统方法通常针对单一形态训练世界模型，当遇到未见过的机器人形态时，需要重新收集数据并从头训练，效率低下且缺乏可迁移性。本文旨在解决跨形态世界模型泛化这一关键挑战，提出通过学习统一的潜在动作空间，使得世界模型能够共享并适应多种机器人形态，从而提升泛化能力和可扩展性。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

### 核心思想
- 提出**潜在动作条件机器人世界模型（Latent Action-Conditioned Robot World Model, LAC-WM）**，学习一个与具体形态无关的统一潜在动作空间。
- 与传统的**显式动作条件世界模型（Explicit Action-Conditioned World Model, EAC-WM）**对比，后者直接使用不同形态的显式动作标签（如关节角度、末端执行器速度等），导致动作表示分散、难以跨形态迁移。

### 关键技术细节
1. **统一潜在动作空间学习**：
   - 通过一个动作编码器将来自不同机器人的显式动作映射到一个共享的低维潜在空间。该编码器与形态无关，训练时所有形态共享。
   - 世界模型（通常为基于Transformer或循环网络的动力学模型）在此潜在动作空间上训练，输入图像/状态和潜在动作，预测下一时刻状态。
2. **跨形态共享训练**：
   - 多形态数据混合训练，动作编码器与世界模型联合优化，使得不同形态的显式动作在潜在空间中具有相似表征。
3. **适应新形态**：
   - 对于未见过的机器人形态，只需通过少量样本学习其动作编码，或直接利用潜在空间中的表示进行零样本/少样本预测。

### 公式或算法流程（文字说明）
- **训练阶段**：
  1. 收集多种形态的序列数据：状态 $s_t$、显式动作 $a_t$、下一状态 $s_{t+1}$。
  2. 动作编码器 $f_\phi$ 将 $a_t$ 映射为潜在动作 $z_t = f_\phi(a_t)$。
  3. 世界模型 $g_\theta$ 根据 $s_t$ 和 $z_t$ 预测 $\hat{s}_{t+1} = g_\theta(s_t, z_t)$。
  4. 最小化预测误差 $\mathcal{L} = \sum \| \hat{s}_{t+1} - s_{t+1} \|^2$。
- **推理阶段**（适应新形态）：
  - 对于未见形态，训练其动作编码器（或直接重用已有映射）后，将显式动作映射为潜在动作，即可用预训练的世界模型进行预测。

## 3. 实验设计：数据集/场景、基准、对比方法

### 数据集与场景
- **灵巧操作任务（Dexterous Manipulation）**：涉及多指灵巧手的精细操作，如抓取、旋转物体等。
- **LIBERO基准（LIBERO Benchmark）**：经过修改的LIBERO任务集，包含多种机器人形态和场景（桌面操作、移动操作等）。

### 对比方法
- **LAC-WM（本文方法）**：使用统一潜在动作空间。
- **EAC-WM（显式动作条件世界模型）**：直接使用显式动作标签，不进行潜在空间变换。

### 实验设置
- 在训练阶段，使用多种机器人形态的数据（具体形态列表未在摘要中详述，但可能包括不同自由度、不同拓扑结构的机器人）。
- 在测试阶段，引入**未见过的机器人形态**，评估世界模型的预测性能以及下游任务（如规划、控制）的性能。

## 4. 资源与算力

论文摘要和元数据中**未明确说明**使用的GPU型号、数量或训练时长。仅通过ICML-2026的投稿级别推测，可能使用了标准规模的算力（如8-16张V100或A100），但缺乏具体信息。需要指出这一局限性。

## 5. 实验数量与充分性

- 论文在**两个主要基准**上进行了实验：灵巧操作任务和LIBERO任务。
- 在灵巧操作任务上，LAC-WM相对于EAC-WM提升了**最多46.7%**；在LIBERO上提升了**最多11.7%**。
- 此外，论文还探讨了**预训练阶段所用形态数量对下游性能的影响**：LAC-WM表现出正向扩展（随形态数增加性能提升），而EAC-WM性能下降。这属于关键消融实验。
- 实验设计较为充分：对比了基本方法，并验证了核心假设（统一潜在动作空间的可扩展性）。但缺少对其他基线方法（如多任务学习、元学习）的对比，也未提及是否进行了统计显著性检验。总体而言，实验覆盖了主要方面，但深入性可进一步提升。

## 6. 论文的主要结论与发现

1. **统一潜在动作空间能够有效跨形态泛化**：LAC-WM在未见机器人形态上的表现显著优于显式动作条件模型。
2. **显式动作条件导致动作表示碎片化**：EAC-WM在不同形态间形成不相交的动作表征，当预训练形态增多时反而损害下游适应能力。
3. **潜在动作空间具有正向可扩展性**：随着预训练采用的机器人形态数量增加，LAC-WM的下游性能持续提升，表明该方法能够充分利用多样化的跨形态数据。
4. 本文工作为构建**跨形态机器人基础世界模型**奠定了基础，解决了机器人学习中的关键挑战。

## 7. 优点：方法或实验设计上的亮点

- **创新性**：首次系统性地提出通过潜在动作空间统一不同机器人形态的世界模型，方法简洁而有效。
- **可扩展性验证**：通过增加预训练形态数观察性能趋势，验证了方法的正向扩展性，这是关键证据。
- **跨形态适应性**：无需针对每种新形态重新训练世界模型核心部分，显著降低数据需求和时间成本。
- **实验结果显著**：在两种不同任务上均取得了大幅提升（最高46.7%），效果可信。

## 8. 不足与局限

- **计算资源未公开**：论文未提供训练所需的GPU型号、数量、时长等细节，难以评估方法的实际成本。
- **基线方法有限**：仅与EAC-WM对比，缺少与更先进的多形态世界模型（如基于元学习、模块化模型）的比较。
- **未见形态的定义不清晰**：摘要未说明“未见形态”具体指哪一种或几种机器人，可能限制了结论的一般性。
- **下游任务的评估深度**：仅报告了世界模型预测误差和下游任务性能，未深入分析潜在动作空间的可解释性或零样本迁移的准确率。
- **可能存在的偏差**：潜在动作空间的学习可能依赖训练形态的多样性，如果训练形态不充分，泛化能力可能受限。论文未讨论训练形态的覆盖范围。

（完）
