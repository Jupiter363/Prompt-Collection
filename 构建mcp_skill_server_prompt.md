# MCP Skill Server 搭建技术方案生成提示词

你是一名资深 Java Agent 平台架构师、MCP 协议专家、Spring AI 工程专家和企业级后端系统设计专家。

目前我的项目已经完成了以下基础工作：

1. MCP Client Gateway 已经按照前期方案搭建成功；
2. MCP Client Gateway 已经能够完成 MCP Server 连接、tools/list 工具发现、tools/call 工具调用、调用日志记录和基础权限过滤；
3. MCP Client Gateway 已经接入到 Agent 主体中；
4. Agent 主体采用 Plan-and-Execute 模式，已经具备 AgentRun、PlanGenerator、PlanAndExecuteService、StepExecutor、SkillMatcher、SkillInvoker、McpSkillInvoker 等核心执行链路；
5. 当前 Agent 可以通过 MCP Client Gateway 调用外部 MCP Tool；
6. 现在需要继续补齐 MCP Server 侧能力，让平台能够远程提供 Skill，使 MCP Client Gateway 可以发现并调用这些 Skill，从而打通完整链路。

现在我要做的不是 MCP Client Gateway，而是要搭建一个 MCP Server，用来把平台内部 Skill、业务能力、测试工具或企业系统能力暴露为标准 MCP Tool，供 MCP Client Gateway 远程连接和调用。

请你基于以上背景，为我设计一套完整、可落地、适合 Java / Spring Boot / Spring AI 技术栈的 MCP Server 搭建方案。

---

## 一、当前项目背景

我现在的整体架构目标是：

```text
用户请求
  ↓
Agent Runtime / Plan-and-Execute
  ↓
SkillMatcher / SkillInvoker
  ↓
McpSkillInvoker
  ↓
MCP Client Gateway
  ↓
远程 MCP Server
  ↓
具体 Skill / 企业业务能力
  ↓
返回 Tool Result
  ↓
Agent 汇总最终结果
```

现在已经完成的是：

```text
Agent 主体
  ↓
MCP Client Gateway
```

现在需要补齐的是：

```text
MCP Server
  ↓
Skill 执行层
```

也就是说，目标是让 MCP Server 远程提供 Skill，MCP Client Gateway 可以通过 tools/list 发现 Skill，通过 tools/call 调用 Skill，Agent 最终可以通过 Planner 自动选择并调用这些远程 Skill。

---

## 二、请先联网调研

在正式输出方案前，请先联网搜索并参考最新资料，重点查找：

1. Model Context Protocol 官方 MCP Server 规范；
2. MCP Server 的 tools/list、tools/call 机制；
3. MCP Streamable HTTP / SSE / stdio transport 的区别；
4. Spring AI MCP Server Starter 的最新用法；
5. Java MCP SDK / Spring AI MCP Server 示例；
6. 企业级 MCP Server 的安全、权限、认证、审计设计；
7. MCP Server 如何把内部业务能力暴露为 Tool；
8. MCP Server 与 Agent / MCP Client Gateway / Skill Registry 的关系。

请在方案中标注关键参考来源，不要凭空生成过时方案。

---

## 三、MCP Server 的目标定位

请先明确这个 MCP Server 的定位。

它不是：

- 不是新的 Agent；
- 不是新的 MCP Client；
- 不是替代 MCP Client Gateway；
- 不是简单 Controller；
- 不是普通 HTTP API 网关。

它应该是：

- 平台内部 Skill 的标准化暴露层；
- Agent 平台对外提供 Tool 能力的协议适配层；
- MCP Client Gateway 可连接的远程工具服务；
- 企业内部业务能力接入 Agent 的 Server 端入口；
- 未来可演进为 MCP Skill Server / Skill Provider。

请你给出一句话定位。

---

## 四、请设计总体架构

请围绕下面链路设计完整架构：

```text
Agent Runtime
  ↓
McpSkillInvoker
  ↓
MCP Client Gateway
  ↓
MCP Server Transport Layer
  ↓
MCP Tool Registry
  ↓
Skill Adapter
  ↓
Skill Executor
  ↓
Local Java Skill / Business API / Database Query / ERP System / Workflow
```

请说明每一层的职责：

1. Agent Runtime 负责什么；
2. MCP Client Gateway 负责什么；
3. MCP Server 负责什么；
4. Tool Registry 负责什么；
5. Skill Adapter 负责什么；
6. Skill Executor 负责什么；
7. 企业系统或本地 Skill 负责什么。

