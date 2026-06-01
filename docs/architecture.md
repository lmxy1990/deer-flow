# DeerFlow 2.0 架构文档

## 概述

DeerFlow 是一个基于 LangGraph 构建的 AI 智能体编排平台。它提供了一个 Web 端对话界面，用户可以与主智能体（Lead Agent）交互，主智能体可以将任务委派给子智能体、在沙箱中执行代码、搜索互联网，并通过 MCP/ACP 协议调用外部工具。

```
┌─────────────────────────────────────────────────────────┐
│                      Nginx :2026                        │
│            /api/* → Gateway    / → Frontend             │
└──────────┬────────────────────────────┬─────────────────┘
           │                            │
   ┌───────▼───────┐           ┌───────▼───────┐
   │   Gateway     │           │   Frontend    │
   │   (FastAPI)   │           │   (Next.js)   │
   │   :8001       │           │   :3000       │
   └───────┬───────┘           └───────────────┘
           │
   ┌───────▼───────────────────────────────┐
   │         deerflow-harness              │
   │  ┌──────────┐  ┌──────────────────┐   │
   │  │ 主智能体  │  │   中间件链       │   │
   │  │ (Lead)   │←─│  (18+ 组件)     │   │
   │  └────┬─────┘  └──────────────────┘   │
   │       │                               │
   │  ┌────▼─────────────────────────────┐ │
   │  │           工具层                  │ │
   │  │  沙箱 · 搜索 · MCP · ACP        │ │
   │  │  子智能体 · 社区工具             │ │
   │  └──────────────────────────────────┘ │
   └───────────────────────────────────────┘
```

---

## 技术栈

### 后端

| 层级 | 技术 | 版本 |
|---|---|---|
| Web 框架 | FastAPI | 0.115+ |
| ASGI 服务器 | uvicorn | 0.34+ |
| 智能体框架 | LangGraph + LangChain | 0.5+ |
| LLM SDK | langchain-openai, langchain-anthropic, langchain-deepseek, langchain-google-genai, langchain-ollama | — |
| ORM | SQLAlchemy (异步) | 2.0+ |
| 数据库 | SQLite (WAL) / PostgreSQL (asyncpg) / 内存 | — |
| 数据库迁移 | Alembic | — |
| 流式传输 | sse-starlette | — |
| 文档处理 | markitdown | — |
| Python | 3.10+ | — |

### 前端

| 层级 | 技术 | 版本 |
|---|---|---|
| 框架 | Next.js (App Router) | 16 |
| UI 库 | React | 19 |
| 开发语言 | TypeScript | 5.8 |
| 样式方案 | Tailwind CSS | 4 |
| UI 组件库 | Shadcn UI (基于 Radix UI) | — |
| 状态管理 | TanStack Query + React Hooks | — |
| 流式客户端 | @langchain/langgraph-sdk (useStream) | — |
| 代码编辑器 | CodeMirror (@uiw/react-codemirror) | — |
| 语法高亮 | shiki | — |
| 动画 | GSAP + Framer Motion | — |
| 包管理器 | pnpm | 10.26+ |

### 基础设施

| 组件 | 技术 |
|---|---|
| 反向代理 | Nginx (Alpine) |
| 容器化 | Docker + Docker Compose |
| 沙箱 | 本地 / Docker (DooD) / Kubernetes |

---

## 项目结构

