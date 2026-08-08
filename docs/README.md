<div class="dpr-home-notice-card">
  <h3 class="dpr-home-notice-title">🚀 Start Here</h3>
  <ul class="dpr-home-notice-list">
    <li><a href="#/tutorial/README">使用教程</a></li>
  </ul>
</div>

## 每次日报
- 最新运行日期：2026-08-08
- 运行时间：2026-08-08 20:57:33 UTC
- 运行状态：成功
- 本次总论文数：17
- 精读区：7
- 速读区：10

### 今日简报（AI）
今日聚焦17篇论文，精读自动驾驶世界模型与机器人操作学习两大方向。最值得关注的是《DF$^3$》的Decoder-Free特征预测及《JoyAI-RA 0.5》的双动作对齐方法，均获9分高分。普通读者可优先浏览速读中的VLA框架（如BridgeVLA++、World-to-Wrist），理解3D操作与任务条件建模的最新趋势。
- 详情：[/202608/08/README](/202608/08/README)

### 精读区论文标签
1. [DF$^3$: World Modeling via Decoder-Free Feature Forecasting in Autonomous Navigation](/202608/08/2608.02428v1-df3-world-modeling-via-decoder-free-feature-forecasting-in-autonomous-navigation)  
   标签：评分：9.0/10、query:human-aigc
   evidence：通过无解码器特征预测进行世界建模，直接对应世界动作模型概念
2. [JoyAI-RA 0.5: Scaling Robot Manipulation Learning via Dual Action Alignment](/202608/08/2608.05674v1-joyai-ra-05-scaling-robot-manipulation-learning-via-dual-action-alignment)  
   标签：评分：9.0/10、query:human-aigc
   evidence：结合世界动力学先验与视觉语义的视觉-语言-世界-动作框架
3. [SpaceVLA: Spatially Grounded VLA for Robotic Manipulation with User-Authored Grasp and Place Anchors](/202608/08/2608.05730v1-spacevla-spatially-grounded-vla-for-robotic-manipulation-with-user-authored-grasp-and-place-anchors)  
   标签：评分：9.0/10、query:vla-humanoid
   evidence：基于OpenVLA和空间锚点从语言与标记RGB生成7自由度抓取放置动作
4. [XEWorld: Can Action-Conditioned World Models Generalize to Unseen Robot Embodiments?](/202608/08/2608.05799v1-xeworld-can-action-conditioned-world-models-generalize-to-unseen-robot-embodiments)  
   标签：评分：9.0/10、query:human-aigc
   evidence：面向机器人操作的动作条件世界模型；跨本体泛化测试平台
5. [Demystifying When and Why VLAs Fail in Contact-Rich Tasks and How to Fix Them](/202608/08/2608.01402v1-demystifying-when-and-why-vlas-fail-in-contact-rich-tasks-and-how-to-fix-them)  
   标签：评分：8.0/10、query:vla-humanoid
   evidence：剖析VLA在接触丰富操作中的失败原因并提出针对性修复，直接关系改进VLA操作
6. [Uncovering and Mitigating Positional Blind Spots in Vision-Language-Action Models](/202608/08/2608.01573v1-uncovering-and-mitigating-positional-blind-spots-in-vision-language-action-models)  
   标签：评分：8.0/10、query:vla-humanoid
   evidence：揭示VLA存在位置盲区：位置无关干扰物移动会导致失败概率剧增
7. [Explicit Language Memory for Long-Horizon Planning in Vision-Language-Action Models](/202608/08/2608.04765v1-explicit-language-memory-for-long-horizon-planning-in-vision-language-action-models)  
   标签：评分：8.0/10、query:vla-humanoid
   evidence：带显式语言记忆的VLA用于长时程规划

### 速读区论文标签
1. [BridgeVLA++: A Data-Efficient, Generalizable, and Memory-Augmented Vision-Language-Action Framework for 3D Manipulation](/202608/08/2608.05042v1-bridgevla-a-data-efficient-generalizable-and-memory-augmented-vision-language-action-framework-for-3d-manipulation)  
   标签：评分：8.0/10、query:vla-humanoid
   evidence：记忆增强的3D操作VLA框架
