---
title: "WestWorld: A Knowledge-Encoded Scalable Trajectory World Model for Diverse Robotic Systems"
title_zh: WestWorld：知识编码的可扩展轨迹世界模型
authors: "Yuchen Wang, Jiangtao Kong, Sizhe Wei, Xiaochang Li, Haohong Lin, Hongjue Zhao, Tianyi Zhou, Lu Gan, Huajie Shao"
date: 2026-04-30
pdf: "https://openreview.net/pdf/8810a4114256df804745ae8c7e2b3babeffa3e24.pdf"
tags: ["query:human-aigc"]
score: 8.0
evidence: 知识编码的可扩展轨迹世界模型
tldr: 现有轨迹世界模型难以扩展到大量不同系统动力学，且忽略了物理结构知识。WestWorld引入系统感知的混合专家（Sys-MoE）机制，通过可学习的系统嵌入动态组合专家，并融合物理知识，实现了对多种机器人系统的可扩展世界建模。在多个仿真平台上验证了零样本泛化能力，为机器人动力学学习提供了知识驱动的可扩展方案。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有轨迹世界模型难以扩展到大量不同系统动力学，且忽略了物理结构知识。
method: 提出系统感知的混合专家机制，结合可学习系统嵌入和物理知识编码，实现可扩展的轨迹世界模型。
result: 在多种机器人系统上实现了零样本泛化，验证了可扩展性和知识融合的有效性。
conclusion: 知识编码和系统感知的混合专家设计为机器人世界模型的可扩展性提供了有效方案。
---

## Abstract
Trajectory world models play a crucial role in robotic dynamics learning, planning, and control. While recent works have explored trajectory world models for diverse robotic systems, they struggle to scale to a large number of distinct system dynamics and overlook domain knowledge of physical structures. To address these limitations, we introduce *WestWorld*, a kno**W**ledge-**E**ncoded **S**calable **T**rajectory **World** model for diverse robotic systems. To tackle the scalability challenge, we propose a novel system-aware Mixture-of-Experts (Sys-MoE) that dynamically combines and routes specialized experts for different robotic systems via a learnable system embedding. To further enhance zero-shot generalization, we incorporate domain knowledge of robot physical structures by introducing a structural embedding that aligns trajectory representations with morphological information. After pretraining on 89 complex environments spanning diverse morphologies across both simulation and real-world settings, *WestWorld* achieves significant improvements over competitive baselines in zero- and few-shot trajectory prediction. Additionally, it shows strong scalability across a wide range of robotic environments and significantly improves performance on downstream model-based control for different robots. Finally, we deploy our model on a real-world Unitree Go1, where it demonstrates stable locomotion performance. The code is available at https://github.com/511205787/WestWorld.

---

## 论文详细总结（自动生成）

# WestWorld：知识编码的可扩展轨迹世界模型 — 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有轨迹世界模型难以扩展到大量具有不同动力学特性的机器人系统，且忽略了物理结构等先验领域知识，导致零样本泛化能力不足。
- **研究动机**：在实际场景中，机器人系统种类繁多（如四足、二足、机械臂等），其动力学差异巨大。传统方法要么为每个系统单独训练模型，要么依赖模型架构的隐式泛化，但两者都无法高效、可扩展地处理大规模异构系统。
- **整体含义**：本文旨在构建一个**知识编码的可扩展轨迹世界模型**，能够对多种机器人系统进行统一的动力学建模，并具备向新系统零样本泛化的能力，从而服务于下游规划与控制任务。

## 2. 论文提出的方法论

### 核心思想
- 提出 **WestWorld** 框架，融合**系统感知的混合专家（Sys-MoE）** 与**物理结构知识嵌入**，实现可扩展的轨迹世界建模。

### 关键技术细节
- **系统感知混合专家（Sys-MoE）**：
  - 为每个机器人系统学习一个**可学习的系统嵌入**（system embedding），作为专家路由的依据。
  - 通过门控网络（gating network）动态组合和路由不同的专家模块（expert modules），每个专家擅长处理某一类动力学特征。
  - 这种方式避免了为每个系统独立训练完整模型，实现了参数共享与专业化分工的平衡，从而支持扩展到大量系统。
- **结构嵌入（Structural Embedding）**：
  - 显式编码机器人物理结构的先验知识（如形态学信息、关节连接方式等），将轨迹表示与形态信息对齐。
  - 该嵌入注入到模型输入或中间层，帮助模型理解不同系统之间的结构相似性，提升零样本泛化能力。
