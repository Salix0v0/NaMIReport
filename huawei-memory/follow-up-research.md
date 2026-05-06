# 四篇论文后续高质量相关论文调研

> 调研日期：2026-05-06
> 调研范围：四篇论文（A-MEM, Mem0, Memory OS, NEMORI）发表之后的领域新进展，重点关注顶会接收情况、机构背景、期刊质量。

---

## 一、四篇原始论文发表venue确认

| 论文 | arXiv | 发表venue | 级别 |
|------|-------|-----------|------|
| A-MEM | 2502.12110 | **NeurIPS 2025 Poster** | CCF-A |
| Mem0 | 2504.19413 | **ECAI 2025** | CCF-B |
| Memory OS | 2506.06326 | **EMNLP 2025 Oral** | CCF-B |
| NEMORI | 2508.03341 | arXiv preprint（截止调研时未见顶会接收） | 预印本 |

### 原始论文机构背景

- **A-MEM**: Wujiang Xu (Rutgers University, Meta实习生), Zujie Liang (Ant Group), Kai Mei, Hang Gao, Juntao Tan (Salesforce Research), Yongfeng Zhang (Rutgers University)
- **Mem0**: Prateek Chhikara, Dev Khant, Saket Aryan, Taranjeet Singh, Deshraj Yadav (Mem0 Inc. — YC S24 公司，已获 $24M Series A 融资)
- **Memory OS**: Jiazheng Kang (北京邮电大学), Mingming Ji (Tencent AI Lab), Zhe Zhao (Tencent AI Lab), Ting Bai (北京邮电大学)
- **NEMORI**: Wenquan Ma, Jiayan Nan, Wenlong Wu, Yize Chen（独立研究者/团队）

---

## 二、2025下半年-2026年重要后续论文

### 2.1 顶会已接收论文 (CCF-A/B)

#### MemEvolve: Meta-Evolution of Agent Memory Systems
- **arXiv**: 2512.18746 (Dec 2025)
- **Venue**: **ICML 2026** (CCF-A)
- **机构**: OPPO AI + LV-NUS Lab (新加坡国立大学)
- **核心思路**: 提出记忆系统的双重进化——内层循环在固定架构下积累经验，外层循环评估架构有效性并自动提出结构修改。将记忆分解为Encode/Store/Retrieve/Manage四个模块，用性能反馈诊断瓶颈。同时发布EvolveLab，统一12种记忆系统的公共接口。
- **与四篇关系**: 直接回应A-MEM的"agentic memory organization" + NEMORI的"adaptive"理念,将二者推进到元进化层面。与"Agent自进化"主题直接相关。
- **质量评估**: ⭐⭐⭐⭐⭐ (ICML 2026, 顶级机构)

#### EMPO²: Exploratory Memory-Augmented LLM Agent via Hybrid On- and Off-Policy Optimization
- **arXiv**: 2602.23008 (Feb 2026)
- **Venue**: **ICLR 2026 Poster** (CCF-A)
- **机构**: Microsoft Research + KAIST
- **核心思路**: 利用记忆增强探索的混合强化学习框架，结合On-Policy和Off-Policy更新。在ScienceWorld上比GRPO提升128.6%。
- **与四篇关系**: 将Memory的使用提升到RL策略优化层面，与Agentic Memory (AgeMem)方向互补。
- **质量评估**: ⭐⭐⭐⭐⭐ (ICLR 2026, Microsoft Research)

#### MemoryAgentBench: Evaluating Memory in LLM Agents
- **arXiv**: 2507.05257 (Jul 2025)
- **Venue**: **ICLR 2026** (CCF-A)
- **机构**: UCSD (Yuanzhe Hu, Yu Wang, Julian McAuley)
- **核心思路**: 基于认知科学理论，定义记忆Agent的四项核心能力：准确检索、测试时学习、长程理解、选择性遗忘。将长上下文数据集重构为增量式多轮交互。
- **与四篇关系**: 为A-MEM、Mem0、Memory OS等系统提供了更全面的评测基准（所有这些系统主要使用LoCoMo评测）。
- **质量评估**: ⭐⭐⭐⭐⭐ (ICLR 2026, UCSD)

