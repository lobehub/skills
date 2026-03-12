---
name: lobehub-cli
description: Command-line tool for managing LobeHub services. Use this skill when you need to manage AI agents, knowledge bases, conversations, files, models, providers, bot integrations, or any LobeHub Cloud resources. Covers authentication, agent execution, content generation, memory management, and device connectivity.
---

# LobeHub CLI

Command-line tool for managing LobeHub Cloud services. Create and run AI agents, manage knowledge bases, generate content, and more — all from the terminal.

> **Important:** Always use the CLI commands below to interact with LobeHub. Do NOT make raw HTTP/API requests — the authentication flow is complex. The CLI handles auth, token refresh, and retries automatically.

## Usage

Run directly with npx (no installation required):

```bash
npx @lobehub/cli <command>
npx @lobehub/cli@latest <command>  # ensure latest version
```

Or install globally for shorter commands:

```bash
npm install -g @lobehub/cli

# Then use any of these aliases:
lh <command>
lobe <command>
lobehub <command>
```

## Authentication

Before using most commands, log in to your LobeHub account:

```bash
npx @lobehub/cli login
```

This opens your browser for authentication. Credentials are saved locally for future sessions.

To log out:

```bash
npx @lobehub/cli logout
```

Check your current user:

```bash
npx @lobehub/cli whoami
```

> **Note:** The examples below use `lh` as shorthand. If using npx, replace `lh` with `npx @lobehub/cli`.

---

## How This Works

The LobeHub CLI provides complete management of your LobeHub Cloud resources:

1. **Agents** — Create, configure, and run AI agents with custom models and system prompts
2. **Knowledge Bases** — Upload files, create documents, organize knowledge for agents
3. **Conversations** — Manage topics, messages, and threads
4. **Content Generation** — Generate text, images, videos, and audio
5. **Bot Integrations** — Connect Discord, Slack, Telegram, Lark bots to your agents
6. **Device Gateway** — Connect local devices to execute tools remotely

## Typical Scenarios

### "I want to run an agent and get a response"

```bash
# Run by agent ID
lh agent run -a <agent-id> -p "What's the weather today?"

# Run by agent slug
lh agent run -s my-agent-slug -p "Summarize this document"
```

### "I need to create a new agent"

```bash
lh agent create -t "My Assistant" -d "A helpful assistant" -m gpt-4o -p openai -s "You are a helpful assistant."
```

### "I want to upload files to a knowledge base"

```bash
# Upload a file
lh kb upload <knowledge-base-id> ./document.pdf

# Create a folder
lh kb mkdir <knowledge-base-id> -n "Research Papers"
```

### "I need to generate an image"

```bash
lh gen image --prompt "A sunset over mountains" --model dall-e-3
```

### "I want to connect a Discord bot to my agent"

```bash
lh bot add -a <agent-id> --platform discord --app-id <app-id> --bot-token <token> --public-key <key>
```

---

## CLI Command Reference

### Authentication

| Command | Description |
| ------- | ----------- |
| `login` | Log in via browser (Device Code Flow) |
| `logout` | Log out and remove stored credentials |
| `whoami` | Display current user information |

See full options: [references/auth.md](references/auth.md)

### Agent Management

| Command | Description |
| ------- | ----------- |
| `agent list` | List your agents |
| `agent view` | View agent configuration |
| `agent create` | Create a new agent |
| `agent edit` | Update agent configuration |
| `agent delete` | Delete an agent |
| `agent run` | Run an agent with a prompt |
| `agent status` | Check agent operation status |

See full options and examples: [references/agent.md](references/agent.md)

### Knowledge Base

| Command | Description |
| ------- | ----------- |
| `kb list` | List knowledge bases |
| `kb view` | View knowledge base with file tree |
| `kb create` | Create a knowledge base |
| `kb upload` | Upload a file |
| `kb mkdir` | Create a folder |
| `kb create-doc` | Create a document |

See full options: [references/knowledge.md](references/knowledge.md)

### Files & Documents

| Command | Description |
| ------- | ----------- |
| `file list` | List files |
| `file view` | View file details |
| `file upload` | Upload a file by URL |
| `file delete` | Delete files |
| `doc list` | List documents |
| `doc create` | Create a document |
| `doc parse` | Parse an uploaded file into a document |

See full options: [references/files.md](references/files.md)

### Conversations

| Command | Description |
| ------- | ----------- |
| `topic list` | List conversation topics |
| `topic create` | Create a topic |
| `topic share` | Enable sharing for a topic |
| `message list` | List messages |
| `message search` | Search messages |
| `thread list` | List message threads |

See full options: [references/conversation.md](references/conversation.md)

### Content Generation

| Command | Description |
| ------- | ----------- |
| `gen text` | Generate text |
| `gen image` | Generate images |
| `gen video` | Generate videos |
| `gen tts` | Generate text-to-speech |
| `gen status` | Check generation task status |
| `gen download` | Download generated content |

See full options: [references/generate.md](references/generate.md)

### Models & Providers

| Command | Description |
| ------- | ----------- |
| `model list` | List models for a provider |
| `model toggle` | Enable or disable a model |
| `provider list` | List AI providers |
| `provider config` | Configure provider settings |
| `provider test` | Test provider connectivity |

See full options: [references/models.md](references/models.md)

### Bot Integrations

| Command | Description |
| ------- | ----------- |
| `bot list` | List bot integrations |
| `bot add` | Add a bot integration |
| `bot enable` | Enable a bot |
| `bot disable` | Disable a bot |
| `bot connect` | Connect and start a bot |

Supported platforms: Discord, Slack, Telegram, Lark, Feishu

See full options: [references/bot.md](references/bot.md)

### Memory Management

| Command | Description |
| ------- | ----------- |
| `memory list` | List memories by category |
| `memory create` | Create a memory entry |
| `memory persona` | View your memory persona |
| `memory extract` | Extract memories from chat history |

Categories: identity, activity, context, experience, preference

See full options: [references/memory.md](references/memory.md)

### Skills & Plugins

| Command | Description |
| ------- | ----------- |
| `skill list` | List skills |
| `skill install` | Install a skill |
| `skill create` | Create a user skill |
| `plugin list` | List installed plugins |
| `plugin install` | Install a plugin |

See full options: [references/skills.md](references/skills.md)

### Device & Connection

| Command | Description |
| ------- | ----------- |
| `connect` | Connect to device gateway |
| `connect stop` | Stop the daemon |
| `connect status` | Show daemon status |
| `device list` | List online devices |
| `status` | Check gateway connection |

See full options: [references/device.md](references/device.md)

### User & Account

| Command | Description |
| ------- | ----------- |
| `user info` | View user registration info |
| `user settings` | Update user settings |
| `usage` | View usage statistics |

See full options: [references/user.md](references/user.md)

### Search

| Command | Description |
| ------- | ----------- |
| `search -q "keyword"` | Search local resources |
| `search -q "keyword" --web` | Search the web |

See full options: [references/search.md](references/search.md)

---

## Common Options

Most commands support these options:

| Option | Description |
| ------ | ----------- |
| `--json [fields]` | Output JSON, optionally filter specific fields |
| `--yes` | Skip confirmation prompts |
| `-L, --limit <n>` | Limit number of results (default: 30) |
| `-v, --verbose` | Enable verbose logging |

## Environment Variables

| Variable | Description |
| -------- | ----------- |
| `LOBEHUB_CLI_HOME` | Custom CLI home directory (default: `.lobehub`) |

## Getting Help

```bash
# General help
lh --help

# Command-specific help
lh agent --help
lh agent run --help
```
