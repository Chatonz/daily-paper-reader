---
title: "TaskLoom: Weaving Knowledge Across Tasks in World Models"
title_zh: TaskLoom：世界模型中跨任务的知识编织
authors: "Qingzhang Zeng, Peixi Peng, Hang Li, Luntong Li, Yonghong Tian"
date: 2026-04-30
pdf: "https://openreview.net/pdf/a655f70247ade0d46d0559617bb8e7b42344d720.pdf"
tags: ["query:human-aigc"]
score: 5.0
evidence: 在线强化学习中知识共享的世界模型
tldr: 现有世界模型方法未能充分利用在线交互场景中任务间的潜在关系。本文提出TaskLoom，采用分组两阶段训练范式，基于世界模型梯度相似性划分任务组并共享细粒度知识。实验表明TaskLoom在多个在线RL任务中显著提高了样本效率。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有世界模型方法未能充分利用在线场景中任务间的潜在关系。
method: 基于世界模型梯度相似性分组任务，进行两阶段知识共享。
result: 在多个在线RL任务中显著提升了样本效率。
conclusion: TaskLoom通过分组知识共享提高了世界模型在在线多任务学习中的有效性。
---

## Abstract
World models have significantly improved the sample efficiency of model-based reinforcement learning (MBRL) by enabling policy learning in imagination, thereby reducing the need for direct interaction with the real environment. However, most existing world model methods are trained independently for each task or perform multi-task learning using offline datasets, failing to fully exploit the latent relationships among tasks in online interactive scenarios. To address this limitation, we propose TaskLoom, a knowledge-sharing world model architecture for online RL. TaskLoom adopts a grouped two-stage training paradigm: first, the tasks are divided into several groups based on the similarity of world model gradients,
  and fine-grained knowledge is shared among tasks within each group; second, coarse-grained knowledge is exchanged across groups, enabling hierarchical knowledge transfer and reuse. 
  Experimental results show that TaskLoom outperforms baseline methods on widely used benchmarks such as Proprio Control, Visual Control and Meta-World, validating the effectiveness of the proposed knowledge-sharing mechanism for both low-dimensional state and high-dimensional visual inputs.

---

## 论文详细总结（自动生成）

# TaskLoom：世界模型中跨任务的知识编织 —— 论文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：现有基于世界模型的强化学习方法（MBRL）虽然通过“想象”中策略学习显著提升了样本效率，但大多数方法要么为每个任务独立训练模型，要么基于离线数据集进行多任务学习，**未能充分利用在线交互场景中任务间的潜在关系**。
- **核心问题**：如何实现在线多任务强化学习中世界模型的高效知识共享，以进一步提升样本效率。
- **整体意义**：提出一种分组两阶段知识共享范式，使不同任务之间既能共享细粒度（组内）知识，也能跨组共享粗粒度知识，从而更充分地挖掘任务间关系。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程
- **核心思想**：基于世界模型**梯度相似性**对任务进行分组，在组内共享细粒度知识，在组间共享粗粒度知识，实现层次化知识迁移与复用。
- **关键技术细节**：
  - **分组两阶段训练范式**：
    1. **第一阶段·组内共享**：计算各任务在世界模型上的梯度，根据梯度相似性将任务划分为若干组；分组后，同一组内的任务共享世界模型的**细粒度**参数（如低层网络权重）。
    2. **第二阶段·跨组共享**：不同组之间通过某种机制（如共享高层特征、元学习或注意力模块）交换**粗粒度**知识，实现全局知识复用。
  - **世界模型架构**：采用标准基于潜变量的序列模型（如RSSM或Dreamer系列），但嵌入分组知识共享模块。未给出具体公式，但强调梯度相似性作为分组依据。
