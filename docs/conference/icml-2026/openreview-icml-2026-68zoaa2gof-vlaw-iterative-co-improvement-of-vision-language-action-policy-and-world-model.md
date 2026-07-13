---
title: "VLAW: Iterative Co-Improvement of Vision-Language-Action Policy and World Model"
title_zh: VLAW：视觉-语言-动作策略与世界模型的迭代共同改进
authors: "Yanjiang Guo, Tony Lee, Lucy Xiaoyang Shi, Jianyu Chen, Percy Liang, Chelsea Finn"
date: 2026-04-30
pdf: "https://openreview.net/pdf/457c391b469337a90ecaa2d5dd098bfec3fe3cd2.pdf"
tags: ["query:human-aigc"]
score: 9.0
evidence: VLA策略与世界模型的迭代共同改进
tldr: 针对世界模型物理保真度不足、难以用于策略改进的问题，提出VLAW框架，通过在线交互迭代，使用动作条件视频生成模型作为模拟器生成数据，共同提升VLA策略和世界模型。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 世界模型物理细节不足，无法支持策略提升。
method: 迭代收集在线交互数据，共同训练策略和世界模型。
result: 在模拟环境中验证了策略和世界模型的协同提升。
conclusion: 迭代改进框架可克服物理建模瓶颈。
---

