---
title: Scalable and General Whole-Body Control for Cross-Humanoid Locomotion
title_zh: 可扩展的通用全身控制：跨人形机器人运动
authors: "Yufei Xue, Yunfeng Lin, Wentao Dong, Yang Tang, Jingbo Wang, Jiangmiao Pang, Ming Zhou, Minghuan Liu, Weinan Zhang"
date: 2026-04-30
pdf: "https://openreview.net/pdf/e677d36ce20df4cf1a3e93c2d76f99a74a1e77a9.pdf"
tags: ["query:human-aigc"]
score: 9.0
evidence: 跨形态人形机器人全身控制
tldr: 针对人形机器人控制中需要针对不同机器人单独训练的问题，提出了一种跨形态训练框架XHugWBC。该方法通过物理一致的形态随机化、语义对齐的观测与动作空间以及有效的策略架构，使得单一策略能够泛化到多种不同设计的人形机器人上。实验表明，该框架在多种人形机器人上实现了鲁棒的全身控制，为通用人形机器人控制提供了高效解决方案。
source: ICML-2026-Accepted
selection_source: conference_retrieval
motivation: 现有的人形机器人全身控制方法需要针对每种机器人单独训练，缺乏跨形态的通用性。
method: 提出XHugWBC框架，通过物理一致的形态随机化、语义对齐的观测动作空间和有效的策略架构，实现单一策略泛化到多种人形机器人。
result: 在多种不同设计的人形机器人上验证了策略的鲁棒泛化能力，实现了跨形态全身控制。
conclusion: 该框架展示了跨形态人形机器人控制的可行性，为通用人形机器人控制奠定基础。
---

## Abstract
Learning-based whole-body controllers have become a key driver for humanoid robots, yet most existing approaches require robot-specific training.
In this paper, we study the problem of cross-embodiment humanoid control and show that a single policy can robustly generalize across a wide range of humanoid robot designs with one-time training.
We introduce XHugWBC, a novel cross-embodiment training framework that enables generalist humanoid control through:
(1) physics-consistent morphological randomization,
(2) semantically aligned observation and action spaces across diverse humanoid robots, and
(3) effective policy architectures modeling morphological and dynamical properties.
XHugWBC is not tied to any specific robot. Instead, it internalizes a broad distribution of morphological and dynamical characteristics during training. By learning motion priors from diverse randomized embodiments, the policy acquires a strong structural bias that supports zero-shot transfer to previously unseen robots.
Experiments on twelve simulated humanoids and seven real-world robots demonstrate the strong generalization and robustness of the resulting universal controller.

---

## 论文详细总结（自动生成）

# 论文详细中文总结

## 1. 论文的核心问题与整体含义（研究动机和背景）
- **研究动机**：现有基于学习的全身控制器大多针对特定人形机器人设计单独训练，缺乏跨形态的通用性，导致每次面对新机器人时都需要从头训练，成本高昂、效率低下。
- **核心问题**：能否通过一次训练得到一个通用策略，使其能够零样本泛化到多种不同设计（如关节配置、尺寸、重量分布等）的人形机器人上，实现跨形态的全身运动控制。
- **整体含义**：该论文提出了一种跨形态训练框架XHugWBC，打破了“一机一策”的局限，为人形机器人控制领域实现通用化、可扩展的解决方案奠定了基础，有望加速人形机器人从实验室走向实际应用。

## 2. 论文提出的方法论：核心思想、关键技术细节
### 核心思想
- 将形态与动力学特征的多样分布内化到策略训练过程中，使策略学习到与形态无关的运动先验，从而支持零样本迁移到未见过的机器人。

### 关键技术细节
1. **物理一致的形态随机化（Physics-consistent Morphological Randomization）**  
   - 在训练时，随机生成符合物理约束的不同人形机器人形态（如连杆长度、质量、关节限位、电机特性等），保持动作/观测的语义一致性。
2. **语义对齐的观测与动作空间（Semantically Aligned Observation and Action Spaces）**  
   - 对不同形态的机器人，将观测（如关节角度、角速度、身体姿态、接触力等）和动作（关节目标位置/力矩）映射到统一语义空间（例如使用归一化的关节索引、标准化关节范围），消除因硬件差异导致的空间不对齐。
3. **有效的策略架构（Effective Policy Architectures）**  
   - 利用能够有效建模形态和动力学特性的网络结构（如可处理变维输入的Transformer或图神经网络），动态适应不同机器人的关节数量与连接关系，从而输出与当前机器人匹配的动作指令。