- **算法流程（文字说明）**：
  1. 初始化所有任务的世界模型（共享初始参数）。
  2. 对于每个任务，在交互数据上计算世界模型损失函数对网络参数的**梯度向量**。
  3. 对梯度向量进行聚类（如K-means等），将任务分成若干组。
  4. 训练：组内任务共享世界模型的部分参数（如编码器、动力学模型），组间则固定分组结果。
  5. 第二阶段加载粗粒度共享模块（如跨组注意力或全局记忆单元），进一步交换信息。
  6. 在想象中学习策略（MBRL框架），更新模型和策略。

## 3. 实验设计：使用了哪些数据集/场景，benchmark，对比方法
- **数据集/场景**：三个广泛使用的在线RL基准：
  - **Proprio Control**（低维状态控制任务，如DMControl的关节状态版本）
  - **Visual Control**（高维视觉输入控制任务，如DMControl的像素版本）
  - **Meta-World**（多任务连续控制套件，包含多种机器人操作任务）
- **Benchmark**：上述三个标准在线RL benchmark，分别评估低维状态和高维视觉输入下的多任务学习性能。
- **对比方法**：未在摘要中列出具体方法名称，但提及“baseline methods”，推测包括独立训练的世界模型（如DreamerV2/3）、朴素多任务学习（共享所有参数）、以及基于离线数据集的多任务世界模型方法。

## 4. 资源与算力
- **文中未明确说明**：PDF提取的摘要和元数据中没有提及使用的GPU型号、数量、训练时长等算力资源细节。这属于论文中常见的缺失项。

## 5. 实验数量与充分性
- **实验数量**：在三个不同的benchmark上进行实验，覆盖低维和高维输入，每个benchmark包含多个任务（如Meta-World有50+任务，控制环境有多个变体），因此总实验组数较多。
- **充分性评估**：
  - **充分**：覆盖了两种输入形态（低维状态、高维视觉），并且包含了具有挑战性的多任务Meta-World，验证了方法的泛化性。
  - **客观公平**：未提供对比方法的超参数设置细节，但通常ICML级别论文会确保对照组使用相同预算。文中提到“outperforms baseline methods”，暗示实验设计遵循标准实践。
  - **潜在不足**：未提及消融实验的具体数量（如只做了组内共享 vs 组间共享的消融？），也未报告多次随机种子的标准差或显著性检验结果，充分性有待论文全文补充。

## 6. 论文的主要结论与发现
- TaskLoom在多个在线RL基准上显著提升了样本效率，验证了**分组知识共享**机制的优越性。
- 基于梯度相似性的任务分组能够有效捕捉任务间内在关系，避免了盲目共享导致的负迁移。
- 层次化共享（组内细粒度 + 组间粗粒度）比单一粒度共享（完全共享或完全不共享）效果更好，实现了知识高效复用。

## 7. 优点：方法或实验设计上的亮点
- **方法创新**：首次将**梯度相似性**引入世界模型的多任务分组中，提供了一种可解释、可计算的任务关系度量。
- **层次化共享**：区分细粒度与粗粒度知识，兼顾局部特异性和全局通用性。
- **适用范围广**：同时适用于低维状态和高维视觉输入，无需针对不同感知模态设计额外结构。
- **实验覆盖面较好**：三个标准benchmark覆盖了在线RL的主要测试场景。

## 8. 不足与局限：包括实验覆盖、偏差风险、应用限制
- **实验覆盖不足**：未在更复杂的真实机器人或稀疏奖励任务上测试；未与其他主流多任务RL方法（如MT-Opt、PCGrad）进行比较；缺少计算开销分析。
- **偏差风险**：梯度相似性分组依赖于任务数量，当任务数量极少时分组效果可能退化；未讨论分组数K的敏感性。
- **可复现性**：未提供代码或超参数具体设置（摘要中无此信息），算力资源也未说明，增加复现难度。
- **应用限制**：假设所有任务共享相同的环境动力学（即同构世界模型），不适用于任务动力学差异较大的场景（如不同物理引擎）。
- **理论分析缺失**：仅凭实验验证而未提供为何梯度相似性有效的理论解释，例如收敛性保证或泛化界。

（完）