同时请说明：

- MCP Server 和 MCP Client Gateway 的边界；
- MCP Server 和普通业务 API 的区别；
- MCP Server 和 Skill Registry 的关系；
- MCP Server 是否应该独立部署；
- MCP Server 是否应该和 Agent 主体解耦；
- MCP Server 是否可以按业务域拆分，例如 ERP MCP Server、供应链 MCP Server、文件 MCP Server。

---

## 五、请设计 MCP Server 的核心能力

请详细设计 MCP Server 至少应该具备的能力。

### 1. Tool 暴露能力

MCP Server 需要能够把内部 Skill 暴露为 MCP Tool。

请说明：

- 如何定义 Tool 名称；
- 如何定义 Tool 描述；
- 如何定义 inputSchema；
- 如何定义 outputSchema；
- 如何定义 Tool annotations；
- 如何把 SkillDefinition 映射为 MCP Tool；
- 如何把 Java 方法映射为 MCP Tool；
- 如何支持静态注册和动态注册。

### 2. tools/list 能力

请说明 MCP Client Gateway 连接 MCP Server 后，如何发现工具列表。

要求说明：

- tools/list 返回哪些字段；
- Tool schema 如何生成；
- Tool 描述如何帮助 Agent Planner 选择工具；
- Tool annotations 如何表达只读、破坏性、幂等等属性；
- 工具列表是否需要缓存；
- 工具变更后如何刷新。

### 3. tools/call 能力

请说明 MCP Client Gateway 调用工具时，MCP Server 如何处理。

要求说明完整流程：

```text
接收 tools/call
  ↓
校验 toolName 是否存在
  ↓
校验 arguments 是否符合 inputSchema
  ↓
校验权限和风险等级
  ↓
调用对应 Skill
  ↓
处理异常和超时
  ↓
标准化 Tool Result
  ↓
返回给 MCP Client Gateway
```

### 4. Skill Adapter 能力

请说明如何把不同类型 Skill 接入 MCP Server：

- Local Java Bean Skill；
- HTTP API Skill；
- Database Query Skill；
- Workflow Skill；
- ERP / 供应链系统 Skill；
- 文件处理 Skill；
- Mock Demo Skill；
- 后续 Python Skill。

请给出统一的 SkillInvoker / SkillAdapter 设计。

### 5. 安全能力

请重点设计：

- MCP Client 身份认证；
- API Key / Token / OAuth2；
- Tool 白名单；
- Tool 风险分级；
- 只读工具默认放行；
- 写操作人工确认或禁用；
- 参数校验；
- 敏感信息脱敏；
- 审计日志；
- 防止 Prompt Injection 污染 Tool Description；
- 防止越权调用内部业务系统。

### 6. 可观测能力

请设计：

- Tool 调用日志；
- 请求 ID / Trace ID；
- 入参摘要；
- 出参摘要；
- 成功失败状态；
- costMs；
- 异常原因；
- 调用方 clientName；
- AgentRunId / StepId 透传；
- Prometheus 指标；
- 健康检查接口。

---

## 六、请给出 Java / Spring Boot 技术选型

请基于 Java 技术栈设计。

推荐考虑：

- Java 17 / Java 21；
- Spring Boot 3.x；
- Spring AI MCP Server Starter；
- Spring Web 或 WebFlux；
- Spring Validation；
- Spring Security；
- MyBatis-Plus / JPA；
- MySQL / PostgreSQL；
- Redis，可选；
- Knife4j / Swagger；
- Actuator；
- Micrometer / Prometheus；
- OpenTelemetry；
- Docker 部署。

请说明：

1. MVP 阶段必须引入哪些依赖；
2. 哪些依赖可以后置；
3. Spring Web 和 WebFlux 如何选择；
4. Streamable HTTP、SSE、stdio 哪种更适合企业远程 Skill Server；
5. 是否建议优先做 Streamable HTTP MCP Server；
6. 如何和现有 MCP Client Gateway 对接。

---

## 七、请设计模块结构

请给出推荐工程结构，例如：

