---
title: Benchmarking World-Model Learning with Environment-Level Queries
title_zh: 用环境级查询评估世界模型学习
authors: "Archana Warrier, Dat Nguyen, Michelangelo Naim, Moksh Jain, Yichao Liang, Karen Schroeder, Cambridge Yang, Joshua B. Tenenbaum, Sebastian Josef Vollmer, Kevin Ellis, Zenna Tavares"
date: 2026-04-30
pdf: "https://openreview.net/pdf/8ec5ad37706b20488c075347fc3907d08e92b338.pdf"
tags: ["query:human-aigc"]
score: 4.0
evidence: 用环境级查询评估世界模型学习
tldr: 现有世界模型评估仅关注观察轨迹上的可测量属性，如下一帧预测，未能测试模型对环境的全局理解。WorldTest提出了一种评估协议，通过环境级查询（如全局结构和反事实后果）来检验世界模型的质量。该方法为世界模型学习提供了更全面的基准，推动了更通用世界模型的发展。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有世界模型评估局限于观察到轨迹上的属性，不能检验模型对环境的全局理解。
method: 提出WorldTest评估协议，利用环境级查询（如全局结构和反事实问题）来全面评估世界模型。
result: 在多个环境上验证了该协议的有效性，揭示了现有世界模型在全局理解上的不足。
conclusion: 环境级查询评估为世界模型学习提供了更全面的基准，有助于推动通用世界模型的发展。
---

## Abstract
World models are central to building AI agents capable of flexible reasoning and planning. Yet current evaluations (i) test only properties measurable from observed interactions, such as next-frame prediction or task return, and (ii) do not test whether a learned model supports diverse queries about the environment. 
      In contrast, humans build *general-purpose* models that can answer many different questions about an environment—including questions that require understanding global structure and counterfactual consequences.
      We propose *WorldTest*: a protocol for evaluating whether agents learn models that support multiple *environment-level queries*—questions whose answers depend on properties of the full environment, not just observed trajectories.
      Individually, these queries can target properties (e.g., reachability or the effects of interventions) that no single rollout distribution determines. Collectively, they assess model generality across query types.
      We instantiate WorldTest as *AutumnBench*, a benchmark of 43 interactive grid-world environments and 129 tasks across three query families for both humans and learning agents.
      Experiments with 517 human participants and five frontier models on AutumnBench show that humans substantially outperform these models, a gap we attribute to differences in exploration and belief updating.

---

## 论文详细总结（自动生成）

# 详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：现有世界模型评估方法仅关注从观测交互中可测量的属性（如下一帧预测、任务回报），未能检验模型对环境的全局理解能力。人类能够构建通用模型，回答关于环境的多种不同问题（包括全局结构和反事实后果），而当前评估协议无法衡量智能体是否学到了这种通用性。
- **研究动机**：推动世界模型学习向更通用方向发展，需要建立一种能全面评估模型对环境整体理解的新协议，而不仅仅局限于局部轨迹上的表现。
- **整体含义**：论文旨在通过引入“环境级查询”（environment-level queries）来评估世界模型，为构建灵活推理和规划的人工智能体提供更可靠的基准。

## 2. 论文提出的方法论：核心思想、关键技术细节、公式或算法流程

- **核心思想**：提出 **WorldTest** 评估协议，通过要求智能体回答多种环境级查询来测试世界模型的质量。这些查询的答案依赖于整个环境的属性（如可达性、干预效果等），而不是仅依赖观测轨迹。单个查询的答案可能无法由任何单一轨迹分布确定，但多个查询的组合能全面评估模型的泛化能力。
- **关键技术细节**：
  - 定义三类查询家族（具体类型未在摘要中详述，但暗示包括全局结构查询和反事实后果查询）。
  - 设计交互式网格世界环境，允许智能体通过探索收集信息，然后回答查询。
  - 评估协议包括：让智能体先在环境中交互（探索），然后提出一系列环境级查询，计算回答准确率。
  - 与人类参与者的行为进行对比，分析差距来源（探索策略和信念更新差异）。
