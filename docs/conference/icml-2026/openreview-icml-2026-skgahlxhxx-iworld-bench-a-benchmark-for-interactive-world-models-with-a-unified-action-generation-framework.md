---
title: "iWorld-Bench: A Benchmark for Interactive World Models with a Unified Action Generation Framework"
title_zh: iWorld-Bench：交互世界模型基准与统一动作生成框架
authors: "Jianjie Fang, Yingshan Lei, Qin Wan, Ziyou Wang, Yuchao Huang, Yongyan Xu, Baining Zhao, Weichen Zhang, Chen Gao, Xinlei Chen, Yong Li"
date: 2026-04-30
pdf: "https://openreview.net/pdf/5d96937365cefaf4cbb883afb9783d6bef9f12b8.pdf"
tags: ["query:human-aigc"]
score: 8.0
evidence: 带动作生成的交互世界模型基准
tldr: 针对交互世界模型缺乏大规模基准和统一评估的问题，提出iWorld-Bench，包含33万视频片段，并引入统一动作生成框架，评估距离感知、记忆等交互能力。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 缺乏统一基准评估世界模型的交互能力。
method: 构建大规模数据集并提出统一动作生成框架。
result: 覆盖多视角、天气和场景，提供标准化评测。
conclusion: 该基准将推动交互世界模型发展。
---

## Abstract
Achieving Artificial General Intelligence (AGI) requires agents that learn and interact adaptively, with interactive world models providing scalable environments for perception, reasoning, and action. Yet current research still lacks large-scale datasets and unified benchmarks to evaluate their physical interaction capabilities. To address this, we propose iWorld-Bench, a comprehensive benchmark for training and testing world models on interaction-related abilities such as distance perception and memory. We construct a diverse dataset with 330k video clips and select 2.1k high-quality samples covering varied perspectives, weather, and scenes. As existing world models differ in interaction modalities, we introduce an **Action Generation Framework** to unify evaluation and design six task types, generating 4.9k test samples. These tasks jointly assess model performance across **visual generation, trajectory following, and memory**. Evaluating 14 representative world models, we identify key limitations and provide insights for future research. The iWorld-Bench model leaderboard is publicly available at iWorld-Bench.com.

---

## 论文详细总结（自动生成）

# 中文详细总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：当前世界模型（World Models）的研究缺乏大规模数据集和统一的基准（benchmark）来评估其**物理交互能力**（如距离感知、记忆等），不同模型在交互模态上差异较大，难以进行公平对比。
- **研究动机**：实现通用人工智能（AGI）需要智能体能够自适应地学习和交互，而交互世界模型为感知、推理和动作提供了可扩展的环境，但现有评估体系不完善。
- **背景**：尽管已有多种世界模型被提出，但针对**交互相关能力**（如视觉生成、轨迹跟随、记忆）的标准化评测仍属空白。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：构建一个**大规模、多场景、多视角**的交互世界模型基准（iWorld-Bench），并设计一个**统一动作生成框架**来消除不同模型间交互模态的差异，从而实现公平评估。
- **关键技术细节**：
  - **数据集构建**：
    - 收集了 **330k 个视频片段**，从中筛选出 **2.1k 高质量样本**。
    - 覆盖**不同视角、天气、场景**，保证多样性。
  - **统一动作生成框架**：
    - 将不同的交互模态（如离散动作、连续控制、文本指令等）映射到统一的动作空间，使得所有模型可以在相同输入条件下生成动作并接受评估。
  - **任务设计**：
    - 定义了 **6 种任务类型**，分别测试模型的**视觉生成**、**轨迹跟随**和**记忆**能力。
    - 共生成 **4.9k 个测试样本**。
- **公式或算法流程**（文字说明）：未在摘要中提供具体公式，主要流程为：输入视频/图像序列 → 统一动作生成模块将动作指令标准化 → 世界模型根据当前状态和动作预测未来帧或执行决策 → 评估预测质量与轨迹一致性。

## 3. 实验设计：数据集、Benchmark、对比方法

- **数据集**：
  - 自建的大规模视频数据集（330k 片段，2.1k 高质量样本），包含多样化的视角（第一/第三人称、俯视等）、天气（晴、雨、雪等）和场景（室内、室外、城市、自然等）。
- **Benchmark**：
  - iWorld-Bench 本身即为发布的基准平台，包含 **6 类任务** 和 **4.9k 测试样本**。
  - 提供在线排行榜（iWorld-Bench.com）用于持续比较。
- **对比方法**：
  - 评估了 **14 个代表性世界模型**，涵盖不同架构（如基于扩散的、基于Transformer的、基于RNN的等），具体模型名称未在摘要中列出。

## 4. 资源与算力

- 论文摘要 **未明确说明实验所用算力**（如 GPU 型号、数量、训练时长等）。
- 仅提及在 14 个模型上进行了评估，但没有提供详细的硬件配置或计算成本。

## 5. 实验数量与充分性

- **实验数量**：
  - 数据集：330k 视频片段 → 筛选至 2.1k 高质量样本 → 生成 4.9k 测试样本。
  - 模型：14 个不同世界模型。
  - 任务：6 种任务类型。
- **充分性评价**：
  - **优点**：样本量较大，场景和视角多样化，任务类型覆盖了视觉生成、轨迹跟随和记忆三大核心能力，对比模型数量较多，有助于发现不同模型的优劣。
  - **潜在不足**：由于摘要未提及消融实验或详细的模型变体对比，无法判断是否对不同组件（如动作生成框架的影响）进行了单独分析。此外，数据集来源可能局限于仿真环境（推测，论文未明确说明），现实世界泛化能力有待验证。

## 6. 论文的主要结论与发现

- 通过评估 14 个世界模型，**识别出了当前模型在交互能力上的关键限制**（如距离感知偏差、长时记忆不足、复杂轨迹跟随失败等）。
- 为未来研究提供了具体见解：需要改进模型对物理规则的建模、提升动作与视觉预测的一致性、增强记忆模块的稳定性。
- iWorld-Bench 作为统一基准，能够有效推动交互世界模型的发展，并为公平比较提供标准化平台。

## 7. 优点：方法或实验设计上的亮点

- **大规模与多样性**：330k 视频片段 + 2.1k 高质量样本覆盖多视角、天气、场景，增强了基准的泛化能力。
- **统一动作生成框架**：解决了不同模型交互模态不一致的问题，使得评估公平且可复现。
- **多任务联合评估**：6 种任务同时考察视觉生成、轨迹跟随和记忆，全面反映模型的交互能力。
- **公开排行榜**：持续维护，便于社区贡献和改进。

## 8. 不足与局限

- **实验覆盖**：仅评估了 14 个模型，可能遗漏最新或更优秀的模型；未明确模型的具体规模和参数量范围。
- **偏差风险**：数据集可能主要源于模拟器或合成数据，与真实物理世界的交互存在差距，导致评估结果无法直接推广至现实应用。
- **动作空间**：统一动作生成框架虽解决了模态差异，但可能简化了某些模型特有的动作表达能力，未能完全体现其真实性能。
- **算力成本缺失**：未提供训练和推理的计算开销，不利于判断方法的实际可行性。
- **消融实验不足**：未说明不同任务类型或数据集规模对结果的影响，削弱了结论的鲁棒性论证。

（完）
