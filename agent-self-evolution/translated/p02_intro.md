# 引言

"并非物种中最聪慧者得以留存；亦非最强壮者得以留存；但得以留存的物种，是那些最能适应并调整自身以应对不断变化之环境的物种。"
— Charles Darwin

大语言模型（Large Language Models, LLMs）已在广泛的任务中展现出卓越的能力。然而，它们从根本上仍是静态的（Luo et al., 2025a），在遇到新任务、演进中的知识领域或动态交互情境时，无法调整其内部参数。随着大语言模型越来越多地被部署在开放式、交互式的环境中，这一局限性成为关键瓶颈。在此类场景下，传统的知识检索机制被证明是不充分的，由此催生了能够实时动态调整感知、推理和行动的智能体。这种对动态、持续适应的迫切需求标志着人工智能领域的一个概念性转变：从扩展静态模型转向发展自进化智能体（self-evolving agents）。尽管监督微调（Supervised Fine-Tuning, SFT）和强化学习（Reinforcement Learning, RL）等成熟技术为改进提供了机制，但我们对自进化的定义不仅仅基于所使用的算法，而在于自主性的 locus。与传统流水线（由人类工程师策划数据并安排更新）不同，自进化智能体能够从新数据、交互和经验中实时持续地学习，从而构建出更加鲁棒、多功能且能够应对复杂动态现实问题的系统（Wang et al., 2024a）。这一转变目前正引领我们迈向一条通向人工超级智能（Artificial Super Intelligence, ASI）的有前景且变革性的道路，在这条道路上，智能体不仅能够以不可预测的速度从经验中学习和进化，还能在广泛的任务中达到或超越人类水平的智能表现（Wang et al., 2025g）。

与受限于无法适应新情境和演进上下文而仍被约束的静态大语言模型不同，自进化智能体被设计为通过从现实世界反馈中持续学习来克服这些局限性。这一进展重塑了我们对智能体的理解。自进化智能体作为一个核心概念，代表了智能系统演进中的重要一步，充当着为更适应性和更自主的人工智能铺平道路的中间角色，如图 1 所示。近期研究越来越关注开发能够从经验中持续学习和适应的自适应智能体架构，例如智能体框架的最新进展（Yin et al., 2025）、提示策略（Fernando et al., 2023）以及不同的进化优化方式。然而，尽管有这些进展，现有的综述主要将智能体进化作为综合智能体分类法中的一个附属组成部分来讨论。先前的综述主要提供了通用智能体发展的系统性概览，但对自进化智能体在受限场景中的自进化机制的覆盖有限（Luo et al., 2025a; Liu et al., 2025a）。

例如，Luo 等人（2025a）讨论了多种进化方式，如自学习和多智能体协同进化，而 Liu 等人（2025a）则明确从智能体不同组件的角度介绍了进化，如工具和提示。此外，一些研究专门关注语言模型本身的进化（Tao et al., 2024），而非更广泛的智能体概念。然而，这些工作处理的是孤立的组件而非整体的智能体系统。因此，目前尚无系统性综述致力于将自进化智能体作为一流研究范式进行全面深入的探讨。这一空白使得一些根本性问题未被充分探索：智能体的哪些方面应该进化？何时应该发生适应？以及如何在实践中实现这种进化？

据我们所知，这是首个专注于自进化智能体的系统性和综合性综述，为理论探究和实际部署提供了清晰的路线图。然而，鉴于这代表了一个正在快速形成的研&#x8BBA领域，其概念边界仍在社区内被积极协商，我们将其定位于指导性综合，而非对已完全建立范式的评论。我们不强加严格的边界，而是旨在将社区中涌现的异构机制组织成连贯的框架。我们围绕三个基础问题来组织分析——进化什么、何时进化、以及如何进化——并为理解每个问题提供结构化框架。具体而言，我们系统地审视单个智能体组件，包括模型、记忆、工具及相应工作流，研究它们各自独特的进化机制（智能体在第 3 节中的进化什么）；然后根据不同时间阶段和不同学习范式（如监督微调、强化学习和推理时进化）来划分现有进化方法（何时进化在第 4 节）。最后，我们总结引导智能体进化的不同信号，如文本反馈或标量奖励，以及不同类型的待进化智能体架构，如单智能体和多智能体进化（如何进化在第 5 节）。此外，我们回顾了某些评估指标和基准，以跟踪自进化智能体的现有进展，强调智能体与评估之间协同进化的重要性（第 6 节）。我们还考察了在编程、教育和医疗等领域的新兴应用，在这些领域中持续适应和进化至关重要（第 7 节）。最后，我们确定了持续存在的挑战并勾勒出有前景的研究方向，以指导自进化智能体的发展（第 8 节）。通过对自进化过程在正交维度上的系统分解，我们提供了一个结构化和实用的框架，使研究人员能够系统地分析、比较和设计更鲁棒、更自适应的智能体系统。综上所述，我们的主要贡献如下：