- **算法流程**（文字说明）：
  1. 构建一个交互式网格世界环境（共43个环境）。
  2. 智能体（或人类）在环境中自由探索一定步数。
  3. 探索阶段结束后，智能体被提出多个环境级查询（共129个任务，分布在三个查询家族中）。
  4. 记录智能体的回答，与真实环境状态进行对比，计算准确率。
  5. 对比不同模型和人类的表现。

## 3. 实验设计：使用的数据集/场景、Benchmark、对比方法

- **数据集/场景**：**AutumnBench**——包含43个交互式网格世界环境，以及129个任务（属于三个查询家族）。这些环境具有不同的结构和复杂性。
- **Benchmark**：WorldTest 协议本身即为提出的评估基准，AutumnBench 是其具体实现。
- **对比方法**：
  - **人类参与者**：517名人类被试，在相同环境下进行探索和回答查询。
  - **五个前沿模型**（frontier models）：具体模型名称未在摘要中列出，可能包括当前主流的强化学习或世界模型学习算法（如 Dreamer、MuZero 等变种）。

## 4. 资源与算力

- **未明确说明**：摘要和元数据中未提及使用了多少GPU、训练时长或具体硬件型号。仅提到在人类和五个前沿模型上进行了实验，但未提供模型的训练资源细节。这可能是因为论文重点在于评估协议，而非模型训练本身。

## 5. 实验数量与充分性

- **实验数量**：
  - 环境数：43个网格世界。
  - 任务数：129个（每个环境可能对应多个查询任务）。
  - 人类参与者：517人。
  - 对比模型：5个前沿模型。
- **充分性评估**：
  - **覆盖度**：环境数量较多（43个），任务种类多样（3个查询家族），人类样本量充分（517人），对比模型数合理（5个）。实验设计考虑了人类基线，有助于衡量模型不足。
  - **公平性**：人类和模型使用相同的环境和查询协议，对比客观。但未提及是否对模型进行了相同探索步数的限制，若人类探索策略更优，可能存在不公平（但论文将此作为分析点）。
  - **消融实验**：未提及是否存在消融研究（如不同查询家族的影响、探索步数的影响等），可能实验设计较为基础。
  - 总体而言，实验在评估协议层面是充分的，但缺乏对模型内部机制的深入剖析。

## 6. 论文的主要结论与发现

- 人类在 AutumnBench 上的表现显著优于五个前沿模型。
- 人类与模型之间的差距主要源于探索策略和信念更新方式的差异（人类能更高效地探索环境并更新对全局结构的理解）。
- 现有世界模型在回答环境级查询方面存在全面不足，说明它们缺乏对环境的全局理解能力。
- 环境级查询评估为世界模型学习提供了更全面的基准，有助于推动通用世界模型的发展。

## 7. 优点：方法或实验设计上的亮点

- **创新性**：首次系统提出使用“环境级查询”来评估世界模型，超越了传统的下一帧预测或任务回报评估，直击模型的全局理解能力。
- **人类基线**：引入大规模人类实验（517人），为模型性能提供了有力参照，并揭示了人类与模型在探索和信念更新上的关键差异。
- **多查询家族**：涵盖三个不同性质的查询类型，避免单一指标偏颇，能更全面地反映模型能力。
- **交互式环境**：AutumnBench 设计为网格世界，便于控制变量和重复实验，同时保持一定的复杂度。

## 8. 不足与局限

- **实验覆盖有限**：仅使用了网格世界环境（43个），未涉及更复杂的连续控制或3D环境，可能限制结论的泛化性。
- **模型选择不明确**：未列举具体五个前沿模型的名称和配置，读者无法复现或判断模型代表性；也未提供模型的训练过程，是否经过专门针对世界模型学习的训练不得而知。
- **缺乏消融研究**：未分析不同查询家族对评估结果的影响，也未探究探索步数、模型架构等变量对性能的影响。
- **偏差风险**：人类在网格世界中的直觉可能优于模型，但实际应用场景中模型可能通过大量预训练获得优势；人类实验的参与者背景未知（如是否为AI领域专家或普通群众），可能引入偏差。
- **应用限制**：该协议要求环境完全可观测或可交互，对于部分可观测或高风险环境（如自动驾驶），探索成本高昂，直接应用受限。

（完）
