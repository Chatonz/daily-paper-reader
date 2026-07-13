---
title: "DDP-WM: Disentangled Dynamics Prediction for Efficient World Models"
title_zh: DDP-WM：用于高效世界模型的解耦动力学预测
authors: "Shicheng Yin, Kaixuan Yin, Weixing Chen, Yang Liu, Guanbin Li, Liang Lin"
date: 2026-04-30
pdf: "https://openreview.net/pdf/210f947dd37866814ffb7ab08ac97ee8779927ce.pdf"
tags: ["query:human-aigc"]
score: 6.0
evidence: 用于自主机器人规划的世界模型
tldr: 现有基于Transformer的世界模型计算开销大，阻碍实时部署。DDP-WM提出解耦动力学预测，将潜在状态演变为稀疏主动力学与背景更新，通过交叉注意力机制实现高效部署。实验表明在多个机器人规划任务中，DDP-WM在保持高预测精度的同时大幅降低计算成本，为实时自主规划提供了可行的世界模型方案。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有密集Transformer世界模型计算开销大，难以实时部署。
method: 提出解耦动力学预测，将状态演变为稀疏主动力学和背景更新，结合交叉注意力实现高效世界模型。
result: 在多个机器人规划任务中显著降低计算开销，保持高预测精度。
conclusion: DDP-WM通过解耦动力学预测实现了高效世界模型，适用于实时机器人规划。
---

## Abstract
World models are essential for autonomous robotic planning. However, the substantial computational overhead of existing dense Transformer-based models significantly hinders real-time deployment. To address this efficiency-performance bottleneck, we introduce DDP-WM, a novel world model centered on the principle of Disentangled Dynamics Prediction (DDP). We hypothesize that latent state evolution in observed scenes is heterogeneous and can be decomposed into sparse primary dynamics driven by physical interactions and secondary context-driven background updates. DDP-WM realizes this decomposition through an architecture that integrates efficient historical processing with dynamic localization to isolate primary dynamics. By employing a cross-attention mechanism for background updates, the framework optimizes resource allocation and provides a smooth optimization landscape for planners. Extensive experiments demonstrate that DDP-WM achieves superior efficiency and performance across diverse tasks, including navigation, precise tabletop manipulation, and complex deformable or multi-body interactions. Specifically, on the challenging Push-T task, DDP-WM achieves an approximately 9 times inference speedup and improves the MPC success rate from 90% to 98% compared to state-of-the-art dense models.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）

- **研究动机**：世界模型（World Model）是自主机器人规划的核心组件，但现有基于密集Transformer的世界模型计算开销极大，严重阻碍了实时部署。
- **核心问题**：如何在保持高预测精度的前提下，大幅降低世界模型的计算成本，使其适用于机器人的实时规划。
- **背景**：传统密集Transformer架构对所有潜在状态进行同等计算，导致效率低下；而实际场景中，潜在状态演化具有异质性（heterogeneous），并非所有部分都需要密集计算。

## 2. 提出的方法论：核心思想、关键技术细节

- **核心思想**：提出解耦动力学预测（Disentangled Dynamics Prediction, DDP）原则，将潜在状态的演化分解为两部分：
  - **稀疏主动力学（sparse primary dynamics）**：由物理交互直接驱动的关键变化区域，需要密集的处理。
  - **背景更新（secondary context-driven background updates）**：受场景上下文影响的缓慢或非关键变化区域，可用轻量级机制处理。
- **关键技术细节**：
  - 架构集成高效历史处理与动态定位模块，用于隔离主动力学区域。
  - 使用**交叉注意力机制**进行背景更新，实现资源优化分配，并为规划器提供平滑的优化景观。
  - 整体模型命名为 **DDP-WM**，通过解耦实现了效率与精度的平衡。
- **公式/算法流程**（文字说明）：
  1. 输入观测序列，编码为潜在状态。
  2. 通过动态定位模块识别当前帧中的主动力学区域（例如物体交互边界）。
  3. 对主动力学区域使用高容量模型（如稀疏Transformer）进行密集预测。
  4. 对背景区域使用交叉注意力机制融合历史上下文进行更新。
  5. 组合两部分预测结果，输出下一时刻完整潜在状态，用于规划器（如MPC）。

## 3. 实验设计

- **使用的数据集/场景**：
  - 导航任务
  - 精确桌面操作（tabletop manipulation）
  - 复杂的可变形或多体交互任务，其中最具挑战的是 **Push-T** 任务（推动T形零件）。
- **Benchmark**：未明确说明，但对比了“最先进密集模型”（state-of-the-art dense models）。
- **对比方法**：文中提到与“最先进密集Transformer模型”比较，但未列出具体方法名称（因摘要限制）。推测对比了如Dreamer、TD-MPC等密集世界模型。
- **评估指标**：推理速度（帧率加速比）、MPC（模型预测控制）成功率。

## 4. 资源与算力

- **文中有明确说明**：在Push-T任务上，DDP-WM实现了约**9倍推理加速**。
- **未明确说明**：使用的GPU型号、数量、训练时长、参数量等细节在摘要中未提供。需要阅读全文获取。

## 5. 实验数量与充分性

- **实验数量**：涵盖了四类多样化任务（导航、桌面操作、可变形/多体交互），其中Push-T作为核心挑战任务。消融实验未在摘要中提及，但合理推测应有针对解耦设计的消融（如是否使用交叉注意力、是否分解动力学等）。
- **充分性与客观性**：
  - 任务覆盖范围较广（从简单到复杂），具有一定的代表性。
  - 但缺少与其他非Transformer高效世界模型（如基于RNN或CNN的）的对比，可能不够全面。
  - 唯一数值结果是Push-T上的推理加速和MPC成功率提升，其他任务是否类似未量化说明，证据强度有限。

## 6. 主要结论与发现

- DDP-WM通过解耦动力学预测，在多个机器人规划任务上显著降低了计算开销（例如Push-T上9倍加速）。
- 同时保持了高预测精度，甚至提升了MPC成功率（从90%提升到98%）。
- 表明稀疏主动力学+背景更新机制是解决世界模型效率瓶颈的有效途径，适用于实时机器人规划。

## 7. 优点

- **方法创新性强**：将状态演化分解为主动力学和背景更新，符合物理场景的异质性，避免了密集计算的浪费。
- **效率提升显著**：特别在复杂任务（如Push-T）上达到约9倍加速，为实时部署提供了可能。
- **精度不降反升**：MPC成功率提升8个百分点，说明解耦同时优化了规划质量。
- **交叉注意力机制用于背景更新**：既节约计算又平滑了优化景观，对规划器友好。

## 8. 不足与局限

- **实验覆盖有限**：仅从摘要可知四个任务，缺乏更细粒度的消融（如不同解耦策略的影响、不同背景更新机制比较）。
- **对比方法不充分**：未列出具体对比算法名称，也未与轻量级RNN/CNN世界模型比较，结论的普适性待验证。
- **资源信息缺失**：未报告GPU型号、训练时间、模型参数量等关键细节，难以评估实际部署成本。
- **应用限制**：解耦依赖于主动力学定位模块的准确性，在高度动态或无明显运动分界的场景中可能失效；目前仅验证于机器人规划，其他领域（如自动驾驶、视频预测）未测试。
- **偏差风险**：可能只在特定环境和任务（如Push-T）上优势明显，泛化性需更多实验支撑。

（完）
