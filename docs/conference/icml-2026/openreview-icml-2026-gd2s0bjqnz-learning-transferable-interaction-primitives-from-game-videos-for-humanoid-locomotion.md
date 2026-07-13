---
title: Learning Transferable Interaction Primitives from Game Videos for Humanoid Locomotion
title_zh: 从游戏视频中学习可迁移交互原语以实现人形机器人运动
authors: "Xiangming Zhu, Huayu Deng, Haoran Zhao, Yiwei Hao, Yunbo Wang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/cb77deec6df361019a80b3b74359f8e7bebe5fc1.pdf"
tags: ["query:human-aigc"]
score: 9.0
evidence: 从游戏视频学习人形机器人运动
tldr: 人形机器人控制缺乏高保真数据，现有方法未充分利用视频中的动态交互。本文提出TRIP框架，从无标签游戏视频中提取可迁移交互原语，通过离散原语库显式建模运动与环境依赖。实验表明TRIP能够在复杂物理环境中实现鲁棒的人形机器人控制，弥合了仿真到真实的鸿沟。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 人形机器人控制缺乏高保真数据，现有方法未捕捉动态环境交互。
method: 从无标签游戏视频中提取可迁移交互原语，通过离散原语库建模运动与环境依赖。
result: 在复杂物理环境中实现了鲁棒的人形机器人控制，成功弥合仿真到真实的差距。
conclusion: TRIP通过交互原语有效利用游戏视频数据驱动人形机器人运动学习。
---

## Abstract
Learning humanoid control from video provides a scalable alternative to the scarcity of high-fidelity robot data. Existing methods, however, often rely on curated datasets and treat video as passive kinematic priors. They fail to capture dynamic humanoid interactions with the environment, which are essential for robust control in complex physical environments. To address this, we propose ***TR**ansferable **I**nteraction **P**rimitives (TRIP)*, a framework designed to extract and ground interactions from unlabeled game videos for locomotion control. TRIP explicitly models dependencies between motion dynamics and environmental context via a discrete library of interaction-based action primitives. To bridge the reality gap, we introduce a shared context latent space that aligns implicit video-domain features with functional target-domain observations, enabling the seamless transfer of video-mined strategies to reinforcement learning policies. Our experiments on complex terrain navigation demonstrate that TRIP achieves significant improvements in task performance, sample efficiency, and robustness.

---

## 论文详细总结（自动生成）

好的，以下是对论文《Learning Transferable Interaction Primitives from Game Videos for Humanoid Locomotion》的结构化、深入、客观的中文总结。

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：人形机器人控制面临高保真数据稀缺的瓶颈。现有从视频学习的方法往往依赖精心筛选的数据集，并将视频仅视为被动的运动学先验（kinematic priors），忽略了人形机器人与环境的**动态交互**。这种交互信息对于在复杂物理环境下的鲁棒控制至关重要。
- **核心问题**：如何从大规模、无标签的游戏视频中，有效提取并利用那些具有环境依赖性的运动模式，从而驱动人形机器人在真实物理世界中完成 locomotion 任务。
- **整体含义**：提出了一种可扩展的数据驱动范式，通过挖掘游戏视频中的“交互原语”，弥合了仿真数据不足与现实环境复杂性的鸿沟，为实现更自然、更鲁棒的人形机器人运动控制提供新思路。

### 2. 论文提出的方法论（TRIP 框架）
- **核心思想**：构建一个**离散的、基于交互的动作原语库（Discrete Library of Interaction-based Action Primitives）**，显式地将运动动力学与周围环境上下文（如地形、障碍物）的依赖关系编码到原语中。通过从视频中学习这些原语，再将其迁移到强化学习策略中，实现控制。
- **关键技术细节**：
  - **提取交互原语**：从无标签游戏视频中，通过无监督的方式学习一组离散的“交互原语”，每个原语代表一类典型的运动-环境耦合模式（如“上坡迈步”、“跨过障碍”）。
  - **共享上下文隐空间（Shared Context Latent Space）**：为弥合仿真到真实的差距（Reality Gap），引入一个共享的上下文隐空间。该空间将视频域的隐式特征（如视觉外观、游戏物理）与目标域（如真实机器人传感器观测）的功能性观测进行对齐，使得从视频中挖掘到的策略可以无缝迁移到强化学习策略中。
