## 7.3 当前评估实践的局限性

尽管前几节概述了核心评估维度及其覆盖范围，但从更广的视角审视，当前的评估实践仍然存在显著的盲点，并阻碍了不同方法之间的公平比较。为了将这些局限性置于具体背景中，我们考察了那些仍未得到充分评估的能力维度，以及在共同设置下进行同类比较时所面临的各种复杂因素。

### 7.3.1 评估不足的能力交叉领域

**长程记忆保留与隐私约束**：尚无基准测试将扩展记忆评估（如 LTMBenchmark（Castillo-Bolado et al., 2024））与严格的安全审计（如 AgentSafetyBench（Zhang et al., 2024i））相结合，这留下了一个悬而未决的问题：智能体能否在成千上万次交互中保持个性化，同时保证敏感信息的零泄露。

**操作约束下的架构适配**：当前的架构搜索方法（例如 AFlow（Zhang et al., 2024c）、ADAS（Hu et al., 2024c））在离线状态下经过较长周期来发现最优工作流程。目前尚无评估检验智能体是否能够自主进化其架构选择策略——即在学习不同查询类型最适合何种拓扑的同时，遵守实时操作约束（毫秒级响应延迟、每次查询的 token 预算）。这不仅需要评估最终架构的质量，还需要评估智能体在严格资源限制下，通过经验是否能够持续改善其选择或生成架构的策略。

**工具生态系统演进**：现有工具基准测试提供的是固定 API；尚无评估能够捕捉工具发现、集成测试和生产率测量的自导向生命周期——这些能力已在类似 Alita 的系统中得到展示，但在标准评估中却付之阙如。

**协作演进下的多智能体安全**：SwarmBench（Ruan et al., 2025）在孤立的时刻节点识别协调失败；但这些失败在长期的多智能体协同演进中是加剧还是衰减，以及不安全行为在智能体相互学习时是否表现出社会传染性，目前仍属未被探索的领域。

### 7.3.2 公平比较面临的挑战

为补充我们对评估基准的讨论，我们提供表 11，该表对在部分匹配条件下（即相似领域、基准测试和骨干模型）评估的一部分代表性自进化智能体进行了对齐。该表旨在明确展示不同方法如何在周边实验背景保持尽可能恒定的情况下，具体化 what/when/how 三个维度的内容。然而，正如该表也清楚表明的那样，真正的"同类比较"（apples-to-apples comparison）目前在很大程度上仍不可行。现有工作在以下方面存在实质性差异：(1) **报告实践**：延迟、成本和安全等关键指标经常被省略或定义不一致；(2) **评估流程**：提示词格式、 rollout 预算、工具访问权限和环境配置的差异很大；(3) **骨干模型选择**：即使名义上相似的模型在规模、训练数据或推理设置上也存在差异；以及 (4) **架构设计**：智能体实现了不同的控制循环、信用分配机制和记忆系统，无法直接比较。由于这些因素相互影响，在方法之间标准化结果可能会过度解读不受控制的差异。因此，表 11 被作为说明性的快照呈现，而非终极的比较结论。

尽管存在这些局限性，该表仍突显出几个定性趋势：使用更丰富的 what 结构（如架构级搜索）和 inter-test when 机制的方法，在多步优化可行的领域中往往能实现更强的性能；而轻量级的 intra-test 反思方法虽然成本效益更高，但收益增幅较小。几乎所有方法都缺乏一致的延迟/成本/安全报告，这凸显了一个关键缺口，限制了更广泛的综合分析。我们希望该表能够作为具体参考，展示当前方法如何在可比设置下将 what/when/how 维度付诸实践，同时推动对标准化报告的需求，以支持未来真正意义上的同类比较。

&nbsp;

**表 11**: 在共同设置下对部分代表性自进化智能体的比较综合。方法按领域分组；重复条目用"–"表示。我们使用 what/when/how 分类法对各方法进行总结，并报告性能表现。延迟、成本和安全指标的报告不一致，限制了完全的同类比较。

| Area | Benchmark | Base model | Method | What | When | How | Perf. (%) |
|------|-----------|------------|--------|------|------|-----|-----------|
| code | SWE | Gemini-1.5-pro | Reflexion (Shinn et al., 2023) | Context / lesson / reflection | Intra-test (ICL) | Reward-based (textual) | 14.3 |
| – | – | – | Learn-by-Interact (Su et al., 2025) | Context / experience / reflection | Intra-test (ICL) | Reward-based (textual) | 18.7 |
| – | – | Claude-3.5-sonnet | Reflexion (Shinn et al., 2023) | Context / lesson / reflection | Intra-test (ICL) | Reward-based (textual) | 54.4 |
| – | – | – | Learn-by-Interact (Su et al., 2025) | Context / experience | Intra-test (ICL) | Reward-based (textual) | 60.0 |
| – | WebArena | Gemini-1.5-pro | Reflexion (Shinn et al., 2023) | Context / lesson / reflection | Intra-test (ICL) | Reward-based (textual) | 20.2 |
| – | – | – | Learn-by-Interact (Su et al., 2025) | Context / experience | Intra-test (ICL) | Reward-based (textual) | 25.6 |
| web | WebArena | Claude-3.5-sonnet | Reflexion (Shinn et al., 2023) | Context / lesson / reflection | Intra-test (ICL) | Reward-based (textual) | 40.4 |
| – | – | – | Learn-by-Interact (Su et al., 2025) | Context / experience | Intra-test (ICL) | Reward-based (textual) | 48.0 |
| – | WebArena-Lite | GLM-4-9B | DigiRL (Bai et al., 2024) | Model policy | Inter-test (RL) | Reward-based (external env.) | 31.5 |
| – | – | – | WebRL (Qi et al., 2024) | Model policy | Inter-test (RL) | Reward-based (external env.) | 43.0 |
| – | – | Llama3.1-8B | DigiRL (Bai et al., 2024) | Model policy | Inter-test (RL) | Reward-based (external env.) | 30.3 |
| – | – | – | WebRL (Qi et al., 2024) | Model policy | Inter-test (RL) | Reward-based (external env.) | 42.4 |
| math | GSM8K | GPT-4o-mini | ADAS (Hu et al., 2024c) | Architecture multi-agent system | / Inter-test (RL / SFT hybrid) | Population-based workflow search | 90.5 |
| – | – | – | AFlow (Zhang et al., 2024c) | Architecture multi-agent topology | / Inter-test | Population-based (MCTS) | 90.8 |
| – | – | – | ScoreFlow (Wang et al., 2025n) | Architecture / multi-agent (query-specific workflow) | Inter-test | Imitation + preference optimization | 94.6 |
| – | MATH | Gemini-1.5-pro-002 | ADAS (Hu et al., 2024c) | Architecture multi-agent system | / Inter-test (RL / SFT hybrid) | Population-based | 80.0 |
| – | – | – | AFlow (Zhang et al., 2024c) | Architecture multi-agent topology | / Inter-test | Population-based | 76.0 |
| – | – | – | Mass (Zhang et al., 2025d) | Architecture / single / multi-agent design search | Inter-test | Population-based evolutionary | 84.7 |
