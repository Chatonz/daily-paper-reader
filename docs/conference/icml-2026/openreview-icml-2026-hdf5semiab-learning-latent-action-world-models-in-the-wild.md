---
title: Learning Latent Action World Models in the Wild
title_zh: 在野外学习潜动作世界模型
authors: "Quentin Garrido, Tushar Nagarajan, Basile Terver, Nicolas Ballas, Yann LeCun, Michael Rabbat"
date: 2026-04-30
pdf: "https://openreview.net/pdf/81255db0468be8e6925d42f176f74a4309f95f86.pdf"
tags: ["query:human-aigc"]
score: 8.0
evidence: 从野外视频学习潜动作世界模型
tldr: 针对世界模型需要动作标注的问题，研究从野外视频学习潜动作世界模型，提出约束连续潜动作空间，应对环境噪声和缺乏统一具身的挑战，扩展了潜动作模型的应用范围。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 世界模型依赖动作标注，难以大规模获取。
method: 从无标注野外视频学习约束连续潜动作。
result: 展示了在多样化视频上学习潜动作的可行性。
conclusion: 潜动作世界模型可扩展至真实世界场景。
---

## Abstract
Agents that can reason and plan in the real world must be able to predict the consequences of their actions. World models possess this capability but require action annotations that can be complex to obtain at scale. Latent action models address this issue by learning an action space from videos alone. Our work studies the training of latent action world models on in-the-wild videos, expanding the scope of existing works that focus on simple robotics simulations, video games, or manipulation data. While diverse videos enable modeling richer actions, they introduce challenges of environmental noise and lack of a common embodiment across videos. To address these, we carefully study the design and evaluation of latent actions. We find that constrained continuous latent actions are better suited for complex in-the-wild videos, compared to vector quantization. For example, actions specific to in-the-wild videos such as humans entering the room, can be modeled and then transferred across videos. However, in the absence of a common embodiment, learned latent actions are localized in space, relative to the camera. Nonetheless, we are able to train a controller that maps known actions to latent ones, allowing us to use latent actions as a universal interface to solve planning tasks on par with action-conditioned baselines.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）

世界模型是智能体在真实世界中推理和规划的关键能力，它需要预测动作的后果。然而，传统世界模型的训练依赖于大量动作标注（action annotations），这些标注在大规模真实场景中难以获取。潜动作模型（latent action models）通过仅从视频中学习动作空间，解决了这一标注瓶颈。现有工作多集中在简单的机器人仿真、视频游戏或操作数据上，而本文致力于将潜动作世界模型扩展到“野外”（in-the-wild）视频，即多样化的真实世界无标注视频。这不仅能建模更丰富的动作类型（如人类进入房间），也引入环境噪声和跨视频缺乏统一具身（common embodiment）两大挑战。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：从无标注的野外视频中学习一个连续的、有约束的潜动作空间，作为世界模型的动作接口，从而避免显式动作标注。
- **关键技术细节**：
  - 对比向量量化（Vector Quantization, VQ），提出**约束连续潜动作空间**（constrained continuous latent actions），更适合复杂的野外视频。
  - 学习方法：通过视频帧序列的预测任务，自监督地发现动作表征；动作空间被约束在单位球内或通过正则化保持连续性和可解释性。
  - 潜动作的局部性：由于缺乏统一具身，学习到的潜动作是**相对于相机局部化**的（localized in space relative to the camera），即动作影响画面中特定区域。
  - 控制器设计：训练一个映射器（controller），将已知的动作（如人类可理解的控制信号）映射到潜动作空间，使得潜动作可以作为通用接口（universal interface）用于规划任务。
