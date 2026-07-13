---
title: Scaling Real-World Robot Policy Evaluation via Discrete Diffusion World Model
title_zh: 通过离散扩散世界模型扩展真实世界机器人策略评估
authors: "Yaxuan Li, Junjie Wen, Zhongyi Zhou, Yefei Chen, Chaomin Shen, Yaxin Peng, Yichen Zhu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/f9f17a2d33f2a4056888cb3509e53f654f9eb3a5.pdf"
tags: ["query:human-aigc"]
score: 6.0
evidence: 用于机器人策略评估的离散扩散世界模型
tldr: 现有世界模型在机器人策略评估中常出现自我纠正导致的误判和伪影。本文提出dWorldEval，以动作为中心的离散扩散世界模型，将动作视为因果驱动因素而非被动条件。在真实场景评估中，dWorldEval显著提高了评估可靠性，为大规模真实世界机器人策略评估提供了实用方案。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有世界模型在策略评估中存在自我纠正误判和伪影问题。
method: 以动作为中心的离散扩散世界模型，将动作视为因果驱动因素。
result: 在真实场景评估中显著提高了评估可靠性。
conclusion: dWorldEval通过动作因果建模提升了世界模型在策略评估中的可靠性。
---

## Abstract
Evaluating generalist robot manipulation policies is costly and difficult to scale in the real world. While emerging world models (e.g., WorldEval, Ctrl-World) offer a promising alternative, the reliability of such evaluation remains a critical bottleneck. 
Specifically, their visual predictions can undermine policy assessment by "self-correcting" failures into false positives or yielding artifacts under out-of-distribution controls.
Even with failure-enriched data, current architectures struggle to capture action-causal dynamics, as they typically treat actions as passive conditions rather than causal drivers.
To address this, we propose dWorldEval, an action-centric discrete-diffusion world model that maps visual observations, language instructions, and action chunks into a shared unified token space and denoises them with a single self-attention backbone where actions function as first-class tokens. 
To realize reliable policy-world interaction, dWorldEval introduces a sparse keyframe memory that anchors global scene state while preserving fine-grained multi-view interaction cues, and leverages Progress-as-text to jointly generate future observations and success indicators.
Extensive experiments on LIBERO, RoboTwin, and real-robot tasks demonstrate that dWorldEval significantly outperforms video diffusion baselines in action controllability, stabilizes long-horizon multi-view rollouts, enabling accurate policy ranking via automatic success estimation.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **研究动机**：在真实世界中评估通用机器人操作策略成本高昂且难以规模化扩展。现有的世界模型（如WorldEval、Ctrl-World）虽然提供了一种有前景的替代方案，但它们在策略评估中的可靠性成为关键瓶颈。具体问题包括：
  - 视觉预测会“自我纠正”失败情况，产生假阳性结果；
  - 在分布外控制下容易产生伪影；
  - 即使使用包含失败数据的数据集进行训练，当前架构也难以捕捉动作的因果动态——它们通常将动作视为被动条件而非因果驱动因素。
- **整体含义**：需要一种更可靠的世界模型，能够准确评估机器人策略，从而取代昂贵的真实世界测试，推动通用机器人策略的大规模评估。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：提出**dWorldEval**，一种以动作为中心的离散扩散世界模型。它通过将动作视为“一等令牌”（first-class tokens），而非被动条件，来建模动作与视觉观测之间的因果动态关系。
- **关键技术细节**：
  - **统一离散令牌空间**：将视觉观测、语言指令和动作块映射到共享的离散令牌空间。
  - **单自注意力骨干网络去噪**：使用单一的Transformer自注意力骨干网络对令牌进行去噪，其中动作令牌与其他令牌平等参与注意力计算，从而强调动作的因果作用。
  - **稀疏关键帧记忆**：为了在长程多视角场景中保持全局场景状态同时保留细粒度的交互线索，引入稀疏关键帧记忆，锚定全局场景状态。
  - **Progress-as-text**：将进度信息表示为文本形式，联合生成未来观测和成功指示器（即同时输出下一帧图像和是否成功的判断）。

### 3. 实验设计：数据集/场景、基准、对比方法

- **数据集与场景**：在**LIBERO**、**RoboTwin**和**真实机器人任务**上进行广泛实验。
- **基准（Benchmark）**：以策略评估的可靠性（如动作可控性、长程多视图展开的稳定性、自动成功估计的准确性）为主要评价指标。
- **对比方法**：视频扩散基线方法（如WorldEval、Ctrl-World等）。dWorldEval在动作可控性上显著优于这些基线，并能够实现通过自动成功估计对策略进行准确排序。

### 4. 资源与算力

- 论文中**未明确说明**使用的GPU型号、数量或训练时长。元数据中也未提及具体算力信息。因此无法给出具体数据，但可以指出这一点。

### 5. 实验数量与充分性

- **实验数量**：涉及三个不同数据集/场景（LIBERO、RoboTwin、真实机器人），每个场景下应该有多组比较实验。此外还有消融实验（如对稀疏关键帧记忆、Progress-as-text等组件的分析）。文中提到“extensive experiments”，但未列出具体数量。
- **充分性与公平性**：实验覆盖了模拟和真实环境，对比了最先进的视频扩散基线，结果显著优于它们。但缺乏在更多样化机器人平台或长时延任务（如24小时连续操作）上的测试。整体上实验设计较为充分，但客观性受限于作者自己提出的方法（可能存在隐式优势）。

### 6. 论文的主要结论与发现

- **主要结论**：dWorldEval通过将动作视为因果驱动因素（作为一等令牌）并采用离散扩散框架，显著提高了世界模型在真实机器人策略评估中的可靠性。它能够稳定生成长程多视角未来观测，并准确估计成功概率，从而对策略进行正确排名。
- **具体发现**：
  - 动作可控性优于视频扩散基线；
  - 在分布外控制下不产生伪影或自我纠正假阳性；
  - 自动成功估计与真实评估高度一致，可替代昂贵的真实世界测试。

### 7. 优点：方法或实验设计上的亮点

- **方法亮点**：
  - 开创性地将动作视为因果驱动因素而非被动条件，解决了世界模型中自我纠正和伪影的核心问题。
  - 离散扩散世界模型结合统一令牌空间和单自注意力骨干，架构简洁高效。
  - 稀疏关键帧记忆机制平衡了全局场景保持与细粒度交互信息。
  - “Progress-as-text”将进度信息文本化，联合生成观测和成功指示，简化了评估流程。
- **实验亮点**：
  - 覆盖模拟（LIBERO、RoboTwin）和真实机器人场景，具有较强说服力。
  - 在长程多视角展开中验证了稳定性。
  - 使用自动成功估计对策略进行排序，直接证明世界模型在策略评估中的实用性。

### 8. 不足与局限

- **实验覆盖**：仅在三个场景上测试，未涉及更多样的机器人硬件、操作任务（如灵巧手、移动操作等）或更复杂的环境（如动态障碍、人类协作）。
- **偏差风险**：对比的基线可能非最新（如Ctrl-World、WorldEval），且未与基于模型预测控制的方法或强化学习中的世界模型对比。可能存在作者自身的优势。
- **应用限制**：
  - 稀疏关键帧记忆需要手动设计关键帧选择策略，可能不适用于所有任务。
  - 离散令牌化可能丢失某些连续视觉细节。
  - 未讨论在真实世界长时运行时的计算效率和实时性。
- **资源未知**：缺乏算力信息，使得可复现性评估困难。

（完）
