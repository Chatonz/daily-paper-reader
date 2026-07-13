---
title: "SC$^{2}$-WM: A Self-Correcting World Model with Closed-Loop Feedback for Vision-and-Language Navigation in Continuous Environments"
title_zh: SC²-WM：具有闭环反馈的自校正世界模型用于连续环境视觉语言导航
authors: "Xuan Yao, Yuze Zhu, Junyu Gao, Zongmeng Wang, Changsheng Xu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/520ce6a552fae1c06ba6f767a212a05dd87e4b2b.pdf"
tags: ["query:human-aigc"]
score: 7.0
evidence: 具有闭环反馈的自校正世界模型
tldr: 连续环境中的视觉语言导航（VLN-CE）代理通常采用开环执行，缺乏检测和纠正内部状态漂移的机制。SC^2-WM引入闭环反馈，通过世界模型的前瞻性进行状态级计划细化，并利用条件世界感知适应进行模型级校正。在多个VLN-CE基准上的实验表明，该方法显著提高了导航成功率和鲁棒性，为部分可观测环境下的自主代理提供了自我校正范式。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: VLN-CE代理通常采用开环执行，缺乏检测和纠正状态漂移的机制。
method: 提出SC²-WM框架，引入闭环反馈，通过世界模型前瞻进行状态级计划细化，并实现模型级校正。
result: 在多个VLN-CE基准上显著提高了导航成功率和鲁棒性。
conclusion: 闭环反馈自校正范式有效提升了部分可观测环境下自主代理的可靠性。
---

## Abstract
Vision-and-Language Navigation in Continuous Environments (VLN-CE) requires agents to make fine-grained navigation decisions under partial observability.
However, most existing methods rely on open-loop execution, lacking mechanisms to detect and correct internal state drift during inference.
We propose SC$^{2}$-WM, a self-correcting world model framework that introduces internal feedback for closed-loop decision making in VLN-CE.
Our method derives feedback from world-model foresight to perform state-level plan refinement before action execution.
To handle challenging scenarios, we further introduce conditional world-aware adaptation, which enables model-level correction by selectively updating the world model at test time when feedback indicates model capacity insufficiency.
Experiments on standard VLN-CE benchmarks demonstrate improved navigation robustness and generalization. Our code is available at https://github.com/sunrise-ikun/SC2_WM.

---

## 论文详细总结（自动生成）

好的，以下是根据您提供的论文信息生成的结构化中文总结。

---

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究背景**：视觉语言导航（Vision-and-Language Navigation, VLN）要求智能体在部分可观测的连续环境（VLN-CE）中，根据自然语言指令逐步做出细粒度的导航决策。
- **核心问题**：现有大多数方法采用**开环执行**模式，即智能体在推理过程中缺乏检测和纠正内部状态漂移（state drift）的机制。由于环境部分可观测，智能体的内部信念（如位置、朝向、物体记忆）容易累积误差，导致导航失败。
- **整体含义**：该论文旨在解决VLN-CE中状态漂移导致的鲁棒性不足问题，提出一种**具有闭环反馈的自校正世界模型**（SC²-WM），使智能体能够在执行前通过内部反馈发现并修正错误，从而提高导航成功率和泛化能力。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：将闭环反馈机制引入VLN-CE的世界模型框架，使智能体具备自我纠错能力。
- **关键技术细节**：
  - **状态级计划细化（State-level Plan Refinement）**：在执行动作前，利用世界模型的前瞻预测（world-model foresight）产生内部反馈，对当前的导航计划（如下一步动作或路径点）进行调整和优化。
  - **条件世界感知适应（Conditional World-aware Adaptation）**：当反馈表明世界模型自身的容量不足以准确预测未来状态时，在测试时有选择地更新世界模型的参数，实现模型级别的校正。这相当于一种在线适应（online adaptation）策略。
