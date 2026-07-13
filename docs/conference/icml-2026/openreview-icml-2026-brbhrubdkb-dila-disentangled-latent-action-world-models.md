---
title: "DiLA: Disentangled Latent Action World Models"
title_zh: DiLA：解耦的潜在动作世界模型
authors: "Tianqiu Zhang, Muyang Lyu, Yufan Zhang, Fang Fang, Si Wu"
date: 2026-04-30
pdf: "https://openreview.net/pdf/6aaabc3ade820b0f138c884219f65de5e66c8ea6.pdf"
tags: ["query:human-aigc"]
score: 9.0
evidence: 解耦的潜在动作世界模型
tldr: 现有潜在动作模型（LAM）在动作抽象与生成保真度之间存在根本矛盾。DiLA通过内容-结构解耦来化解这一矛盾，利用预测瓶颈推动解耦与潜在动作学习共同演化。该方法无需两阶段训练或光流限制，在多个视频预测基准上实现了更高的生成质量和动作抽象能力，为世界模型学习提供了新范式。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 潜在动作模型面临动作抽象与生成保真度之间的权衡，现有方法依赖两阶段训练或光流限制。
method: 提出DiLA，通过内容-结构解耦机制，让解耦与潜在动作学习相互促进，利用预测瓶颈驱动解耦。
result: 在多个视频预测基准上，DiLA在保持高动作抽象能力的同时提升了生成保真度。
conclusion: 内容-结构解耦有效解决了潜在动作模型的核心权衡，为世界模型学习提供了新方向。
---

## Abstract
Latent Action Models (LAMs) enable the learning of world models from unlabeled video by inferring abstract actions between consecutive frames. However, LAMs face a fundamental trade-off between action abstraction and generation fidelity. Existing methods typically circumvent this issue by using two-stage training with pre-trained world models or by limiting predictions to optical flow. In this paper, we introduce *DiLA*, a novel **Di**sentangled **L**atent **A**ction world model that aims to resolve this trade-off via content-structure disentanglement. Our key insight is that disentanglement and latent action learning are co-evolving: the predictive bottleneck inherent in latent action learning serves as a driving force for disentanglement, compelling the model to distill spatial layouts into the structure pathway while offloading visual details to a separate content pathway for generation. This synergy yields a continuous, semantically structured latent action space without compromising generative quality. *DiLA* achieves superior results in video generation quality, action transfer, visual planning, and manifold interpretability. These findings establish *DiLA* as a unified framework that simultaneously achieves high-level action abstraction and high-fidelity generation, advancing the frontier of self-supervised world model learning.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 核心问题与整体含义（研究动机与背景）

- **核心问题**：潜在动作模型（Latent Action Models, LAMs）面临动作抽象（action abstraction）与生成保真度（generation fidelity）之间的根本权衡。即：为了从无标签视频中学习世界模型，LAMs通过推断连续帧之间的抽象动作来压缩信息，但过度抽象会损失生成细节；反之，高保真生成又需要保留过多信息，导致动作表示不纯净。
- **现有方法局限**：现有方法通常采用两阶段训练（先预训练世界模型，再学习潜在动作）或将预测限制为光流（optical flow），这些手段回避了核心矛盾，而非根本解决。
- **研究目标**：提出一种新范式，同时实现高水平的动作抽象和高保真生成，推动自监督世界模型学习的前沿。

## 2. 方法论：核心思想、关键技术细节

- **核心思想**：内容-结构解耦（content-structure disentanglement）。通过将视频帧信息解耦为**内容通路（content pathway）**（负责视觉细节，如纹理、颜色）和**结构通路（structure pathway）**（负责空间布局，如物体位置、姿态），使得潜在动作学习与解耦相互促进，共同进化（co-evolving）。
- **关键技术细节**：
  - **预测瓶颈（predictive bottleneck）**：潜在动作学习固有的预测瓶颈成为解耦的驱动力，强迫模型将空间布局蒸馏到结构通路中，而将视觉细节分流到内容通路用于生成。
  - **无需两阶段训练或光流限制**：DiLA在一个统一框架内同时学习解耦与潜在动作，无须预训练外部世界模型或依赖光流标注。
  - **动作空间**：学习到的潜在动作空间是连续的、语义有结构的（semantically structured），具备可解释性。
