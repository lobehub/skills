# Agent Management

Create, configure, and run AI agents.

---

## agent list

List your agents.

### Usage

```bash
lh agent list [options]
```

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `-L, --limit <n>` | 30 | Maximum number of items |
| `-k, --keyword <keyword>` | - | Filter by keyword |
| `--json [fields]` | - | Output JSON |

### Examples

```bash
# List all agents
lh agent list

# Search by keyword
lh agent list -k "assistant"

# Get JSON output
lh agent list --json
```

---

## agent view

View agent configuration.

### Usage

```bash
lh agent view [agentId] [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `agentId` | No | Agent ID (use --slug if not provided) |

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `-s, --slug <slug>` | - | Agent slug |
| `--json [fields]` | - | Output JSON |

### Examples

```bash
# View by ID
lh agent view agent_abc123

# View by slug
lh agent view -s my-assistant
```

---

## agent create

Create a new agent.

### Usage

```bash
lh agent create [options]
```

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `-t, --title <title>` | Yes | Agent title |
| `-d, --description <desc>` | No | Description |
| `-m, --model <model>` | No | Model ID (e.g., gpt-4o, claude-3-opus) |
| `-p, --provider <provider>` | No | Provider ID (e.g., openai, anthropic) |
| `-s, --system-role <role>` | No | System role prompt |
| `--group <groupId>` | No | Group ID |

### Examples

```bash
# Create a basic agent
lh agent create -t "My Assistant" -d "A helpful assistant"

# Create with model and system prompt
lh agent create \
  -t "Code Reviewer" \
  -d "Reviews code and suggests improvements" \
  -m gpt-4o \
  -p openai \
  -s "You are an expert code reviewer. Analyze code for bugs, performance issues, and best practices."
```

---

## agent edit

Update agent configuration.

### Usage

```bash
lh agent edit [agentId] [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `agentId` | No | Agent ID (use --slug if not provided) |

### Options

| Option | Description |
| ------ | ----------- |
| `--slug <slug>` | Agent slug |
| `-t, --title <title>` | New title |
| `-d, --description <desc>` | New description |
| `-m, --model <model>` | New model ID |
| `-p, --provider <provider>` | New provider ID |
| `-s, --system-role <role>` | New system role prompt |

### Examples

```bash
# Update title
lh agent edit agent_abc123 -t "Updated Assistant"

# Update by slug
lh agent edit -s my-assistant -m claude-3-opus -p anthropic
```

---

## agent delete

Delete an agent.

### Usage

```bash
lh agent delete <agentId> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `agentId` | Yes | Agent ID |

### Options

| Option | Description |
| ------ | ----------- |
| `--yes` | Skip confirmation prompt |

### Examples

```bash
# Delete with confirmation
lh agent delete agent_abc123

# Skip confirmation
lh agent delete agent_abc123 --yes
```

---

## agent run

Run an agent with a prompt.

### Usage

```bash
lh agent run [options]
```

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `-a, --agent-id <id>` | No* | Agent ID |
| `-s, --slug <slug>` | No* | Agent slug |
| `-p, --prompt <text>` | Yes | User prompt |
| `-t, --topic-id <id>` | No | Reuse an existing topic |
| `--no-auto-start` | No | Do not auto-start the agent |
| `--json` | No | Output full JSON event stream |
| `-v, --verbose` | No | Show detailed tool call info |
| `--replay <file>` | No | Replay events from a saved JSON file (offline) |

*Either `--agent-id` or `--slug` is required.

### Output

Streams the agent's response in real-time. Tool calls and results are displayed when using `--verbose`.

### Examples

```bash
# Run by agent ID
lh agent run -a agent_abc123 -p "What's the capital of France?"

# Run by slug
lh agent run -s my-assistant -p "Summarize this document"

# Continue a conversation
lh agent run -a agent_abc123 -t topic_xyz789 -p "Tell me more"

# Verbose output with tool details
lh agent run -s code-reviewer -p "Review this code" -v

# JSON output for processing
lh agent run -a agent_abc123 -p "Hello" --json
```

---

## agent duplicate

Duplicate an agent.

### Usage

```bash
lh agent duplicate <agentId> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `agentId` | Yes | Agent ID to duplicate |

### Options

| Option | Description |
| ------ | ----------- |
| `-t, --title <title>` | Title for the duplicate |

### Examples

```bash
# Duplicate with default title
lh agent duplicate agent_abc123

# Duplicate with custom title
lh agent duplicate agent_abc123 -t "My Assistant Copy"
```

---

## agent pin / unpin

Pin or unpin an agent for quick access.

### Usage

```bash
lh agent pin <agentId>
lh agent unpin <agentId>
```

---

## agent status

Check agent operation status.

### Usage

```bash
lh agent status <operationId> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `operationId` | Yes | Operation ID |

### Options

| Option | Description |
| ------ | ----------- |
| `--json [fields]` | Output JSON |
| `--history` | Include step history |
| `--history-limit <n>` | Number of history entries (default: 10) |

### Examples

```bash
# Check status
lh agent status op_abc123

# Include history
lh agent status op_abc123 --history

# JSON output
lh agent status op_abc123 --json
```

---

## Agent Knowledge Base Management

### agent kb-files

List knowledge bases and files associated with an agent.

```bash
lh agent kb-files <agentId> [--json]
lh agent kb-files -s <slug> [--json]
```

### agent add-file

Associate files with an agent.

```bash
lh agent add-file <agentId> --file-ids id1,id2,id3 [--enabled]
```

### agent remove-file

Remove a file from an agent.

```bash
lh agent remove-file <agentId> --file-id <fileId>
```

### agent toggle-file

Toggle a file on/off for an agent.

```bash
lh agent toggle-file <agentId> --file-id <fileId> --enable
lh agent toggle-file <agentId> --file-id <fileId> --disable
```

### agent add-kb

Associate a knowledge base with an agent.

```bash
lh agent add-kb <agentId> --kb-id <kbId> [--enabled]
```

### agent remove-kb

Remove a knowledge base from an agent.

```bash
lh agent remove-kb <agentId> --kb-id <kbId>
```

### agent toggle-kb

Toggle a knowledge base on/off for an agent.

```bash
lh agent toggle-kb <agentId> --kb-id <kbId> --enable
lh agent toggle-kb <agentId> --kb-id <kbId> --disable
```