- 我们建立了一个统一的理论框架，用于表征智能体系统中的自进化过程，围绕三个基本维度：进化什么、如何进化以及何时进化，为未来的自进化智能体系统提供清晰的设计指导。

- 我们进一步研究了为自进化智能体量身定制的评估基准或环境，强调了与适应性、鲁棒性和现实世界复杂性相关的新兴指标和挑战。

- 我们展示了跨多个领域的关键实际应用，包括自主软件工程、个性化教育、医疗保健和智能虚拟助手，阐明了自进化智能体的实践潜力。

- 我们确定了关键的开放性挑战和有前景的未来研究方向，强调了安全性、个性化、多智能体协同进化和可扩展性等方面。

通过以上工作，我们的综述为研究人员和实践者提供了更结构化的分类法，从不同角度理解、比较和推进自进化智能体研究。随着基于大语言模型的智能体越来越多地被集成到关键任务应用中，理解其进化动力学变得至关重要，其范围超越了学术研究，涵盖了工业应用、监管考虑和更广泛的社会影响。

&nbsp;

| | 策略 | SCA（Zhou et al., 2025e），Self-Rewarding Self-Improving（Simonds et al., 2025） |
|---|---|---|
| | 模型 | SCoRe（Kumar et al., 2024），PAG（Jiang et al., 2025b），TextGrad（Yellamraju et al., 2024），AutoRule（Wang & Xiong, 2025），SRLM（Wang et al., 2025f） |
| | 课程 | SCA（Zhou et al., 2025e），AgentGen（Hu et al., 2024b），Reflexion（Shinn et al., 2023），AdaPlanner（Sun et al., 2023），SICA（Robeyns et al., 2025b），Self-Refine（Madaan et al., 2023b），Learn-by-interact（Su et al., 2025），RAGEN（Wang et al., 2025q），DYSTIL（Wang et al., 2025c） |
| | 记忆 | SAGE（Liang et al., 2024），Mem0（Chhikara et al., 2025），MemInsight（Salama et al., 2025），REMEMBER（Zhang et al., 2024a），Expel（Zhao et al., 2024a），Agent Workflow Memory（Wang et al., 2024j），Richelieu diplomacy agent（Guan et al., 2024），ICE（Qian et al., 2024a） |
| | 上下文 | APE（Zhou et al., 2022），ORPO（Yang et al., 2023），ProTeGi（Pryzant et al., 2023），PromptAgent（Wang et al., 2023d），REVOLVE（Zhang et al., 2024e） |
| **进化什么** | 提示 | PromptBreeder（Fernando et al., 2023），DSPy（Khattab et al., 2023），Trace（Wang et al., 2023c），TextGrad（Yellamraju et al., 2024），SPO（Xiang et al., 2025），LLM-AutoDiff（Yin & Wang, 2025），EvoAgent（Yuan et al., 2024b） |
| | 创建 | Voyager（Wang et al., 2023a），Alita（Qiu et al., 2025b），ATLASS（Haque et al., 2025），CREATOR（Qian et al., 2023b），SkillWeaver（Zheng et al., 2025a），CRAFT（Yuan et al., 2024a） |
| | 工具 | LearnAct（Zhao et al., 2024b），DRAFT（Qu et al., 2025），ToolLLM（Qin et al., 2023），Toolformer（Schick et al., 2023），Gorilla（Patil et al., 2024） |
| | 选择 | ToolGen（Wang et al., 2025k），AgentSquare（Shang et al., 2025），Darwin Godel Machine（Zhang et al., 2025h），COLT（Qu et al., 2024a），TOOLRET（Shi et al., 2025c），ToolRerank（Zheng et al., 2024b），PTR（Gao & Zhang, 2024），SSO（Nottingham et al., 2024） |
| | 单智能体 | AgentSquare（Shang et al., 2025），Darwin Godel Machine（Zhang et al., 2025h），Gödel Agent（Yin et al., 2025），AlphaEvolve（Novikov et al., 2025），TextGrad（Yellamraju et al., 2024），EvoFlow（Zhang et al., 2025c），MASS（Zhou et al., 2025a） |
| | 架构 | AFlow（Zhang et al., 2024c），ADAS（Hu et al., 2024c），AutoFlow（Li et al., 2024d），GPTSwarm（Zhuge et al., 2024），ScoreFlow（Wang et al., 2025n），FlowReasoner（Gao et al., 2025），ReMA（Wan et al., 2025），GIGPO（Feng et al., 2025b） |
| | | ICL | Reflexion（Shinn et al., 2023），SELF（Madaan et al., 2023a），AdaPlanner（Sun et al., 2023），TrustAgent（Hua et al., 2024） |
| | 测试时内 | SFT | Self-Adaptive LM（Zweiger et al., 2025），TTT-NN（Hardt & Sun, 2023），SIFT（Hübotter et al., 2024） |
| **何时进化** | 自进化 | RL | LADDER（Simonds & Yoshiyama, 2025），Ttrl（Zuo et al., 2025） |
| | | SFT | SELF（Lu et al., 2023），STaR（Zelikman et al., 2022），Quiet-STaR（Zelikman et al., 2024），SiriuS（Zhao et al., 2025b），Chen 等（Chen et al., 2025b） |
| 自进化智能体 | 测试时际 | | | |
| | 自进化 | RL | RAGEN（Wang et al., 2025q），Learning-Like-Humans（Zhang et al., 2025a），WebRL（Qi et al., 2024），DigiRL（Bai et al., 2024） |
| | | 文本反馈 | Reflexion（Shinn et al., 2023），AdaPlanner（Sun et al., 2023），AgentS2（Agashe et al., 2025），SELF（Lu et al., 2023），Self-Refine（Madaan et al., 2023a），SCoRe（Kumar et al., 2024），PAG（Jiang et al., 2025b），TextGrad（Yellamraju et al., 2024） |
| | | 内部奖励 | CISC（Taubenfeld et al., 2025），Self-Ensemble（Xu et al., 2025b），SRSI（Simonds et al., 2025），Self-Certainty（Kang et al., 2025），Self-Rewarding Language Models（Yuan et al., 2025b） |
| **如何进化** | 基于奖励的 | | | |
| 自进化 | 外部奖励 | Self-Train LM（Shafayat et al., 2025），MM-UPT（Wei et al., 2025c），CoVo（Zhang et al., 2025j），SWE-Dev（Du et al., 2025），SICA（Robeyns et al., 2025a），Feedback Friction（Jiang et al., 2025a），USEagent（Applis et al., 2025），DYSTIL（Wang et al., 2025c），OTCPO（Wang et al., 2025h），AutoRule（Wang & Xiong, 2025），EGSR（Zhang et al., 2025a），LADDER（Simonds & Yoshiyama, 2025），RAGEN（Wang et al., 2025q），SPIRAL（Liu et al., 2025d） |
| | | 隐式奖励 | Reward Is Enough（Song et al., 2025），Endogenous reward（Li et al., 2025e） |
| | | 自生成 | STaR（Zelikman et al., 2022），V-STaR（Hosseini et al., 2024），AdaSTaR（Koh et al., 2025），STIC（Deng et al., 2024），GENIXER（Zhao et al., 2024c） |
| | 模仿与示范学习 | 其他 | SiriuS（Zhao et al., 2025b），SOFT（Tang et al., 2025），RISE（Qu et al., 2024b），IoE（Li et al., 2024b） |
| | | 单智能体 | DGM（Zhang et al., 2025h），GENOME（Zhang et al., 2025r），SPIN（Chen et al., 2024f），SPC（Chen et al., 2025c），STL（Mendes & Ritter, 2025） |
| | 基于种群与进化方法 | | | |
| | | 多智能体 | EvoMAC（Hu et al., 2024d），Puppeteer（Dang et al., 2025），MDTeamGPT（Chen et al., 2025e），MedAgentSim（Almansoori et al., 2025b） |
| | | 记忆 | Mobile-Agent-E（Wang et al., 2025o），MobileSteward（Liu et al., 2025f） |
| | | 课程学习 | WebRL（Qi et al., 2024），Voyager（Wang et al., 2023a） |
| **在何处进化** | 通用领域 | | | |
| | 模型-智能体协同进化 | WebEvolver（Fang et al., 2025b），UI-Genie（Xiao et al., 2025a），Absolute-Zero（Zhao et al., 2025a） |
| | | 编码、GUI | EvoMac（Hu et al., 2024d），SICA（Robeyns et al., 2025a），AgentCoder（Dang et al., 2025），QuantAgent（Wang et al., 2024d） |
| | 专门领域 | 金融等 | Arxiv-copilot（Lin et al., 2024），Voyager（Wang et al., 2023a） |
| | | 其他 | |