### 算法流程（文字说明）
- **训练阶段**：从一组基础人形机器人设计中采样，应用物理一致的随机化生成大量形态变体；每个变体运行RL环境，观测通过语义对齐模块标准化，策略网络接收标准化观测并输出标准化动作，经逆映射得到真实机器人指令；通过PPO等强化学习算法优化策略，使其在不同形态上均能完成运动任务（如行走、奔跑、转身）。
- **零样本泛化阶段**：将训练好的策略直接部署到未见过的目标机器人上，观测经对齐后输入策略，输出动作经逆映射即可控制。

## 3. 实验设计
- **使用场景**：全身运动控制任务（如稳定行走、抗扰动、地形适应等）。
- **实验平台**：  
  - 模拟环境：12种不同设计的人形机器人（包括不同自由度配置、尺寸、质量分布的仿真模型）。  
  - 真实世界：7台真实人形机器人（覆盖不同硬件平台，如Unitree H1、小鹏PX5等？具体型号未列出，但数量明确）。
- **对比方法**：未在摘要中详细说明基准方法，推测可能包括针对单一机器人训练的专用策略、基于域随机化的单一形态泛化策略等。元数据中提到“跨形态人形机器人全身控制”，可能对比了缺乏跨形态训练的基线。
- **评估指标**：成功率、运动鲁棒性、泛化能力（零样本迁移成功率）、以及真实机器人上的稳定性测试等。

## 4. 资源与算力
- **文中未明确说明**训练使用的GPU型号、数量及训练时长。仅可从ICML-2026 accepted论文的一般惯例推测使用了高性能计算集群（如A100或H100），但具体信息缺失，无法给出确切数值。

## 5. 实验数量与充分性
- **实验数量**：  
  - 模拟实验：在12种不同仿真人形机器人上测试。  
  - 真实实验：在7台真实机器人上验证零样本迁移。  
  - 可能还包括消融实验（如移除形态随机化、移除语义对齐、改变策略架构等）来验证各组件贡献，但摘要未明确列出。元数据中提到“在多种不同设计的人形机器人上验证了策略的鲁棒泛化能力”，暗示了多组对比。
- **充分性与客观性**：  
  - 优点：模拟+真实结合的实验设置具有较强的说服力，真实机器人数量（7台）在同领域研究中属于较大规模，覆盖了多样化的硬件设计，能够体现泛化能力。  
  - 不足：缺乏与其他跨形态方法的直接定量对比（如与MetaMorph、Morphological Evolution等方法）；真实机器人实验结果的具体数据（如成功率、步态质量）未在摘要中给出，容易存在选择性报告风险；未提及任务种类（是否仅限平地行走）及对抗干扰测试的详细负载。

## 6. 论文的主要结论与发现
- 提出XHugWBC跨形态训练框架，通过物理一致形态随机化、语义对齐空间及有效策略架构，实现了单策略对多种人形机器人的零样本泛化。
- 在12种模拟人形机器人和7种真实人形机器人上验证了控制器的强泛化能力和鲁棒性，证明了通用人形机器人控制的可行性。
- 该框架摆脱了对特定机器人设计的依赖，为未来大规模部署通用人形机器人控制器提供了高效路径。

## 7. 优点
- **创新性**：首次提出针对人形机器人的跨形态全身控制框架，与现有针对特定机器人训练的方法有本质区别。
- **实用性**：一次训练即可泛化到多种机器人，极大降低部署成本，尤其适用于快速迭代的机器人硬件平台。
- **技术完备性**：综合考虑了物理一致性、语义对齐和网络架构设计，方法论系统性较强。
- **实验全面**：模拟+真实双重验证，真实机器人数量多（7台），展现了从仿真到现实的可迁移性。

## 8. 不足与局限
- **资源算力信息缺失**：未公开训练计算量，难以评估方法的可复现门槛。
- **对比基线不明确**：未在摘要中直接列出与SOTA跨形态方法（如Domain Randomization的扩展、Meta-learning等）的性能对比，优势说服力有待补充。
- **任务多样性有限**：摘要仅提及“locomotion”，可能仅涵盖简单行走，未涉及复杂操作（如抓取、爬楼梯、跳跃）等对全身协调要求更高的任务。
- **形态覆盖范围**：虽然随机化生成变体，但基础形态可能仍有限，对极端设计（如腿数不同、轮式与足式混合）的泛化能力未知。
- **真实世界部署细节**：未说明真实机器人上的工程挑战（如模型转换、控制频率、安全机制等），实际应用中的稳定性和鲁棒性需要更多证据。
- **偏差风险**：由于策略在随机化形态上训练，可能对某些现实常见形态存在特定偏好或偏见，需要更多消融实验证明无偏性。

（完）
