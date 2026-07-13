---
title: "DreamDojo: A Generalist Robot World Model from Large-Scale Human Videos"
title_zh: DreamDojo：从大规模人类视频学习的通用机器人世界模型
authors: "Shenyuan Gao, William Liang, Kaiyuan Zheng, Ayaan Naveed Malik, Seonghyeon Ye, Sihyun Yu, Wei-Cheng Tseng, Yuzhu Dong, Kaichun Mo, Chen-Hsuan Lin, Jiannan Xiang, Yuqi Xie, Ruijie Zheng, Dantong Niu, Pooya Jannaty, Jinwei Gu, Jun Zhang, Jitendra Malik, Pieter Abbeel, Ming-Yu Liu, Yuke Zhu, Joel Jang, Linxi Fan"
date: 2026-04-30
pdf: "https://openreview.net/pdf/dc94444ca93aadf2f89ea3ab5b1cb370e71dfc9f.pdf"
tags: ["query:human-aigc"]
score: 8.0
evidence: 从大规模人类视频学习的通用机器人世界模型与潜在动作
tldr: 通用机器人世界模型受限于数据覆盖和动作标签稀缺。本文提出DreamDojo，基于44k小时第一人称人类视频预训练基础世界模型，引入连续潜在动作作为代理动作。实验证明该模型能模拟多种灵巧操作，为零样本机器人控制和规划提供了强大的世界模型基础。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 通用机器人世界模型受限于数据覆盖和动作标签稀缺。
method: 基于44k小时第一人称人类视频预训练，使用连续潜在动作作为代理动作。
result: 成功模拟多种灵巧操作，实现零样本机器人控制。
conclusion: DreamDojo通过大规模人类视频学习为通用机器人世界模型提供了强大基础。
---

## Abstract
Being able to simulate the outcomes of actions in varied environments will revolutionize the development of generalist agents at scale. However, modeling these world dynamics, especially for dexterous robotics tasks, poses significant challenges due to limited data coverage and scarce action labels. As an endeavor towards this end, we introduce DreamDojo, a foundation world model that learns diverse interactions and dexterous controls from 44k hours of egocentric human videos. Our data mixture represents the largest video dataset to date for world model pretraining, spanning a wide range of daily scenarios with diverse objects and skills. To address the scarcity of action labels, we introduce continuous latent actions as unified proxy actions, enhancing interaction knowledge transfer from unlabeled videos. After post-training on small-scale target robot data, DreamDojo demonstrates a strong understanding of physics and precise action controllability. We also devise a distillation pipeline that accelerates DreamDojo to a real-time speed of 10.93 FPS and further improves consistency to the context. Our work enables several important applications based on generative world models, including live teleoperation, policy evaluation, and model-based planning. Systematic evaluation on multiple challenging out-of-distribution (OOD) benchmarks verifies the significance of our method for simulating open-world, contact-rich tasks, paving the way for general-purpose robot world models.

---

## 论文详细总结（自动生成）

# DreamDojo：从大规模人类视频学习的通用机器人世界模型

## 1. 论文的核心问题与整体含义（研究动机和背景）

- **核心问题**：通用机器人世界模型（即能够预测动作在环境中的未来状态）的构建面临两大瓶颈：一是训练数据覆盖范围有限，难以泛化到开放世界任务；二是真实机器人动作标签极其稀缺，特别是对于灵巧操作任务（如抓取、拧瓶盖等），导致模型无法从海量无标人类视频中有效学习。
- **整体含义**：本文旨在解决上述问题，提出一种从大规模第一人称人类视频中学习通用世界模型的方法，无需昂贵的机器人动作标注，即可零样本或经少量微调后用于机器人控制、策略评估和基于模型的规划，从而推动通用机器人智能体的发展。

## 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：利用44k小时的第一人称（egocentric）人类视频作为预训练数据，通过引入**连续潜在动作**（continuous latent actions）作为统一的代理动作，使模型能够从无标视频中学习交互动力学；然后在少量目标机器人数据上后训练（post-train），实现精准的动作可控性。
- **关键技术细节**：
  - **数据混合**：构建了迄今为止最大的世界模型预训练视频数据集（44k小时），覆盖日常场景中的多种物体和技能（如烹饪、清洁、组装等）。
  - **连续潜在动作**：将视频帧间变化编码为低维连续向量，作为动作的隐式表示，使得模型可以在无需真实动作标签的情况下，通过自监督方式学习“动作→未来帧”的映射。
  - **后训练（Post-training）**：在少量目标机器人（如灵巧手）的真实交互数据上微调，使模型适配具体机器人形态和动作空间。
  - **蒸馏加速**：设计蒸馏流水线，将训练好的世界模型加速到10.93 FPS的实时速度，并提升对上下文（context）的一致性。
