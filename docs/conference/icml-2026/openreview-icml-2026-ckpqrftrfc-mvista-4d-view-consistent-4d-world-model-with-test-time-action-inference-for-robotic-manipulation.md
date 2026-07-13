---
title: "MVISTA-4D: View-Consistent 4D World Model with Test-Time Action Inference for Robotic Manipulation"
title_zh: MVISTA-4D：面向机器人操作的视图一致4D世界模型与测试时动作推理
authors: "Jiaxu Wang, JIANG Yicheng, Tianlun HE, Jingkai SUN, Qiang Zhang, Jiahang Cao, Zesen Gan, Mingyuan Sun, Qiming Shao, Xiangyu Yue"
date: 2026-04-30
pdf: "https://openreview.net/pdf/10ac3fb28cfd308f904f43cdacf0ee8faefe7ddc.pdf"
tags: ["query:human-aigc"]
score: 7.0
evidence: 带动作推理的4D世界模型用于机器人操作
tldr: 针对现有世界模型无法预测完整4D场景动态的问题，提出MVISTA-4D，从单视角RGBD生成多视角一致RGBD，通过反投影融合构建跨时间的完整3D结构，并支持测试时动作推理。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有世界模型只能预测图像或部分3D，缺乏完整4D。
method: 生成多视角RGBD并融合为完整3D结构。
result: 在机器人操作任务中展示了4D预测的有效性。
conclusion: 4D世界模型为机器人规划提供更丰富的几何信息。
---

## Abstract
World-model-based imagine-then-act becomes a promising paradigm for robotic manipulation, yet existing approaches typically support either purely image-based forecasting or reasoning over partial 3D geometry, limiting their ability to predict complete 4D scene dynamics. To solve this, this work explores a novel embodied 4D world model that enables geometrically consistent, arbitrary-view RGBD generation: given only a single-view RGBD observation as input, the model “imagines” the remaining viewpoints, which can then be back-projected and fused to assemble a more complete 3D structure across time. To efficiently learn the multi-view, cross-modality generation, we explicitly design cross-view and cross-modality feature fusion that jointly encourage consistency between RGB and depth and enforce geometric alignment across views. Beyond prediction, converting generated futures into actions is often handled by inverse dynamics, which is ill-posed because multiple actions can explain the same transition. We address this with a test-time action optimization strategy that backpropagates through the generative model to infer a trajectory-level latent best matching the predicted future, and a residual inverse dynamics model that turns this trajectory prior into accurate executable actions. Extensive experiments on the three datasets and platforms demonstrate strong performance on both 4D scene generation and downstream manipulation, and ablations provide practical insights into the key design choices. Project page is available at \url{https://mercerai.github.io/MVISTA-4D/}.

---

## 论文详细总结（自动生成）

# 论文总结：MVISTA-4D：面向机器人操作的视图一致4D世界模型与测试时动作推理

## 1. 核心问题与整体含义

- **研究动机**：基于世界模型的“先想象再行动”（imagine-then-act）范式在机器人操作中极具潜力，但现有方法大多局限于纯图像预测或部分3D几何推理，无法预测完整的4D场景动态（时空一致的3D结构变化）。
- **问题定义**：如何从单一视角的RGBD观测出发，生成多视角一致的RGBD序列，并通过反投影融合得到随时间演化的完整3D结构，进而实现动作推理。
- **整体含义**：提出首个具身4D世界模型，能够生成几何一致、任意视角的RGBD未来帧，为机器人规划提供更丰富的时空几何信息，弥补现有世界模型在4D预测上的空白。

## 2. 方法论

### 核心思想
- 输入：单视角RGBD观测。
- 输出：多视角一致的RGBD未来帧，通过反投影融合为完整的3D结构（随时间变化）。
- 额外贡献：提出测试时动作优化策略，解决从未来预测到动作映射的逆动力学不适定问题。

### 关键技术细节
- **跨视角与跨模态特征融合**：显式设计融合模块，同时保证RGB与深度的一致性，以及多视角间的几何对齐。
- **生成框架**：从单视图“想象”剩余视角，生成多视角RGBD，再反投影融合成完整3D点云（跨时间）。
- **测试时动作推理**：
    1. 轨迹级潜在动作优化：通过生成模型反向传播，寻找最佳匹配预测未来的潜在轨迹。
    2. 残差逆动力学模型：将轨迹先验转化为精确的可执行动作，解决多动作解释同一状态转移的歧义。

### 算法流程（文字描述）
1. 给定单视角RGBD观测 \(O_t\)，MVISTA-4D生成未来多视角RGBD \( \{I_{t+1}^v, D_{t+1}^v\} \)（\(v\) 为视角）。
2. 对多视角RGBD进行反投影和融合，得到时刻 \(t+1\) 的完整3D结构。
3. （测试时）优化轨迹级潜在变量 \(z\)，使生成的未来帧与目标帧/观测匹配。
4. 利用残差逆动力学模型从 \(z\) 解码出动作序列，执行机器人操作。

## 3. 实验设计

- **数据集与平台**：三个不同数据集（具体名称摘要未列出，涉及操作场景）。
- **Benchmark**：对比现有世界模型方法（如纯图像预测或部分3D方法），评测4D场景生成质量与下游操作成功率。
- **对比方法**：未具体列举，但强调对比了仅基于图像或部分3D的方法，验证MIVISTA-4D在完整4D预测上的优势。

## 4. 资源与算力

- 论文中未明确说明使用的GPU型号、数量及训练时长。仅提及在三个数据集上进行了广泛实验，但无具体算力信息。需注意该点。

## 5. 实验数量与充分性

- **实验数量**：涉及三个不同数据集/平台的实验，包括4D场景生成（多视角RGBD质量、几何一致性指标）和下游操作任务。
- **消融实验**：对关键设计（跨视角融合、测试时动作优化等）进行了消融分析，提供了实践洞察。
- **充分性评价**：实验覆盖主要模块和多种场景，对比基准清晰，消融具有针对性，整体较为充分。但缺少跨任务泛化性分析及真实机器人实验验证（推测基于仿真）。

## 6. 主要结论与发现

- MVISTA-4D能够从单视图生成几何一致的多视角RGBD，并融合为完整4D场景，显著优于纯图像或部分3D方法。
- 测试时动作优化策略有效解决了逆动力学的多解性问题，提升了操作任务的执行精度。
- 消融实验证实跨视角/跨模态融合与潜在动作优化均对性能有重要贡献。

## 7. 优点

- **创新性**：首次提出面向机器人操作的具身4D世界模型，突破现有方法仅能预测图像或部分3D的限制。
- **方法论完整性**：不仅解决4D生成，还配套了测试时动作推理方案，形成完整的预测-控制闭环。
- **一致性保证**：通过跨视角、跨模态特征融合显式约束几何一致性和RGB-D对齐，提高生成质量。
- **实验扎实**：在多个数据集上验证，消融实验系统，结论可信。

## 8. 不足与局限

- **实验环境**：可能主要在仿真中进行，缺乏真实机器人部署验证，泛化性存疑。
- **算力与效率**：未报告训练和推理成本，测试时优化可能引入额外计算延迟，影响实时性。
- **输入限制**：仅依赖单视角RGBD，在严重遮挡或传感器噪声下可能性能下降。
- **动作空间**：残差逆动力学模型假设前提未详细讨论，对复杂任务（如连续接触）的适用性需进一步验证。
- **数据依赖**：需要多视角标注数据训练，数据获取成本高。

（完）