```
deer-flow/
├── backend/
│   ├── app/                          # 应用层（FastAPI 网关 + IM 渠道）
│   │   ├── gateway/
│   │   │   ├── app.py                # FastAPI 应用工厂 (create_app)
│   │   │   └── routers/              # API 路由处理器
│   │   └── channels/                 # IM 集成（Telegram、Slack、飞书等）
│   ├── packages/
│   │   └── harness/                  # deerflow-harness（可发布的 PyPI 包）
│   │       └── deerflow/
│   │           ├── agents/           # 主智能体 + 中间件链
│   │           ├── sandbox/          # 代码执行沙箱抽象
│   │           ├── community/        # 社区工具集成
│   │           ├── subagents/        # 子智能体委派系统
│   │           ├── tools/            # 工具组装与注册
│   │           ├── mcp/              # 模型上下文协议（MCP）集成
│   │           ├── models/           # LLM 模型工厂
│   │           ├── skills/           # 技能发现与加载
│   │           ├── config/           # 基于 Pydantic 的配置系统
│   │           ├── runtime/          # RunManager、StreamBridge、持久化
│   │           ├── persistence/      # SQLAlchemy ORM + 数据库迁移
│   │           ├── tracing/          # LangSmith / Langfuse 集成
│   │           ├── guardrails/       # 工具调用前授权
│   │           └── uploads/          # 文件上传管理
│   └── langgraph.json                # LangGraph Studio 注册
├── frontend/
│   └── src/
│       ├── app/                      # Next.js App Router 页面
│       ├── components/
│       │   ├── ui/                   # Shadcn UI 基础组件
│       │   ├── workspace/            # 聊天工作区组件
│       │   └── landing/              # 着陆页模块
│       └── core/
│           ├── api/                  # LangGraph SDK 客户端 + 请求封装
│           ├── threads/              # 会话线程状态管理 Hooks
│           ├── artifacts/            # 产物加载
│           ├── i18n/                 # 国际化（中文、英文）
│           ├── settings/             # 用户偏好设置（localStorage）
│           ├── memory/               # 持久化记忆
│           ├── skills/               # 技能管理
│           └── uploads/              # 文件上传处理
├── skills/
│   ├── public/                       # 23 个内置技能（已提交）
│   └── custom/                       # 用户自定义技能（已忽略）
├── docker/                           # Docker Compose + Nginx 配置
├── scripts/                          # 安装、诊断、部署脚本
├── config.example.yaml               # 参考配置文件
└── Makefile                          # 构建/运行命令
```

### 后端两层架构边界

后端严格区分两个层级：

- **Harness**（`deerflow.*`）：可发布的包，包含所有智能体逻辑。**绝不**导入 `app.*`。
- **App**（`app.*`）：应用特定代码（网关 API、IM 渠道）。**可以**导入 `deerflow.*`。

此边界由 CI 测试（`test_harness_boundary.py`）强制执行。

---

## 智能体系统

### 主智能体（Lead Agent）

核心智能体由 `backend/packages/harness/deerflow/agents/lead_agent/agent.py` 中的 `make_lead_agent()` 创建，使用 LangChain 的 `create_agent()` 构建：

- **动态选择的 LLM**：每个请求可独立配置模型
- **合并的工具集**：来自配置、内置、MCP、ACP、社区等多个来源
- **系统提示词模板**：注入技能、记忆和子智能体指令
- **ThreadState**：扩展自 LangGraph 的 `AgentState`

```python
class ThreadState(AgentState):
    sandbox: NotRequired[SandboxState | None]
    thread_data: NotRequired[ThreadDataState | None]
    title: NotRequired[str | None]
    artifacts: Annotated[list[str], merge_artifacts]
    todos: Annotated[list | None, merge_todos]
    uploaded_files: NotRequired[list[dict] | None]
    viewed_images: Annotated[dict[str, ViewedImageData], merge_viewed_images]
```

### 中间件链

智能体通过一个有序的 18+ 中间件链执行：

```
请求 → ThreadData → Uploads → Sandbox → DanglingToolCall → LLMErrorHandling
     → Guardrail → SandboxAudit → ToolErrorHandling → DynamicContext
     → Summarization → Todo → TokenUsage → Title → Memory
     → ViewImage → DeferredToolFilter → SubagentLimit
     → LoopDetection → SafetyFinishReason → Clarification → 响应
```

关键中间件说明：

| 中间件 | 职责 |
|---|---|
| SandboxMiddleware | 获取和管理代码执行沙箱 |
| DynamicContextMiddleware | 将当前日期和用户记忆注入上下文 |
| SummarizationMiddleware | 接近 token 限制时压缩上下文 |
| TodoMiddleware | 任务跟踪，支持计划模式 |
| LoopDetectionMiddleware | 检测并中断重复的工具调用循环 |
| ClarificationMiddleware | 拦截澄清请求，中断智能体执行 |
| SubagentLimitMiddleware | 限制并发子智能体委派数量（最多 3 个） |
| GuardrailMiddleware | 工具调用前的授权检查 |
| MemoryMiddleware | 将对话排入异步记忆更新队列 |
| TitleMiddleware | 首次交互后自动生成会话标题 |

### 工具系统

工具由 `get_available_tools()` 从多个来源组装：

| 来源 | 示例 |
|---|---|
| 沙箱工具 | bash, ls, read/write/str_replace, glob, grep |
| 社区工具 | Tavily 搜索, Jina 抓取, Firecrawl, DuckDuckGo, Exa, Serper |
| MCP 工具 | 从配置的 MCP 服务器动态加载 |
| ACP 工具 | 外部智能体通信协议智能体 |
| 子智能体工具 | `task` 工具，用于委派给专业子智能体 |

