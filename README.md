# MewCode

终端 AI 编程助手（Python + Textual），支持 Anthropic / OpenAI / OpenAI 兼容接口，以及 MCP、权限模式、Skills、Teams 等能力。

## 环境要求

- Python **3.11+**
- 推荐安装 [uv](https://docs.astral.sh/uv/)（项目含 `uv.lock`，依赖安装更快更稳）
- 可用的大模型 API Key（OpenAI、Anthropic，或国内兼容 OpenAI 协议的服务）

## 快速开始

### 1. 克隆仓库

```bash
git clone https://github.com/<你的用户名>/MewCode.git
cd MewCode
```

### 2. 安装依赖

**方式 A：使用 uv（推荐）**

```bash
uv sync
```

**方式 B：使用 pip + venv**

```bash
# Windows PowerShell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -e .

# macOS / Linux
python3 -m venv .venv
source .venv/bin/activate
pip install -e .
```

### 3. 配置 API

在以下任一路径创建 `config.yaml`（任选其一即可）：

| 路径 | 说明 |
|------|------|
| `~/.mewcode/config.yaml` | 用户全局配置（推荐） |
| `.mewcode/config.yaml` | 当前项目配置 |
| `.mewcode/config.local.yaml` | 本地覆盖（勿提交密钥） |

可复制示例配置后修改：

```bash
# Windows PowerShell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.mewcode" | Out-Null
Copy-Item config.example.yaml "$env:USERPROFILE\.mewcode\config.yaml"

# macOS / Linux
mkdir -p ~/.mewcode
cp config.example.yaml ~/.mewcode/config.yaml
```

然后用编辑器打开配置文件，填入自己的 `api_key` / `base_url` / `model`。

也可不写 `api_key`，改用环境变量：

| protocol | 环境变量 |
|----------|----------|
| `anthropic` | `ANTHROPIC_API_KEY` |
| `openai` / `openai-compat` | `OPENAI_API_KEY` |

### 4. 启动

```bash
# uv
uv run mewcode

# 或已激活 venv / 已安装入口脚本后
mewcode
```

常用参数：

```bash
mewcode --mode plan          # 规划模式
mewcode -p "解释这段代码"     # 非交互：执行后打印结果
mewcode --remote             # WebSocket 远程模式（浏览器访问 http://localhost:18888）
```

## 配置说明（简要）

`providers` 至少配置一个，必填字段：`name`、`protocol`、`base_url`、`model`。

- **protocol**：`anthropic` | `openai` | `openai-compat`
- **permission_mode**：`default` | `acceptEdits` | `plan` | `bypassPermissions`
- 可选：`thinking`、`context_window`、`max_output_tokens`、`mcp_servers` 等

完整字段示例见仓库根目录 [`config.example.yaml`](config.example.yaml)。

## 开发与测试

```bash
uv sync --group dev
uv run pytest
```

## 安全提示

- **不要**把真实 API Key 提交到 Git
- 本地配置目录 `.mewcode/` 与根目录 `config.yaml` 已在 `.gitignore` 中忽略
- 分享仓库时只保留 `config.example.yaml` 这类不含密钥的示例

## 项目结构（概览）

```
MewCode/
├── mewcode/           # 主程序包
├── tests/             # 测试
├── config.example.yaml
├── pyproject.toml
├── uv.lock
└── README.md
```

## License

请按课程/团队约定补充许可证信息。