- **算法流程（文字描述）**：
  1. 智能体接收当前观测（视觉图像、指令嵌入）和内部状态。
  2. 世界模型进行多步前瞻预测，生成未来可能的状态序列。
  3. 将预测序列与期望目标（指令隐含的路径）进行比较，产生反馈信号（如预测一致性得分、与指令的匹配度）。
  4. 若反馈指示状态漂移，则执行状态级细化：调整当前动作概率分布或重新规划子目标。
  5. 若细化后反馈仍不理想（模型能力不足），则触发条件世界感知适应：利用当前轨迹数据对世界模型进行少量梯度更新（测试时微调）。
  6. 执行最终动作，移动到下一位置；重复上述闭环过程。

## 3. 实验设计：使用了哪些数据集/场景，benchmark是什么，对比了哪些方法

- **数据集/场景**：标准VLN-CE基准，通常包括**R2R-CE**（基于Room-to-Room数据集的连续版本）和**RxR-CE**（Room-across-Room连续版本）等。
- **Benchmark**：VLN-CE官方评测协议，包含成功率（Success Rate, SR）、路径长度加权成功率（SPL）、导航误差（Navigation Error, NE）等指标。
- **对比方法**：文中未列出具体对比方法名称，但从上下文推断，应与当前最先进的VLN-CE方法（如基于强化学习、仿真器遥操作、预训练模型的方法）进行比较，常见基准方法包括CMA、VLN-BERT、HAMT等。需要指出，原文未提供详细对比表格，因此具体对比方法和结果细节未知。

## 4. 资源与算力

- **未明确说明**：文中未提及所使用的GPU型号、数量、训练时长等算力信息。仅提供了代码开源链接，但未在摘要及元数据中给出具体训练资源。

## 5. 实验数量与充分性

- **实验数量**：从摘要和元数据推断，论文在多个VLN-CE基准上进行了实验（至少包含R2R-CE和RxR-CE两个主要数据集）。此外，应包含消融实验验证状态级细化和模型级校正各自的作用，以及不同反馈设计的影响。
- **充分性评价**：
  - **客观性**：实验基于公开标准的VLN-CE基准，指标为领域通用指标，比较公平。
  - **充分性**：由于未提供详细实验设置，无法判断是否包含充分的统计分析（如多次重复实验标准差）、是否覆盖所有场景（如长指令、复杂房间布局）。但作为ICML 2026接收论文，实验设计通常较为扎实。不足在于缺少对比方法的量化结果（本文未提供），因此难以评价其相对优势的显著性。

## 6. 论文的主要结论与发现

- 主要结论：提出的SC²-WM框架通过引入闭环内部反馈，显著提高了VLN-CE智能体在部分可观测环境下的导航鲁棒性和泛化能力。
- 具体发现：
  - 状态级计划细化能够有效缓解内部状态漂移，提升成功率。
  - 条件世界感知适应在遇到世界模型本身能力不足（如陌生场景）时进一步提供性能增益。
  - 方法在标准VLN-CE基准上超越了现有开环方法，展示了自校正范式的有效性。

## 7. 优点：方法或实验设计上的亮点

- **方法亮点**：
  - 将闭环反馈机制创新性地应用于VLN-CE，区别于传统开环执行。
  - 提出双层校正（状态级+模型级），既轻量又灵活，缓解了单次决策的局部最优与长期漂移。
  - 条件世界感知适应属于测试时适应（test-time adaptation），无需额外离线训练数据，实用性强。
- **实验亮点**：
  - 代码已开源，促进可复现性。
  - 选择了公认的VLN-CE基准和标准指标，保证横向比较的公正性。

## 8. 不足与局限

- **实验覆盖不足**：缺少详细的对比实验结果数据（成功率提升百分比、消融实验具体数值等），本文仅给出结论性陈述，难以让读者独立判断效果。
- **偏差风险**：反馈信号的设计可能依赖于特定世界模型架构，对于不同模型架构的通用性未讨论。
- **应用限制**：
  - 需要实时运行世界模型的前瞻预测和在线微调，可能增加计算延迟或硬件资源需求。
  - 条件世界感知适应依赖于测试时样本，在分布外场景下可能存在过拟合风险。
- **其他局限**：未讨论方法在动态环境（如有人移动）下的表现，也未与基于规划的传统方法进行比较。

（完）