```text
mcp-skill-server
├── controller
│   └── HealthController.java
├── config
│   ├── McpServerConfig.java
│   ├── McpToolRegisterConfig.java
│   └── SecurityConfig.java
├── tool
│   ├── ToolDefinition.java
│   ├── ToolRegistry.java
│   ├── ToolSchemaBuilder.java
│   └── ToolAnnotationBuilder.java
├── skill
│   ├── SkillDefinition.java
│   ├── SkillInvoker.java
│   ├── LocalJavaSkillInvoker.java
│   ├── HttpApiSkillInvoker.java
│   ├── DatabaseSkillInvoker.java
│   └── MockSkillInvoker.java
├── adapter
│   ├── SkillToMcpToolAdapter.java
│   └── McpToolResultAdapter.java
├── service
│   ├── ToolDiscoveryService.java
│   ├── ToolCallService.java
│   └── ToolAuditService.java
├── security
│   ├── ToolPermissionChecker.java
│   ├── ToolRiskClassifier.java
│   └── SensitiveDataMasker.java
├── persistence
│   ├── entity
│   ├── mapper
│   └── repository
└── common
    ├── Result.java
    ├── BizException.java
    └── JsonUtils.java
```

请说明：

- 每个包的职责；
- 哪些是 MVP 必须；
- 哪些可以后续扩展；
- 如何避免 MCP 协议代码和业务 Skill 强耦合。

---

## 八、请设计核心数据模型

请设计 MCP Server 侧需要的数据表或领域对象。

至少包括：

1. `mcp_tool_definition`：用于保存 Tool 元信息；
2. `mcp_skill_mapping`：用于保存 MCP Tool 和内部 Skill 的映射关系；
3. `mcp_tool_call_log`：用于保存工具调用审计日志；
4. `mcp_client_credential`：用于保存允许访问该 Server 的 Client 凭证；
5. `mcp_tool_permission`：用于保存 Tool 权限策略；
6. `mcp_tool_version`，可选：用于后续 Tool 版本管理。

每张表请给出：

- 字段；
- 字段说明；
- 索引；
- 是否 MVP 必须；
- 和现有 Agent / Skill 表的关系。

---

## 九、请设计核心接口与协议映射

虽然 MCP Server 对外主要走 MCP 协议，但为了方便管理和测试，也可以保留管理接口。

请设计：

### 1. MCP 协议能力

- initialize；
- tools/list；
- tools/call；
- resources/list，可选；
- prompts/list，可选。

### 2. 管理接口

- `GET /api/mcp-server/health`；
- `GET /api/mcp-server/tools`；
- `POST /api/mcp-server/tools/register`；
- `POST /api/mcp-server/tools/{toolName}/enable`；
- `POST /api/mcp-server/tools/{toolName}/disable`；
- `GET /api/mcp-server/tool-call-logs`；
- `POST /api/mcp-server/tools/{toolName}/test-call`。

每个接口请给出：

- URL；
- Method；
- Request 示例；
- Response 示例；
- 是否 MVP 必须。

---

## 十、请设计 Tool / Skill 示例

请至少设计 3 个可用于 MVP 演示的 MCP Tool。

### 示例 1：订单查询 Tool

```text
toolName: query_purchase_order
作用：根据采购订单号查询订单状态
风险等级：READ_ONLY
```

### 示例 2：供应商付款状态查询 Tool

```text
toolName: query_supplier_payment_status
作用：根据供应商名称或订单号查询付款状态
风险等级：READ_ONLY
```

### 示例 3：Mock 文件检索 Tool

```text
toolName: search_mock_file
作用：根据关键词检索模拟文件信息
风险等级：READ_ONLY
```

每个 Tool 请给出：

- Tool 描述；
- inputSchema；
- outputSchema；
- Java 方法示例；
- 返回结果示例；
- 如何被 MCP Client Gateway 发现；
- 如何被 Agent Planner 选择。

---

## 十一、请给出核心代码示例

请给出关键代码示例，要求基于 Java / Spring Boot / Spring AI MCP Server。

至少包括：

1. pom.xml 关键依赖；
2. application.yml 配置；
3. MCP Server 启动配置；
4. 一个 Java Tool Bean 示例；
5. Tool 注册方式；
6. Tool 入参 DTO；
7. Tool 返回结果 DTO；
8. SkillInvoker 接口；
9. LocalJavaSkillInvoker 示例；
10. ToolAuditService 示例；
11. 异常处理示例；
12. 和 MCP Client Gateway 联调的配置示例。

代码不需要覆盖所有细节，但要保证结构真实、可落地。

---

## 十二、请设计和现有 Agent 主体的联调流程

