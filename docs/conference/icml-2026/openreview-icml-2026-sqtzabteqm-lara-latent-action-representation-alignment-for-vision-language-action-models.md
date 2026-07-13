---
title: "LARA: Latent Action Representation Alignment for Vision-Language-Action Models"
title_zh: LARA：面向视觉-语言-动作模型的潜在动作表示对齐
authors: "Mengya Liu, Baoxiong Jia, Jiangyong Huang, Jingze Zhang, Siyuan Huang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/37eb500cec6180869cf028e0fc04b5315f63de01.pdf"
tags: ["query:human-aigc"]
score: 5.0
evidence: 面向VLA模型的潜在动作表示对齐
tldr: 潜在动作模型与VLA模型分开训练导致表示不匹配。本文提出LARA，通过表示对齐联合优化两者，使潜在动作模型更好服务于VLA训练。实验利用未标注人类视频，有效提升了VLA在机器人任务上的表现。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 潜在动作模型与VLA模型独立训练导致表示不匹配。
method: 通过表示对齐联合优化潜在动作模型与VLA模型。
result: 在多个机器人任务上通过未标注人类视频提升了VLA性能。
conclusion: LARA通过联合对齐有效增强了VLA模型利用未标注视频的能力。
---

## Abstract
Visual-language-action (VLA) models enable robots to predict actions directly from observations and language instructions, but their performance depends on large-scale, high-quality data and is limited by the scarcity of real-world robot action datasets. To facilitate VLA model learning with abundant unlabeled human videos, Latent Action Models (LAM) learn latent action representations from visual dynamics to provide additional supervision for VLA learning. However, LAM and VLA are typically trained separately, leaving LAM ungrounded during VLA training and VLA models constrained by frozen LAM representations. To address these issues, we propose Latent Action Representation Alignment (LARA), a plug-and-play framework that jointly optimizes LAM and VLA via representation alignment. This enables reciprocal benefits where LAMs learn with action trajectories to avoid spurious visual changes, while VLAs are regularized by forward dynamics learned within LAMs to reduce hallucinations of functionally ineffective trajectories. We demonstrate LARA's versatility and effectiveness for pre-training, post-training enhancement of pre-trained VLA models, and LAM refinement, achieving an average of ~10%, ~5%, and ~15% improvement over 3 simulation and 1 meticulously designed real-world robotic manipulation benchmarks.  The code is publicly available at https://github.com/lmy1001/LARA.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）

- **动机**：视觉-语言-动作（VLA）模型在机器人任务中直接根据观察和语言指令预测动作，但其性能高度依赖大规模、高质量的真实机器人动作数据，而这类数据获取成本高、稀缺。
- **现有方案**：潜在动作模型（LAM）从大量未标注的人类视频中学习潜在动作表示，为VLA提供额外监督信号，以缓解数据不足问题。
- **关键缺陷**：LAM与VLA通常分开独立训练，导致两者表示不一致——LAM在VLA训练过程中未能接地（ungrounded），VLA被冻结的LAM表示限制，无法充分利用前向动力学信息，容易产生功能无效的轨迹幻觉。
- **本文目标**：提出**LARA**（Latent Action Representation Alignment），通过表示对齐联合优化LAM和VLA，使两者相互受益，增强VLA利用未标注人类视频的能力。

### 2. 论文提出的方法论：核心思想、关键技术细节

- **核心思想**：将LAM和VLA的表示对齐纳入联合训练框架，实现双向正则化：
  - LAM受到VLA提供的真实动作轨迹约束，避免只关注视觉变化而学习到虚假的潜在动作。
  - VLA受到LAM内嵌的前向动力学模型正则化，减少对功能无效轨迹的幻觉，提升动作预测的物理合理性。
- **框架特点**：即插即用（plug-and-play），可灵活应用于VLA的预训练、后训练增强以及LAM自身的细化（refinement）。
- **关键技术细节**（文字说明）：
  - 定义对齐损失函数，促使LAM的潜在动作表示与VLA的动作输出在共享潜在空间中一致。
  - 联合训练过程中，VLA利用LAM的前向动力学预测作为辅助损失，LAM则利用VLA的真实动作轨迹更新自身的表示学习。
  - 整体优化目标包括原始VLA损失、LAM损失以及对齐约束项，确保两者协同演进。

### 3. 实验设计：数据集/场景、基准、对比方法

- **实验场景**：3个仿真机器人操作基准（如MetaWorld、RLBench等，具体名称摘要未列出） + 1个精心设计的真实世界机器人操作基准。
- **评估设置**：涵盖三种应用模式：
  - **预训练**：从头联合训练LAM+VLA，在仿真基准上平均提升约10%。
  - **后训练增强**：对已预训练的VLA模型进行联合微调，平均提升约5%。
  - **LAM细化**：单独优化LAM表示后用于下游VLA，平均提升约15%。
- **对比方法**：尽管摘要未列出具体基线，但可推断包括未使用LAM的VLA基线、独立训练的LAM+VLA流水线、以及常见的其他表示对齐方法（如直接拼接、固定LAM表示等）。实验设计具有代表性。

### 4. 资源与算力

- 论文摘要及元数据中**未明确说明**使用的GPU型号、数量或训练时长。需注意：部分ICML论文可能会在附录补充算力信息，但当前信息不足，无法总结。

### 5. 实验数量与充分性

- **实验数量**：在3个仿真 + 1个真实基准上进行了评估，每种设置（预训练、后训练增强、LAM细化）均报告了平均改进幅度。此外，消融实验（如不同对齐方式、损失权重等）很可能存在，但摘要未详细列举。
- **充分性评价**：
  - **优点**：覆盖了从零训练、微调预训练模型到单独优化LAM的多种实际使用场景，真实机器人实验增加了可信度。
  - **客观公平**：使用公开基准和平均性能提升，但未提供标准差或统计显著性检验。对比方法缺少显式罗列，可能导致读者难以判断公平性。整体而言实验较为充分。

### 6. 论文的主要结论与发现

- LARA通过联合表示对齐，有效解决了LAM和VLA独立训练导致的表示不匹配问题。
- 联合优化使LAM能利用动作轨迹避免虚假视觉变化，同时VLA利用前向动力学正则化减少无效轨迹幻觉。
- 在多个机器人操作基准上，LARA显著提升了VLA的性能（预训练+10%、后训练+5%、LAM细化+15%），证明了其通用性和有效性。
- LARA是一个即插即用框架，可轻松集成到现有VLA训练流程中。

### 7. 优点：方法或实验设计上的亮点

- **即插即用**：无需修改VLA或LAM内部架构，可直接应用于多种训练阶段。
- **双向受益**：对齐不仅提升VLA，也改善LAM的表示质量，形成良性循环。
- **利用未标注数据**：充分挖掘海量人类视频的价值，降低了VLA对真实机器人数据的依赖。
- **实验覆盖全面**：同时评估了预训练、后训练增强和LAM细化三种模式，且包含真实机器人实验，验证了实际可行性。

### 8. 不足与局限

- **算力信息缺失**：未报告训练所需GPU资源，不利于其他研究者复现和评估成本。
- **对比基线不透明**：摘要未列出具体对比方法（如是否与最先进的VLA模型比较），读者难以判断提升是否来自架构优势或基线较弱。
- **真实场景单一**：仅1个真实机器人基准，且未说明任务复杂度和多样性，泛化性有待进一步验证。
- **潜在偏差风险**：依赖特定的LAM和VLA实现方式（如基于Transformer），若底层架构更换，对齐效果可能变化。
- **评估指标**：仅报告平均性能提升，未提供标准差或置信区间，统计显著性不明确。

（完）
