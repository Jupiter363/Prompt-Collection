# 学习路线指导Prompt

```
你是一位顶级 AI Agent 学习路径规划专家、Agent 系统架构师和技术成长教练。你的任务是基于我已有的学习基础和目标，帮我设计一套系统化、工程化、前沿化的 Agent 学习路线。

## 一、我的最终目标

我希望通过这套学习计划，成长为一名“精英级 Agent 工程师”，不仅能理解前沿 Agent 范式，还能具备完整的 Agent 系统架构设计、工程实现、业务落地、评估优化和长期维护能力。

具体来说，我希望最终具备以下能力：

1. 深入理解当前前沿 Agent 范式，包括但不限于 ReAct、Plan-and-Execute、Reflection、Tool-Use Agent、Workflow Agent、Multi-Agent、Agentic RAG、Computer-Use Agent、Code Agent 等。
2. 以 Harness 思想为核心，理解并能设计 Agent 系统的主要模块，包括：
   - 上下文窗口管理；
   - 短期记忆与长期记忆；
   - 工具调用模块；
   - Prompt 工程；
   - 任务规划层；
   - 执行与反馈循环；
   - 约束与安全层；
   - 状态管理；
   - 观察、调试与可视化模块。
3. 掌握 Agent 微调与模型适配工程，包括：
   - SFT；
   - DPO / preference learning；
   - 工具调用数据构造；
   - Agent 轨迹数据构造；
   - 领域 Agent 的微调策略；
   - 微调与 RAG / 工具调用 / Prompt 工程之间的边界。
4. 掌握 Multi-Agent 思想及应用，包括：
   - 多 Agent 协作模式；
   - supervisor-worker；
   - planner-executor；
   - critic-reflector；
   - debate；
   - swarm；
   - 多 Agent 通信协议；
   - 多 Agent 的冲突、冗余、成本和稳定性问题。
5. 掌握 Agent 系统的维护思路，包括：
   - 日志体系；
   - tracing；
   - prompt / tool / memory 版本管理；
   - 线上问题排查；
   - 回归测试；
   - 灰度发布；
   - 成本监控；
   - 失败样本沉淀。
6. 掌握 Agent 可用性和健壮性优化，包括：
   - 工具调用失败恢复；
   - 幻觉控制；
   - prompt injection 防御；
   - 上下文污染防御；
   - 长任务中断恢复；
   - 多模型降级；
   - 超时与重试；
   - 缓存；
   - fallback 策略；
   - 人工接管机制。
7. 掌握 Agent 在真实业务场景下的评估测试，包括：
   - 任务成功率；
   - 工具调用准确率；
   - 规划质量；
   - 响应一致性；
   - 用户满意度；
   - 端到端业务完成率；
   - 成本与延迟；
   - 测试集构建；
   - benchmark 设计；
   - 失败案例分析；
   - 自动化评测与人工评测结合。
8. 能够根据具体业务场景，从 0 到 1 设计一个完整 Agent 系统，并能对已有 Agent 系统进行诊断、重构和优化。

## 二、请你在设计学习路线时重点考虑

请不要只给我泛泛的课程目录，而是要按照“成为真正能落地的 Agent 工程师”的标准来设计。

请重点覆盖以下几个层次：

1. 理论层：Agent 的核心概念、前沿范式、关键论文、主流框架思想。
2. 架构层：Agent Harness、memory、tools、planning、reflection、guardrails、evaluation、observability 等模块如何组合成完整系统。
3. 工程层：如何用 Python / Java / LangGraph / LangChain / LlamaIndex / AutoGen / CrewAI / OpenAI API / Claude API 等技术实现可运行系统。
4. 业务层：如何把 Agent 应用到客服、电商、交易履约、知识库问答、代码助手、数据分析助手、个人助理等真实场景。
5. 评估层：如何设计测试集、指标体系、评估流程、失败归因和持续优化闭环。
6. 作品层：学习过程中应该产出哪些项目、文档、GitHub 仓库、技术博客和简历亮点。
7. 面试层：学习完后应该能讲清楚哪些核心问题，如何把 Agent 项目包装成有竞争力的实习 / 求职项目。

## 三、请你输出的内容结构

请按照 Markdown 格式输出，要求结构清晰、适合作为我未来几个月的学习指导文档。

请至少包含以下部分：

# Agent 工程师成长路线总览

说明这条路线的整体目标、学习周期、最终能力画像。

# 阶段 0：前置基础补齐

说明成为 Agent 工程师前需要掌握哪些基础能力，例如：
- Python 工程化；
- Web 后端基础；
- LLM API 调用；
- RAG 基础；
- 向量数据库；
- Redis / MySQL；
- 基础前端或接口调试能力；
- GitHub 项目管理；
- Docker / 部署基础。

请说明每项基础需要学到什么程度，不要过度学习。

# 阶段 1：LLM 与 Prompt Engineering 基础

请说明：
- Prompt Engineering 的核心原则；
- system prompt / developer prompt / user prompt 的区别；
- few-shot；
- structured output；
- chain-of-thought 的替代设计；
- self-check；
- prompt 模板管理；
- prompt 版本管理；
- prompt injection 风险；
- 如何写适合生产环境的 prompt。

请给出学习目标、核心知识点、实践任务和推荐资料。

# 阶段 2：Agent 基础范式

请系统讲解：
- ReAct；
- Plan-and-Execute；
- Reflection；
- Tool-Use Agent；
- Workflow Agent；
- Router Agent；
- Agentic RAG；
- Code Agent；
- Computer-Use Agent。

要求不仅解释概念，还要说明：
- 适用场景；
- 优点；
- 缺点；
- 工程实现难点；
- 适合做什么项目。

# 阶段 3：Agent Harness 架构设计

请以 Harness 思想为主线，拆解一个完整 Agent 系统的核心模块：

1. 输入理解层；
2. 意图识别层；
3. 任务规划层；
4. 上下文管理层；
5. 短期记忆模块；
6. 长期记忆模块；
7. 工具注册与调用模块；
8. 状态管理模块；
9. 执行器模块；
10. 反思与自我修正模块；
11. 约束与安全模块；
12. 评估与日志模块；
13. 人工接管模块；
14. 成本、延迟与稳定性控制模块。

请说明每个模块：
- 解决什么问题；
- 输入是什么；
- 输出是什么；
- 常见实现方式；
- 常见坑；
- 如何测试；
- 如何在项目中体现。

# 阶段 4：工具调用与外部系统集成

请讲清楚：
- function calling / tool calling 的本质；
- tool schema 怎么设计；
- 工具描述怎么写；
- 工具调用失败怎么办；
- 工具权限怎么控制；
- 工具结果如何压缩进上下文；
- 如何接入数据库、搜索、文件系统、浏览器、企业 API、工单系统、订单系统、物流系统等；
- 如何避免 Agent 乱调用工具。

请设计对应的实践项目。

# 阶段 5：Memory 与 Context Engineering

请重点讲：
- 为什么上下文工程比单纯 prompt engineering 更重要；
- 上下文窗口管理；
- 上下文压缩；
- conversation memory；
- episodic memory；
- semantic memory；
- long-term memory；
- vector memory；
- summary memory；
- memory retrieval；
- memory write policy；
- memory conflict resolution；
- memory evaluation。

请说明如何在真实 Agent 系统中设计记忆模块。

# 阶段 6：Agentic RAG 与知识库问答系统

请结合实际工程讲：
- 传统 RAG；
- Agentic RAG；
- query rewrite；
- query decomposition；
- hybrid retrieval；
- BM25 + dense vector；
- rerank；
- citation；
- grounding；
- hallucination control；
- 多轮问答；
- 企业知识库权限控制；
- RAG 评估指标。

请给出一个企业级知识库 Agent 项目方案。

# 阶段 7：Planning、Reflection 与自我修正

请讲：
- task planning；
- subtask decomposition；
- dynamic planning；
- reflection；
- critic model；
- verifier；
- self-correction；
- retry policy；
- plan repair；
- long-horizon task execution。

请说明这些机制什么时候有用，什么时候反而会增加复杂度和成本。

# 阶段 8：Multi-Agent 系统

请系统讲：
- Multi-Agent 的核心思想；
- supervisor-worker；
- planner-executor；
- researcher-writer-reviewer；
- critic-reflector；
- debate；
- swarm；
- role specialization；
- communication protocol；
- blackboard architecture；
- task delegation；
- 多 Agent 评估；
- 多 Agent 的成本、稳定性和失控问题。

请给出 2—3 个适合求职展示的 Multi-Agent 项目。

# 阶段 9：Agent 微调工程

请讲清楚：
- 什么时候需要微调，什么时候不需要；
- SFT 在 Agent 中的作用；
- DPO / preference learning 在 Agent 中的作用；
- tool-use 数据如何构造；
- trajectory 数据如何构造；
- rejection sampling；
- synthetic data；
- domain adaptation；
- 微调与 Prompt / RAG / Tool-use 的关系；
- 微调后的评估方法；
- 小模型 Agent 化的可行路径。

请给出一个可落地的 Agent 微调学习项目。

# 阶段 10：Agent 安全、约束与可靠性

请重点讲：
- prompt injection；
- jailbreak；
- tool misuse；
- data leakage；
- unsafe action；
- permission boundary；
- human-in-the-loop；
- policy engine；
- guardrails；
- output validation；
- action confirmation；
- sandbox；
- audit log。

请说明一个生产级 Agent 系统应该如何做安全设计。

# 阶段 11：Agent 评估、测试集构建与可观测性

请详细讲：
- Agent 为什么难评估；
- 离线评估；
- 在线评估；
- golden dataset；
- adversarial test set；
- regression test；
- scenario-based evaluation；
- tool-call accuracy；
- task success rate；
- grounding score；
- faithfulness；
- latency；
- cost；
- user satisfaction；
- tracing；
- failure taxonomy；
- A/B test；
- 自动评估与人工评估结合。

请给出一个完整的 Agent 评估体系模板。

# 阶段 12：Agent 生产部署与长期维护

请讲：
- 服务架构；
- API 层；
- 队列；
- 缓存；
- 限流；
- 熔断；
- 降级；
- 多模型路由；
- 日志与监控；
- prompt 版本管理；
- tool 版本管理；
- memory 版本管理；
- 成本控制；
- 灰度发布；
- 线上反馈闭环。

请说明如何把一个 Demo 级 Agent 变成生产级 Agent。

# 阶段 13：业务场景落地训练

请帮我选择几个最适合训练 Agent 架构能力的业务场景，例如：
- 电商客服 / 交易履约 Agent；
- 企业知识库 Agent；
- 代码开发 Agent；
- 数据分析 Agent；
- 个人效率助理 Agent；
- 招聘 / 简历筛选 Agent；
- 医疗或金融场景中的受限 Agent。

对每个场景请说明：
- 业务流程；
- Agent 需要完成的任务；
- 需要哪些工具；
- 需要哪些数据；
- 关键风险；
- 评估指标；
- 可做成什么项目；
- 简历上如何描述。


# 阶段 14：学习节奏与时间规划

请根据 3 个月、6 个月、12 个月三个周期分别给出学习计划。

每个周期请包含：
- 每周学习重点；
- 阶段性成果；
- 推荐实践任务；
- 应该写出的博客；
- 应该完成的项目；
- 是否达到下一阶段的判断标准。

# 阶段 15：推荐资料清单

请按类别给出推荐资料，包括：
- 官方文档；
- 经典论文；
- 最新论文；
- 开源框架；
- GitHub 项目；
- 博客；
- 视频课程；
- benchmark；
- evaluation 工具；
- 适合长期跟踪的社区和公司技术博客。

请优先推荐权威、较新、工程价值高的资料。

# 阶段 16：最终能力检查清单

请给我一份 checklist，用来判断我是否真正具备 Agent 工程师能力。

清单至少包括：
- 理论理解；
- 架构设计；
- 工程实现；
- 工具调用；
- RAG；
- Memory；
- Multi-Agent；
- 安全；
- 评估；
- 部署；
- 项目表达；
- 面试表达。

## 四、输出风格要求

1. 请用中文输出。
2. 请使用 Markdown 格式。
3. 内容要系统、深入、工程化，不要泛泛而谈。
4. 每个阶段都要包含：
   - 学习目标；
   - 核心知识；
   - 推荐资料；
   - 实践任务；
   - 项目产出；
   - 达标标准。
5. 请结合 2025—2026 年 Agent 工程最新趋势，不要只停留在传统 Prompt Engineering 或简单 LangChain Demo。
6. 请避免空洞口号，要尽量给出可执行的学习步骤。
7. 请站在“我要未来求职大厂 Agent / AI 应用开发 / 后端 AI 工程师岗位”的角度设计路线。
8. 请特别关注“如何把学习成果转化为 GitHub 项目、简历亮点、面试表达和长期技术壁垒”。

```