#### Agentic Memory (AgeMem): Learning Unified Long-Term and Short-Term Memory Management
- **arXiv**: 2601.01885 (Jan 2026)
- **机构**: **Alibaba Group**
- **核心思路**: 将LTM和STM统一管理，把记忆操作(store/retrieve/update/summarize/discard)作为可调用工具，用三步渐进式RL + Step-wise GRPO训练统一策略。在5个长程benchmark上全面超越baselines。
- **与四篇关系**: 与A-MEM形成鲜明对比——A-MEM使用启发式Zettelkasten方法，AgeMem使用RL学习最优记忆策略。代表了从"设计记忆"到"学习记忆"的范式转变。
- **质量评估**: ⭐⭐⭐⭐ (Alibaba, 领域影响力大)

#### MemoryArena: Benchmarking Agent Memory in Interdependent Multi-Session Agentic Tasks
- **arXiv**: 2602.16313 (Feb 2026)
- **机构**: MIT Media Lab + UCSD + UW
- **核心思路**: 在完整agentic任务中嵌入记忆评测——网页导航、偏好约束规划、渐进式信息搜索、序列形式推理。在LoCoMo上接近饱和的模型在这里跌到40-60%。
- **与四篇关系**: 暴露了A-MEM/Mem0/Memory OS等系统在LoCoMo评测上的"天花板效应"，提供了更真实、更难的评测。
- **质量评估**: ⭐⭐⭐⭐ (MIT + UCSD, 重要benchmark)

### 2.2 高质量预印本（有望被顶会接收）

#### MemOS: A Memory OS for AI System
- **arXiv**: 2507.03724 (Jul 2025, 持续更新至v2.0 Dec 2025)
- **机构**: 多机构合作（含Memory³团队，上海交大等多校）
- **核心思路**: 比Memory OS of AI Agent（Kang et al.）更宏大的框架——统一三种记忆基底：Plaintext Memory / Activation Memory / Parameter Memory。提出MemCube作为通用封装单元，支持记忆的类型转换、调度和治理。
- **与Memory OS的区别**: Memory OS of AI Agent (EMNLP 2025) 聚焦于对话Agent的分层存储 (STM/MTM/LPM)。MemOS是系统级的完整Memory Operating System，覆盖参数记忆、激活记忆和外部记忆。
- **质量评估**: ⭐⭐⭐⭐ (团队强，框架完整，持续维护)

#### MemSkill: Learning and Evolving Memory Skills for Self-Evolving Agents
- **arXiv**: 2602.02474 (Feb 2026)
- **机构**: Haozhen Zhang, Quanyu Long, Jianzhu Bao 等
- **核心思路**: 将记忆操作重构为可学习、可进化的"记忆技能"。包含Controller（学习选择技能）+ Executor（执行）+ Designer（定期review失败案例、进化技能库）的闭环流程。
- **与四篇关系**: 直接推进了NEMORI的"学习什么值得记忆"思路——不仅学习选择什么，还学习如何提取、如何整合、如何修剪。
- **质量评估**: ⭐⭐⭐⭐ (思路新颖，与自进化直接相关)

#### MemMachine: A Ground-Truth-Preserving Memory System for Personalized AI Agents
- **arXiv**: 2604.04853 (Apr 2026)
- **机构**: Shu Wang, Edwin Yu 等（独立团队/创业公司）
- **核心思路**: 保留episodic ground truth + 自适应分层检索。在LoCoMo上达到0.9169（截至2026年3月最强公开发布结果之一），LongMemEval上93.0%。比Mem0节省约80%的输入token。
- **与四篇关系**: 直接对标Mem0，在性能和效率上均有显著提升。
- **质量评估**: ⭐⭐⭐ (工业级系统，benchmark表现强)

