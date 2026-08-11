<div class="dpr-home-notice-card">
  <h3 class="dpr-home-notice-title">🚀 Start Here</h3>
  <ul class="dpr-home-notice-list">
    <li><a href="#/tutorial/README">使用教程</a></li>
  </ul>
</div>

## 每次日报
- 最新运行日期：2026-08-11
- 运行时间：2026-08-11 20:32:43 UTC
- 运行状态：成功
- 本次总论文数：20
- 精读区：8
- 速读区：12

### 今日简报（AI）
今日20篇论文聚焦世界动作模型，两篇满分精读围绕视频扩散先验蒸馏与自适应执行机制；速读涉及视觉-语言-动作模型的解码、推测解码与任务规划迭代优化。核心方向：将视频生成先验迁移至世界模型，并通过执行决策提升动作预测质量。建议优先精读两篇满分论文，再结合速读材料拓展对VLA模型推理效率的理解。
- 详情：[/202608/11/README](/202608/11/README)

### 精读区论文标签
1. [Vid2WAM: Distilling Video Diffusion Priors into World Action Models](/202608/11/2608.08558v1-vid2wam-distilling-video-diffusion-priors-into-world-action-models)  
   标签：评分：10.0/10、query:human-aigc
   evidence：直接面向世界动作模型，将视频扩散先验蒸馏到WAM
2. [Rethink Before You Execute: Adaptive Execution for World Action Models](/202608/11/2608.09492v1-rethink-before-you-execute-adaptive-execution-for-world-action-models)  
   标签：评分：10.0/10、query:human-aigc
   evidence：提出TempoWAM，通过监测任务进度自适应决定WAM何时重规划
3. [GWM-VLA: Geometry-Aware Latent World Modeling for Vision-Language-Action Learning](/202608/11/2608.07619v1-gwm-vla-geometry-aware-latent-world-modeling-for-vision-language-action-learning)  
   标签：评分：9.0/10、query:vla-humanoid
   evidence：几何感知的潜在世界建模用于视觉语言动作学习
4. [LUCID: Latent-Skill Unified Control via Imagined Dynamics for Long-Horizon Humanoid Loco-Manipulation](/202608/11/2608.07746v1-lucid-latent-skill-unified-control-via-imagined-dynamics-for-long-horizon-humanoid-loco-manipulation)  
   标签：评分：9.0/10、query:human-aigc
   evidence：人形移动操作结合学习动力学世界模型与高层规划
5. [4D-WAM: Infusing Spatiotemporal Awareness into World Action Models through Trajectory Fields](/202608/11/2608.08023v1-4d-wam-infusing-spatiotemporal-awareness-into-world-action-models-through-trajectory-fields)  
   标签：评分：9.0/10、query:human-aigc
   evidence：通过轨迹场向世界动作模型注入时空感知，增强3D动态结构利用
6. [SG-WAM: Text-Grounded and Spatial-aware Semantic Guidance for World-Action Models](/202608/11/2608.08839v1-sg-wam-text-grounded-and-spatial-aware-semantic-guidance-for-world-action-models)  
   标签：评分：9.0/10、query:human-aigc
   evidence：世界行动模型，语义引导增强指令理解
7. [JEPA-WAM: Learning Vision-Language-Action Policies with Joint-Embedding World Modeling](/202608/11/2608.09381v1-jepa-wam-learning-vision-language-action-policies-with-joint-embedding-world-modeling)  
   标签：评分：9.0/10、query:human-aigc
   evidence：将潜空间转移预测与视觉-语言-动作生成耦合的潜空间世界动作模型
8. [HarnessWAM: Bridging Prediction and Deliberation in World Action Models](/202608/11/2608.09516v1-harnesswam-bridging-prediction-and-deliberation-in-world-action-models)  
   标签：评分：9.0/10、query:human-aigc
   evidence：弥合世界动作模型预测与深思差距的智能体框架

### 速读区论文标签
1. [LIRA: Local Cross-Layer Information Routing for Vision-Language-Action Decoding](/202608/11/2608.07596v1-lira-local-cross-layer-information-routing-for-vision-language-action-decoding)  
   标签：评分：8.0/10、query:vla-humanoid
   evidence：视觉-语言-动作模型解码方法