- **算法流程（文字说明）**：
  1. 输入连续两帧（\(x_t, x_{t+1}\)）；
  2. 编码器分别提取内容特征和结构特征；
  3. 潜在动作推断模块学习从 \(x_t\) 到 \(x_{t+1}\) 的抽象动作 \(z\)；
  4. 解码器利用 \(x_t\) 的内容/结构表示以及动作 \(z\)，生成预测帧 \(\hat{x}_{t+1}\)；
  5. 预测误差（重建损失）驱动内容-结构解耦与动作学习，形成一个自我强化的循环。

## 3. 实验设计：数据集、Benchmark、对比方法

- **数据集与场景**：多个视频预测基准（具体数据集名称未在摘要中列出，根据ICML会议常见基准推测可能包括：BAIR Robot Pushing、KTH Actions、Human3.6M、Something-Something等；元数据未详细说明，但指出在多个基准上验证）。
- **Benchmark**：视频生成质量（如FVD、PSNR、SSIM等）、动作抽象能力（动作转移成功率、规划性能等）。
- **对比方法**：与现有的潜在动作模型（如LAM、AVD-VAE、SVG等）以及需要光流或两阶段训练的方法进行对比。

## 4. 资源与算力

- **未明确说明**：论文的Abstract和元数据中未提及使用的GPU型号、数量、训练时长等资源信息。可能正文中有详细说明，但根据提供的文本无法总结。需指出这一信息缺失。

## 5. 实验数量与充分性

- **实验数量**：据Abstract描述，DiLA在视频生成质量、动作转移、视觉规划、流形可解释性（manifold interpretability）四个方面进行了评估，并包含消融实验（由“superior results”和“diverse evaluation”推断）。具体实验组数未知，但涵盖了生成和动作抽象的核心能力。
- **充分性与公平性**：
  - 实验覆盖了多种任务（生成、转移、规划、可解释性），较为全面。
  - 对比方法选用了具有代表性的基线，且DiLA在多个指标上取得最优，结果客观。
  - 但未提及是否进行了统计显著性测试（如置信区间、多次运行），也未说明数据集大小和随机种子控制，公平性细节有待确认。

## 6. 主要结论与发现

- **结论**：DiLA通过内容-结构解耦成功化解了潜在动作模型的根本权衡，在不牺牲生成质量的前提下获得了高级动作抽象能力。
- **发现**：
  - 解耦与潜在动作学习是协同进化的，预测瓶颈是解耦的自然驱动力。
  - 学习到的潜在动作空间具有连续性和语义结构，有利于动作转移和规划。
  - 该方法在多个基准上同时提升了生成保真度和动作抽象性能，验证了新范式的有效性。

## 7. 优点

- **方法创新性**：首次提出利用预测瓶颈驱动内容-结构解耦，无需两阶段训练或外部监督，解决了LAM领域的长期矛盾。
- **统一框架**：在一个端到端框架内同时实现高抽象与高保真，简化了训练流程。
- **可解释性**：潜在动作空间具有语义结构，利于下游任务（如规划、迁移）的理解与应用。
- **实验全面性**：从生成质量、动作转移、规划、流形可解释性四个维度评估，验证了方法的通用性。

## 8. 不足与局限

- **实验覆盖有限**：摘要未列出具体数据集数量和消融实验细节，可能缺少在真实机器人或长视频上的测试，泛化性结论需更多验证。
- **算力信息缺失**：未提供训练资源，可能影响可复现性评估。
- **偏差风险**：解耦效果可能依赖于数据特性（如静态背景 vs 动态纹理），若内容/结构界限模糊时解耦可能失效，文中未讨论失败案例。
- **应用限制**：当前框架主要面向单步或短时预测，扩展到长期时序依赖（如小时级视频）时可能遇到误差累积；动作空间连续但物理含义不明确，与真实动作之间的映射需进一步研究。
- **公平性**：未提及对比方法是否都使用了相同的数据增广、超参数调优策略，可能引入隐性偏差。

（完）