#### Adaptive Memory Admission Control (A-MAC)
- **arXiv**: 2603.04549 (Mar 2026)
- **Venue**: **ICLR 2026 Workshop MemAgent**
- **机构**: Workday AI
- **核心思路**: 用5个互补信号（有用性、可靠性、冗余度、时间相关性、持久性）+ 学习的线性准入策略来决定记忆的admit/update/reject。
- **与四篇关系**: 直接回应了NEMORI提出的核心问题——"什么值得记忆"，但使用了更轻量、更可审计的规则学习方法。
- **质量评估**: ⭐⭐⭐ (Workshop论文但思路实用)

### 2.3 重要综述与调查

#### Memory for Autonomous LLM Agents: Mechanisms, Evaluation, and Emerging Frontiers
- **arXiv**: 2603.07670 (Mar 2026)
- **亮点**: 最全面的2025-2026 agent memory综述，覆盖AgeMem/MemBench/MemoryAgentBench/MemoryArena等最新工作，用POMDP形式化记忆过程。明确将四篇论文全部纳入分析框架。
- **质量评估**: ⭐⭐⭐⭐ (领域必读综述)

#### Graph-based Agent Memory: Taxonomy, Techniques, and Applications
- **arXiv**: 2602.05665 (Feb 2026)
- **亮点**: 聚焦Graph-based记忆，将A-MEM和Mem0的graph变体等系统做了统一分类学。
- **质量评估**: ⭐⭐⭐

#### A Survey on the Security of Long-Term Memory in LLM Agents
- **arXiv**: 2604.16548 (Apr 2026)
- **亮点**: 首个聚焦Agent Memory安全性的综述，讨论记忆投毒、记忆控制流攻击等新威胁模型。
- **质量评估**: ⭐⭐⭐ (新方向，重要性高)

### 2.4 其他值得关注的论文

| 论文 | arXiv | 亮点 |
|------|-------|------|
| Mesh Memory Protocol | 2604.19540 | 多Agent系统的语义基础设施，角色索引的逐字段准入 |
| Joint Optimization of Multi-agent Memory System | 2603.12631 | 多Agent记忆构建与检索的联合优化 |
| StructMemEval (Evaluating Memory Structure) | 2602.11243 | 评测Agent记忆结构组织能力，发现LLMs不会自动正确组织记忆 |
| Memory in the LLM Era: Modular Architectures | 2604.01707 | 将记忆方法分解为四个模块化组件的统一框架+SOTA |
| Mem^p: Exploring Agent Procedural Memory | 2508.06433 | 首次探索Agent程序性记忆（如何做事的记忆） |
| Learn to Memorize (Adaptive Memory Framework) | 2508.16629 | 自适应记忆存储，根据应用场景提取关键信息 |
| MIRIX | 2507.07957 | 六组件记忆系统（Core/Episodic/Semantic/Procedural/Resource/Knowledge Vault） |

---

## 三、关键趋势分析

### 3.1 与Agent自进化的交叉

2025下半年-2026年最显著的趋势是 **Memory与自进化的深度融合**：

1. **MemEvolve (ICML 2026)** 直接提出记忆架构的元进化——不仅是记忆内容的更新，更是记忆系统本身的进化
2. **MemSkill** 让记忆操作本身成为可进化的技能
3. **Agentic Memory (AgeMem)** 用RL学习最优记忆策略，替代人工设计的启发式规则
4. **EMPO² (ICLR 2026)** 将记忆用作RL探索的工具

这四条线共同指向：**从"手工设计记忆系统"到"学习/进化记忆系统"的范式转变**。

### 3.2 评测基准的升级

- LoCoMo正在"饱和"（MemoryArena显示顶部系统达到~90%），需要更难的benchmark
- **MemoryAgentBench (ICLR 2026)** 和 **MemoryArena** 代表了下一代评测：更认知科学导向、更真实的多session依赖任务
- 四篇论文都在LoCoMo上评测，后续工作需要在新的benchmark上重新验证

### 3.3 工业界的强烈兴趣

