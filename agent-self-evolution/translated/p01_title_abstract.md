# 自进化智能体综述

**Self-Evolving Agents 调研：迈向人工超级智能之路的演进时机、方式与前景**

Huan-ang Gao<sup>γ†</sup>, Jiayi Geng<sup>α†</sup>, Wenyue Hua<sup>ϵ†</sup>, Mengkang Hu<sup>ω†</sup>, Xinzhe Juan<sup>σµ†</sup>, Hongzhang Liu<sup>ξ†</sup>, Shilong Liu<sup>α†</sup>, Jiahao Qiu<sup>αδ†</sup>, Xuan Qi<sup>γ†</sup>, Qihan Ren<sup>σ†</sup>, Yiran Wu<sup>ρ†</sup>, Hongru Wang<sup>k†✉</sup>, Han Xiao<sup>τ†</sup>, Yuhang Zhou<sup>λ†</sup>, Shaokun Zhang<sup>ρ†</sup>, Jiayi Zhang<sup>π</sup>, Jinyu Xiang, Yixiong Fang<sup>θ</sup>, Qiwen Zhao<sup>ζ</sup>, Dongrui Liu<sup>σ</sup>, Cheng Qian<sup>β</sup>, Zhenhailong Wang<sup>β</sup>, Minda Hu<sup>τ</sup>, Huazheng Wang<sup>η</sup>, Qingyun Wu<sup>ρ</sup>, Heng Ji<sup>β</sup>, Mengdi Wang<sup>αδ✉</sup>

<sup>α</sup> Princeton University, <sup>δ</sup> Princeton AI Lab, <sup>γ</sup> Tsinghua University, <sup>θ</sup> Carnegie Mellon University, <sup>ξ</sup> University of Sydney, <sup>σ</sup> Shanghai Jiao Tong University, <sup>ρ</sup> Pennsylvania State University, <sup>µ</sup> University of Michigan, <sup>η</sup> Oregon State University, <sup>τ</sup> The Chinese University of Hong Kong, <sup>λ</sup> Fudan University, <sup>π</sup> The Hong Kong University of Science and Technology (Guangzhou), <sup>ω</sup> The University of Hong Kong, <sup>ϵ</sup> University of California, Santa Barbara, <sup>ζ</sup> University of California San Diego, <sup>k</sup> University of Edinburgh, <sup>β</sup> University of Illinois Urbana-Champaign

arXiv:2507.21046v4 [cs.AI] 16 Jan 2026

Published in Transactions on Machine Learning Research (01/2026)

Github Repo: https://github.com/CharlesQ9/Self-Evolving-Agents

<sup>†</sup> Equal contribution and the order is determined alphabetically, <sup>✉</sup> Corresponding Author

Reviewed on OpenReview: https://openreview.net/forum?id=CTr3bovS5F

---

## 摘要

大型语言模型（Large Language Models, LLMs）在各类任务中展现出了卓越的能力，但其本质上是静态的——无法根据新任务、不断发展的知识领域或动态变化的交互环境来调整自身内部参数。随着 LLMs 日益广泛地部署于开放式、交互式环境中，这种静态特性已成为一个关键瓶颈，迫切需要能够实时自适应推理、行动和进化的智能体。这一范式转变——从扩展静态模型到开发自进化智能体——引发了学界对架构和方法的日益增长的兴趣，使智能体能够通过数据、交互和经验实现持续学习和适应。本文首次对自进化智能体进行了系统而全面的综述，围绕三个基础维度组织该领域的研究：**演进什么（What）**、**何时演进（When）** 和 **如何演进（How）**。我们深入探讨了智能体各组件（模型、记忆、工具、架构）的进化机制，按照阶段对适应方法进行分类（如测试时内/intra-test-time、测试时间间/inter-test-time），并分析了引导进化适应的算法和架构设计（如标量奖励/scalar rewards、文本反馈/textual feedback、单智能体与多智能体系统）。此外，我们还分析了针对自进化智能体的评估指标和基准测试，展示了在编程、教育、医疗等领域的应用，并指出了安全、可扩展性及协同进化动力学方面的关键挑战与研究方向。通过提供理解和设计自进化智能体的结构化框架，本综述为在研究和实际部署中推进更自适应、更有能力、更稳健且更通用的智能体系统绘制了路线图，并最终揭示了人工超级智能（Artificial Super Intelligence, ASI）的实现前景——在这种智能形态下，智能体能够自主进化，并在广泛的任务中展现出超越人类水平的智能。

---

**原文标题：**

A Survey of Self-Evolving Agents: What, When, How, and Where to Evolve on the Path to Artificial Super Intelligence

---

**图 1 描述：**

图 1：一幅概念性轨迹图，展示了从大型语言模型（LLMs）到基础智能体（foundation agents），再到自进化智能体（self-evolving agents）——我们的研究焦点——最终迈向假设中的**人工超级智能（Artificial Super Intelligence, ASI）**的演进路径。在这条路径上，智能水平和自适应能力逐步提升，标志着向更自主、更智能的 AI 系统的一次转变。自进化智能体之后的研究方向仍属开放领域，有待持续探索。

---

**原始英文文本对照：**

Figure 1: A conceptual trajectory illustrating the progression from large language models (LLMs) to foundation agents, and then to self-evolving agents—our focus, and ultimately toward the hypothetical Artificial Super Intelligence (ASI). Along this path, intelligence and adaptivity increase, marking a shift toward more autonomous and agentic AI systems. The future directions beyond self-evolving agents remain open and subject to ongoing exploration.