2. [World-to-Wrist: Task-Conditioned Future Wrist Modeling for Fine-Grained Robot Manipulation](/202608/08/2608.05369v1-world-to-wrist-task-conditioned-future-wrist-modeling-for-fine-grained-robot-manipulation)  
   标签：评分：8.0/10、query:vla-humanoid
   evidence：通过任务条件未来手腕建模实现精细机器人操作的VLA模型
3. [In-Context VLA: Endowing Vision-Language-Action Models with Language via In-Context Post-Training and Agentic Tool Use](/202608/08/2608.05738v1-in-context-vla-endowing-vision-language-action-models-with-language-via-in-context-post-training-and-agentic-tool-use)  
   标签：评分：8.0/10、query:vla-humanoid
   evidence：通过上下文后训练与智能体工具使用增强VLA
4. [Beyond Flat Policies: Hierarchical Post-Training for Embodied Agents in Robotic Manipulation](/202608/08/2608.05999v1-beyond-flat-policies-hierarchical-post-training-for-embodied-agents-in-robotic-manipulation)  
   标签：评分：8.0/10、query:vla-humanoid
   evidence：面向VLA操控策略的层次化后训练
5. [DyPES-VLA: Learning Shared Dynamics Priors and Embodiment-Specific Control for Cross-Embodiment Manipulation](/202608/08/2608.06374v1-dypes-vla-learning-shared-dynamics-priors-and-embodiment-specific-control-for-cross-embodiment-manipulation)  
   标签：评分：8.0/10、query:vla-humanoid
   evidence：面向机器人操作的跨具身VLA模型，学习共享动力学先验与具身专属控制，直接推进基于VLA的动作生成方法。
6. [Action Chunk Scheduling for Batched Robot Policy Serving](/202608/08/2608.00337v1-action-chunk-scheduling-for-batched-robot-policy-serving)  
   标签：评分：7.0/10、query:vla-humanoid
   evidence：面向批量VLA机器人策略推理的服务系统，支持视觉语言动作模型的可扩展部署
7. [Embedding Large Language Models into Flow Controls: An Agentic Framework for Adaptive and Trustworthy Automated Cooking](/202608/08/2608.04768v1-embedding-large-language-models-into-flow-controls-an-agentic-framework-for-adaptive-and-trustworthy-automated-cooking)  
   标签：评分：7.0/10、query:vla-humanoid
   evidence：利用大语言模型智能体将烹饪需求分解为可执行的机器人控制程序，进行动作生成
8. [VLAff: Vision-Language-Affordance Model for Unified Actionable Affordances](/202608/08/2608.05215v1-vlaff-vision-language-affordance-model-for-unified-actionable-affordances)  
   标签：评分：7.0/10、query:vla-humanoid
   evidence：从人类视频学习可操作可供性以支持操作技能
9. [LAWM-3D: Learning 3D-Aware Latent Actions from Human Videos for Generalizable Robot World Models](/202608/08/2608.05706v1-lawm-3d-learning-3d-aware-latent-actions-from-human-videos-for-generalizable-robot-world-models)  
   标签：评分：7.0/10、query:human-aigc
   evidence：从人类视频自监督学习3D感知潜在动作，用于机器人世界模型，与动作空间学习和世界模型泛化密切相关。
10. [SkillMemo: Expert-guided Skill Memory Framework for Compositional Embodied Manipulation](/202608/08/2608.05970v1-skillmemo-expert-guided-skill-memory-framework-for-compositional-embodied-manipulation)  
   标签：评分：7.0/10、query:vla-humanoid
   evidence：面向组合操作技能的基于技能记忆的框架，结合扩散策略与视觉-语言-动作模型


<div class="dpr-home-promo-card">
  <h3 class="dpr-home-promo-title">💬 社区与支持</h3>
  <ul class="dpr-home-promo-list">
    <li>欢迎 Star / Fork / Issue / PR</li>
    <li>QQ群：583867967（欢迎交流，已有：1151人）</li>
  </ul>
</div>