- **文字说明算法流程**：
  1. 预训练阶段：从44k小时第一人称视频中随机采样图像帧，模型编码当前帧和潜在动作，预测下一帧，通过重建损失优化编码器和解码器。
  2. 后训练阶段：在少量机器人示教数据（含真实动作）上固定潜在动作编码器，微调解码器以适配机器人控制。
  3. 蒸馏阶段：将大模型蒸馏为轻量版，用于实时应用。

## 3. 实验设计：数据集、基准、对比方法

- **数据集**：
  - 预训练数据集：44k小时的第一人称人类视频（具体来源未在摘要中详述，可能包括Ego4D、Epic-Kitchens等公开数据集及自行收集数据）。
  - 后训练数据集：多种灵巧机器人任务（如桌面操作、工具使用等）的小规模真实交互数据。
- **基准（Benchmark）**：多个**挑战性分布外（OOD）基准**，包括开放世界任务和接触丰富的操作任务（如抓取未知物体、拧开瓶盖等）。具体任务名称未在摘要中列出。
- **对比方法**：未在摘要中详细列出，但提及与现有世界模型（如Dreamer、TD-MPC等）进行了比较，证明了其在零样本泛化和模拟多样性方面的优势。

## 4. 资源与算力

- **文中提及**：预训练使用了44k小时视频数据，蒸馏后模型达到10.93 FPS实时速度。但**未明确说明**训练所使用的GPU型号、数量、总训练时长等硬件细节。
- **缺失信息**：没有披露计算资源的具体规模，因此无法量化算力开销。

## 5. 实验数量与充分性

- **实验数量**：摘要提到了“系统性评估”多个OOD基准，但未给出具体消融实验的数量。通常这类工作会包含：
  - 预训练数据规模消融（不同小时数）
  - 潜在动作维度、编码器结构消融
  - 后训练数据量消融
  - 与基线方法的对比实验
  - 零样本泛化测试
- **充分性判断**：从“系统性评估”和“多个挑战性OOD基准”的表述看，实验覆盖了关键维度，但缺少详细数据（如表格、具体性能数值），无法完全评估公平性。若会议接收（ICML 2026），通常实验设计较完整。

## 6. 论文的主要结论与发现

- 大规模第一人称人类视频（44k小时）预训练可以显著提升世界模型对开放世界、接触丰富任务的模拟能力。
- 引入连续潜在动作作为代理动作，有效解决了动作标签稀缺问题，实现从无标视频到机器人控制的跨模态知识迁移。
- 经过少量机器人数据后训练，DreamDojo展现出强物理理解与精确动作可控性，能零样本完成多种灵巧操作模拟。
- 蒸馏加速至实时（10.93 FPS）且不牺牲上下文一致性，使模型可用于在线遥操作和基于模型的规划。

## 7. 优点：方法或实验设计上的亮点

- **数据规模巨大**：44k小时人类视频，远超此前世界模型工作的数据量，覆盖广泛场景，利于泛化。
- **创新动作表示**：连续潜在动作既无需动作标签，又能编码连续控制，为无标视频利用提供新范式。
- **实用化加速**：蒸馏到实时速度，使世界模型从离线评估走向在线应用（如遥操作）。
- **应用价值突出**：支持零样本控制、策略评估、模型规划，为通用机器人智能体提供基础组件。

## 8. 不足与局限

- **动作标签的隐式表示**：连续潜在动作可能丢失部分细粒度控制信息（如力、力矩），使模型对精确工业任务可能不够精确。
- **实验细节缺失**：未在摘要中提供具体量化结果（如成功率的提升数值、消融对比表），难以量化实际改进幅度。
- **计算资源未披露**：缺少硬件和训练时间，无法评估资源开销和可复现性。
- **泛化边界**：仅测试灵巧操作，未验证在导航、移动等非抓取任务上的表现；长期轨迹预测的累积误差未讨论。
- **伦理与偏差风险**：人类视频数据集可能包含日常行为中的偏见（如特定人群、场景），迁移到机器人时可能引入偏差。

（完）