请重点说明怎么验证全链路：

```text
MCP Server 启动
  ↓
MCP Client Gateway 配置远程 Server 地址
  ↓
MCP Client Gateway 调用 tools/list
  ↓
MCP Client Gateway 保存 Tool Snapshot
  ↓
Agent SkillDefinition 绑定 MCP Tool
  ↓
用户向 Agent 提问
  ↓
PlanGenerator 生成 SKILL_CALL Step
  ↓
SkillMatcher 匹配 MCP Skill
  ↓
McpSkillInvoker 调用 MCP Client Gateway
  ↓
MCP Client Gateway 调用 MCP Server tools/call
  ↓
MCP Server 执行内部 Skill
  ↓
返回 Tool Result
  ↓
Agent 汇总最终结果
```

请给出：

- 联调前置条件；
- 联调步骤；
- Postman / Swagger 测试顺序；
- 数据库需要准备哪些数据；
- 如何判断 tools/list 成功；
- 如何判断 tools/call 成功；
- 如何判断 Agent 全链路成功；
- 常见错误和排查方式。

---

## 十三、请设计 MVP 开发顺序

请按最小闭环优先原则给出开发顺序。

### 第一阶段：最小 MCP Server

目标：

- Server 能启动；
- Client Gateway 能连上；
- tools/list 能返回工具；
- tools/call 能调用一个 Mock Tool。

### 第二阶段：Skill Adapter

目标：

- 支持 Local Java Skill；
- 支持 HTTP API Skill；
- 支持 SkillDefinition 到 MCP Tool 的映射；
- 支持 inputSchema 参数校验。

### 第三阶段：审计与安全

目标：

- 记录 Tool 调用日志；
- 增加 Client 鉴权；
- 增加 Tool 白名单；
- 增加风险等级；
- 增加敏感信息脱敏。

### 第四阶段：Agent 全链路联调

目标：

- Agent 能通过已有 MCP Client Gateway 调用新 MCP Server；
- Plan Step 能匹配远程 MCP Tool；
- ToolCallRecord 能记录完整调用；
- Agent 能生成最终结果。

请每个阶段给出：

- 开发任务；
- 关键类；
- 核心接口；
- 验收标准；
- 不做哪些复杂功能。

---

## 十四、请输出风险与注意事项

请重点分析：

1. MCP Server 版本和 Spring AI 版本兼容问题；
2. Streamable HTTP / SSE / stdio 选择错误导致联调困难；
3. Tool schema 描述不清导致 Agent 选错工具；
4. inputSchema 不严格导致参数错误；
5. Tool 名称设计不规范导致 Planner 难以匹配；
6. Tool 具备真实业务副作用导致安全风险；
7. MCP Server 暴露内部系统能力带来的越权风险；
8. 公司内网部署无法拉取外部依赖；
9. Agent 调用链路变长导致问题排查困难；
10. Client Gateway 和 Server 之间错误格式不统一。

每个风险都给出解决方案。

---

## 十五、最终输出要求

请最终输出一份完整的《MCP Skill Server 搭建技术方案》。

要求包括：

1. 背景与目标；
2. 当前已完成链路说明；
3. MCP Server 在全链路中的定位；
4. 总体架构图；
5. MCP Client Gateway 与 MCP Server 的边界；
6. MCP Server 核心模块设计；
7. Java / Spring Boot / Spring AI 技术选型；
8. 工程结构；
9. 数据表设计；
10. Tool / Skill 映射设计；
11. tools/list 与 tools/call 流程；
12. 安全与权限设计；
13. 审计与可观测设计；
14. 核心代码示例；
15. 与现有 Agent 主体和 MCP Client Gateway 的联调流程；
16. MVP 开发顺序；
17. 验收标准；
18. 风险与排查清单；
19. 后续演进方向。

输出风格要求：

- 按企业级技术方案写；
- 不要泛泛讲 MCP 概念；
- 要结合我已经完成 MCP Client Gateway 和 Agent 主体的事实；
- 不要重复设计 MCP Client Gateway；
- 重点放在 MCP Server 如何远程提供 Skill；
- 方案要适合 Java Web / Spring Boot 项目落地；
- 每个模块要说明职责、输入、输出、核心逻辑；
- 开发顺序要能指导我直接开始编码；
- 如果信息不足，请先列出需要确认的问题，但不要停止输出，请在合理假设下继续给出方案。
