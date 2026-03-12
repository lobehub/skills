# Conversations

Manage conversation topics, messages, and threads.

---

# Topics

---

## topic list

List topics.

### Usage

```bash
lh topic list [options]
```

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `--agent-id <id>` | - | Filter by agent ID |
| `-L, --limit <n>` | 30 | Page size |
| `--page <n>` | 1 | Page number |
| `--json [fields]` | - | Output JSON |

### Examples

```bash
# List all topics
lh topic list

# Filter by agent
lh topic list --agent-id agent_abc123

# Paginate
lh topic list --page 2 -L 20
```

---

## topic search

Search topics.

### Usage

```bash
lh topic search <keywords> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `keywords` | Yes | Search keywords |

### Options

| Option | Description |
| ------ | ----------- |
| `--agent-id <id>` | Filter by agent ID |
| `--json [fields]` | Output JSON |

---

## topic create

Create a topic.

### Usage

```bash
lh topic create [options]
```

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `-t, --title <title>` | Yes | Topic title |
| `--agent-id <id>` | No | Agent ID |
| `--favorite` | No | Mark as favorite |

### Examples

```bash
lh topic create -t "Project Discussion"
lh topic create -t "Code Review" --agent-id agent_abc123 --favorite
```

---

## topic edit

Update a topic.

### Usage

```bash
lh topic edit <id> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `-t, --title <title>` | New title |
| `--favorite` | Mark as favorite |
| `--no-favorite` | Unmark as favorite |

---

## topic delete

Delete one or more topics.

### Usage

```bash
lh topic delete <ids...> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--yes` | Skip confirmation prompt |

---

## topic clone

Clone a topic.

### Usage

```bash
lh topic clone <id> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `-t, --title <title>` | New title for the cloned topic |

---

## topic share / unshare

Enable or disable sharing for a topic.

### Usage

```bash
lh topic share <id> [--visibility <v>]
lh topic unshare <id>
```

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `--visibility <v>` | link | Visibility: private or link |

---

## topic share-info

View sharing info for a topic.

### Usage

```bash
lh topic share-info <id> [--json]
```

---

## topic import

Import a topic.

### Usage

```bash
lh topic import [options]
```

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `--agent-id <id>` | Yes | Agent ID |
| `--data <json>` | Yes | Topic data as JSON string |
| `--group-id <id>` | No | Group ID |
| `--json` | No | Output JSON |

---

## topic recent

List recent topics.

### Usage

```bash
lh topic recent [options]
```

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `-L, --limit <n>` | 10 | Number of items |
| `--json [fields]` | - | Output JSON |

---

# Messages

---

## message list

List messages.

### Usage

```bash
lh message list [options]
```

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `--topic-id <id>` | - | Filter by topic ID |
| `--agent-id <id>` | - | Filter by agent ID |
| `-L, --limit <n>` | 30 | Page size |
| `--page <n>` | 1 | Page number |
| `--user` | - | Only show user messages |
| `--json [fields]` | - | Output JSON |

---

## message search

Search messages.

### Usage

```bash
lh message search <keywords> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--json [fields]` | Output JSON |

---

## message create

Create a message.

### Usage

```bash
lh message create [options]
```

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `-r, --role <role>` | Yes | Message role (user, assistant, system) |
| `-c, --content <content>` | Yes | Message content |
| `--agent-id <id>` | No | Agent ID |
| `--topic-id <id>` | No | Topic ID |
| `--session-id <id>` | No | Session ID |
| `--json` | No | Output JSON |

### Examples

```bash
lh message create -r user -c "Hello, how are you?" --topic-id topic_abc123
```

---

## message edit

Update a message.

### Usage

```bash
lh message edit <id> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `-c, --content <content>` | New content |
| `--role <role>` | New role |

---

## message delete

Delete one or more messages.

### Usage

```bash
lh message delete <ids...> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--yes` | Skip confirmation prompt |

---

## message add-files

Add files to a message.

### Usage

```bash
lh message add-files <id> --file-ids <ids>
```

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `--file-ids <ids>` | Yes | Comma-separated file IDs |

---

## message count

Count messages.

### Usage

```bash
lh message count [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--start <date>` | Start date (ISO format) |
| `--end <date>` | End date (ISO format) |
| `--json` | Output JSON |

---

## message word-count

Count total words in messages.

### Usage

```bash
lh message word-count [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--start <date>` | Start date (ISO format) |
| `--end <date>` | End date (ISO format) |
| `--json` | Output JSON |

---

## message rank-models

Rank models by message usage.

### Usage

```bash
lh message rank-models [--json]
```

---

## message heatmap

Get message activity heatmap.

### Usage

```bash
lh message heatmap [--json]
```

---

# Threads

---

## thread list

List threads by topic.

### Usage

```bash
lh thread list --topic-id <id> [options]
```

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `--topic-id <id>` | Yes | Topic ID |
| `--json [fields]` | No | Output JSON |

---

## thread list-all

List all threads for the current user.

### Usage

```bash
lh thread list-all [--json [fields]]
```

---

## thread delete

Delete a thread.

### Usage

```bash
lh thread delete <id> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--remove-children` | Also remove child messages |
| `--yes` | Skip confirmation prompt |
