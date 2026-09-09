---
created: 2026-09-08
type: learning
tags: [AI, Agent, 学习路线]
aliases: [AI Agent 学习路径, Agent 开发学习]
source: Hermes Agent + 社区资料整理
status: in-progress
start_date: 2026-09-08
target_date: 2026-12-31
---

# AI Agent 学习路线

## 学习目标

从零开始系统学习 AI Agent 开发，掌握从基础概念到生产部署的完整技能链，最终能独立构建多 Agent 协作系统。

---

## 第一阶段：基础准备（2-3 周）

### 1.1 Python 进阶

| 主题 | 要点 | 资源 |
|---|---|---|
| 类型系统 | Type Protocol、泛型、Pydantic | Python 官方文档 |
| 异步编程 | asyncio、aiohttp、异步生成器 | Real Python |
| 设计模式 | 策略、观察者、工厂、单例 | 《Head First 设计模式》 |
| 函数式工具 | functools、itertools、operator | 官方文档 |

### 1.2 LLM 基础

| 主题 | 要点 |
|---|---|
| Transformer 架构 | Self-Attention、位置编码、KV Cache |
| 主流模型 | GPT、Claude、Gemini、LLaMA、Qwen 系列差异 |
| Prompt Engineering | Few-shot、Chain-of-Thought、ReAct、结构化输出 |
| Tokenizer | BPE、SentencePiece、tiktoken 计算 |

### 1.3 API 调用

```python
# OpenAI SDK 示例
from openai import OpenAI
client = OpenAI()
response = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "Hello"}],
    tools=[...]
)
```

**实践**：用 Python 封装一个通用 LLM 调用类，支持多 Provider 切换。

---

## 第二阶段：工具链入门（3-4 周）

### 2.1 Function Calling / Tool Use

| 概念 | 说明 |
|---|---|
| 工具定义 | JSON Schema 描述函数签名 |
| 并行调用 | 单次回复触发多个工具 |
| 工具选择 | 模型自主判断何时调用、调用哪个 |
| 错误处理 | 工具失败时的重试与降级策略 |

### 2.2 RAG（检索增强生成）

```
用户提问 → 向量化 → 向量数据库检索 → 拼接上下文 → LLM 生成
```

| 组件 | 选型 |
|---|---|
| Embedding | OpenAI text-embedding-3、BGE、m3e |
| 向量数据库 | Chroma、Milvus、Pinecone、Weaviate |
| 文档解析 | Unstructured、Marker、MinerU |
| 分块策略 | 递归分块、语义分块、滑动窗口 |

### 2.3 框架对比

| 框架 | 定位 | 适用场景 |
|---|---|---|
| **OpenAI Agents SDK** | 官方轻量 | 快速原型、单 Agent |
| **CrewAI** | 多 Agent 协作 | 角色分工、团队协作 |
| **AutoGen** | 微软出品 | 对话式多 Agent |
| **LangGraph** | 图编排 | 复杂工作流、状态机 |
| **LlamaIndex** | RAG 优先 | 知识库问答 |
| **Hermes Agent** | 全功能 Agent OS | 生产部署、多平台 |

**实践**：用 CrewAI 构建一个"研究员 + 撰稿人"双 Agent 协作系统。

---

## 第三阶段：Agent 核心能力（4-6 周）

### 3.1 记忆系统

| 类型 | 实现 | 工具 |
|---|---|---|
| 短期记忆 | 对话上下文窗口 | 内置 |
| 工作记忆 | 当前任务状态 | Session State |
| 长期记忆 | 向量数据库 + 图数据库 | Mem0、Zep、Honcho |
|  episodic 记忆 | 事件序列存储 | 自定义 |

### 3.2 规划与推理

| 策略 | 说明 |
|---|---|
| ReAct | Reasoning + Acting 交替执行 |
| Plan-and-Execute | 先规划再逐步执行 |
| Tree of Thoughts | 多路径探索 + 回溯 |
| Reflexion | 自我反思 + 迭代改进 |

### 3.3 多 Agent 协作

```
┌─────────────────────────────────────────────┐
│              Orchestrator Agent              │
│            （任务分解 + 调度）                 │
├─────────┬─────────┬─────────┬───────────────┤
│ Researcher│ Coder  │ Reviewer│   Executor    │
│  信息收集  │ 代码生成 │ 质量审查 │   执行验证     │
└─────────┴─────────┴─────────┴───────────────┘
```

