# ReAct 范式学习提示词：基于 LangChain 与 LangGraph

```markdown
你是一名资深 Agent 系统架构师、LangChain / LangGraph 工程实践导师和 AI 工程学习规划专家。

我现在准备开始系统学习 Agent 的三种基础范式，其中第一阶段先学习 **ReAct 范式**。我希望通过 **LangGraph 和 LangChain** 这两个常用 Agent 框架来理解和实践 ReAct，因此请你围绕“ReAct 范式 + LangGraph + LangChain 实践”帮我制定一份系统学习指导。

---

# 一、学习目标

我的阶段性目标是：

1. 理解 ReAct 范式的核心思想：
   - Reasoning 与 Acting 如何交替进行；
   - Thought / Action / Observation 的基本循环；
   - ReAct 与普通 Chain、Tool Calling、Function Calling 的区别；
   - ReAct 适合什么任务，不适合什么任务。

2. 掌握 ReAct 在工程中的实现方式：
   - 如何设计工具；
   - 如何让模型选择工具；
   - 如何处理工具返回结果；
   - 如何控制循环次数、防止死循环；
   - 如何做异常兜底和输出约束。

3. 对比学习 LangChain 和 LangGraph：
   - LangChain 中 ReAct Agent 的基本用法；
   - LangGraph 中 ReAct / Tool-use Agent 的构建方式；
   - 两者在状态管理、流程控制、可观测性、工程扩展性上的区别；
   - 哪些场景适合用 LangChain，哪些场景更适合用 LangGraph。

4. 最终产出一个最小可运行 Demo：
   - 场景要足够简单，工作量不要太大；
   - 重点是帮助我理解 ReAct 的思想，而不是堆复杂功能；
   - Demo 最好能体现工具调用、推理决策、观察结果、最终回答这条完整链路。

---

# 二、资料检索要求

请你联网检索并参考最新、权威的学习资料，优先参考以下来源：

1. ReAct 原始论文或官方介绍；
2. LangChain 官方文档；
3. LangGraph 官方文档；
4. OpenAI / Anthropic / LangChain 官方关于 Agent、Tool Calling、Function Calling、Agent 架构的说明；
5. 高质量工程博客或示例项目。

请你不要只罗列链接，而是要帮我判断这些资料分别适合学习什么内容。

对于每份资料，请说明：

- 资料名称；
- 链接；
- 适合学习的内容；
- 推荐阅读顺序；
- 是否必须阅读；
- 阅读时应该重点关注哪些章节或代码位置。

如果资料过多，导致最终 Markdown 内容超过上下文窗口，请不要强行展开全部内容，而是把资料链接、关键章节、关键代码文件位置整理到 Markdown 中，方便我后续逐个学习。

---

# 三、请重点讲清楚的问题

请围绕以下问题进行讲解：

## 1. ReAct 范式基础

请解释：

- ReAct 是什么；
- 为什么要把 Reasoning 和 Acting 结合起来；
- Thought / Action / Observation / Final Answer 分别代表什么；
- ReAct 相比普通 Prompt Chain 的优势；
- ReAct 容易出现的问题，比如工具误用、循环失控、幻觉 Action、观察结果理解错误等。

## 2. ReAct 工程实现思路

请从工程角度讲清楚：

- 一个 ReAct Agent 通常由哪些模块组成；
- LLM、Prompt、Tool、Parser、Executor、Memory / State 分别负责什么；
- 工具应该如何设计；
- 工具描述为什么会影响模型选择；
- Agent 如何决定下一步调用哪个工具；
- 如果没有合适工具，Agent 应该如何处理；
- 如何设置最大迭代次数；
- 如何设计异常处理和兜底回复。

## 3. LangChain 中的 ReAct

请讲清楚：

- LangChain 实现 ReAct 的基本方式；
- create_react_agent / AgentExecutor / tools / prompt 的作用；
- LangChain 适合用来快速搭建什么类型的 Agent；
- LangChain 在复杂流程控制方面有哪些局限；
- 给出一个最小代码结构示例，不需要太复杂。

## 4. LangGraph 中的 ReAct

请讲清楚：

- LangGraph 相比 LangChain 的核心优势；
- StateGraph、Node、Edge、Conditional Edge、State 分别是什么；
- LangGraph 如何表达 ReAct 循环；
- LangGraph 为什么更适合复杂 Agent 编排；
- 给出一个最小代码结构示例，不需要太复杂。

## 5. LangChain 与 LangGraph 对比

请从以下维度做对比：

| 维度 | LangChain | LangGraph |
|---|---|---|
| 上手难度 |  |  |
| 适合场景 |  |  |
| 流程控制能力 |  |  |
| 状态管理能力 |  |  |
| 可观测性 |  |  |
| 复杂 Agent 扩展能力 |  |  |
| 推荐学习顺序 |  |  |

最后请给出你的学习建议：

- 初学者应该先学哪个；
- 如果目标是成为 Agent 工程师，应该重点掌握哪个；
- 两者应该如何配合学习。

---

# 四、实践 Demo 要求

请你帮我设计一个最小实践项目，要求如下：

## Demo 目标

这个 Demo 不追求复杂功能，而是帮助我真正理解 ReAct 的完整流程。

要求体现：

1. 用户输入一个问题；
2. Agent 进行推理；
3. Agent 判断是否需要调用工具；
4. Agent 调用工具；
5. 工具返回 Observation；
6. Agent 根据 Observation 继续推理；
7. Agent 给出最终答案。

## Demo 场景要求

请你帮我选择一个最简单、适合入门的场景。

优先考虑以下方向：

- 本地知识库查询小助手；
- 课程学习资料查询助手；
- 简单天气 / 时间 / 计算器工具助手；
- GitHub README 问答助手；
- Markdown 笔记检索助手；
- 简单订单状态查询助手。

要求：

- 不依赖复杂数据库；
- 不依赖复杂前端；
- 最好只用 Python 脚本或简单命令行运行；
- 工具数量控制在 2—3 个；
- 能分别用 LangChain 和 LangGraph 实现对比版本；
- 最终能产出一个可运行 Demo。

## Demo 输出内容

请你给出：

1. 推荐 Demo 方向；
2. 为什么选这个方向；
3. 项目目录结构；
4. 需要安装的依赖；
5. 每个文件的作用；
6. LangChain 版本实现思路；
7. LangGraph 版本实现思路；
8. 核心代码示例；
9. 如何运行；
10. 如何验证 Agent 是否真的发生了 ReAct 循环；
11. 后续可以如何扩展。

---

# 五、输出格式要求

请你最终整理成一份适合作为长期学习笔记的 Markdown 文档。

文档结构建议如下：

```markdown
# ReAct 范式学习指南：基于 LangChain 与 LangGraph

## 1. 学习目标

## 2. ReAct 范式核心思想

## 3. ReAct 的工程组成

## 4. ReAct 的适用边界与常见问题

## 5. LangChain 中的 ReAct 实现

## 6. LangGraph 中的 ReAct 实现

## 7. LangChain 与 LangGraph 对比

## 8. 推荐学习资料与阅读顺序

## 9. 最小实践 Demo 设计

## 10. Demo 项目结构

## 11. LangChain 版本实现方案

## 12. LangGraph 版本实现方案

## 13. 运行与验证方法

## 14. 后续扩展方向

## 15. 学习路线与检查清单
```

请注意：

- 内容要系统，但不要堆砌概念；
- 要以工程实践为导向；
- 要告诉我“为什么这样学”和“学完能做什么”；
- 不要只给链接，要帮我筛选和解释资料价值；
- 如果内容太多，请优先保证资料链接、关键章节、Demo 方案和学习路线完整；
- Markdown 要适合我直接保存为学习笔记。
```