**图 2：自进化智能体的分类体系。** 在该分类体系中，智能体从进化什么、何时进化、如何进化和在何处进化四个维度进行分析，每个叶节点标注了代表性的方法与系统。

&nbsp;

**进化什么？**&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**何时进化？**&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**在何处进化？**

&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;任务完成

&emsp;&emsp;&emsp;&emsp;记忆&emsp;&emsp;&emsp;&emsp;&emsp;提示&emsp;&emsp;&emsp;&emsp;&emsp;上下文&emsp;&emsp;&emsp;&emsp;&emsp;通用领域

&emsp;&emsp;&emsp;&emsp;存储/检索&emsp;&emsp;指令&emsp;&emsp;&emsp;&emsp;&emsp;测试时内&emsp;&emsp;&emsp;&emsp;测试时际&emsp;&emsp;通用应用

&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;自进化&emsp;&emsp;&emsp;&emsp;&emsp;自进化

&emsp;&emsp;智能体&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;方法&emsp;&emsp;ICL&emsp;&emsp;&emsp;SFT&emsp;&emsp;&emsp;RL&emsp;&emsp;&emsp;&emsp;专门领域

&emsp;&emsp;规划、推理&emsp;&emsp;&emsp;调用/返回&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;编码&emsp;&emsp;GUI&emsp;&emsp;金融