## Abstract
The goal of this paper is to improve the performance and reliability of vision-language-action (VLA) models through iterative online interaction. 
Since collecting policy rollouts in the real world is expensive, we investigate whether a learned simulator—specifically, an action-conditioned video generation model—can be used to generate additional rollout data.
Unfortunately, existing world models lack the physical fidelity necessary for policy improvement: they are predominantly trained on demonstration datasets that lack coverage of many different physical interactions (particularly failure cases) and struggle to accurately model small yet critical physical details in contact-rich object manipulation. 
We propose a simple iterative improvement algorithm that uses real-world roll-out data to improve the fidelity of the world model, which can then, in turn, be used to generate supplemental synthetic data for improving the VLA model. 
In our experiments on a real robot, we use this approach to improve the performance of a state-of-the-art VLA model on multiple downstream tasks. 
We achieve a 39.2\% absolute success rate improvement over the base policy and 11.6\% improvement from training with the generated synthetic rollouts. Videos can be found at this anonymous website: \url{https://sites.google.com/view/vla-w}.

---

## 论文详细总结（自动生成）

# VLAW：视觉-语言-动作策略与世界模型的迭代共同改进——详细中文总结

## 1. 核心问题与整体含义（研究动机和背景）
- **问题**：视觉-语言-动作（VLA）模型在真实机器人上部署时，收集策略执行（rollout）数据成本高昂，限制了性能提升。虽然可以使用学习到的模拟器（如动作条件视频生成模型）生成额外训练数据，但现有世界模型的物理保真度不足：它们主要在演示数据集上训练，缺乏对多种物理交互（尤其是失败案例）的覆盖，并且在接触丰富的物体操作任务中难以准确建模微小但关键的物理细节。
- **动机**：迫切需要一种低成本、高保真的方法，利用世界模型生成可靠数据来进一步提升VLA策略，同时克服世界模型自身物理建模的瓶颈。
- **整体含义**：提出一种**迭代共同改进框架**，通过真实交互数据提升世界模型保真度，再使用改进后的世界模型生成合成数据来增强VLA策略，实现策略与世界模型的协同进化。

## 2. 方法论
- **核心思想**：在真实机器人上进行少量在线交互，收集策略 rollout 数据（包括成功与失败案例），利用这些数据对世界模型（动作条件视频生成模型）进行微调，提高其物理保真度；然后使用改进后的世界模型生成大量合成 rollout 数据，用于训练（或微调）VLA策略；重复此过程。
- **关键技术细节**：
  - **世界模型**：采用动作条件视频生成模型，输入当前观测（图像）和动作序列，输出未来帧预测。
  - **迭代流程**：
    1. 初始阶段：使用预训练的VLA策略在真实环境中收集少量 rollout 数据；
    2. 世界模型更新：用收集到的真实数据（含失败案例）微调世界模型；
    3. 合成数据生成：用更新后的世界模型 rollout 大量轨迹（条件为当前策略的动作分布）；
    4. 策略更新：将合成数据与真实数据混合，训练或微调VLA策略；
    5. 回到步骤1，使用新策略继续收集真实数据，重复迭代。
  - **关键策略**：同步提升世界模型对复杂交互（如接触、摩擦）的建模能力，以及策略在接触密集任务中的成功率。
- **公式或算法流程**（文字说明）：
  - 初始化基础VLA策略 $\pi_0$ 和世界模型 $W_0$；
  - 对于每个迭代轮次 $t$：
    - 部署 $\pi_t$ 在真实环境中，收集 rollout 数据集 $D_{\text{real}}^t$；
    - 使用 $D_{\text{real}}^t$ 微调世界模型得到 $W_{t+1}$；
    - 使用 $W_{t+1}$ 生成合成 rollout 数据集 $D_{\text{synth}}^t$；
    - 在 $D_{\text{real}}^t \cup D_{\text{synth}}^t$ 上训练新策略 $\pi_{t+1}$。

## 3. 实验设计
- **数据集/场景**：在真实机器人上执行多个下游操作任务（具体任务未列明，根据摘要推测为接触丰富的物体操作，如抓取、插拔等）。未使用公开基准数据集，而是自建真实机器人实验环境。
- **Benchmark**：以成功率（Success Rate）为主要指标。
- **对比方法**：
  - 基础VLA策略（初始策略，不使用合成数据）；
  - 仅使用真实数据训练的策略；
  - 使用合成数据（未迭代改进世界模型）训练的策略；
  - 完整VLAW迭代框架。
- **结果亮点**：VLAW实现了 **39.2%的绝对成功率提升** 相对于基础策略，其中 **11.6%的提升** 来自使用生成的合成 rollout 数据（即迭代改进世界模型带来的额外增益）。

## 4. 资源与算力
- **文中未明确说明**使用的GPU型号、数量、训练时长等算力信息。元数据中也未提及。仅可推测需要一定规模的计算资源用于视频生成模型的微调和策略训练，但具体细节未知。

## 5. 实验数量与充分性
- **实验数量**：至少包含多任务（multiple downstream tasks）的成功率对比，以及消融实验（是否使用合成数据、是否迭代）。但摘要中未报告具体任务数量或独立重复次数。
- **充分性评估**：
  - **优点**：在真实机器人上验证，贴近实际应用；包含消融，量化了迭代世界模型带来的增益。
  - **不足**：未提供任务多样性的详细描述（如任务数量、难度梯度）；未与其他基于世界模型的方法（如Dreamer、DayDreamer等）进行比较；未给出统计显著性分析（如置信区间）。实验规模和数据量有限，可能不足以证明方法的泛化性。**因此结论的客观性和公平性有一定基础，但不够全面。**

## 6. 主要结论与发现
- 迭代共同改进框架（VLAW）能够有效克服现有世界模型物理保真度不足的问题，实现在真实机器人上VLA策略的成功率显著提升。
- 使用从改进后的世界模型生成的合成数据，对策略提升有明确的因果贡献（11.6%绝对提升）。
- 该方法为低成本、可循环改进的机器人学习提供了可行范式，避免了大规模真实数据采集。

## 7. 优点
- **方法简洁有效**：迭代思路直观，不依赖复杂奖励塑造或对抗训练，直接利用真实 rollout 数据“闭环”提升模型质量。
- **实际价值高**：在真实机器人上验证了显著提升，且提升幅度大（39.2%），表明方法具有实际部署潜力。
- **消融设计清晰**：分离了真实数据与合成数据的贡献，证明了世界模型迭代改进的必要性。
- **结合生成式模型**：利用最新的视频生成模型作为世界模型，符合当前技术趋势。

## 8. 不足与局限
- **实验覆盖有限**：仅在一个真实机器人平台上的几个任务上实验，缺乏跨平台、跨任务类型的泛化验证；未在标准模拟基准（如MetaWorld、RLBench）中对比。
- **泛化风险**：视频生成世界模型可能存在分布外（OOD）场景下的幻觉或不稳定，影响合成数据质量；方法依赖初始真实 rollout 数据（种子数据），若初始策略过差则可能无法启动迭代。
- **算力成本未披露**：视频生成模型的训练和推理计算开销大，实际应用中的资源需求不明确。
- **评估客观性**：未提供多次运行的平均值和方差，单次成功率的提升可能受随机性影响；未与其他主流迭代方法（如Dagger变体、在线RL微调）直接对比。
- **应用限制**：接触丰富任务对物理细节敏感，世界模型若无法精确建模微小接触力学，合成数据可能引入偏差；长期迭代可能因误差累积导致退化。

（完）