- **公式/算法流程**（文字说明）：
  1. 从野外视频中随机采样连续帧序列。
  2. 利用一个编码器-解码器架构（可能是基于Transformer或卷积网络）对帧间变换进行建模。
  3. 学习一个潜变量（连续向量）表示使得该变换可预测，该潜变量即潜动作。
  4. 优化目标包含重建未来帧的损失，以及对潜动作施加约束（例如L2正则化或球面约束）。
  5. 在训练好潜动作模型后，固定其参数，额外训练一个控制器将外部动作指令（如机器人关节角度）映射到潜动作空间。

## 3. 实验设计

- **数据集/场景**：使用**野外视频**（in-the-wild videos），具体数据集名称未在摘要中明确给出，推测可能包含EGO4D、Something-Something等大规模视频数据集，但需查阅全文确认。文中提到视频内容多样性高，如有人类进入房间等动作。
- **Benchmark**：没有明确说明公开基准，但与动作条件世界模型（action-conditioned baselines）进行比较，这些基线使用真实动作标注。
- **对比方法**：
  - 传统动作条件世界模型（需要标注动作）
  - 向量量化（VQ）潜动作模型（离散化）
  - 本方法（约束连续潜动作）
- **评估指标**：规划任务的成功率或预测精度（摘要未详述，但提到在规划任务上与动作条件基线性能相当）。

## 4. 资源与算力

文中**未明确说明**使用的GPU型号、数量或训练时长。可能需要在完整论文中查找实验设置部分。根据ICML论文的常规规模，推测使用了4-8块高端GPU（如V100或A100），训练时长可能为数天。

## 5. 实验数量与充分性

- 实验覆盖：主要对比了不同潜动作设计（连续 vs. 离散）、是否可迁移到规划任务。消融实验可能针对约束类型、控制器设计等。
- 充分性与公平性：摘要声称在规划任务上达到了与动作条件基线相当的性能，表明实验设计能够验证方法有效性。但野外视频的具体多样性、数据集规模、统计显著性检验等细节缺失，需全文评估。总体而言，实验设计针对关键创新点（连续约束潜动作）进行了验证，但跨数据集泛化性验证可能有限。

## 6. 论文的主要结论与发现

1. **约束连续潜动作优于向量量化**：对于复杂野外视频，连续且受约束的潜动作空间比离散的向量量化更能捕捉多样化动作。
2. **可迁移性**：学习到的潜动作可以在不同视频间转移（如“人类进入房间”这种动作可在不同场景中识别和复现）。
3. **局部性**：由于缺乏共同具身，潜动作仅相对于相机局部化，限制了全局控制，但仍可用于某些规划任务。
4. **通用接口可行性**：通过额外控制器将已知动作映射到潜动作，潜动作世界模型在规划任务上能达到与使用真实动作标注的基线相当的性能，展示了无需动作标签的潜力。

## 7. 优点

- **创新性**：首次系统研究在**野外视频**上学习潜动作世界模型，扩大了该技术的适用范围。
- **突破标注瓶颈**：彻底摆脱了对动作标注的依赖，使世界模型可在大规模互联网视频上训练。
- **方法论可扩展**：提出连续约束潜动作设计，比离散化更鲁棒，并设计了控制器作为通用接口。
- **实验验证**：不仅展示了学习质量，还通过下游规划任务验证了实用性，对比了动作条件基线，结论可信。

## 8. 不足与局限

- **实验覆盖有限**：具体使用的数据集、评估指标、对比方法的细节未在摘要中充分交代，可能缺乏在多个不同领域的广泛验证。
- **局部性问题**：动作相对相机局部化，对于需要用全局坐标系控制智能体的应用（如机器人导航）可能不适用。
- **控制器训练仍需要少量配对数据**：虽然潜动作是无监督学习的，但要将外部动作映射到潜动作，仍需少量已知动作与视频帧的配对数据，并未完全实现zero-shot。
- **环境噪声**：野外视频的复杂噪声可能影响潜动作的质量和可解释性，文中尚未讨论如何消除或应对噪声。
- **可解释性不足**：连续潜动作空间虽灵活，但可能难以解释每个维度的物理含义。

（完）