### 子智能体

内置子智能体：

- **general-purpose**：通用研究和多步骤任务
- **bash**：Shell 命令执行

支持注册自定义子智能体。`task` 工具将工作委派给具有隔离上下文的子智能体。

---

## 数据流

```
用户输入（浏览器）
    │
    ▼
Next.js 前端 ──SSE──→ Nginx :2026
    │                      │
    │  LangGraph SDK       │  /api/* 代理
    │  client.runs.stream()│
    │                      ▼
    │               FastAPI Gateway :8001
    │                      │
    │               RunManager.create_run()
    │                      │
    │               run_agent() 工作线程
    │                      │
    │               make_lead_agent()
    │                      │
    │               ┌──────▼──────┐
    │               │  LangGraph  │
    │               │  智能体循环  │
    │               │  + 中间件   │
    │               └──────┬──────┘
    │                      │
    │           ┌──────────┼──────────┐
    │           ▼          ▼          ▼
    │        沙箱       搜索       MCP/ACP
    │       (代码)     (网络)     (外部)
    │           │          │          │
    │           └──────────┼──────────┘
    │                      │
    │               StreamBridge (SSE)
    │                      │
    ◄──────────────────────┘
    │
    ▼
useStream hook → React 状态 → UI 重新渲染
```

**完整流程**：

1. 用户在 Next.js 前端输入消息
2. 前端通过 LangGraph SDK 调用 `client.runs.stream()`
3. Nginx 将 `/api/langgraph/*` 重写为 `/api/*` 并代理到 Gateway
4. Gateway 通过 `RunManager` 创建运行任务
5. `run_agent()` 调用 `make_lead_agent()` 构建 LangGraph 智能体
6. 智能体通过中间件链执行，按需使用各种工具
7. 事件通过 `StreamBridge` 以 SSE 方式流式回传
8. 前端的 `useStream` hook 接收事件并更新 React 状态

---

## 前后端通信

### SSE 流式传输（主要方式）

`@langchain/langgraph-sdk` 客户端提供流式接口：

- `client.threads.*` — 会话线程的增删改查
- `client.runs.stream()` — 智能体执行的 SSE 流式传输
- `client.runs.joinStream()` — 重新加入已有流
- `client.runs.wait()` — 阻塞式运行

### REST API（辅助接口）

直接调用 Gateway 的 HTTP 端点，用于：

| 端点 | 功能 |
|---|---|
| `/api/models` | 模型列表 |
| `/api/mcp` | MCP 配置 |
| `/api/memory` | 记忆管理 |
| `/api/skills` | 技能管理 |
| `/api/threads/{id}/uploads` | 文件上传 |
| `/api/threads/{id}/artifacts` | 产物服务 |
| `/api/threads/{id}/suggestions` | 追问建议 |
| `/api/threads/{id}/runs/{rid}/feedback` | 反馈管理 |
| `/api/v1/auth` | 身份认证 |

### CSRF 防护

所有状态变更请求（POST/PUT/DELETE）都包含从 `csrf_token` cookie 读取的 `X-CSRF-Token` 请求头。

---

## 配置系统

### config.yaml

主应用配置文件，带版本跟踪（`config_version: 11`）：

| 配置节 | 内容 |
|---|---|
| `models[]` | LLM 提供商配置（API 密钥、基础 URL、模型名称） |
| `tools` | 工具启用/禁用、社区工具配置 |
| `sandbox` | 沙箱模式（本地/Docker/K8s）、资源限制 |
| `skills` | 技能配置 |
| `memory` | 长期记忆设置 |
| `summarization` | 上下文摘要阈值 |
| `subagents` | 子智能体启用/禁用、自定义智能体定义 |
| `channels` | IM 渠道配置 |
| `database` | 存储后端模式（内存/SQLite/PostgreSQL） |
| `guardrails` | 工具调用前授权提供者 |
| `loop_detection` | 重复工具调用检测阈值 |

### extensions_config.json

运行时可修改的配置：

- MCP 服务器定义（stdio/SSE/HTTP 传输协议）
- 技能启用/禁用状态

### .env

密钥和 API Key：

- `OPENAI_API_KEY`、`ANTHROPIC_API_KEY`、`DEEPSEEK_API_KEY` 等 LLM 密钥
- `TAVILY_API_KEY`、`JINA_API_KEY`、`FIRECRAWL_API_KEY` 等搜索工具密钥
- `LANGSMITH_API_KEY`、`LANGFUSE_*` 等可观测性密钥
- IM 渠道 Token（Telegram、Slack 等）