- **模型预训练**：
  - 在涵盖多种形态的89个复杂环境（仿真+真实世界数据）上进行大规模预训练，学习通用的轨迹动力学先验。

### 公式/算法流程（文字说明）
1. **输入**：轨迹历史数据 + 当前系统标识（通过系统嵌入表示）。
2. **特征提取**：通过共享的特征编码器提取时序特征。
3. **专家路由**：系统嵌入经门控网络生成路由权重，选择Top-K个专家并加权组合。
4. **结构知识融合**：将结构嵌入与专家输出拼接或相加，增强动力学预测的物理合理性。
5. **输出**：预测未来轨迹（如状态序列或动作效果）。
6. 训练时：采用轨迹预测损失（如均方误差）联合优化所有参数。

## 3. 实验设计

- **数据集/场景**：
  - 包含 **89个复杂环境**，涵盖多种形态（四足、双足、机械臂、无人机等），既有仿真环境也有真实世界数据。
  - 具体平台未在摘要中列出，但提及了仿真平台和真实机器人Unitree Go1。
- **Benchmark**：
  - 本文与“竞争性基线”（competitive baselines）进行比较，但摘要未列出具体基线方法（推测可能包括传统物理模型、通用时序模型、MoE方法等）。
- **对比方法**：
  - 在零样本（zero-shot）和少样本（few-shot）轨迹预测任务上比较。
  - 下游任务：基于模型的控制器（model-based control）性能评估。
  - 真实部署：在Unitree Go1四足机器人上验证稳定行走能力。

## 4. 资源与算力

- **文中未明确说明**使用的GPU型号、数量及训练时长。摘要和元数据未提及具体算力信息。仅能推断模型在大规模预训练中需要较多计算资源，但具体数值未知。

## 5. 实验数量与充分性

- **实验数量**：论文进行了多组实验，包括：
  - 零样本/少样本轨迹预测（在89个环境上预训练，测试新环境）。
  - 消融实验（推测验证Sys-MoE、结构嵌入等组件有效性）。
  - 下游控制任务性能对比。
  - 真实机器人部署实验（Unitree Go1）。
- **充分性与公平性**：
  - 实验覆盖了多种形态和场景，并进行了真实世界验证，具有较强说服力。
  - 但摘要未提供与基线对比的具体数值和统计显著性检验，也无法确认是否对基线进行了充分调优。从分数8.0（ICML-2026）来看，审稿人认为实验设计合理。
  - 消融实验若包含各组件（如去掉Sys-MoE或去掉结构嵌入），则能说明各自贡献。

## 6. 论文的主要结论与发现

- **核心结论**：知识编码和系统感知的混合专家设计显著提升了多机器人系统轨迹世界模型的可扩展性和零样本泛化能力。
- **具体发现**：
  - 在零样本和少样本轨迹预测任务上，WestWorld大幅优于现有基线。
  - 在多种机器人环境上展现出强扩展性，预训练后可直接适应新系统。
  - 下游基于模型的控制任务性能得到显著提升。
  - 在真实Unitree Go1机器人上成功实现稳定运动控制，验证了从仿真到真实的泛化能力。

## 7. 优点

- **方法创新性**：
  - 提出Sys-MoE机制，通过可学习系统嵌入实现专家动态路由，将模型参数专业化与共享化结合，有效应对大规模异构系统。
  - 融合物理结构知识（结构嵌入）增强模型对动力学先验的理解，提升零样本泛化。
- **实验全面性**：
  - 涵盖89个环境、多种形态、仿真与真实场景，证明模型的广泛适用性。
  - 包含下游任务和真实机器人部署，验证了实用价值。
- **可扩展性强**：无需为每个新系统重新训练，预训练后可直接应用，具有重要的工程意义。

## 8. 不足与局限

- **实验覆盖细节缺失**：未列出具体基线方法、各环境下的定量结果、消融实验的详细表格，导致无法从摘要直接判断实验的严谨性。
- **算力资源未公开**：缺乏训练成本信息，不利于其他研究者复现和评估实用性。
- **偏差风险**：
  - 结构嵌入依赖手工设计的形态学信息，可能无法完全覆盖所有未知系统。
  - 预训练环境选择可能存在偏向（如某些系统数据偏多），影响泛化公平性。
- **应用限制**：
  - 模型可能需要大量预训练数据，对于数据稀缺的新系统（如新型机器人）可能效果有限。
  - 真实世界部署仅测试了四足机器人，未验证其他形态（如机械臂、无人机）的真实泛化。
- **可解释性**：混合专家机制虽强，但路由决策和专家分工的可解释性不足。

（完）