- **Mem0 Inc.** 获得$24M Series A，将学术论文转化为产品
- **Alibaba** 发布AgeMem，**Microsoft Research** 发布EMPO²
- **OPPO AI** 的MemEvolve被ICML 2026接收
- **Workday AI** 发布A-MAC（ICLR Workshop）
- **Letta (MemGPT团队)** 获$10M种子轮，开发Memory-first coding agent
- 多个创业公司(Memobase, Zep, Cognee)在mem0之后进入市场

### 3.4 机构分布

| 机构类型 | 代表性工作 |
|----------|-----------|
| 中国大厂 | Alibaba (AgeMem), OPPO (MemEvolve), Tencent (Memory OS) |
| 美国大厂 | Microsoft Research (EMPO²), Workday AI (A-MAC) |
| 顶尖高校 | Rutgers (A-MEM), UCSD (MemoryAgentBench), MIT (MemoryArena), BUPT+Tencent (Memory OS) |
| 创业公司 | Mem0 Inc., MemMachine团队, Zep, Cognee, Letta |

---

## 四、对组会汇报的建议

### 四篇论文的定位更新

- **A-MEM** 已被NeurIPS 2025接收，且有544次引用，是该领域最有影响力的工作之一
- **Mem0** 已被ECAI 2025接收，作为工业产品持续迭代（2026年4月发布新token-efficient算法）
- **Memory OS** 已被EMNLP 2025 Oral接收，但后续被MemOS（更宏大的框架）在一定程度上覆盖
- **NEMORI** 截止调研时未见顶会接收，但其"预测误差驱动记忆蒸馏"的思想在MemSkill、A-MAC等后续工作中得到呼应

### 建议补充汇报的内容

1. **MemEvolve (ICML 2026)** 作为"自进化+Memory"的直接证据，强烈建议纳入
2. **Agentic Memory (AgeMem)** 作为RL学习记忆策略的代表
3. **MemoryAgentBench + MemoryArena** 展示评测体系的发展
4. 简提MemOS、MemSkill等后续方向

---

## 五、参考文献（新增推荐阅读）

```bibtex
@inproceedings{memevolve2025,
  title={MemEvolve: Meta-Evolution of Agent Memory Systems},
  author={Guibin Chen et al.},
  booktitle={International Conference on Machine Learning (ICML)},
  year={2026},
  note={arXiv:2512.18746}
}

@inproceedings{empo2-2026,
  title={Exploratory Memory-Augmented LLM Agent via Hybrid On- and Off-Policy Optimization},
  author={Zeyuan Liu and Jeonghye Kim and Xufang Luo and Dongsheng Li and Yuqing Yang},
  booktitle={International Conference on Learning Representations (ICLR)},
  year={2026},
  note={arXiv:2602.23008}
}

@inproceedings{memoryagentbench2026,
  title={Evaluating Memory in LLM Agents via Incremental Multi-Turn Interactions},
  author={Yuanzhe Hu and Yu Wang and Julian McAuley},
  booktitle={International Conference on Learning Representations (ICLR)},
  year={2026},
  note={arXiv:2507.05257}
}

@article{agemem2026,
  title={Agentic Memory: Learning Unified Long-Term and Short-Term Memory Management for Large Language Model Agents},
  author={Yu et al.},
  journal={arXiv preprint arXiv:2601.01885},
  year={2026}
}

@article{memskill2026,
  title={MemSkill: Learning and Evolving Memory Skills for Self-Evolving Agents},
  author={Haozhen Zhang and Quanyu Long and Jianzhu Bao and Tao Feng and Weizhi Zhang and Haodong Yue and Wenya Wang},
  journal={arXiv preprint arXiv:2602.02474},
  year={2026}
}

@article{memos2025,
  title={MemOS: A Memory OS for AI System},
  author={Zhiyu Li and Shichao Song and Chenyang Xi and Hanyu Wang and Chen Tang and Simin Niu and others},
  journal={arXiv preprint arXiv:2507.03724},
  year={2025}
}

@article{memorysurvey2026,
  title={Memory for Autonomous LLM Agents: Mechanisms, Evaluation, and Emerging Frontiers},
  journal={arXiv preprint arXiv:2603.07670},
  year={2026}
}
```