---

## 数据库与存储

### 三种存储后端模式

| 模式 | Checkpointer | 应用数据 | 适用场景 |
|---|---|---|---|
| `memory`（默认） | `MemorySaver` | 内存 | 开发环境，无持久化 |
| `sqlite` | SQLite (WAL) | 同一个 `.db` 文件 | 单节点生产环境 |
| `postgres` | PostgreSQL | 同一数据库，独立连接池 | 多节点生产环境 |

### 持久化层

基于 SQLAlchemy 异步 ORM，配合 Alembic 数据库迁移。数据模型包括：用户、运行记录、运行事件、会话线程元数据、反馈。

### 记忆系统

基于文件的 JSON 存储，路径为 `.deer-flow/users/{user_id}/memory.json`。存储用户上下文、历史记录和离散事实，支持分类和置信度评分。

### 线程本地存储

每个线程独立目录：`.deer-flow/users/{user_id}/threads/{thread_id}/user-data/{workspace,uploads,outputs}`

---

## 沙箱系统

三种执行模式：

| 模式 | 说明 |
|---|---|
| **本地（Local）** | 直接在宿主机文件系统执行 |
| **Docker（DooD）** | 通过宿主机 Docker 守护进程在隔离容器中执行 |
| **Kubernetes** | 通过 Provisioner 服务（端口 8002）在 K8s Pod 中执行 |

沙箱工具：`bash`、`ls`、`read_file`、`write_file`、`str_replace`、`glob`、`grep`。

---

## 第三方集成

### LLM 提供商

支持 OpenAI、Anthropic/Claude、DeepSeek、Google Gemini、火山引擎/豆包、Ollama、vLLM、OpenRouter、Codex CLI、Claude Code OAuth，以及任何 OpenAI 兼容 API。

### 搜索与网络工具

| 工具 | 功能 |
|---|---|
| Tavily | 网页搜索 + 内容抓取 |
| Jina AI | 通过 Reader API 抓取网页，支持可读性提取 |
| Firecrawl | 网页爬取 |
| DuckDuckGo | 图片搜索 |
| Serper | Google 搜索 API |
| Exa | 神经网络搜索 |
| InfoQuest | BytePlus 智能搜索/爬取 |

### IM 渠道

| 渠道 | 协议 |
|---|---|
| Telegram | Bot API，长轮询 |
| Slack | Socket Mode |
| 飞书/Lark | WebSocket |
| 微信 | 腾讯 iLink，长轮询 |
| 企业微信 | WebSocket |
| 钉钉 | Stream Push，WebSocket |
| Discord | 可选 |

### 可观测性

- **LangSmith**：LLM 调用追踪
- **Langfuse**：会话/用户关联的替代追踪方案

---

## 技能系统

技能是结构化的能力模块 — 包含 `SKILL.md` 文件的目录，文件中有 YAML 前置元数据（名称、描述、许可证、允许的工具）和工作流指令。

**位置**：
- `skills/public/`：23 个内置技能（已提交到版本库）
- `skills/custom/`：用户自定义技能（已忽略）

**内置技能包括**：deep-research（深度研究）、report-generation（报告生成）、ppt-generation（PPT 生成）、web-design-guidelines（网页设计规范）、frontend-design（前端设计）、image-generation（图片生成）、video-generation（视频生成）、podcast-generation（播客生成）、data-analysis（数据分析）、chart-visualization（图表可视化）、code-documentation（代码文档）、academic-paper-review（学术论文审阅）、systematic-literature-review（系统文献综述）、consulting-analysis（咨询分析）、newsletter-generation（通讯生成）、github-deep-research（GitHub 深度研究）等。

技能按需加载（惰性加载），启用后会列在智能体的系统提示词中。

---

## 部署

### Docker Compose（生产环境）

```yaml
services:
  nginx:        # 反向代理，端口 2026，统一入口
  frontend:     # Next.js 生产构建
  gateway:      # FastAPI + uvicorn（4 个工作进程）
  provisioner:  # （可选）K8s 沙箱 Provisioner，端口 8002
```

### Make 命令

| 命令 | 功能 |
|---|---|
| `make setup` | 运行安装向导 |
| `make install` | 安装所有依赖 |
| `make dev` | 启动开发服务器 |
| `make start` / `make stop` | 启动/停止生产服务 |
| `make up` / `make down` | Docker Compose 启动/停止 |
| `make docker-build` | 构建 Docker 镜像 |
