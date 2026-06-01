# 🦌 DeerFlow - 2.0

[English](./README.md) | 中文 | [日本語](./README_ja.md) | [Français](./README_fr.md) | [Русский](./README_ru.md)

[![Python](https://img.shields.io/badge/Python-3.12%2B-3776AB?logo=python&logoColor=white)](./backend/pyproject.toml)
[![Node.js](https://img.shields.io/badge/Node.js-22%2B-339933?logo=node.js&logoColor=white)](./Makefile)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

<a href="https://trendshift.io/repositories/14699" target="_blank"><img src="https://trendshift.io/api/badge/repositories/14699" alt="bytedance%2Fdeer-flow | Trendshift" style="width: 250px; height: 55px;" width="250" height="55"/></a>
> 2026年2月28日，DeerFlow在2.0版本发布后荣获 🏆 GitHub Trending 第一名。感谢我们出色的社区——是你们创造了这一切！💪🔥

DeerFlow（**D**eep **E**xploration and **E**fficient **R**esearch **Flow**）是一个开源的**超级代理框架**，能够编排**子代理**、**记忆**和**沙盒**来完成几乎任何任务——由**可扩展技能**驱动。

https://github.com/user-attachments/assets/a8bcadc4-e040-4cf2-8fda-dd768b999c18

> [!NOTE]
> **DeerFlow 2.0 是从零开始重写的版本。** 与 v1 没有共享任何代码。如果你在寻找原始的深度研究框架，它在 [`1.x` 分支](https://github.com/bytedance/deer-flow/tree/main-1.x) 上维护——仍然欢迎向该分支贡献。活跃开发已经转移到 2.0。

## 官方网站

[<img width="2880" height="1600" alt="image" src="https://github.com/user-attachments/assets/a598c49f-3b2f-41ea-a052-05e21349188a" />](https://deerflow.tech)

在我们的[**官方网站**](https://deerflow.tech)上了解更多并查看**实际演示**。

## 字节跳动火山引擎编程计划

<img width="4808" height="2400" alt="英文方舟" src="https://github.com/user-attachments/assets/2ecc7b9d-50be-4185-b1f7-5542d222fb2d" />

- 我们强烈推荐使用豆包-Seed-2.0-Code、DeepSeek v3.2 和 Kimi 2.5 来运行 DeerFlow
- [了解更多](https://www.byteplus.com/en/activity/codingplan?utm_campaign=deer_flow&utm_content=deer_flow&utm_medium=devrel&utm_source=OWO&utm_term=deer_flow)
- [中国大陆地区的开发者请点击这里](https://www.volcengine.com/activity/codingplan?utm_campaign=deer_flow&utm_content=deer_flow&utm_medium=devrel&utm_source=OWO&utm_term=deer_flow)

## InfoQuest

DeerFlow 已全新集成字节跳动自研的智能搜索和爬取工具集——[InfoQuest（支持免费在线体验）](https://docs.byteplus.com/en/docs/InfoQuest/What_is_Info_Quest)

<a href="https://docs.byteplus.com/en/docs/InfoQuest/What_is_Info_Quest" target="_blank">
  <img
    src="https://sf16-sg.tiktokcdn.com/obj/eden-sg/hubseh7bsbps/20251208-160108.png"   alt="InfoQuest_banner"
  />
</a>

---

## 目录

- [🦌 DeerFlow - 2.0](#-deerflow---20)
  - [官方网站](#官方网站)
  - [字节跳动火山引擎编程计划](#字节跳动火山引擎编程计划)
  - [InfoQuest](#infoquest)
  - [目录](#目录)
  - [一行命令设置代理](#一行命令设置代理)
  - [快速开始](#快速开始)
    - [配置](#配置)
    - [运行应用程序](#运行应用程序)
      - [部署规模](#部署规模)
      - [方案一：Docker（推荐）](#方案一docker推荐)
      - [方案二：本地开发](#方案二本地开发)
    - [高级功能](#高级功能)
      - [沙盒模式](#沙盒模式)
      - [MCP 服务器](#mcp-服务器)
      - [即时通讯渠道](#即时通讯渠道)
      - [LangSmith 追踪](#langsmith-追踪)
      - [Langfuse 追踪](#langfuse-追踪)
      - [同时使用两个提供商](#同时使用两个提供商)
  - [从深度研究到超级代理框架](#从深度研究到超级代理框架)
  - [核心特性](#核心特性)
    - [技能与工具](#技能与工具)
      - [Claude Code 集成](#claude-code-集成)
    - [子代理](#子代理)
    - [沙盒与文件系统](#沙盒与文件系统)
    - [上下文工程](#上下文工程)
    - [长期记忆](#长期记忆)
  - [推荐模型](#推荐模型)
  - [嵌入式 Python 客户端](#嵌入式-python-客户端)
  - [文档](#文档)
  - [⚠️ 安全注意事项](#️-安全注意事项)
    - [不当部署可能带来安全风险](#不当部署可能带来安全风险)
    - [安全建议](#安全建议)
  - [贡献指南](#贡献指南)
  - [许可证](#许可证)
  - [致谢](#致谢)
    - [核心贡献者](#核心贡献者)
  - [Star History](#star-history)

## 一行命令设置代理

如果你使用 Claude Code、Codex、Cursor、Windsurf 或其他编码代理，可以用一句话将设置说明交给它：

```text
如果需要，请帮我克隆 DeerFlow，然后按照 https://raw.githubusercontent.com/bytedance/deer-flow/main/Install.md 引导进行本地开发设置
```

该提示适用于编码代理。它告诉代理在需要时克隆仓库，在可用时选择 Docker，并在需要时停止并显示下一条命令以及用户仍需提供的任何缺失配置。

## 快速开始

### 配置

1. **克隆 DeerFlow 仓库**

   ```bash
   git clone https://github.com/bytedance/deer-flow.git
   cd deer-flow
   ```

2. **运行设置向导**

   在项目根目录（`deer-flow/`）下运行：

   ```bash
   make setup
   ```

   这将启动一个交互式向导，引导你选择 LLM 提供商、可选的网络搜索，以及执行/安全偏好（如沙盒模式、bash 访问和文件写入工具）。它会生成一个最小的 `config.yaml` 并将你的密钥写入 `.env`。大约需要 2 分钟。

   该向导还允许你配置可选的网络搜索提供商，或者暂时跳过。

   随时运行 `make doctor` 来验证你的设置并获取可操作的修复提示。

   > **高级/手动配置**：如果你更喜欢直接编辑 `config.yaml`，可以运行 `make config` 来复制完整模板。参见 `config.example.yaml` 获取完整参考，包括 CLI 支持的提供商（Codex CLI、Claude Code OAuth）、OpenRouter、Responses API 等。

   <details>
   <summary>手动模型配置示例</summary>

   ```yaml
   models:
     - name: gpt-4o
       display_name: GPT-4o
       use: langchain_openai:ChatOpenAI
       model: gpt-4o
       api_key: $OPENAI_API_KEY

     - name: openrouter-gemini-2.5-flash
       display_name: Gemini 2.5 Flash (OpenRouter)
       use: langchain_openai:ChatOpenAI
       model: google/gemini-2.5-flash-preview
       api_key: $OPENROUTER_API_KEY
       base_url: https://openrouter.ai/api/v1

     - name: gpt-5-responses
       display_name: GPT-5 (Responses API)
       use: langchain_openai:ChatOpenAI
       model: gpt-5
       api_key: $OPENAI_API_KEY
       use_responses_api: true
       output_version: responses/v1

     - name: qwen3-32b-vllm
       display_name: Qwen3 32B (vLLM)
       use: deerflow.models.vllm_provider:VllmChatModel
       model: Qwen/Qwen3-32B
       api_key: $VLLM_API_KEY
       base_url: http://localhost:8000/v1
       supports_thinking: true
       when_thinking_enabled:
         extra_body:
           chat_template_kwargs:
             enable_thinking: true
   ```

   OpenRouter 和类似的 OpenAI 兼容网关应使用 `langchain_openai:ChatOpenAI` 加 `base_url` 配置。如果你更喜欢使用特定提供商的环境变量名，请显式将 `api_key` 指向该变量（例如 `api_key: $OPENROUTER_API_KEY`）。

   要将 OpenAI 模型路由到 `/v1/responses`，继续使用 `langchain_openai:ChatOpenAI` 并设置 `use_responses_api: true` 和 `output_version: responses/v1`。

   对于 vLLM 0.19.0，使用 `deerflow.models.vllm_provider:VllmChatModel`。对于 Qwen 风格的推理模型，DeerFlow 通过 `extra_body.chat_template_kwargs.enable_thinking` 切换推理，并在多轮工具调用对话中保留 vLLM 的非标准 `reasoning` 字段。旧版 `thinking` 配置会自动规范化以保持向后兼容。推理模型可能还需要服务器启动时使用 `--reasoning-parser ...`。如果你的本地 vLLM 部署接受任何非空 API 密钥，你仍然可以将 `VLLM_API_KEY` 设置为占位符值。

   CLI 支持的提供商示例：

   ```yaml
   models:
     - name: gpt-5.4
       display_name: GPT-5.4 (Codex CLI)
       use: deerflow.models.openai_codex_provider:CodexChatModel
       model: gpt-5.4
       supports_thinking: true
       supports_reasoning_effort: true

     - name: claude-sonnet-4.6
       display_name: Claude Sonnet 4.6 (Claude Code OAuth)
       use: deerflow.models.claude_provider:ClaudeChatModel
       model: claude-sonnet-4-6
       max_tokens: 4096
       supports_thinking: true
   ```

   - Codex CLI 读取 `~/.codex/auth.json`
   - Claude Code 接受 `CLAUDE_CODE_OAUTH_TOKEN`、`ANTHROPIC_AUTH_TOKEN`、`CLAUDE_CODE_CREDENTIALS_PATH` 或 `~/.claude/.credentials.json`
   - ACP 代理条目与模型提供商是分开的——如果你配置 `acp_agents.codex`，请将其指向 Codex ACP 适配器，例如 `npx -y @zed-industries/codex-acp`
   - 在 macOS 上，如果需要，显式导出 Claude Code 认证：

   ```bash
   eval "$(python3 scripts/export_claude_code_oauth.py --print-export)"
   ```

   API 密钥也可以在 `.env` 中手动设置（推荐）或在 shell 中导出：

   ```bash
   OPENAI_API_KEY=your-openai-api-key
   TAVILY_API_KEY=your-tavily-api-key
   ```

   </details>

### 运行应用程序

#### 部署规模

下表可作为选择如何运行 DeerFlow 的实用起点：

| 部署目标 | 起点 | 推荐 | 备注 |
|---------|-----------|------------|-------|
| 本地评估 / `make dev` | 4 vCPU, 8 GB RAM, 20 GB 可用 SSD | 8 vCPU, 16 GB RAM | 适合一个开发者或一个使用托管模型 API 的轻量级会话。`2 vCPU / 4 GB` 通常不够。 |
| Docker 开发 / `make docker-start` | 4 vCPU, 8 GB RAM, 25 GB 可用 SSD | 8 vCPU, 16 GB RAM | 镜像构建、绑定挂载和沙盒容器需要比纯本地开发更多的空间。 |
| 长期运行服务器 / `make up` | 8 vCPU, 16 GB RAM, 40 GB 可用 SSD | 16 vCPU, 32 GB RAM | 适合共享使用、多代理运行、报告生成或较重的沙盒工作负载。 |

- 这些数字仅涵盖 DeerFlow 本身。如果你还托管本地 LLM，请单独规划该服务的规模。
- Linux 加 Docker 是持久服务器的推荐部署目标。macOS 和 Windows 最好作为开发或评估环境使用。
- 如果 CPU 或内存使用率持续过高，请先减少并发运行数，然后升级到下一档规模。

#### 方案一：Docker（推荐）

**开发模式**（热重载，源代码挂载）：

```bash
make docker-init    # 拉取沙盒镜像（仅在首次或镜像更新时）
make docker-start   # 启动服务（自动从 config.yaml 检测沙盒模式）
```

`make docker-start` 仅在 `config.yaml` 使用 provisioner 模式时启动 `provisioner`（`sandbox.use: deerflow.community.aio_sandbox:AioSandboxProvider` 配合 `provisioner_url`）。

Docker 构建默认使用上游 `uv` 注册表。如果你在受限网络中需要更快的镜像源，请在运行 `make docker-init` 或 `make docker-start` 前导出 `UV_INDEX_URL=https://pypi.tuna.tsinghua.edu.cn/simple` 和 `NPM_REGISTRY=https://registry.npmmirror.com`。

后端进程会在下次访问配置时自动获取 `config.yaml` 的更改，因此在开发期间模型元数据更新不需要手动重启。

> [!TIP]
> 在 Linux 上，如果 Docker 命令失败并显示 `permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock`，请在重试前将你的用户添加到 `docker` 组并重新登录。完整修复方法请参见 [CONTRIBUTING.md](CONTRIBUTING.md#linux-docker-daemon-permission-denied)。

**生产模式**（本地构建镜像，挂载运行时配置和数据）：

```bash
make up     # 构建镜像并启动所有生产服务
make down   # 停止并移除容器
```

访问地址：http://localhost:2026

统一的 nginx 端点默认是同源的，不会发出浏览器 CORS 头。如果你运行分源或端口转发的浏览器客户端，请将 `GATEWAY_CORS_ORIGINS` 设置为逗号分隔的精确源，例如 `http://localhost:3000`；然后 Gateway 会应用 CORS 允许列表和匹配的 CSRF 源检查。

详细的 Docker 开发指南请参见 [CONTRIBUTING.md](CONTRIBUTING.md)。

#### 方案二：本地开发

如果你更喜欢在本地运行服务：

前提条件：先完成上面的"配置"步骤（`make setup`）。`make dev` 需要在项目根目录下有一个有效的 `config.yaml`。设置 `DEER_FLOW_PROJECT_ROOT` 来显式定义该根目录，或设置 `DEER_FLOW_CONFIG_PATH` 来指向特定的配置文件。运行时状态默认在项目根目录下的 `.deer-flow` 中，可以通过 `DEER_FLOW_HOME` 移动；技能默认在项目根目录下的 `skills/` 中，可以通过 `DEER_FLOW_SKILLS_PATH` 移动。启动前运行 `make doctor` 验证你的设置。
在 Windows 上，请从 Git Bash 运行本地开发流程。原生 `cmd.exe` 和 PowerShell shell 不支持基于 bash 的服务脚本，WSL 也不能保证，因为某些脚本依赖于 Git for Windows 工具（如 `cygpath`）。

1. **检查前提条件**：
   ```bash
   make check  # 验证 Node.js 22+、pnpm、uv、nginx
   ```

2. **安装依赖**：
   ```bash
   make install  # 安装后端 + 前端依赖 + pre-commit hooks
   ```

3. **（可选）预拉取沙盒镜像**：
   ```bash
   # 如果使用基于 Docker/Container 的沙盒，推荐执行
   make setup-sandbox
   ```

4. **（可选）加载示例记忆数据用于本地审查**：
   ```bash
   python scripts/load_memory_sample.py
   ```
   这会将示例数据复制到默认的本地运行时记忆文件中，以便审查者可以立即测试 `设置 > 记忆`。
   最短审查流程请参见 [backend/docs/MEMORY_SETTINGS_REVIEW.md](backend/docs/MEMORY_SETTINGS_REVIEW.md)。

5. **启动服务**：
   ```bash
   make dev
   ```

6. **访问地址**：http://localhost:2026

#### 启动模式

DeerFlow 在 Gateway API 内部运行代理运行时。开发模式启用热重载；生产模式使用预构建的前端。

| | **本地前台** | **本地守护进程** | **Docker 开发** | **Docker 生产** |
|---|---|---|---|---|
| **开发** | `./scripts/serve.sh --dev`<br/>`make dev` | `./scripts/serve.sh --dev --daemon`<br/>`make dev-daemon` | `./scripts/docker.sh start`<br/>`make docker-start` | — |
| **生产** | `./scripts/serve.sh --prod`<br/>`make start` | `./scripts/serve.sh --prod --daemon`<br/>`make start-daemon` | — | `./scripts/deploy.sh`<br/>`make up` |

| 操作 | 本地 | Docker 开发 | Docker 生产 |
|---|---|---|---|
| **停止** | `./scripts/serve.sh --stop`<br/>`make stop` | `./scripts/docker.sh stop`<br/>`make docker-stop` | `./scripts/deploy.sh down`<br/>`make down` |
| **重启** | `./scripts/serve.sh --restart [flags]` | `./scripts/docker.sh restart` | — |

Gateway 拥有 `/api/langgraph/*` 并将这些公开的 LangGraph 兼容路径转换为其 nginx 后面的原生 `/api/*` 路由器。

#### Docker 生产部署

`deploy.sh` 支持分开构建和启动：

```bash
# 一步（构建 + 启动）
deploy.sh

# 两步（先构建，稍后启动）
deploy.sh build              # 构建所有镜像
deploy.sh start              # 启动预构建的镜像

# 停止
deploy.sh down
```

### 高级功能
#### 沙盒模式

DeerFlow 支持多种沙盒执行模式：
- **本地执行**（在主机上直接运行沙盒代码）
- **Docker 执行**（在隔离的 Docker 容器中运行沙盒代码）
- **Docker + Kubernetes 执行**（通过 provisioner 服务在 Kubernetes pod 中运行沙盒代码）

对于 Docker 开发，服务启动遵循 `config.yaml` 沙盒模式。在本地/Docker 模式下，`provisioner` 不会启动。

沙盒配置指南请参见 [Sandbox Configuration Guide](backend/docs/CONFIGURATION.md#sandbox) 以配置你偏好的模式。

#### MCP 服务器

DeerFlow 支持可配置的 MCP 服务器和技能来扩展其功能。
对于 HTTP/SSE MCP 服务器，支持 OAuth 令牌流程（`client_credentials`、`refresh_token`）。
详细说明请参见 [MCP Server Guide](backend/docs/MCP_SERVER.md)。

#### 即时通讯渠道

DeerFlow 支持从消息应用接收任务。配置后渠道会自动启动——无需公共 IP。

| 渠道 | 传输方式 | 难度 |
|---------|-----------|------------|
| Telegram | Bot API（长轮询） | 简单 |
| Slack | Socket 模式 | 中等 |
| 飞书 / Lark | WebSocket | 中等 |
| 微信 | 腾讯 iLink（长轮询） | 中等 |
| 企业微信 | WebSocket | 中等 |
| 钉钉 | Stream 推送（WebSocket） | 中等 |

**在 `config.yaml` 中配置：**

```yaml
channels:
  # LangGraph 兼容的 Gateway API 基础 URL（默认：http://localhost:8001/api）
  langgraph_url: http://localhost:8001/api
  # Gateway API URL（默认：http://localhost:8001）
  gateway_url: http://localhost:8001

  # 可选：所有移动渠道的全局会话默认值
  session:
    assistant_id: lead_agent  # 或自定义代理名称；自定义代理通过 lead_agent + agent_name 路由
    config:
      recursion_limit: 100
    context:
      thinking_enabled: true
      is_plan_mode: false
      subagent_enabled: false

  feishu:
    enabled: true
    app_id: $FEISHU_APP_ID
    app_secret: $FEISHU_APP_SECRET
    # domain: https://open.feishu.cn       # 中国（默认）
    # domain: https://open.larksuite.com   # 国际

  wecom:
    enabled: true
    bot_id: $WECOM_BOT_ID
    bot_secret: $WECOM_BOT_SECRET

  slack:
    enabled: true
    bot_token: $SLACK_BOT_TOKEN     # xoxb-...
    app_token: $SLACK_APP_TOKEN     # xapp-...（Socket 模式）
    allowed_users: []               # 空 = 允许所有人

  telegram:
    enabled: true
    bot_token: $TELEGRAM_BOT_TOKEN
    allowed_users: []               # 空 = 允许所有人

  wechat:
    enabled: false
    bot_token: $WECHAT_BOT_TOKEN
    ilink_bot_id: $WECHAT_ILINK_BOT_ID
    qrcode_login_enabled: true      # 可选：当 bot_token 为空时允许首次二维码引导
    allowed_users: []               # 空 = 允许所有人
    polling_timeout: 35
    state_dir: ./.deer-flow/wechat/state
    max_inbound_image_bytes: 20971520
    max_outbound_image_bytes: 20971520
    max_inbound_file_bytes: 52428800
    max_outbound_file_bytes: 52428800

    # 可选：按渠道/按用户会话设置
    session:
      assistant_id: mobile-agent  # 也支持自定义代理名称
      context:
        thinking_enabled: false
      users:
        "123456789":
          assistant_id: vip-agent
          config:
            recursion_limit: 150
          context:
            thinking_enabled: true
            subagent_enabled: true

  dingtalk:
    enabled: true
    client_id: $DINGTALK_CLIENT_ID             # 你的钉钉应用的 Client ID
    client_secret: $DINGTALK_CLIENT_SECRET     # 你的钉钉应用的 Client Secret
    allowed_users: []                          # 空 = 允许所有人
    card_template_id: ""                       # 可选：AI 卡片模板 ID，用于流式打字机效果
```

备注：
- `assistant_id: lead_agent` 直接调用默认的 LangGraph 助手。
- 如果 `assistant_id` 设置为自定义代理名称，DeerFlow 仍然通过 `lead_agent` 路由，并将该值注入为 `agent_name`，因此自定义代理的 SOUL/配置对即时通讯渠道生效。
- 即时通讯渠道工作者在内部调用 Gateway 的 LangGraph 兼容 API，并自动附加进程本地的内部认证以及线程和运行创建所需的 CSRF cookie/头对。

在你的 `.env` 文件中设置相应的 API 密钥：

```bash
# Telegram
TELEGRAM_BOT_TOKEN=123456789:ABCdefGHIjklMNOpqrSTUvwxYZ

# Slack
SLACK_BOT_TOKEN=xoxb-...
SLACK_APP_TOKEN=xapp-...

# 飞书 / Lark
FEISHU_APP_ID=cli_xxxx
FEISHU_APP_SECRET=your_app_secret

# 微信 iLink
WECHAT_BOT_TOKEN=your_ilink_bot_token
WECHAT_ILINK_BOT_ID=your_ilink_bot_id

# 企业微信
WECOM_BOT_ID=your_bot_id
WECOM_BOT_SECRET=your_bot_secret

# 钉钉
DINGTALK_CLIENT_ID=your_client_id
DINGTALK_CLIENT_SECRET=your_client_secret
```

**Telegram 设置**

1. 与 [@BotFather](https://t.me/BotFather) 聊天，发送 `/newbot`，并复制 HTTP API 令牌。
2. 在 `.env` 中设置 `TELEGRAM_BOT_TOKEN` 并在 `config.yaml` 中启用该渠道。

**Slack 设置**

1. 在 [api.slack.com/apps](https://api.slack.com/apps) 创建 Slack 应用 → Create New App → From scratch。
2. 在 **OAuth & Permissions** 下，添加 Bot Token Scopes：`app_mentions:read`、`chat:write`、`im:history`、`im:read`、`im:write`、`files:write`。
3. 启用 **Socket Mode** → 生成具有 `connections:write` 作用域的 App-Level Token（`xapp-…`）。
4. 在 **Event Subscriptions** 下，订阅机器人事件：`app_mention`、`message.im`。
5. 在 `.env` 中设置 `SLACK_BOT_TOKEN` 和 `SLACK_APP_TOKEN` 并在 `config.yaml` 中启用该渠道。

**飞书 / Lark 设置**

1. 在[飞书开放平台](https://open.feishu.cn/)创建应用 → 启用**机器人**能力。
2. 添加权限：`im:message`、`im:message.p2p_msg:readonly`、`im:resource`。
3. 在**事件**下，订阅 `im.message.receive_v1` 并选择**长连接**模式。
4. 复制 App ID 和 App Secret。在 `.env` 中设置 `FEISHU_APP_ID` 和 `FEISHU_APP_SECRET` 并在 `config.yaml` 中启用该渠道。

**微信设置**

1. 在 `config.yaml` 中启用 `wechat` 渠道。
2. 在 `.env` 中设置 `WECHAT_BOT_TOKEN`，或设置 `qrcode_login_enabled: true` 进行首次二维码引导。
3. 当 `bot_token` 为空且二维码引导启用时，查看后端日志获取 iLink 返回的二维码内容并完成绑定流程。
4. 二维码流程成功后，DeerFlow 会将获取的令牌持久化到 `state_dir` 以供后续重启使用。
5. 对于 Docker Compose 部署，将 `state_dir` 保持在持久卷上，以便 `get_updates_buf` 游标和保存的认证状态在重启后保持。

**企业微信设置**

1. 在企业微信 AI 机器人平台上创建机器人并获取 `bot_id` 和 `bot_secret`。
2. 在 `config.yaml` 中启用 `channels.wecom` 并填写 `bot_id` / `bot_secret`。
3. 在 `.env` 中设置 `WECOM_BOT_ID` 和 `WECOM_BOT_SECRET`。
4. 确保后端依赖包含 `wecom-aibot-python-sdk`。该渠道使用 WebSocket 长连接，不需要公共回调 URL。
5. 当前集成支持入站文本、图像和文件消息。代理生成的最终图像/文件也会发送回企业微信对话。

**钉钉设置**

1. 在[钉钉开发者控制台](https://open.dingtalk.com/)创建钉钉应用并启用**机器人**能力。
2. 在机器人配置页面将消息接收模式设置为 **Stream 模式**。
3. 复制 `Client ID` 和 `Client Secret`，在 `.env` 中设置 `DINGTALK_CLIENT_ID` 和 `DINGTALK_CLIENT_SECRET`，并在 `config.yaml` 中启用该渠道。
4. *（可选）* 要启用流式 AI 卡片回复（打字机效果），请在[钉钉卡片平台](https://open.dingtalk.com/document/dingstart/typewriter-effect-streaming-ai-card)创建 **AI 卡片**模板，然后在 `config.yaml` 中将 `card_template_id` 设置为模板 ID。你还需要申请 `Card.Streaming.Write` 和 `Card.Instance.Write` 权限。


当 DeerFlow 在 Docker Compose 中运行时，即时通讯渠道在 `gateway` 容器内执行。在这种情况下，不要将 `channels.langgraph_url` 或 `channels.gateway_url` 指向 `localhost`；使用容器服务名称，例如 `http://gateway:8001/api` 和 `http://gateway:8001`，或设置 `DEER_FLOW_CHANNELS_LANGGRAPH_URL` 和 `DEER_FLOW_CHANNELS_GATEWAY_URL`。

**命令**

渠道连接后，你可以直接从聊天中与 DeerFlow 交互：

| 命令 | 说明 |
|---------|-------------|
| `/new` | 开始新对话 |
| `/status` | 显示当前线程信息 |
| `/models` | 列出可用模型 |
| `/memory` | 查看记忆 |
| `/help` | 显示帮助 |

> 没有命令前缀的消息被视为普通聊天——DeerFlow 会创建一个线程并进行对话式回复。

#### LangSmith 追踪

DeerFlow 内置了 [LangSmith](https://smith.langchain.com) 集成用于可观测性。启用后，所有 LLM 调用、代理运行和工具执行都会被追踪并在 LangSmith 仪表板中可见。

将以下内容添加到你的 `.env` 文件：

```bash
LANGSMITH_TRACING=true
LANGSMITH_ENDPOINT=https://api.smith.langchain.com
LANGSMITH_API_KEY=lsv2_pt_xxxxxxxxxxxxxxxx
LANGSMITH_PROJECT=xxx
```

#### Langfuse 追踪

DeerFlow 还支持 [Langfuse](https://langfuse.com) 可观测性，用于 LangChain 兼容的运行。

将以下内容添加到你的 `.env` 文件：

```bash
LANGFUSE_TRACING=true
LANGFUSE_PUBLIC_KEY=pk-lf-xxxxxxxxxxxxxxxx
LANGFUSE_SECRET_KEY=sk-lf-xxxxxxxxxxxxxxxx
LANGFUSE_BASE_URL=https://cloud.langfuse.com
```

如果你使用自托管的 Langfuse 实例，请将 `LANGFUSE_BASE_URL` 设置为你的部署 URL。

**追踪关联字段。** 每次代理运行都用 Langfuse 的保留追踪属性进行注释，以便会话和用户页面自动激活：

- `session_id` = LangGraph `thread_id` — 将同一对话的所有追踪分组
- `user_id` = 来自 `get_effective_user_id()` 的有效用户（在无认证模式下回退到 `default`）
- `trace_name` = 助手 ID（默认为 `lead-agent`）
- `tags` = `[env:<DEER_FLOW_ENV>, model:<model_name>]`（未设置时省略）

这些被注入到图形调用根部的 `RunnableConfig.metadata` 中，用于 Gateway 路径（`runtime/runs/worker.py::run_agent`）和嵌入式路径（`client.py::DeerFlowClient.stream`），因此任何 LangChain 兼容的回调都可以读取它们。设置 `DEER_FLOW_ENV`（或 `ENVIRONMENT`）来按部署环境标记追踪。

#### 同时使用两个提供商

如果同时启用了 LangSmith 和 Langfuse，DeerFlow 会附加两个追踪回调，并向两个系统报告相同的模型活动。

如果某个提供商被显式启用但缺少必需的凭据，或者其回调初始化失败，DeerFlow 会在模型创建期间追踪初始化时快速失败，错误消息会指明导致失败的提供商。

对于 Docker 部署，追踪默认禁用。在 `.env` 中设置 `LANGSMITH_TRACING=true` 和 `LANGSMITH_API_KEY` 来启用它。

## 从深度研究到超级代理框架

DeerFlow 最初是一个深度研究框架——社区用它做了很多事情。自发布以来，开发者已经将其推向研究之外：构建数据管道、生成幻灯片、启动仪表板、自动化内容工作流程。这些都是我们从未预料到的。

这告诉我们一些重要的事情：DeerFlow 不仅仅是一个研究工具。它是一个**框架**——一个为代理提供基础设施以实际完成工作的运行时。

所以我们从头开始重建了它。

DeerFlow 2.0 不再是一个你拼接在一起的框架。它是一个超级代理框架——开箱即用，完全可扩展。基于 LangGraph 和 LangChain 构建，它附带代理开箱即用所需的一切：文件系统、记忆、技能、沙盒感知执行，以及为复杂多步骤任务规划和生成子代理的能力。

直接使用它。或者拆解它，让它成为你自己的。

## 核心特性

### 技能与工具

技能是让 DeerFlow 能够完成*几乎任何事情*的关键。

标准的代理技能是一个结构化的能力模块——一个定义工作流程、最佳实践和对支持资源引用的 Markdown 文件。DeerFlow 内置了用于研究、报告生成、幻灯片创建、网页、图像和视频生成等的技能。但真正的力量在于可扩展性：添加你自己的技能、替换内置技能，或将它们组合成复合工作流程。

技能是渐进式加载的——仅在任务需要时加载，而不是一次性全部加载。这保持了上下文窗口的精简，并使 DeerFlow 即使在对令牌敏感的模型上也能良好工作。

当你通过 Gateway 安装 `.skill` 归档文件时，DeerFlow 接受标准的可选 frontmatter 元数据，如 `version`、`author` 和 `compatibility`，而不是拒绝其他有效的外部技能。

工具遵循相同的理念。DeerFlow 附带核心工具集——网络搜索、网络获取、文件操作、bash 执行——并支持通过 MCP 服务器和 Python 函数自定义工具。可以替换任何东西。可以添加任何东西。

Gateway 生成的后续建议现在在解析 JSON 数组响应之前，会规范化纯字符串模型输出和块/列表风格的富内容，因此特定提供商的内容包装器不会静默丢弃建议。

```
# 沙盒容器内的路径
/mnt/skills/public
├── research/SKILL.md
├── report-generation/SKILL.md
├── slide-creation/SKILL.md
├── web-page/SKILL.md
└── image-generation/SKILL.md

/mnt/skills/custom
└── your-custom-skill/SKILL.md      ← 你的技能
```

#### Claude Code 集成

`claude-to-deerflow` 技能让你可以直接从 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) 与正在运行的 DeerFlow 实例交互。发送研究任务、检查状态、管理线程——所有这些都无需离开终端。

**安装技能**：

```bash
npx skills add https://github.com/bytedance/deer-flow --skill claude-to-deerflow
```

然后确保 DeerFlow 正在运行（默认在 `http://localhost:2026`），并在 Claude Code 中使用 `/claude-to-deerflow` 命令。

**你可以做什么**：
- 向 DeerFlow 发送消息并获取流式响应
- 选择执行模式：flash（快速）、standard、pro（规划）、ultra（子代理）
- 检查 DeerFlow 健康状态、列出模型/技能/代理
- 管理线程和对话历史
- 上传文件进行分析

**环境变量**（可选，用于自定义端点）：

```bash
DEERFLOW_URL=http://localhost:2026            # 统一代理基础 URL
DEERFLOW_GATEWAY_URL=http://localhost:2026    # Gateway API
DEERFLOW_LANGGRAPH_URL=http://localhost:2026/api/langgraph  # LangGraph API
```

完整的 API 参考请参见 [`skills/public/claude-to-deerflow/SKILL.md`](skills/public/claude-to-deerflow/SKILL.md)。

### 子代理

复杂任务很少能一次性完成。DeerFlow 会分解它们。

主代理可以动态生成子代理——每个都有自己的作用域上下文、工具和终止条件。子代理在可能时并行运行，报告结构化结果，主代理将所有内容综合成连贯的输出。当启用令牌使用追踪时，已完成的子代理使用量会归因到分发步骤。

这就是 DeerFlow 处理需要几分钟到几小时任务的方式：一个研究任务可能会扇出成十几个子代理，每个探索不同的角度，然后汇聚成一份报告——或一个网站——或一个带有生成视觉效果的幻灯片。一个框架，多只手。

### 沙盒与文件系统

DeerFlow 不仅仅*谈论*做事。它有自己的计算机。

每个任务都有自己的执行环境和完整的文件系统视图——技能、工作空间、上传、输出。代理读取、写入和编辑文件。它可以查看图像，并且在安全配置时执行 shell 命令。

使用 `AioSandboxProvider`，shell 执行在隔离的容器内运行。使用 `LocalSandboxProvider`，文件工具仍然映射到主机上的按线程目录，但默认禁用主机 bash，因为它不是安全的隔离边界。仅对完全受信任的本地工作流程重新启用主机 bash。

这是具有工具访问权限的聊天机器人与具有实际执行环境的代理之间的区别。

```
# 沙盒容器内的路径
/mnt/user-data/
├── uploads/          ← 你的文件
├── workspace/        ← 代理的工作目录
└── outputs/          ← 最终交付物
```

### 上下文工程

**隔离的子代理上下文**：每个子代理在自己的隔离上下文中运行。这意味着子代理无法看到主代理或其他子代理的上下文。这对于确保子代理能够专注于手头的任务而不被主代理或其他子代理的上下文分散注意力非常重要。

**总结**：在会话内，DeerFlow 积极管理上下文——总结已完成的子任务，将中间结果卸载到文件系统，压缩不再立即相关的内容。这使它能够在长时间、多步骤任务中保持敏锐，而不会耗尽上下文窗口。

**严格的工具调用恢复**：当提供商或中介中断工具调用循环时，DeerFlow 现在会在强制停止的助手消息上剥离提供商级别的原始工具调用元数据，并在下一次模型调用之前为悬挂的调用注入占位符工具结果。这可以防止严格验证 `tool_call_id` 序列的 OpenAI 兼容推理模型因格式错误的历史记录而失败。

### 长期记忆

大多数代理在对话结束的那一刻就忘记了所有事情。DeerFlow 会记住。

跨会话，DeerFlow 会构建关于你的个人资料、偏好和积累知识的持久记忆。你使用得越多，它就越了解你——你的写作风格、你的技术栈、你的重复工作流程。记忆存储在本地，由你控制。

记忆更新现在在应用时会跳过重复的事实条目，因此重复的偏好和上下文不会在会话间无限积累。

## 推荐模型

DeerFlow 是模型无关的——它适用于任何实现 OpenAI 兼容 API 的 LLM。话虽如此，它在以下模型上表现最好：

- **长上下文窗口**（100k+ 令牌）用于深度研究和多步骤任务
- **推理能力**用于自适应规划和复杂分解
- **多模态输入**用于图像理解和视频理解
- **强大的工具使用**用于可靠的函数调用和结构化输出

## 嵌入式 Python 客户端

DeerFlow 可以作为嵌入式 Python 库使用，无需运行完整的 HTTP 服务。`DeerFlowClient` 提供对所有代理和 Gateway 功能的直接进程内访问，返回与 HTTP Gateway API 相同的响应架构。HTTP Gateway 还暴露 `DELETE /api/threads/{thread_id}` 以在 LangGraph 线程本身被删除后移除 DeerFlow 管理的本地线程数据：

```python
from deerflow.client import DeerFlowClient

client = DeerFlowClient()

# 聊天
response = client.chat("为我分析这篇论文", thread_id="my-thread")

# 流式（LangGraph SSE 协议：values, messages-tuple, end）
for event in client.stream("hello"):
    if event.type == "messages-tuple" and event.data.get("type") == "ai":
        print(event.data["content"])

# 配置与管理——返回 Gateway 对齐的字典
models = client.list_models()        # {"models": [...]}
skills = client.list_skills()        # {"skills": [...]}
client.update_skill("web-search", enabled=True)
client.upload_files("thread-1", ["./report.pdf"])  # {"success": True, "files": [...]}
```

所有返回字典的方法都在 CI 中根据 Gateway Pydantic 响应模型进行验证（`TestGatewayConformance`），确保嵌入式客户端与 HTTP API 架构保持同步。完整的 API 文档请参见 `backend/packages/harness/deerflow/client.py`。

## 文档

- [贡献指南](CONTRIBUTING.md) - 开发环境设置和工作流程
- [配置指南](backend/docs/CONFIGURATION.md) - 设置和配置说明
- [架构概述](backend/CLAUDE.md) - 技术架构详情
- [后端架构](backend/README.md) - 后端架构和 API 参考

## ⚠️ 安全注意事项

### 不当部署可能带来安全风险

DeerFlow 具有关键的高权限功能，包括**系统命令执行、资源操作和业务逻辑调用**，默认设计为**部署在本地可信环境（仅通过 127.0.0.1 回环接口访问）**。如果你在不受信任的环境中部署代理——例如局域网、公共云服务器或其他多端点可访问的环境——而没有严格的安全措施，可能会带来安全风险，包括：

- **未经授权的非法调用**：代理功能可能被未经授权的第三方或恶意互联网扫描器发现，触发批量未授权请求，执行系统命令和文件读写等高风险操作，可能导致严重的安全后果。
- **合规和法律风险**：如果代理被非法调用进行网络攻击、数据窃取或其他非法活动，可能导致法律责任和合规风险。

### 安全建议

**注意：我们强烈建议在本地可信网络环境中部署 DeerFlow。** 如果你需要跨设备或跨网络部署，必须实施严格的安全措施，例如：

- **IP 白名单**：使用 `iptables`，或部署带有访问控制列表（ACL）的硬件防火墙/交换机，来**配置 IP 白名单规则**并拒绝来自所有其他 IP 地址的访问。
- **认证网关**：配置反向代理（例如 nginx）并**启用强预认证**，阻止任何未认证的访问。
- **网络隔离**：在可能的情况下，将代理和可信设备放在**同一专用 VLAN** 中，与其他网络设备隔离。
- **保持更新**：持续关注 DeerFlow 的安全功能更新。

## 贡献指南

我们欢迎贡献！请参见 [CONTRIBUTING.md](CONTRIBUTING.md) 了解开发设置、工作流程和指南。

回归覆盖包括 `backend/tests/` 中的 Docker 沙盒模式检测和 provisioner kubeconfig 路径处理测试。
后端阻塞 IO 诊断可从仓库根目录使用 `make detect-blocking-io` 获得：它静态扫描后端业务代码中可能在后端事件循环上运行的阻塞 IO，打印简洁的摘要，并将完整的 JSON 发现写入 `.deer-flow/blocking-io-findings.json`。
JSON 包含紧凑的审查记录，带有 `priority`、`location`、`blocking_call`、`event_loop_exposure`、`reason` 和 `code`。
Gateway 工件服务现在强制将活动 Web 内容类型（`text/html`、`application/xhtml+xml`、`image/svg+xml`）作为附件下载而不是内联渲染，减少生成工件的 XSS 风险。

## 许可证

本项目是开源的，根据 [MIT 许可证](./LICENSE) 提供。

## 致谢

DeerFlow 建立在开源社区的杰出工作之上。我们深深感谢所有为 DeerFlow 的实现做出贡献的项目和贡献者。真的，我们站在巨人的肩膀上。

我们要向以下项目表示诚挚的感谢，感谢它们的宝贵贡献：

- **[LangChain](https://github.com/langchain-ai/langchain)**：他们卓越的框架为我们的 LLM 交互和链提供了支持，实现了无缝集成和功能。
- **[LangGraph](https://github.com/langchain-ai/langgraph)**：他们在多代理编排方面的创新方法对于实现 DeerFlow 复杂的工作流程起到了关键作用。

这些项目体现了开源协作的变革力量，我们很自豪能在它们的基础上构建。

### 核心贡献者

衷心感谢 `DeerFlow` 的核心作者，他们的愿景、热情和奉献使这个项目成为现实：

- **[Daniel Walnut](https://github.com/hetaoBackend/)**
- **[Henry Li](https://github.com/magiccube/)**

你们坚定不移的承诺和专业知识一直是 DeerFlow 成功背后的推动力。我们很荣幸有你们引领这段旅程。

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=bytedance/deer-flow&type=Date)](https://star-history.com/#bytedance/deer-flow&Date)