&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;医疗&emsp;&emsp;教育&emsp;&emsp;其他

模型

&emsp;&emsp;模型&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;工具&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**如何进化？**

&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;基于奖励&emsp;&emsp;&emsp;&emsp;模仿与示范&emsp;&emsp;&emsp;基于种群

&emsp;&emsp;单智能体&emsp;&emsp;&emsp;多智能体&emsp;&emsp;文本&emsp;&emsp;自生成&emsp;&emsp;&emsp;单智能体&emsp;&emsp;多智能体&emsp;&emsp;**评估**

&emsp;&emsp;查询&emsp;&emsp;&emsp;&emsp;&emsp;查询&emsp;&emsp;&emsp;内部&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;目标与指标

&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;外部&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;适应性&emsp;&emsp;保留性

&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;隐式&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;跨智能体&emsp;&emsp;&emsp;&emsp;泛化性&emsp;&emsp;效率&emsp;&emsp;安全性

&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;混合

**跨维度进化维度**&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;**评估范式**

在线/离线&emsp;&emsp;在线/离线策略&emsp;&emsp;粒度&emsp;&emsp;静态&emsp;&emsp;短时域&emsp;&emsp;长时域

答案&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;答案

**图 3：自进化智能体的全面概览。** 从左到右、从上到下，该图反映了第 3-7 节的组织结构。进化什么（第 3 节）将智能体组件分解为：模型、上下文、工具和架构，展示进化发生的位置。何时进化（第 4 节）区分测试时内与测试时际自进化，对应于 ICL、SFT 和 RL 范式。如何进化（第 5 节）总结了方法论家族——基于奖励、模仿与示范以及基于种群——以及跨维度维度，如在线/离线、在线/离线策略和奖励粒度。在何处进化（第 6 节）对比通用目的和领域特定部署（如编程、GUI、金融、医疗、教育）。评估（第 7 节）概述了目标与指标——适应性、泛化性、效率、安全性——以及相应的评估范式（静态、短时域、长时域）。总体而言，该分类体系映射了综述的推理流程：定义进化什么、何时进化以及如何进化，为评估和推进自进化智能体奠定了基础。