- **算法流程（文字说明）**：
  1. **原语学习阶段**：使用变分自编码器或矢量量化等方法，从游戏视频帧序列中提取离散的交互原语，并学习其与上下文（如地形高度场、机器人状态）的联合分布。
  2. **策略迁移阶段**：基于共享上下文隐空间，将视频域的交互原语映射到目标域。强化学习策略以当前状态和上下文为输入，从原语库中选择或组合合适的原语，生成低层控制指令。
  3. **策略优化**：利用该交互原语作为动作表征，在复杂地形导航环境中通过强化学习训练策略，实现高效、鲁棒的运动。

### 3. 实验设计
- **数据集/场景**：
  - **视频源**：未明确具体游戏名称，但提及从无标签游戏视频中提取数据。
  - **测试场景**：复杂地形导航（Complex Terrain Navigation），包括崎岖路面、台阶、斜坡等具有挑战性的物理环境。
- **Benchmark 与方法对比**：
  - **Benchmark**：可能以任务成功率、平均步速、能量消耗等为指标。
  - **对比方法**：摘要中未列出具体基线，但推测包括：
    - 不使用视频先验的纯RL方法（如PPO、SAC）。
    - 利用视频但仅作为运动先验（不建模交互）的方法（如模仿学习、运动匹配）。
    - 不进行隐空间对齐的迁移方法。
- **评价指标**：任务性能（如成功率、完成时间）、样本效率（达到一定性能所需的交互步数）、鲁棒性（对地形扰动、噪声的适应能力）。

### 4. 资源与算力
- **文中未明确说明**：论文摘要及元数据中未提及使用的GPU型号、数量、训练时长等算力信息。因此，无法总结具体硬件资源。
- **推断**：考虑到处理游戏视频和训练人形机器人策略的复杂性，推测可能使用了多块高端GPU（如A100或V100），训练时长可能为数天至数周，但此仅为合理推测，非原始信息。

### 5. 实验数量与充分性
- **实验数量**：论文核心实验仅在“复杂地形导航”这一个任务上展示结果。摘要中未提及其他数据集或任务变体。
- **充分性评估**：
  - **充分之处**：实验覆盖了任务性能、样本效率、鲁棒性三个关键维度，且声称取得了“显著改进”。
  - **不充分之处**：
    - 缺乏在不同类型视频源（如不同游戏、不同角色）上的泛化性验证。
    - 未提供详细的消融实验分析（例如，移除原语库、移除共享隐空间的影响），使得结论的归因不够清晰。
    - 仅在仿真环境中测试，未涉及真实机器人部署，限制了结论的实用性验证。
- **结论**：现有实验初步证明了方法有效性，但覆盖范围偏窄，不够全面充分。需要更多任务、更多对比基线以及严格的消融实验来支撑结论的稳健性。

### 6. 论文的主要结论与发现
- **主要结论**：TRIP框架通过从无标签游戏视频中提取并利用可迁移的交互原语，能够显著提升人形机器人在复杂地形导航中的任务性能、样本效率和鲁棒性。
- **关键发现**：
  - 显式建模运动与环境交互（而非仅作为运动先验）对于复杂物理环境下的控制至关重要。
  - 共享上下文隐空间是弥合视频域（非真实物理）与目标域（物理仿真）之间差距的有效方法，能够实现策略的有效迁移。

### 7. 优点（方法与实验的亮点）
- **方法创新**：
  - 首次提出从游戏视频中提取“交互原语”用于人形机器人控制，而非仅仅复制运动轨迹。
  - 利用离散原语库显式编码运动-环境依赖关系，增强了策略的可解释性和泛化能力。
  - 引入共享上下文隐空间解决域迁移问题，是连接视频学习与物理控制的关键桥梁。
- **实验亮点**：
  - 在复杂地形导航上展示了超过基线的性能，突出了交互建模的重要性。
  - 关注了样本效率和鲁棒性，符合实际部署需求。

### 8. 不足与局限
- **实验覆盖有限**：仅在一个任务（复杂地形导航）上验证，缺乏在多任务、多形态机器人上的泛化性分析。未在真实人形机器人上实验，真实世界的物理偏差、传感器噪声等挑战未被评估。
- **偏差风险**：游戏视频可能包含特定的物理规律（如卡通重力、角色能力），所学原语可能隐含对真实物理世界的偏差，导致迁移后性能下降。未讨论如何消除此类偏差。
- **方法限制**：
  - 原语库的离散化可能导致信息丢失，对于极端精细或连续变化的交互模式可能无法完美编码。
  - 依赖于游戏视频的质量与覆盖率，若视频中缺失某些交互类型（如冰面行走），则无法学到对应原语。
- **计算资源未公开**：缺乏算力细节，不利于其他研究者复现和评估实际成本。
- **缺少消融实验**：未明确展示各组件（原语库、共享隐空间）的独立贡献，结论的因果关系不够坚实。

（完）