2. [WA-SpecDec: World-Aware Speculative Decoding for Vision-Language-Action Models](/202608/11/2608.08725v1-wa-specdec-world-aware-speculative-decoding-for-vision-language-action-models)  
   标签：评分：8.0/10、query:vla-humanoid
   evidence：面向闭环VLA动作生成的全局感知投机解码方法
3. [SHRIMP: Iterative Refinement of Robot Task Plans](/202608/11/2608.08884v1-shrimp-iterative-refinement-of-robot-task-plans)  
   标签：评分：8.0/10、query:vla-humanoid
   evidence：基于大语言模型从自然语言自动生成分层机器人任务计划并支持迭代修正
4. [WorldSimProbe: Diagnosing Simulator Faithfulness in Action-Conditioned World Models for Embodied Manipulation](/202608/11/2608.09298v1-worldsimprobe-diagnosing-simulator-faithfulness-in-action-conditioned-world-models-for-embodied-manipulation)  
   标签：评分：8.0/10、query:human-aigc
   evidence：面向具身操作的动作条件世界模型模拟器保真度诊断
5. [SLIM-0.5B: Learning Action-Grounded Predictive Latents for Robot Manipulation](/202608/11/2608.09771v1-slim-05b-learning-action-grounded-predictive-latents-for-robot-manipulation)  
   标签：评分：8.0/10、query:vla-humanoid
   evidence：紧凑的基于动作的预测潜在表示策略，桥接世界模型与动作生成
6. [GraphThink: Graph-Enhanced LLM Thinking for Long-Horizon Embodied Task Planning](/202608/11/2608.07905v1-graphthink-graph-enhanced-llm-thinking-for-long-horizon-embodied-task-planning)  
   标签：评分：7.0/10、query:vla-humanoid
   evidence：图增强 LLM 规划用于长时程具身任务规划
7. [Multi-modal Interactive Control of Robotic Arm based on Offline Large Language Models](/202608/11/2608.08183v1-multi-modal-interactive-control-of-robotic-arm-based-on-offline-large-language-models)  
   标签：评分：7.0/10、query:vla-humanoid
   evidence：基于离线大语言模型的多模态交互式机械臂控制
8. [Skills in Weights, Memory in Code: Hybrid Learning for Memory-Dependent Robot Manipulation](/202608/11/2608.09410v1-skills-in-weights-memory-in-code-hybrid-learning-for-memory-dependent-robot-manipulation)  
   标签：评分：7.0/10、query:vla-humanoid
   evidence：VLA操作结合编程代理进行记忆管理
9. [RoboSeg: Online Part-Level Semantic Reconstruction for Robotic Manipulation via a Single Eye-in-Hand Camera](/202608/11/2608.09778v1-roboseg-online-part-level-semantic-reconstruction-for-robotic-manipulation-via-a-single-eye-in-hand-camera)  
   标签：评分：7.0/10、query:vla-humanoid
   evidence：结合VLM功能部件发现与在线重建实现面向任务的抓取，服务机器人操作
10. [Compiling and Benchmarking Task-State Horizons for Embodied Agents](/202608/11/2608.08036v1-compiling-and-benchmarking-task-state-horizons-for-embodied-agents)  
   标签：评分：6.0/10、query:vla-humanoid
   evidence：为具身智能体的长时程任务规划评估提供基准和编译器
11. [Action- and Language-Conditioned Video Assessment for Embodied Control](/202608/11/2608.08273v1-action--and-language-conditioned-video-assessment-for-embodied-control)  
   标签：评分：6.0/10、query:vla-humanoid
   evidence：为具身控制提供视觉-语言反馈评估方法
12. [Hierarchical Fast--Slow ReAct Agent for Zero-Shot Object-Goal Navigation](/202608/11/2608.09816v1-hierarchical-fast--slow-react-agent-for-zero-shot-object-goal-navigation)  
   标签：评分：6.0/10、query:vla-humanoid
   evidence：语言模型智能体用于目标导航


<div class="dpr-home-promo-card">
  <h3 class="dpr-home-promo-title">💬 社区与支持</h3>
  <ul class="dpr-home-promo-list">
    <li>欢迎 Star / Fork / Issue / PR</li>
    <li>QQ群：583867967（欢迎交流，已有：1151人）</li>
  </ul>
</div>