| 模式 | 说明 |
|---|---|
| 层级式 | 上级分配、下级执行 |
| 协作式 | 平等协商、投票决策 |
| 竞争式 | 多方案 PK、最优选择 |

### 3.4 安全与对齐

| 主题 | 要点 |
|---|---|
| Prompt Injection | 输入过滤、指令隔离 |
| 工具滥用 | 权限沙箱、操作审批 |
| 幻觉检测 | 事实核查、置信度阈值 |
| 输出过滤 | 敏感词、PII 检测 |

**实践**：为 Agent 添加三层安全沙箱（输入过滤 + 工具权限 + 输出审查）。

---

## 第四阶段：工程化与进阶（4-6 周）

### 4.1 可观测性

| 工具 | 用途 |
|---|---|
| LangSmith | LangChain 应用追踪 |
| Langfuse | 开源 LLM 可观测性 |
| OpenTelemetry | 分布式追踪 |
| Weights & Biases | 实验追踪 |

### 4.2 评估体系

| 维度 | 指标 |
|---|---|
| 任务完成率 | 端到端成功率 |
| 效率 | Token 消耗、延迟、工具调用次数 |
| 质量 | 输出准确性、完整性、格式合规 |
| 安全 | 注入成功率、违规率 |

### 4.3 部署架构

```
用户 → API Gateway → Agent Service → LLM Provider
                ↓
        ┌───────┴───────┐
        ↓               ↓
   Tool Services    Memory Store
   (微服务)         (向量DB + 图DB)
```

| 组件 | 选型 |
|---|---|
| 服务框架 | FastAPI / LitServe |
| 消息队列 | Redis / RabbitMQ |
| 状态管理 | Redis / PostgreSQL |
| 容器化 | Docker + Docker Compose |
| 编排 | Kubernetes |

### 4.4 MCP（Model Context Protocol）

| 概念 | 说明 |
|---|---|
| MCP Server | 标准化工具暴露协议 |
| MCP Client | Agent 侧的工具调用方 |
| 资源 | 文件、数据库、API 的抽象 |
| 提示 | 可复用的 Prompt 模板 |

**实践**：用 Hermes Agent 接入 3 个 MCP 服务器（搜索、文件、数据库）。

---

## 第五阶段：项目实战（持续）

### 推荐项目

| 项目 | 涉及技能 |
|---|---|
| **个人 AI 助手** | 全栈：记忆 + 工具 + 多平台 + 安全 |
| **代码审查 Agent** | Git 集成 + 静态分析 + 报告生成 |
| **自动化新闻聚合** | 爬虫 + 摘要 + 分类 + 定时推送 |
| **客服 Agent** | RAG + 工单系统 + 人工转接 |
| **数据分析 Agent** | SQL 生成 + 可视化 + 洞察提取 |

---

## 学习资源

### 文档

| 资源 | 链接 |
|---|---|
| OpenAI Agents SDK | https://openai.github.io/openai-agents-python/ |
| CrewAI Docs | https://docs.crewai.com/ |
| LangGraph Docs | https://langchain-ai.github.io/langgraph/ |
| Hermes Agent Docs | https://hermes-agent.nousresearch.com/docs |
| Anthropic MCP | https://modelcontextprotocol.io/ |

### 课程

| 课程 | 平台 |
|---|---|
| AI Agents in LangGraph | DeepLearning.AI |
| Multi AI Agent Systems with crewAI | DeepLearning.AI |
| Building Systems with ChatGPT API | DeepLearning.AI |

### 论文

| 论文 | 核心贡献 |
|---|---|
| ReAct (2022) | 推理+行动交替 |
| Reflexion (2023) | 自我反思改进 |
| AutoGen (2023) | 多 Agent 对话框架 |
| LATS (2024) | 树搜索 + 反思 |

---

## 相关链接

- [[Hermes-Agent-架构分析]]
- [[CrewAI-快速入门]]
- [[RAG-系统设计]]
- [[MCP-协议详解]]
- [[LLM-安全攻防]]

---

## 总结

> **核心理念**：Agent = LLM + 工具 + 记忆 + 规划 + 安全
> 
> **学习路径**：基础 → 工具链 → 核心能力 → 工程化 → 项目实战
> 
> **关键原则**：先跑通再优化，先单 Agent 再多 Agent，先安全再开放。

---

*由 Hermes Agent 创建于 2026-09-08 · 状态：进行中*
